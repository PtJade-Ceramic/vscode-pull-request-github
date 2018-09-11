Welcome to the vscode-pull-request-github wiki!

# FAQ

### 1. How does authentication to GitHub work?

The authentication workflow is oAuth based, where GitHub Pull Requests initially makes a request to a new Auth endpoint, which then triggers a traditional oAuth flow to GitHub. Once the OAuth flow is completed, the token is returned to VS Code, and stored in an encrypted store (KeyChain or alike) locally on your computer.

See https://github.com/Microsoft/vscode-pull-request-github/issues/93 for details

### 2. Is GitHub Enterprise supported?

### 3. What about supporting other providers such as Gitlab and Bitbucket?

### 4. Where can I see the roadmap for the extension?



