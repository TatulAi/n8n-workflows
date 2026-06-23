# Before pushing a workflow — sanitization checklist

n8n's normal **Download** export does NOT include credential secrets, but a few things can still leak. Run through this before committing any workflow to this public repo.

- [ ] Open the exported `.json` in a text editor.
- [ ] Search for: `Bearer`, `apiKey`, `api_key`, `token`, `password`, `secret`, `Authorization`, `sk-`, `sk_live`, `pk_live`. Any real value found → replace with a placeholder like `YOUR_API_KEY`.
- [ ] Check **HTTP Request** nodes specifically — keys pasted from cURL commands can end up embedded here.
- [ ] Check credential **names** (not the secrets, just the labels). Rename anything that reveals your name, a client, or internal systems to something generic like `Gmail account` or `OpenAI account`.
- [ ] Search for real email addresses or internal domain names baked into node settings.
- [ ] Never commit a `credentials.json` file (the CLI `export:credentials --decrypted` output) — that contains real secrets in plain text.

When in doubt, leave it out.
