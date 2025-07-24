<p align="center">
  <img src="logo.png" title="JuNe WebServer" width="314" height="170">
</p>

# [JuNe WebServer](https://github.com/EduardoRuizM/june-webserver "JuNe WebServer")
JuNe WebServer is a ultra-lightweight Node.js HTTP / HTTPS server to run HTML projects.
And for development with Hot Module Replacement (HMR) to automatically update the page when a change occurs (using WebSockets).

- Creates a HTTP or HTTPS server (IPv4 / IPv6).
- Serves the files included in the folder.
- All main MIME types supported.
- Checks index files to load as default in folders.
- Monitors files changes in folder and subfolders (dev mode).
- Opens default browser to show the webpage (dev mode).
- Support for HTTP/2.
- Detects if SSL certificates are renewed (different datetime) and restarts automatically.
- Binaries compiled (x64 bits) for: 🐧Linux, 🪟 Windows and 🍎MacOS.
- Just 1 file and 8 Kb.

![8 Kb](https://img.shields.io/github/size/EduardoRuizM/june-webserver/webserver.js) ![NPM Downloads](https://img.shields.io/npm/dt/june-webserver)

### 👉 JuNe Server was developed initially for JavaScript Framework [JuNe PaulaJS](https://github.com/EduardoRuizM/june-paulajs "JuNe PaulaJS")

# Author
[Eduardo Ruiz](https://github.com/EduardoRuizM) <<eruiz@dataclick.es>>

# JuNe / JUst NEeded Philosophy
1. **Source code using less code as possible**
  So you can understand code and find bugs easier.
2. **Few and optimized lines is better**
  Elegant design.
3. **Avoid external dependencies abuse/bloated, and possible third-party bugs**
  Less files size, better and faster to the interpreter.
4. **Clear and useful documentation with examples and without verbose**
  Get to the point.
5. **Avoid showing unsolicited popups, notifications or messages in frontend**
  For better User eXperience.
6. **Simple UI**, without many menus/options and with few clicks to get to sites.
7. Consequences of having a lot of code (and for simple things): Having to work and search through many files and folders with a lot of wasted time, successive errors due to missing unknown files, madness to move a code to another project, errors due to recursive dependencies difficult to locate, complexity or impossibility to migrate to new versions, unfeasibility to follow the trace with so much code, risk of new errors if the functionality is extended, problems not seen at the first sight, general slowness in the whole development due to excessive and unnecessary code.

# Installation
The best way is to install JuNe WebServer globally to run wherever you want with `npm install -g june-webserver`
Then run with `webserver [parameters]`

...or if local installation `node webserver [parameters]` / `npm start` (only to use default parameters).

### Running from binaries (x64 bits)
You can also download compiled binaries:
[🐧Linux](https://drive.google.com/file/d/1trMw2La5ctz45J8D1q9zw7ficMR4gFGs/view?usp=sharing "Linux") (20 Mb), [🪟 Windows](https://drive.google.com/file/d/1JBNyxFWd30J9pFb5wPX-dfh99A3KKUUu/view?usp=sharing "Windows") (17 Mb) or [🍎MacOS](https://drive.google.com/file/d/19kUNRZ6_1Cs-M5Nx0FldoJ6qKrDKNgBQ/view?usp=sharing "MacOS") (20 Mb).

# Parameters
Passed as parameter (prefixed with hyphen) on command line, or an array object on class creation.

| Object | Definition | Required | Default | Sample |
| --- | --- | :---: | --- | --- |
| url | URL (and port) for running | ✔ | http://localhost:8180 | - |
| folder | Web project folder | ✔ | Current Work Directory | - |
| cert | SSL cert file path for HTTPS | - | - | cert.pem |
| key | SSL key file path for HTTPS | - | - | key.pem |
| http2 | Use HTTP/2 (certs required) | - | 0 | 1 |
| index | Index files to scan in folders default (sep by space) | - | index.html index.htm | - |
| if404 | Returns the specified file if path does not exist | - | - | index.html |
| alias | Map URL location to different filesystem path | - | - | - |
| dev | Development mode | - | false | 1 |
| hmr | HMR Port in Dev mode | - | 30795 | - |
| script | (only in Dev mode) Optional code (instead reload) to run when update | - | location.reload() | - |

Set `-dev 1` for activate development mode.

For development mode:
- `<head>` tag must exist in HTML files, then JuNe WebServer adds a JavaScript code with WebSockets to check for changes and reload if necessary.
- `script` Custom JavaScript code to run on project update or location.reload()

### Using alias for URL mapping
To define URL path aliases using the format **/request1|path1[/request2|path2]** where each pair maps a request path to a local directory.
Allowing the server to serve files from pathX when a client accesses /requestX, example: `/shared|/var/home/mypath`
Sample for `package.json`
🐧 Linux: `"start": "node webserver.js -if404 index.html -alias \"/js/|/var/home/myjs\" -dev 1"` all **/js** request to **/var/home/myjs**
🪟 Windows: `"start": "node webserver.js -if404 index.html -alias \"/js/|D:\\Documents\\myjs\" -dev 1"` all **/js** request to **D:\Documents\myjs**

### Projects with process in a file
Some projects process paths or HTML files internally in a single file, usually *index.html* such as JavaScript frameworks with routing system.
So if web server does not find a path, it must send the request to that file, you can do that with parameter `-if404 index.html`

### Allowed extensions to MIME types
html, htm, css, xml, txt, ics, png, gif, webp, avif, jpg, jpeg, ico, svg, mp3, mpg, mpeg, ogg, aac, opus, mp4, webm, js, mjs, json, pdf, zip, ttf, woff2.

### Samples on command line
Basic server with path and index.html
`webserver -url http://localhost:8180 -folder /var/www/myproject`

Load myfile.html
`webserver -url http://localhost:8180 -folder /var/www/myproject -index myfile.html`

Load myfile.html or myindex.html
`webserver -url http://localhost:8180 -folder /var/www/myproject -index "myfile.html myindex.html"`

JuNe PaulaJS project
`webserver -url http://localhost:8180 -folder /var/www/myproject -if404 index.html`

Development mode
`webserver -url http://localhost:8180 -folder /var/www/myproject -dev 1`

Development mode with JuNe PaulaJS project
`webserver -url http://localhost:8180 -folder /var/www/myproject -if404 index.html -dev 1`

Development mode with custom script when changes
`webserver -url http://localhost:8180 -folder /var/www/myproject -dev 1 -script "alert('Changes')"`

### Sample declaring class
const webserver = WebServer({url: 'http://myapp.com:8180', folder: '/var/www/myproject'});

## Certificates for SSL localhost
Generate a self-signed certificate, only for localhost development purposes.
Avoid browser warning ´Potential Security Risk´ with a Certification Authority entity (CA).
1) Create file `localhost.ext` (add more IPs or domains if needed):
```
authorityKeyIdentifier = keyid,issuer
basicConstraints = CA:FALSE
keyUsage = digitalSignature, nonRepudiation, keyEncipherment, dataEncipherment
subjectAltName = @alt_names
[alt_names]
IP.1 = 127.0.0.1
DNS.1 = localhost
```
2) Generate certificates (for 10 years) to use on your HTTP server `localhost.crt` and `localhost.key`
```
openssl genrsa -out CA.key -des3 2048
openssl req -x509 -sha256 -new -nodes -days 3650 -key CA.key -out CA.pem
openssl genrsa -out localhost.crypted.key -des3 2048
openssl req -new -key localhost.crypted.key -out localhost.csr
openssl x509 -req -in localhost.csr -CA CA.pem -CAkey CA.key -CAcreateserial -days 3650 -sha256 -extfile localhost.ext -out localhost.crt
openssl rsa -in localhost.crypted.key -out localhost.key
```
3) To avoid warning: Browser ➜ Certificates ➜ Import ➜ Authorities ➜ `CA.pem`

# [JuNe](https://just-needed.com "JuNe") Development Ecosystem
Everything you need to develop your project:
### Backend
- [JuNe BackServer](https://github.com/EduardoRuizM/june-backserver "JuNe BackServer") With request routing, tokens, file upload, send Emails, WebSockets, SSE and captcha.
- [JuNe WebServer](https://github.com/EduardoRuizM/june-webserver "JuNe WebServer") Web server with HMR.

### Frontend
- [JuNe PaulaJS](https://github.com/EduardoRuizM/june-paulajs "JuNe PaulaJS") Powerful JavaScript framework
- [JuNe CSS](https://github.com/EduardoRuizM/june-css "JuNe CSS") Full responsive CSS library with icons.
