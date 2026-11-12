# Estimateup

A Node.js backend foundation built with **Express** and **MongoDB/Mongoose**, with configuration for authentication routing and email delivery.

The current repository contains the server entry point, email configuration, and dependency files. Some modules referenced by the application are missing, so additional files are required before the server can run.

## Technologies

| Technology | Purpose |
|------------|---------|
| Node.js | JavaScript runtime |
| Express | HTTP server and middleware |
| MongoDB / Mongoose | Database integration |
| dotenv | Environment configuration |
| cors | Cross-origin request handling |
| Nodemailer | Email transport configuration |

The package manifest also includes `bcryptjs`, `jsonwebtoken`, `cookie-parser`, and `connect-mongo`. Their use cannot be verified because the related application modules are not included.

## Included Functionality

The server entry point:

- Loads environment variables using `dotenv`.
- Creates an Express application.
- Enables CORS with credentials.
- Parses JSON and URL-encoded request bodies.
- References a database connection module.
- Mounts an authentication router.
- Configures the server to listen on port `5000`.

The email configuration creates a Gmail transporter and exports it for use by other modules.

## Repository Contents

| File | Description |
|------|-------------|
| `app.js` | Express application entry point |
| `config.js` | Email transporter configuration |
| `package.json` | Package metadata, scripts, and dependencies |
| `package-lock.json` | Dependency lockfile |

## Current Project Status

The following referenced modules are not included:

| Missing Module | Referenced By |
|----------------|---------------|
| `db/conn.js` | `app.js` |
| `router/auth.js` | `app.js` |
| `model/userSchema.js` | `config.js` |

Additionally, `config.js` imports `nodemailer`, but the package is not declared in `package.json`.

The available source does not establish the application's estimation workflow, API endpoints, authentication behavior, or frontend.

## Getting Started

### 1. Clone the Repository

```bash
git clone https://github.com/SumairSalam/Estimateup.git
cd Estimateup
```

### 2. Install Declared Dependencies

```bash
npm ci
```

If you intend to use the email configuration, install its missing dependency:

```bash
npm install nodemailer
```

### 3. Restore the Missing Modules

Before starting the server, provide:

- A MongoDB connection module at `db/conn.js`
- An Express router at `router/auth.js`
- The user model referenced by `config.js`, or remove that import if it is unnecessary

The database schema and route implementations must be supplied separately.

### 4. Configure Environment Variables

The application loads a `.env` file through `dotenv.config()`.

Move email credentials out of source code and read them from environment variables. For example:

```env
MONGODB_URI=your_mongodb_connection_string
EMAIL_USER=your_email_address
EMAIL_PASS=your_email_app_password
```

These are suggested variable names. The restored database module and email configuration must explicitly read them.

Do not commit `.env` files or credentials to version control.

### 5. Start the Server

After restoring the missing modules and completing configuration:

```bash
node app.js
```

The server is configured to listen at:

```text
http://localhost:5000
```

No active root route is defined in the included `app.js`. Available endpoints depend on the missing authentication router.

## Package Script Notes

The current package configuration needs adjustment:

- `main` points to `index.js`, but the included entry point is `app.js`.
- The `server` script is incomplete.
- The `test` script is a placeholder that exits with an error.

A suggested scripts configuration is:

```json
{
  "scripts": {
    "start": "node app.js",
    "server": "node app.js"
  }
}
```

After updating `package.json`, start the application with:

```bash
npm start
```

## Configuration Notes

- Port `5000` is hardcoded in `app.js`.
- CORS currently reflects request origins and allows credentials. Configure an explicit frontend origin before deployment.
- Email configuration uses Gmail.
- Email credentials should be supplied through environment variables.
- Cookie parsing is commented out in the server entry point.

## Next Steps

- Add the missing database, router, and model files.
- Document the implemented API endpoints.
- Correct package scripts and entry-point metadata.
- Add environment-based database, email, port, and CORS configuration.
- Add request validation and centralized error handling.
- Add tests for the implemented routes.
- Document the estimation workflow once its implementation is available.

## Maintainer

[Sumair Salam](https://github.com/SumairSalam)

## License

The package metadata declares `ISC`. No standalone license file is included in the current repository.
