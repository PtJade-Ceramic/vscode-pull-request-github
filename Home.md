Welcome to the vscode-pull-request-github wiki!

# FAQ

### 1. How does authentication to GitHub work?

The authentication workflow is OAuth based, where GitHub Pull Requests initially makes a request to a new Auth endpoint, which then triggers a traditional OAuth flow to GitHub. Once the OAuth flow is completed, the token is returned to VS Code, and stored in an encrypted store (KeyChain or alike) locally on your computer.

See https://github.com/Microsoft/vscode-pull-request-github/issues/93 for details

### 2. Is GitHub Enterprise supported?

GitHub Enterprise isn't fully supported currently. We are tracking a few outstanding issues, and we are awaiting an update to be released for GitHub Enterprise instances

Follow this query to see where we are, https://github.com/Microsoft/vscode-pull-request-github/issues?utf8=%E2%9C%93&q=label%3AGitHubEnterprise+

### 3. What about supporting other providers such as Gitlab and Bitbucket?

To build this extension, we introduced a new proposed api for adding comments that is meant to be generic (in the release notes here: https://code.visualstudio.com/updates/v1_27#_comment-providers). This extension is meant only to add support for GitHub pull requests - trying to make it integrate with other git providers would make it bloated. 

Instead our intent is to have a separate extension for each Pull Request provider. We encourage the community to look into this.

GitLab support, https://github.com/Microsoft/vscode-pull-request-github/issues/356

### 4. Where can I see the roadmap for the extension?

The roadmap for this extension is stil in the making. Next steps for us is to graduate out of public preview.

