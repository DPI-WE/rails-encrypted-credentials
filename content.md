# Encrypted Credentials 🤫

## Introduction to Secure Credentials Storage
In the world of web development, securing sensitive information such as API keys, database passwords, and access tokens is paramount. Ruby on Rails provides a powerful mechanism for this: encrypted credentials. This lesson will guide you through understanding, managing, and utilizing encrypted credentials in your Rails applications.

## The Basics of Environment Variables
Before diving into Rails-specific features, let's touch on a universal approach to handling sensitive data: environment variables. Environment variables are a common way to store credentials outside your application's source code to keep them secure and out of version control. Check out this lesson on [Using Environment Variables](https://learn.firstdraft.com/lessons/52-storing-credentials-securely) for more information.

**Pro Tip**: Always add your `.env` files or any file that contains environment variables to your `.gitignore` to prevent them from being accidentally committed to your version control system.

## Elevating Security with Rails credentials
Rails goes a step further with its credentials feature, offering an enhanced level of security. With Rails credentials, all sensitive information can be stored in one place, encrypted, and safely included in your version control system. Changes to secrets and credentials can be deployed in tandem with your application's code changes, ensuring a seamless transition. This eliminates the need for multiple `.env` files and supports atomic deploys, where key changes are seamlessly integrated with the code.

<aside>
 "atomic" refers to an operation or series of operations that are completed as a single unit. This means that the operation either fully succeeds or fully fails, with no intermediate states. If an error occurs during an atomic operation, the system should be left unchanged as if the operation had never been started. This concept is crucial for maintaining data integrity and consistency, especially in environments where multiple processes might be accessing or modifying data simultaneously.
</aside>

## Understanding Encryption
To appreciate the security Rails credentials offer, it's essential to grasp the basics of encryption. Think of encryption like a digital safe. Information is locked away with a key, and only the correct key can unlock it to retrieve the information.

- **Symmetric encryption** uses the same key for encryption and decryption.
- **Asymmetric encryption** uses a public key for encryption and a private key for decryption, enhancing security.

## Working with Application Credentials in Rails

- **Credentials File**: `credentials.yml.enc` is an encrypted file where all your application's secrets are safely stored. This file can and should be checked into version control.
- **Master Key**: This symmetric encryption key is used to encrypt and decrypt the `config/credentials.yml.enc` file. It's stored in `config/master.key` and should never be committed to your version control. Instead, it should be shared securely with your team or set as an environment variable (`ENV["RAILS_MASTER_KEY"]`).

## Managing Credentials
Rails provides a set of commands to manage your application's credentials securely.

### Show
Use `bin/rails credentials:show` in the terminal to see your decrypted credentials.

### Edit
Use `EDITOR="code --wait" bin/rails credentials:edit` in the terminal to modify credentials. To reset, delete `credentials.yml.enc` and rerun the edit command.

### Use
In your application, access your credentials using `Rails.application.credentials.your_secret_key`. Rails will handle decryption at runtime, ensuring your secrets are safe.

### Security
Remember, the security of your `master.key` is crucial. If it's compromised, all your encrypted credentials are at risk.












## Example
Let's add a secret API key to our credentials:

1. Open and edit your credentials file: `EDITOR="code --wait" bin/rails credentials:edit`
2. Add your API key

```yaml
payment_api_key: my-super-secret-key
```

3. Save and close the file. Rails encrypts this information with your master.key.

4. Access this key in your application like so: `Rails.application.credentials.payment_api_key`.


## Best Practices and Tips

1. Securely store your `master.key` in a password manager or another secure location accessible only to your team.
2. Ensure `config/master.key` is listed in your `.gitignore` to prevent accidental commits.

## Helpful Commands

- **View Credentials:** `bin/rails credentials:show`.
- **Edit Credentials:** `EDITOR="code --wait" bin/rails credentials:edit`.
- **Get Help:** `bin/rails credentials:help`.

## Quiz

- What is the primary purpose of using encrypted credentials in a Rails application?
- To securely store sensitive information such as API keys and passwords.
  - Correct! Encrypted credentials help protect sensitive information.
- To enhance application performance.
  - Not quite. While important for security, encrypted credentials do not directly affect performance.
- To improve user authentication.
  - Not quite. Encrypted credentials are primarily for securing sensitive information.
{: .choose_best #encrypted_credentials_purpose title="Purpose of Encrypted Credentials" points="1" answer="1" }

- Why should you add your `.env` files to your `.gitignore`?
- To improve application performance.
  - Not quite. The main reason is to secure sensitive information.
- To enable faster deployments.
  - Not quite. The main reason is to prevent accidental exposure of sensitive information.
- To prevent sensitive information from being accidentally committed to version control.
  - Correct! Adding `.env` files to `.gitignore` helps keep sensitive information secure.
{: .choose_best #env_files_gitignore title="Adding .env Files to .gitignore" points="1" answer="3" }

- What is the benefit of using Rails credentials over multiple `.env` files?
- Rails credentials allow all sensitive information to be stored in one encrypted file and safely included in version control.
  - Correct! Rails credentials provide a secure and centralized way to manage sensitive information.
- Rails credentials improve database performance.
  - Not quite. Rails credentials focus on security, not performance.
- Rails credentials automatically generate API keys.
  - Not quite. Rails credentials securely store, but do not generate, API keys.
{: .choose_best #rails_credentials_benefit title="Benefit of Rails Credentials" points="1" answer="1" }

- What is the difference between symmetric and asymmetric encryption?
- Symmetric encryption is faster than asymmetric encryption.
  - Not quite. While often true, the main difference lies in the key usage.
- Symmetric encryption is more secure than asymmetric encryption.
  - Not quite. Security depends on the context, but the main difference is in key usage.
- Symmetric encryption uses the same key for encryption and decryption, while asymmetric encryption uses a public key for encryption and a private key for decryption.
  - Correct! This is the fundamental difference between symmetric and asymmetric encryption.
{: .choose_best #encryption_difference title="Difference Between Symmetric and Asymmetric Encryption" points="1" answer="3" }

- How can you access a credential named `payment_api_key` in your Rails application code?
- Using `Rails.application.credentials.payment_api_key`
  - Correct! This is the proper way to access credentials in your code.
- Using `ENV['payment_api_key']`
  - Not quite. This would access an environment variable, not a Rails credential.
- Using `Rails.config.payment_api_key`
  - Not quite. The correct way is `Rails.application.credentials.payment_api_key`.
{: .choose_best #access_credentials_code title="Accessing Credentials in Code" points="1" answer="1" }

## Resources
By understanding and utilizing Rails' encrypted credentials, you can ensure that your application's sensitive information remains secure, both in transit and at rest. For more in-depth information on managing security and credentials in Rails, refer to the [official Rails guides](https://edgeguides.rubyonrails.org/security.html#custom-credentials)
