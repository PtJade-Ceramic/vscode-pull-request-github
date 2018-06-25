## Developing

* Clone the repository
* Run `npm install`
* Compile in the background
  * Run `npm run compile`
  * Run `npm run build-preview`
  * Or you can directly start these two tasks by Command Palette -> Run Build Task
* F5, launch the extension in latest VSCode Insiders.

## Dogfood

**Installation**

We generated VSIXs from source code right now so you can download them from https://github.com/Microsoft/vscode-pull-request-github/releases and then follow below steps to enable this extension

* Go to Extension Viewlet
* Click on the dropdown (`···` icon) on the title bar of the viewlet
* Click *Install from VSIX*
* Open terminal and run `code-insiders --enable-proposed-api Microsoft.vscode-pull-request-github` to allow this extension to use proposed APIs.

**Authentication**

There are two ways of doing authentication

* GitHub access token, this is the recommended way right now. The config name is `github.accessToken`. Please make sure the token you put there has proper access to *repo* and *user*
* If there is no GitHub access token, the extension will try to use the local Git Credential Manager. Whether the authentication will work depends on if your local credentials work.
  * [ ] 🏃 There is an known bug when you are using ssh and the `passphrase` expires, the extension will fail slightly. 