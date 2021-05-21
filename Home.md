Welcome to the vscode-pull-request-github wiki!

# FAQ

### 1. How does authentication to GitHub work?

The authentication workflow is OAuth based, where GitHub Pull Requests initially makes a request to a new Auth endpoint, which then triggers a traditional OAuth flow to GitHub. Once the OAuth flow is completed, the token is returned to VS Code, and stored in an encrypted store (KeyChain or alike) locally on your computer.

See https://github.com/Microsoft/vscode-pull-request-github/issues/93 for details

### 2. Is GitHub Enterprise supported?

GitHub Enterprise has limited support beginning in version 0.27.0 of the extension, thanks to community member @kabel. Our team still does not have access to Enterprise instances to test with, so there are likely to still be some issues, particularly in areas around opening or generating GitHub links. We welcome any help on improving our support.

VS Code version 1.57 or above is required to use this. At the time of this writing, this is the VS Code Insider's version, which can be downloaded [here](https://code.visualstudio.com/insiders/) and used side-by-side with the stable version of VS Code. The changes to the extension are only available in the [nightly](https://marketplace.visualstudio.com/items?itemName=GitHub.vscode-pull-request-github-insiders)
version of the extension right now, but should be released to stable in June 2021. To use the nightly version of the extension, please make sure that the stable version of the extension is uninstalled or disabled - they will conflict when simultaneously enabled.

To sign in with GitHub Enterprise, update the `github-enterprise.uri` setting in VS Code to your server URL. You can then use the Accounts icon to start the sign in flow, and you will be asked to provide a Personal Access Token. The extension uses 'read:user', 'user:email', 'repo' scopes, so create a PAT with these permissions. Steps for signing in can be found here: https://github.com/microsoft/vscode/pull/115940#issuecomment-838838680

### 3. Why isn't the extension starting?

If you're using an OSS build of Visual Studio Code (for example, the archlinux community build), the extension will fail to activate unless you launch with the flag `--enable-proposed-api GitHub.vscode-pull-request-github`. In the official build of VSCode, we have a `product.json` file that has a list of extensions that are allowed to use the proposed APIs. Since this is absent in the OSS build, the flag is needed to enable the proposed api for this extension.

### 4. What about supporting other providers such as Gitlab and Bitbucket?

To build this extension, we introduced a new proposed api for adding comments that is meant to be generic (in the release notes here: https://code.visualstudio.com/updates/v1_27#_comment-providers). This extension is meant only to add support for GitHub pull requests - trying to make it integrate with other git providers would make it bloated. 

Instead our intent is to have a separate extension for each Pull Request provider. We encourage the community to look into this.

GitLab support, https://github.com/Microsoft/vscode-pull-request-github/issues/356

### 5. Where can I see the roadmap for the extension?

The roadmap for this extension is still in the making. Next steps for us is to graduate out of public preview.

