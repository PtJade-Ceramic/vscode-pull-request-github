Welcome to the vscode-pull-request-github wiki!

# FAQ

### 1. How does authentication to GitHub work?

The authentication workflow is OAuth based, where GitHub Pull Requests initially makes a request to a new Auth endpoint, which then triggers a traditional OAuth flow to GitHub. Once the OAuth flow is completed, the token is returned to VS Code, and stored in an encrypted store (KeyChain or alike) locally on your computer.

See https://github.com/Microsoft/vscode-pull-request-github/issues/93 for details

### 2. Is GitHub Enterprise supported?

Yes! There are two ways of authenticating to GitHub Enterprise, depending on which version your organization is running.

#### Integrated sign in

If your GitHub Enterprise is one of the following versions, you can authenticate in the same way as you would on GitHub, by clicking on the Sign In button when the dialog asking you to sign in shows up on the bottom right corner.

- 2.14.5 and above
- 2.13.11 and higher 2.13.x
- 2.12.19 and higher 2.12.x
- 2.11.25

#### I get a 404 when trying to sign in!

That means your server doesn't supported integrated sign in. See below for an alternate way of authenticating.

#### Personal Access Token authentication

If your GitHub Enterprise does not support integrated sign in, or if the integrated sign in process fails, you can create a personal access token to use as your password.

1. Go to https://github.com/settings/tokens
2. Generate a token with the the following scopes: `repo`, `read:user`, `user:email`, and `write:discussion` (see [this guide](https://help.github.com/articles/creating-a-personal-access-token-for-the-command-line/) on how to create a PAT for more details). Note that `write:discussion` doesn't exist on older versions of GitHub Enterprise and will be treated as optional for those, but is required for newer versions.
3. In VS Code, run the command (⌘⇧P by default) `GitHub Pull Requests: Manually Provide Authentication Response` and paste your token. It will prompt you for the server to use the token with—enter the hostname of your GHE server here.

#### I did all that but I still can't login to my GitHub Enterprise instance!

If your GitHub Enterprise is running with a self-signed certificate, VSCode will not be able to make requests to it, for security purposes, because the OS doesn't trust your server. You can check whether this is the case by browsing to your server and checking the certificate information shown in the lock icon.

In order to connect to a server like this, you'll need to import the certificate into your machine and trust it. You can export the certificate from your browser by clicking on the lock icon (in chrome, for example), clicking on `Certificate`, `Details`, `Open File`, and exporting the certificate as PKCS #7 (.p7b extension), including all the certificates in the path:

![image](https://user-images.githubusercontent.com/310137/46096931-c9e66000-c1c0-11e8-84bc-d32a05289fa8.png)

You can then double click on the exported file and import it into your user trust store 

![image](https://user-images.githubusercontent.com/310137/46097068-26e21600-c1c1-11e8-8b38-2df6a4d71a18.png)

Restart vscode, and you'll be able to connect to your server. 

### 3. Why isn't the extension starting?

If you're using an OSS build of Visual Studio Code (for example, the archlinux community build), the extension will fail to activate unless you launch with the flag `--enable-proposed-api GitHub.vscode-pull-request-github`. In the official build of VSCode, we have a `product.json` file that has a list of extensions that are allowed to use the proposed APIs. Since this is absent in the OSS build, the flag is needed to enable the proposed api for this extension.

### 4. What about supporting other providers such as Gitlab and Bitbucket?

To build this extension, we introduced a new proposed api for adding comments that is meant to be generic (in the release notes here: https://code.visualstudio.com/updates/v1_27#_comment-providers). This extension is meant only to add support for GitHub pull requests - trying to make it integrate with other git providers would make it bloated. 

Instead our intent is to have a separate extension for each Pull Request provider. We encourage the community to look into this.

GitLab support, https://github.com/Microsoft/vscode-pull-request-github/issues/356

### 5. Where can I see the roadmap for the extension?

The roadmap for this extension is still in the making. Next steps for us is to graduate out of public preview.

