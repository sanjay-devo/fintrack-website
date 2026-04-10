# FinTrack Website

A clean and polished finance tracker built with HTML, Tailwind CSS, and vanilla JavaScript. This lightweight app lets you register or sign in, then save income and expense entries under your own Firebase user profile.

## Features

- Register or login with email/mobile and password
- Per-user transaction storage in Firebase Realtime Database
- Add income and expense transactions quickly
- Track today’s income and expense separately
- View real-time balance updates
- Delete entries with confirmation modal
- Dark/light theme toggle
- Responsive layout for mobile and desktop
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

## Notes

- User authentication data and transactions are stored in Firebase.
- Each user has their own `users/{userId}/transactions` node.
- Session state is stored locally so signed-in users remain logged in.
- Theme preference is also saved locally to preserve light/dark mode.
- The dashboard header is optimized for mobile with a compact greeting and a clean desktop header.
