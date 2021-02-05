Welcome to the vscode-pull-request-github wiki!

# FAQ

### 1. How does authentication to GitHub work?

The authentication workflow is OAuth based, where GitHub Pull Requests initially makes a request to a new Auth endpoint, which then triggers a traditional OAuth flow to GitHub. Once the OAuth flow is completed, the token is returned to VS Code, and stored in an encrypted store (KeyChain or alike) locally on your computer.

See https://github.com/Microsoft/vscode-pull-request-github/issues/93 for details

### 2. Is GitHub Enterprise supported?

As of version 0.16.0 of the extension, we are discontinuing support for GitHub Enterprise. At the beginning of this project, we had resources to test against Enterprise, but we have now been without that for quite some time. Thank you to all of the community members that have helped fill these gaps. As we continue to add features to the extension, it's become increasingly difficult to maintain Enterprise support. This iteration we moved to a new method of authentication built into VSCode in an effort to unify authentication and account management, and this API currently doesn't support Enterprise accounts.

### 3. Why isn't the extension starting?

If you're using an OSS build of Visual Studio Code (for example, the archlinux community build), the extension will fail to activate unless you launch with the flag `--enable-proposed-api GitHub.vscode-pull-request-github`. In the official build of VSCode, we have a `product.json` file that has a list of extensions that are allowed to use the proposed APIs. Since this is absent in the OSS build, the flag is needed to enable the proposed api for this extension.

### 4. What about supporting other providers such as Gitlab and Bitbucket?

To build this extension, we introduced a new proposed api for adding comments that is meant to be generic (in the release notes here: https://code.visualstudio.com/updates/v1_27#_comment-providers). This extension is meant only to add support for GitHub pull requests - trying to make it integrate with other git providers would make it bloated. 

Instead our intent is to have a separate extension for each Pull Request provider. We encourage the community to look into this.

GitLab support, https://github.com/Microsoft/vscode-pull-request-github/issues/356

### 5. Where can I see the roadmap for the extension?

The roadmap for this extension is still in the making. Next steps for us is to graduate out of public preview.

