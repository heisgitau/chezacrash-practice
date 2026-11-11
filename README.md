# Mwangaza Kenya

A mobile-first classroom simulator for Kenyan financial concepts, with an optional original crash-game practice page. Every balance and game stake is virtual. This is **not** a bank, gambling operator, payment service, or M-PESA integration.

## What works today

- Responsive web app with sign-in and demo account registration.
- Virtual KES ledger, demo transfers, simulated bill payments, and statements.
- Original crash-game practice flow at <http://127.0.0.1:8000/game.html>.
- Game stakes and cash-outs post only to the virtual ledger and are marked simulated.
- Security headers and `no-store` API responses.
- Real deposits, withdrawals, and payment-provider callbacks are not implemented.

## Run on Windows

Install Python 3.12 or newer, then double-click `start-local.bat`. When the server reports it is ready, open <http://127.0.0.1:8000>. The API health check is <http://127.0.0.1:8000/api/health>.

Run the backend tests with:

```powershell
python -m pip install -r requirements-dev.txt
python -m pytest -q
```

For local PWA installation, use `localhost` or serve the application through HTTPS; installation is not supported on an ordinary HTTP LAN address.

## Publish a free virtual-only preview

The repository includes [render.yaml](./render.yaml) for a Render **Free** web service. Render assigns a free `onrender.com` address after deployment; the exact subdomain is assigned by Render and is not guaranteed to match the service name.

1. Create a GitHub account if you do not already have one, then install GitHub Desktop.
2. In GitHub Desktop, choose **File → Add local repository**, select this project folder, and create a repository if prompted. Review the files before publishing; do not add credentials or private data.
3. Choose **Publish repository** in GitHub Desktop. A private GitHub repository is fine if your Render account can access it.
4. Create/sign in to a Render account at <https://dashboard.render.com/register> and connect the GitHub account.
5. In Render, choose **New → Blueprint**, select the published repository, review the `chezacrash-practice` service, and apply it. Confirm the plan is **Free**.
6. Wait for the first deployment to finish, open the assigned `onrender.com` URL, then use **Create account**. The preloaded sample accounts are disabled on this deployment.

This is only a public virtual-credit preview—not a real-money product. Render says free web services sleep after 15 minutes without inbound traffic, take about a minute to wake, and have an ephemeral filesystem. This configuration stores its SQLite database there, so accounts, passwords, virtual balances, and rounds can be erased after a restart, sleep, or redeploy. Free services are not for production. Do not collect sensitive/personal data or reuse a password from another site.

## Real-money boundary

The API reports `real_money_enabled: false`. The game page uses virtual credits only; its displayed KSh amounts have no monetary value. Do not accept deposits or promise withdrawals using this project.

The official Daraja 3.0 catalogue documents asynchronous STK Push and B2C flows. STK Push uses a public `CallBackURL`; B2C uses public `ResultURL` and `QueueTimeOutURL` endpoints. Those callbacks require an owned, deployed HTTPS domain and provider configuration. This workspace has no such domain, production credentials, verified callback processing, KYC/AML onboarding, or approved real-money game controls. No production integration has been enabled. Do not put keys, passkeys, certificates, or customer data in source code or chat.

The virtual game is a prototype, not a certified RNG, audited game, or representation of any third-party game. Do not deploy it for real-money wagering.

## Checks

```powershell
python -m pytest -q
python -m compileall -q backend
```
