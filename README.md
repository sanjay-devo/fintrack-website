# FinTrack Website

A clean and polished finance tracker built with HTML, Tailwind CSS, and vanilla JavaScript. This lightweight app lets you register or sign in, then save income and expense entries under your own Firebase user profile.

## Features

- Register with separate email and mobile fields, plus password
- Login using either email or mobile number
- Per-user transaction storage in Firebase Realtime Database
- Add income and expense transactions quickly
- Track today’s income and expense separately
- View real-time balance updates
- Delete entries with confirmation modal
- Dark/light theme toggle
- Responsive layout for mobile and desktop
- Separate `login.html` and `register.html` pages with protected `index.html`
- Compact mobile header greeting with full name shown on desktop
- Polished UI with smooth transitions and modern controls

## How to Use

1. Open `index.html` in your browser.
2. Use the login or register tab to sign in.
3. Add transactions using the `Expense` or `Income` buttons.
4. Enter the amount and optional description.
5. Save the transaction to update your balance and recent activity.
6. Delete transactions from the recent activity list if needed.
7. Use the theme toggle in the header to switch between light and dark mode.

## Tech Stack

- HTML
- Tailwind CSS
- Vanilla JavaScript
- Firebase Realtime Database (REST API)

## Favicon Setup

The FinTrack app uses a favicon link added to the `<head>` section of every HTML file (`index.html`, `login.html`, and `register.html`). The favicon is loaded from a shared JPEG icon URL and works across desktop and mobile browsers.

```html
<link rel="icon" type="image/jpeg" href="https://indiacybercafe.com/wp-content/uploads/2026/04/Fintech_logo_design.jpeg">
```

## Sitemap

A `sitemap.xml` file is included for search engines and crawlers. It lists the main app pages and their relative crawl priority for the live deployment.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<urlset xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">
  <url>
    <loc>http://ft.indiacybercafe.com/index.html</loc>
    <priority>1.0</priority>
  </url>
  <url>
    <loc>http://ft.indiacybercafe.com/login.html</loc>
    <priority>0.8</priority>
  </url>
  <url>
    <loc>http://ft.indiacybercafe.com/register.html</loc>
    <priority>0.8</priority>
  </url>
</urlset>
```

## Notes

- User authentication data and transactions are stored in Firebase.
- Each user has their own `users/{userId}/transactions` node.
- The app also creates `email_index/{normalizedEmail}` and `mobile_index/{normalizedMobile}` to resolve logins by email or phone.
- Session state is stored locally so signed-in users remain logged in.
- Theme preference is also saved locally to preserve light/dark mode.
- The dashboard is protected so `index.html` redirects to `login.html` when no session exists.

## Firebase Security Rules

Copy and paste the JSON below into Firebase Console → Realtime Database → Rules:

```json
{
  "rules": {
    ".read": false,
    ".write": false,
    "users": {
      "$userId": {
        ".read": true,
        ".write": true,
        "id": {
          ".validate": "newData.isString()"
        },
        "name": {
          ".validate": "newData.isString()"
        },
        "email": {
          ".validate": "newData.isString()"
        },
        "mobile": {
          ".validate": "newData.isString()"
        },
        "password": {
          ".validate": "newData.isString() && newData.val().length >= 6"
        },
        "transactions": {
          "$transactionId": {
            ".validate": "newData.hasChildren(['id','title','amount','type','dateStr']) && newData.child('amount').isNumber() && (newData.child('type').val() === 'income' || newData.child('type').val() === 'expense')"
          }
        }
      }
    },
    "email_index": {
      "$emailKey": {
        ".read": true,
        ".write": true,
        ".validate": "newData.isString()"
      }
    },
    "mobile_index": {
      "$mobileKey": {
        ".read": true,
        ".write": true,
        ".validate": "newData.isString()"
      }
    }
  }
}
```

Steps to apply:
1. Open Firebase Console.
2. Go to Realtime Database → Rules.
3. Paste the JSON.
4. Click Publish.

Warning:

- These rules are required because the current app uses custom email/mobile sign-in without Firebase Authentication.
- This setup is okay for development, but it is not secure for production.
- For production security, switch to Firebase Authentication and server-side validation.
