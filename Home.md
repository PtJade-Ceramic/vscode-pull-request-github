Welcome to the vscode-pull-request-github wiki!

# FAQ

### 1. How does authentication to GitHub work?

The authentication workflow is OAuth based, where GitHub Pull Requests initially makes a request to a new Auth endpoint, which then triggers a traditional OAuth flow to GitHub. Once the OAuth flow is completed, the token is returned to VS Code, and stored in an encrypted store (KeyChain or alike) locally on your computer.

See https://github.com/Microsoft/vscode-pull-request-github/issues/93 for details

### 2. Is GitHub Enterprise supported?

#### Version 0.51.* and moving forward

Version 0.51.* works with VS Code insiders version 1.72+ and has improved GitHub Enterprise support:

- No PAT needed!
- Initial testing + fixes for several GitHub Enterprise version.
- GitHub Enterprise 3.1 and up tested.

If you encounter any problems, please open an issue an include the GitHub Enterprise version you're using. This is a work in progress and the extension provides many features to test so there will inevitably still be areas that need work.

#### Version 0.50.0 and lower

GitHub Enterprise has limited support beginning in version 0.27.0 of the extension, thanks to community member @kabel.

To sign in with GitHub Enterprise, update the `github-enterprise.uri` setting in VS Code to your server URL. You can then use the Accounts icon to start the sign in flow, and you will be asked to provide a Personal Access Token. The extension uses 'read:user', 'user:email', 'repo', and 'workflow' scopes, so create a PAT with these permissions. Steps for signing in can be found here: https://github.com/microsoft/vscode/pull/115940#issuecomment-838838680

### 3. Why isn't the extension starting?

If you're using an OSS build of Visual Studio Code (for example, the archlinux community build), the extension will fail to activate unless you launch with the flag `--enable-proposed-api GitHub.vscode-pull-request-github`. In the official build of VSCode, we have a `product.json` file that has a list of extensions that are allowed to use the proposed APIs. Since this is absent in the OSS build, the flag is needed to enable the proposed api for this extension.

### 4. When will the next release occur?

We align our releases and milestones with the main [VS Code project](https://github.com/microsoft/vscode/issues?q=is%3Aopen+is%3Aissue+label%3Aiteration-plan). You can view the iteration plan there, and that will tell you approximately when the next full release will be. Patch releases are not aligned with the VS Code project and will occur as needed.

If there's a change you want to have before the next release, you can always install the [nightly build](https://marketplace.visualstudio.com/items?itemName=GitHub.vscode-pull-request-github-insiders) (and disable the stable version of the extension).

### 5. What about supporting other providers such as Gitlab and Bitbucket?

To build this extension, we introduced a new proposed api for adding comments that is meant to be generic (in the release notes here: https://code.visualstudio.com/updates/v1_27#_comment-providers). This extension is meant only to add support for GitHub pull requests - trying to make it integrate with other git providers would make it bloated. 

Instead our intent is to have a separate extension for each Pull Request provider. We encourage the community to look into this.

GitLab support, https://github.com/Microsoft/vscode-pull-request-github/issues/356

### 6. Where can I see the roadmap for the extension?

The roadmap for this extension is still in the making. Next steps for us is to graduate out of public preview.

