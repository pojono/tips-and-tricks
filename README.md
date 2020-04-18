# Tips-And-Tricks

## Запустить web-сервер на локальном компьютере

1. Open terminal or cmd and install the `http-server` module globally on your machine
  ```
  npm i -g http-server 
  ```
3. Run it using CLI (specifying the folder you'd like to serve files from)
  ```
  http-server ./[yourfolder] -p 1337
  ```
4. Now you should be able to access your files (via something like http://localhost:1337/myfile.html) in a web browser.

## Расшарить локальный порт
1. Download ngrok: https://dashboard.ngrok.com/get-started/setup
2. Unzip it:
  ```
  unzip /path/to/ngrok.zip
  ```
3. Running this command will add your authtoken to the default ngrok.yml configuration file. This will grant you access to more features and longer session times. Running tunnels will be listed on the status page of the dashboard.
  ```
  ./ngrok authtoken YOUR_TOKEN
  ```
4. To start a HTTP tunnel forwarding to your local port 80, run this next:
  ```
  ./ngrok http 80
  ```
  Or tcp forwarging:
  ```
  ./ngrok tcp 8080
  ```
