# LeaveFlow

A lightweight employee leave management website, built with **HTML5, CSS3, vanilla JavaScript, Bootstrap 5 and Bootstrap Icons**. There is no backend, no build step and no installation: it runs by opening `index.html` and deploys to GitHub Pages as-is.

Available in **English (LTR)** and **Arabic (RTL)** with a one-click language toggle.

> ## ⚠️ Demonstration only
> Accounts, passwords and leave requests are stored in the browser's **LocalStorage**, in plain text, on the visitor's own device. This is **not secure authentication** and not a real database. Anyone with access to the browser can read or change the data. Do **not** use real passwords or real employee data. A production system needs a server, hashed passwords, sessions and a proper database.

---

## Features

- Register (Full Name, Employee ID, Department, Email, Username, Password) with duplicate **username** and **Employee ID** checks
- Login with username and password, plus a ready-made demo account
- Employee dashboard: welcome message, department, total / submitted counts, recent requests
- New leave request form (Annual, Sick, Emergency, Other) with validation, generated request IDs (e.g. `LF-2026-0004`) and a success notification
- My Leave Requests table with search and filters (leave type, status)
- Employee profile: edit name, email and department; change password
- Arabic / English with full RTL layout (swaps Bootstrap's LTR and RTL builds automatically)
- Responsive design, navy / blue / orange corporate theme
- There is **no approval workflow**: every request stays in the `Submitted` status

## Demo account

| Username | Password   |
|----------|------------|
| `demo`   | `Demo@123` |

The demo account is created automatically the first time the site is opened, together with three sample requests. The login page has a **Use demo account** button.

## Project structure

```
LeaveFlow/
├── index.html            Landing page
├── login.html            Login
├── register.html         Registration
├── dashboard.html        Employee dashboard
├── leave-request.html    New leave request
├── my-requests.html      My leave requests (search + filters)
├── profile.html          Employee profile
├── css/
│   └── style.css         All custom styles
├── js/
│   ├── language.js       Translations (EN/AR), RTL/LTR switching
│   ├── auth.js           Storage, login/register/profile, navbar, toasts
│   ├── dashboard.js      Dashboard statistics and recent requests
│   └── leave.js          Leave form and requests table
├── assets/
│   └── logo.png
├── .nojekyll             Tells GitHub Pages to serve files as-is
└── README.md
```

All paths are **relative** (no leading `/`), so the site works from any sub-path such as `https://username.github.io/LeaveFlow/`.

## Run locally

1. Download or clone the project.
2. Double-click `index.html` (or drag it into your browser).

That's it. No server, Node.js or npm is needed.

> Bootstrap and Bootstrap Icons are bundled in `assets/vendor/`, so the site works fully offline.

## Deploy to GitHub Pages

1. **Create a repository** on GitHub (for example `LeaveFlow`). Public is fine.
2. **Upload the project files** so that `index.html` is at the **root** of the repository (not inside an extra folder):
   - *Web upload:* open the repository → **Add file → Upload files** → drag in the **contents** of the `LeaveFlow` folder (including the `css`, `js` and `assets` folders and the hidden `.nojekyll` file) → **Commit changes**.
   - *Git command line:*
     ```bash
     cd LeaveFlow
     git init
     git add .
     git commit -m "Add LeaveFlow"
     git branch -M main
     git remote add origin https://github.com/<your-username>/LeaveFlow.git
     git push -u origin main
     ```
3. In the repository, open **Settings → Pages**.
4. Under **Build and deployment**, set **Source** to **Deploy from a branch**, choose branch **main** and folder **/ (root)**, then click **Save**.
5. Wait a minute or two. Your site will be live at:
   ```
   https://<your-username>.github.io/LeaveFlow/
   ```

### Troubleshooting

| Problem | Fix |
|---|---|
| 404 page | `index.html` must be at the repository root, and Pages must be set to the `main` branch `/ (root)`. |
| Page has no styling or icons | Make sure the `css/` and `assets/` folders were uploaded. |
| Changes don't show | Hard refresh (Ctrl/Cmd + Shift + R). GitHub Pages can take a minute to rebuild. |
| A page redirects to login | Protected pages need a signed-in user. Log in first. |

## How the data is stored

| LocalStorage key | Contents |
|---|---|
| `lf_users`    | Array of registered accounts (including plain-text passwords, demo only) |
| `lf_requests` | Array of leave requests |
| `lf_session`  | Username of the signed-in user |
| `lf_lang`     | `en` or `ar` |

LocalStorage is per browser and per site address, so accounts created on one device or browser do not appear on another.

**Reset all data:** open the browser developer tools → Application (or Storage) → Local Storage → delete the keys above and reload. The demo account and sample requests are re-created.

## Customising

- **Colours:** edit the variables at the top of `css/style.css` (`--lf-navy`, `--lf-blue`, `--lf-orange`).
- **Text and translations:** every visible string lives in `js/language.js`. To add or change text, edit the `en` and `ar` dictionaries and use `data-i18n="your.key"` in the HTML.
- **Departments:** update the `<select>` options in `register.html` and `profile.html`, the `DEPARTMENTS` list in `js/auth.js`, and the `dept.*` translations.
- **Leave types:** update the options in `leave-request.html` and `my-requests.html` and the `type.*` translations (and the icon map in `LF.typeChip` in `js/auth.js`).

## Browser support

Current versions of Chrome, Edge, Firefox and Safari.

## License

Free to use and modify for learning and demonstration purposes.
