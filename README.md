# Bluehaven frontend

This is a Vue 3, Vue Router, and Vite frontend:

- `/` — the public resort site and ticket-booking demo.
- `/admin` — the admin demo login page; click **Masuk ke Admin** to continue without credentials.
- `/admin/dashboard` — the admin dashboard demo (requires entering through the admin login page).

Run `npm install`, then `npm run dev`. Both routes are served by the single `index.html` application entry. Run `npm run build` to create the production build in `dist/`.

The page data and interactions remain frontend-only and are not connected to a backend.

## Frontend structure

- `src/components/user/` contains focused home sections: facilities, ticket pricing, and the gallery carousel.
- `src/components/admin/` contains the admin shell components, including its sidebar and header.
- `src/UserPage.vue` and `src/AdminPage.vue` compose the page-level layouts.
- `src/legacy/` contains existing DOM-driven interactions that have not yet been migrated to Vue state.

New UI sections should be implemented as focused Vue single-file components and composed by their page. Keep page-specific state and interactions close to the component that owns them; migrate legacy behavior incrementally so existing booking and admin flows remain intact.
