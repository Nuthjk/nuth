# Gruop_2-project

A warehouse management system converted to a web application while keeping the same Python business logic and database model.

## Run the web app

```bash
python main.py
```

Then open http://127.0.0.1:5000 in a browser.

On first launch, create the administrator account. After that, the app keeps the same warehouse features as the original Python desktop version:

- Dashboard and stock summaries
- Product management
- Stock in and stock out records
- Transaction history
- CSV exports
- User role management for admin accounts

The original Tkinter code remains available under the `warehouse/` package for reference.

## Deploy to Vercel with Turso

Vercel functions cannot persist writes to the local `warehouse.db`. To persist
employee accounts and inventory between requests, create a Turso database:

1. Create a Turso database (for example, `turso db create warehouse --tursodb`)
   and generate an auth token with `turso db tokens create warehouse`.
2. In the Vercel project's **Settings > Environment Variables**, set
   `TURSO_DATABASE_URL` to the database URL and `TURSO_AUTH_TOKEN` to the token.
3. Redeploy. The app creates its tables on startup. On a new database, create
   the first administrator account from the login page.

Keep the auth token private and never commit it. Without Turso variables, the
local app uses `warehouse.db`; existing local data is not copied to Turso.
