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
