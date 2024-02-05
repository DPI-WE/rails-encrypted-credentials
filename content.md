# Using Environment Variables

- Environment variables are a common way to store credentials.
- Remember to add `.env` files to `.gitignore` to prevent accidental commits.

## Rails `credentials` for Enhanced Security

- Rails `credentials` commands enable secure storage of access tokens, database passwords, etc., within the codebase.
- This eliminates the need for multiple `.env` files and supports atomic deploys, where key changes are seamlessly integrated with the code.

## Understanding Encryption

- **Basic Concept:** Think of encryption as a safe. Data goes in, gets locked with a key, and only the correct key can decrypt it.
- **Symmetric Encryption:** The same key encrypts and decrypts data.
- **Asymmetric Encryption:** Uses a public key for encryption and a private key for decryption.

## Application Credentials in Ruby on Rails

- **Credentials File:** `credentials.yml.enc` is used for storing encrypted credentials and is safe for version control.
- **Master Key:**
  - Employs symmetric encryption.
  - The `master.key file` is the encryption key, not stored in version control but shared securely or kept as an environment variable (`ENV["RAILS_MASTER_KEY"]`).

## Managing Credentials
- **Editing:** Use `EDITOR="code --wait" bin/rails credentials:edit` in the terminal to modify credentials. To reset, delete `credentials.yml.enc` and rerun the edit command.
- **Using:** Access credentials in your code, e.g., `Rails.application.credentials.payment_api_key`. Rails decrypts them automatically at runtime.
- **Security:** The master key's security is paramount. If compromised, so are your credentials.

## Example

- Add a secret API key to `credentials.yml.enc`. Something like this:
`payment_api_key: my-super-secret-key`
- Rails encrypts this with `master.key`.
- Access in code like `Rails.application.credentials.payment_api_key`.

## Tips

- Securely store the master key, e.g., in a password manager accessible to your team.
- Ensure `config/master.key` is in your `.gitignore`.

## Helpful Commands

- **View Credentials:** `bin/rails credentials:show`.
- **Edit Credentials:** `EDITOR="code --wait" bin/rails credentials:edit`.
- **Learn More:** `bin/rails credentials:help`.

## Resources
https://edgeguides.rubyonrails.org/security.html#custom-credentials

