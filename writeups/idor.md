# Finding and Fixing an IDOR in My Own App

## Context

I built a small multi-vendor marketplace app (FastAPI backend on a Raspberry Pi,
Flutter frontend) to learn API development. While testing it, I noticed something
that should not have been possible.

## What I found

Any user could delete any shop's products. I could open the app as a customer,
tap a product, and delete it. There was no login check on the delete request.

## Why this is a vulnerability

This is **Broken Access Control**, listed as **A01:2021** on the OWASP Top 10.
Specifically, it's an **Insecure Direct Object Reference (IDOR)**.

The server was trusting the client. The delete endpoint accepted any request
and acted on it without verifying who was asking, or whether they had any
right to delete that specific product.

It's a common mistake because the frontend looked fine. The delete button was
only visible in the owner's view. But anyone who knew the API endpoint could
call it directly with a tool like `curl` and bypass the UI entirely.

### Reproducing it

With the app running locally, I could delete a product that did not belong to
me by sending a single request, with no token and no session:

```bash
curl -X DELETE http://192.168.56.10:8000/products/42
```

The server responded `200 OK` and the product was gone from the database. That
was the whole vulnerability — one unauthenticated request.

## How I fixed it

I rebuilt the authentication and authorisation flow properly, on the server:

1. **Shop creation now requires a PIN.** The PIN is hashed (SHA-256 for now)
   and stored on the server. It is never sent back to the client.
2. **Login issues a bearer token.** When a shop owner logs in with the correct
   PIN, the server generates a random token and stores it against that merchant.
3. **Every write request carries the token.** The client sends it in the
   `Authorization: Bearer <token>` header. If the header is missing or the
   token is invalid, the request is rejected with `401 Unauthorized`.
4. **The server checks ownership, not just identity.** Even with a valid token,
   the server looks up the product being deleted and confirms its `shop_id`
   matches the authenticated merchant. If it doesn't, the request is rejected
   with `403 Forbidden`.

The key change was moving the decision from the client to the server. The UI
still hides the delete button from non-owners, but that is now cosmetic — the
real enforcement happens on every request, regardless of what the client sends.

### The check, in short

```python
@app.delete("/products/{product_id}")
def delete_product(
    product_id: int,
    merchant=Depends(current_merchant),
):
    product = db.get_product(product_id)
    if product is None:
        raise HTTPException(404)
    if product.shop_id != merchant.shop_id:
        raise HTTPException(403)
    db.delete(product)
    return {"status": "deleted"}
