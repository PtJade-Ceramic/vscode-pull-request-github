To allow us early dogfood new features and bug fixes, we added a nightly build for GH PR. The nightly build is a standalone extension and published to the marketplace as [GitHub Pull Request Nightly Build](https://marketplace.visualstudio.com/items?itemName=GitHub.vscode-pull-request-github-insiders).

Below is how we set up the nightly build CD on Azure Pipeline.

## Azure Pipeline setup

Firstly, you need a Azure Devops organization, which you probably already have as it's necessary for [publishing an VS Code extension to the marketplace](https://code.visualstudio.com/api/working-with-extensions/publishing-extension#get-a-personal-access-token). Then you need to create a project if you haven't done that yet

![image](https://user-images.githubusercontent.com/876920/50455807-43e3cd80-0905-11e9-82ef-e87ffdb00be8.png)

Secondly we need to create a build pipeline: 

* Link with a git repository
* Choose a template to start from

![image](https://user-images.githubusercontent.com/876920/50455864-9cb36600-0905-11e9-83d4-bc5a51f9295c.png)

VS Code extensions are Nodejs applications so we can choose the Nodejs template or an empty one for better customization.


## Tasks/Configuration

Once we create a build pipeline, the next step is setting up customized tasks, here is an overall look of GH PR nightly build's pipeline

<img width="1458" alt="image" src="https://user-images.githubusercontent.com/876920/50456120-33345700-0907-11e9-87c9-da069fa6ede7.png">

For every task, we need to specific a task runner. We used three different task runners in our pipeline

* Node Tool Installer.
* Yarn Tool Installer as we use Yarn in our project
* Command Line. For all other tasks, we write our own shell scripts.

<img width="1458" alt="image" src="https://user-images.githubusercontent.com/876920/50456129-40e9dc80-0907-11e9-88bb-efcf1a7beb09.png">

### Install Dependencies

```
yarn
yarn vsce
```

`vsce` is necessary here as we are going to publish from command line.

### Generate Package.json

As mentioned at the very beginning, the nightly build will be a new extension, so there are two properties we need to modify

* Extension ID
* Version

Updating the extension id is easy, for example, we change `vscode-pull-request-github` to `vscode-pull-request-github-insiders`. While updating the version is a bit more complex but the rules are straightforward

1. Every nightly build has an unique version
2. The version only increments
3. We are still able to publish manually

The algorithm for generating a version number which meets #1 and #2 can be [simple and stupid](https://github.com/Microsoft/vscode-pull-request-github/blob/master/ci.js#L9-L16) but to support #3, we can add an Environment Variable `VERSION` and pass that to our script through `args`.

<img width="1433" alt="image" src="https://user-images.githubusercontent.com/876920/50456788-c1aad780-090b-11e9-9700-17d10d760fe8.png">

*Generate Package.json* script:

```shell
node ./ci.js -v "$VERSION" -i "$NAME" -n "$DISPLAYNAME" -d "$DESCRIPTION" -p "$PUBLISHER"
```

<img width="1433" alt="image" src="https://user-images.githubusercontent.com/876920/50456884-734a0880-090c-11e9-919d-9940d49483a7.png">

### Publish

To publish through command line, we need to pass in [Personal Access Token](https://code.visualstudio.com/api/working-with-extensions/publishing-extension#get-a-personal-access-token) through Environment Variable again. Apparently we don't want to put the PAT in source code.

## Trigger/Schedule

Once we have the build pipeline setup, we can save the configuration in a yml file and push that to our repository (xterm [example](https://github.com/xtermjs/xterm.js/blob/master/azure-pipelines.yml)), but you don't necessarily need to if you have some customized scripts you don't want to expose.

The last step is setting triggers for the pipeline. The one we use for GH PR nightly build is 

* Every Mon to Fri 8:00 from master
* Only when there are new commit after the last version


<img width="1433" alt="image" src="https://user-images.githubusercontent.com/876920/50457090-e2742c80-090d-11e9-977e-9ea9c76f1e61.png">

