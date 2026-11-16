# Zxyn Hosting Bot

Telegram hosting bot source and basic repository files.

## Files

- `hosts.py` — bot application
- `requirements.txt` — Python dependencies
- `Procfile` — worker process command for platforms that support Procfiles
- `runtime.txt` — Python runtime hint
- `.env.example` — environment-variable template
- `.gitignore` — excludes secrets and runtime data

## Before running

1. Create a new Telegram bot with BotFather.
2. If the token previously embedded in `hosts.py` was ever shared or committed, revoke it in BotFather and generate a new one.
3. Set the environment variables listed in `.env.example` in your hosting provider.
4. Install dependencies with `pip install -r requirements.txt`.
5. Start with `python hosts.py` (or use the Procfile on a compatible worker platform).

Do not commit `.env`, bot tokens, databases, uploaded scripts, or logs.

## Important security warning

This application accepts uploaded Python/JavaScript files and starts them as operating-system processes. That is arbitrary code execution. The current design does **not** provide a secure sandbox between users, and uploaded scripts may access the host's files, environment variables, network, and other processes.

Do not expose this service to public users or run untrusted uploads on a personal account/server as-is. A production deployment needs strong isolation (separate containers/VMs per user), strict CPU/memory/process/time limits, restricted filesystem and network access, and controlled dependency installation. A normal web-service deployment or a Procfile does not provide those protections.

## Storage note

The bot stores its database, uploaded scripts, and recovery data on local disk. Some hosting providers use ephemeral filesystems, so data may disappear after redeploys/restarts unless persistent storage is configured and the application paths are adjusted to use it.
