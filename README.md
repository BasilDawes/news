# News
Home of my newsletters

**Features:**
- 🖌️ Easily create with liquid templates & mjml for email compatibility
- 👁️ Email open analytics with integrated pixel tracking server
- 📋 Subscribe/unsubscribe
- 📤 Automated bulk sending
- ⚙️ Easy to repurpose for yourself, can run entirely in GitHub

## Developing
### Web
1. `pnpm install`
2. `pnpm dev`
3. Deployments are made automatically on push to GitHub

### Server (optional)
1. Install rust toolchain (rustc, cargo)
2. `cd target/debug`
2. `cargo run` or `cargo build --release`

### Mailer (python script)
1. [Install python](https://www.python.org/downloads/)
2. `pip install dotenv tqdm requests` **OR** install dependancies with `pdm add`
3. `cp .sample.env .env`
4. Make & populate `recipients.csv` with format `<name>,<email>`
5. `python3 newsletter-mailer.py` (will confirm before sending)

## Newsletter formatting
- Body images are bigger than their container b/c I found they still looked blurry. I resized 25%. Looks good and still small filesize

## Personalization
The mailer script makes the following substitutions:
- `$name`: Recipient name
- `$tracking`: Recipient name, URI encoded
- `$email`: Recipient email, used for unsubscribing
- `$address`: Sender's physical address, read from `.env`

## Server endpoints
- `/hello/<info>`: Tracking pixel which logs iso_datetime, ip, user_agent, `info` to `access.csv`
- `/subscribe/<email>/<name>`: Adds `name,email` to `recipients.csv`
- `/unsubscribe/<email>`: Removes `email` from `recipients.csv`
