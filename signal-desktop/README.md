# Signal Desktop
This guid is written by using Signal Desktop on branch Master version 1.30.0-beta.4

## Requirement
* NVM 12.4.0

## How To
1. Install requirement

on MacOS, Install xcode
```
xcode-select --install # Install Command Line Tools if you haven't already.
sudo xcode-select --switch /Library/Developer/CommandLineTools # Enable command line tools
```

On Win7, Install .Net 4.5.1 & Windows SDK 8.1 & Windows Build Tools
```
npm install --global --production --add-python-to-path windows-build-tools
```

On Linux, Install python, gcc, g++, make
```
sudo apt-get install python, gcc, g++, make
```

2. Clone signal-desktop

3. Mount signal desktop directory
```
cd Signal-Desktop
```

4. Install yarn
```
npm install —global yarn
```

5. Install & build with yarn
```
yarn install —frozen-lockfile
```

6. Generate final JS & CSS
```
yarn grunt
```

7. Generate full-set icon
```
yarn icon-gen
```

8. Build with webpack
```
yarn build:webpack
```

9. You can test with
```
yarn test 
```

10. Start the app
```
yarn start
```

11. To connect to own production server, `create local-development.json`, the value is the same as `production.json` but without `updateEnabled`.
```
{
  "serverUrl": "https://domain.com",
  "cdnUrl": "https://cdn-domain.com",
  "serverTrustRoot": "public-key-generated-in-signal-server-step-4",
  "updatesEnabled": true
}
```

## Using own Server
1. Update `config/deafult.json`, set serverUrl & cdnUrl by using your Server URL & your CDN url, **don’t include trailing slash on serverUrl and cdnUrl**.

2. Update `config/default.json`, set certificateAuthority using CA’s SSL Certificate.

3. Update `config/default.json`, set serverTrustRoot using your CAPublicKey (Also used in android as UNIDENTIFIED SENDER TRUST ROOT).

4. Update `js/modules/web_api.js`, find functions called `getAttachment` and `putAttachment`, then replace `${cdnUrl}/attachments/${id}` with `${cdnUrl}/` **(Do this if you do the same in android client)**.

5. Still on the same functions, set a default value for `certificateAuthority` variable (see below) **new line in your certificateAuthority needs to be formatted to “\n”**.

**change this**
```
...
certificateAuthority,
...
```


**to this**
```
...
certificateAuthority: "-----BEGIN CERTIFICATE----- ... -----END CERTIFICATE-----\n",
...
```


6. `yarn generate`

7. `yarn build`

8. `yarn start`


## FAQ
Q: How could I get certificate authority?

A: I called it the certificate of the certificate issuer. You can try browsing a https web using chrome, click on lock pad beside the URL address bar, then click on "Certificate (Valid)", you will see the top most & orange certificate, that is what you need, drag it to your desktop to save it.
