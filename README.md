# ReURI
### Welcome to [ReURI](https://reuri.okello.io), a simple url encoder and decoder.
ReURI is a simple tool for converting urls between their encoded forms, eg. `https%3A%2F%2Fexample.com` and their
unencoded eg. `https://example.com`.
## Why??
I had an issue when I was looking at my server access logs where some urls where encoded by the browser. I wanted
to be able to follow those links and see where they lead to. I could make a a CLI tool to do that, but I decided to make it
a web app so others can use it.

## Why Vue?
It is simple and I am good at using it.

## Self Hosting
If you want to self host ReURI, it's simple. 
Clone the repo:
```shell
git clone https://github.com/keystroke3/ReURI.git
```
[Install yarn](https://classic.yarnpkg.com/lang/en/docs/install/)
```shell
npm install --global yarn
```
Install dependencies and build:
```shell
cd ReURI
yarn install
yarn build
```
Use a http server to serve the files in `dist` directory.  

### Node
```shell
npm install http-server -g
http-server dist -p 3000
```
### Python
You can use python's built in http server
```shell
python -m http.server 3000 --directory dist
```
### Apache2
```apache
<VirtualHost *:3000>
    ServerAdmin webmaster@localhost
    DocumentRoot /path/to/ReURI/dist
    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```
### Nginx
```Nginx
server {
    listen 80;
    server_name awesome-server-name.tld;
    location / {
        root /path/to/ReURI/dist/;
        add_header Cache-Control "public, no-transform";
        try_files $uri $uri/ /index.html =404;
    }
    access_log /some/path/nginx_access.log;
    error_log /some/path/nginx_error.log;

}
```

## Todo
- [ ] Add file support

For queries, compliments, complaints: Twitter: [@keystroke3](https://twitter.com/keystroke_3), Email: [keystroke33@gmail.com](mailto:keystroke33@gmail.com)

