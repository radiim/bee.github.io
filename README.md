# Fitpay CSS Whitelabeling Instructions.

Fitpay's WebView implementation supports overriding of the built-in CSS by providing a ```themeOverrideCssUrl``` value in the config object passed to the WebView when the WebView is invoked. Config object is a Base64-encoded value of the JSON representing config values. For example, config JSON: 

```{
  "clientId": "pagare",
  "version": "UNKNOWN",
  "devices": [],
  "themeOverrideCssUrl": "https://localhost:8080/default-oem.css"
}``` 
would result in the following Base64-encoded value: 

```ew0KICAiY2xpZW50SWQiOiAicGFnYXJlIiwNCiAgInZlcnNpb24iOiAiVU5LTk9XTiIsDQogICJkZXZpY2VzIjogW10sDQogICJ0aGVtZU92ZXJyaWRlQ3NzVXJsIjogImh0dHBzOi8vbG9jYWxob3N0OjgwODAvZGVmYXVsdC1vZW0uY3NzIg0KfQ==```

This Base64-encoded value can then be passed to the WebView: 

```https://localhost:8001/walletAccess?config=ew0KICAiY2xpZW50SWQiOiAicGFnYXJlIiwNCiAgInZlcnNpb24iOiAiVU5LTk9XTiIsDQogICJkZXZpY2VzIjogW10sDQogICJ0aGVtZU92ZXJyaWRlQ3NzVXJsIjogImh0dHBzOi8vbG9jYWxob3N0OjgwODAvZGVmYXVsdC1vZW0uY3NzIg0KfQ%3D%3D```

To Base64-encode JSON object one of the many Base64 encoders available online can be used.

CSS content referenced by the ```themeOverrideCssUrl``` value should be accessible from End User devices. Note that the URL needs to be an HTTPS URL. One option would be to host the CSS content on github pages similar to how this repository hosts ```default-oem.css`` file and then reference the CSS file like so: https://fitpaycss.github.io/default-oem.css 

For rapid development we recommend setting up a local environment for CSS modification and then pushing it out to be hosted externally once the modifications are implemented. 

All that you'll need to set up locally is a Web Server capable of serving content over HTTPS and a text editor of your choice to modify the CSS files. There are multiple options available as far as the web server setup is concerned. Here are sample instructions on how to get set up with ```http-server``` available as an NPM module.

1. Download and install Node (NPM comes pre-packaged with Node distribution): https://nodejs.org/en/download/
2. Install the http-server module : ```npm install http-server -g```
3. Download key.pem and cert.pem files from this repository : https://raw.githubusercontent.com/fitpaycss/fitpaycss.github.io/master/key.pem https://raw.githubusercontent.com/fitpaycss/fitpaycss.github.io/master/cert.pem
4. Copy key.pem and cert.pem files to the directory where you'll be working on the CSS file
5. Start http-server: ```http-server -S```
6. If everything worked, you should be able to reference your CSS file locally, for example: https://localhost:8080/default-oem.css


