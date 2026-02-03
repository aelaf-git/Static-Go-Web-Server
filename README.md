# Go HTTP Server with Static Pages and Simple Form

This project is a small Go web server that serves static HTML from a `static/` directory and exposes a couple of basic HTTP endpoints. It is a minimal, learning-friendly example that demonstrates:
- Serving static files with Go's `http.FileServer`
- Handling GET and POST routes with `http.HandleFunc`
- Parsing form data from an HTML `<form>`

The server listens on port `8080` and provides a simple “hello” endpoint plus a form submission handler.

## Features
- **Static site hosting**: Files under `static/` are served at the root path `/`.
- **Hello endpoint**: `GET /hello` responds with a short greeting.
- **Form handling**: `POST /form` parses form values and echoes them back.

## Endpoints
- `GET /`  
  Serves `static/index.html` (and any other files in `static/`).

- `GET /hello`  
  Returns `Hello!` if the request method is `GET`. Any other method returns a 404.

- `POST /form`  
  Expects form fields named `name` and `address`. Responds with:
  - A confirmation line (`POST request successful`)
  - The provided `Name`
  - The provided `Address`

## Project Structure
- `main.go`  
  The Go application entry point. Sets up the HTTP server, routes, and handlers.

- `static/index.html`  
  A basic static page shown at the root path.

- `static/form.html`  
  A simple HTML form that POSTs to `/form`.

## How It Works
- The server uses `http.FileServer(http.Dir("./static"))` to serve files under `/`.
- Custom handlers are registered for `/form` and `/hello`.
- The form handler calls `r.ParseForm()` and then reads `name` and `address` via `r.FormValue(...)`.

## Run the Server
1. From the project directory, run:
   ```bash
   go run main.go
   ```
2. Open these in your browser:
   - `http://localhost:8080/` to view the static page.
   - `http://localhost:8080/form.html` to submit the form.
   - `http://localhost:8080/hello` to see the greeting.

## Notes
- The server logs to stdout and exits if it cannot start listening on `:8080`.
