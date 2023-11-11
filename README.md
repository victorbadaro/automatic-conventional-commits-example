# automatic-conventional-commits-example
![image](https://img.shields.io/badge/EN-blue?link=.%2FREADME.md)
![image](https://img.shields.io/badge/PT-blue?link=.%2FLEIAME.md)

This repository serves as an example for implementing automatic [conventional commits](https://www.conventionalcommits.org/) in a project. It demonstrates how to streamline the commit message formatting and structure for better readability and automated versioning.

## Prerequisites

Before you begin, ensure you have met the following requirements:

1. You have created a `package.json` file for your project. If you haven't created one, you can initialize a new `package.json` file using one of the following commands:
    ```bash
    npm init -y
    # or
    yarn init -y
    ```
2. You have Git installed. If not, you can download it [here](https://git-scm.com/downloads).
3. You have initialized a local Git repository. If you haven't initialized a Git repository yet, you can do so by executing the following command in your project directory:
    ```bash
    git init
    ```

## Configuration
You can adhere to a commit convention and also (if you want) add interactivity to your `git commit` command.

### Adhere to a commit convention
Here, you're gonna need some dependencies ([commitlint](https://github.com/conventional-changelog/commitlint) and [husky](https://github.com/typicode/husky)), set them up and add the `commit-msg` [hook](https://git-scm.com/docs/githooks#_commit_msg).

1. Install the commitlint dependencies:
    ```bash
    npm install -D @commitlint/config-conventional @commitlint/cli
    # or
    yarn add -D @commitlint/config-conventional @commitlint/cli
    ```
2. Configure commitlint to use conventional config:
    ```bash
    echo "module.exports = { extends: ['@commitlint/config-conventional'] };" > commitlint.config.js
    ```
3. Install husky:
    ```bash
    npm install -D husky
    # or
    yarn add -D husky
    ```
4. Activate [git hooks](https://git-scm.com/docs/githooks):
    ```bash
    npx husky install
    # or
    yarn husky install
    ```
5. Add the `commit-msg` hook:
    ```bash
    npx husky add .husky/commit-msg  'npx --no -- commitlint --edit ${1}'
    ```

If you're facing any configuration errors, check the [commitlint guide](https://commitlint.js.org/#/guides-local-setup).<br/>
It's done! Now you can try to commit some new changes (you might want to check the conventional commits specification [here](https://www.conventionalcommits.org/)):
```bash
git commit -m "some new message" # ❌ this will fail
git commit -m "foo: some new message" # ❌ this will fail
git commit -m "feat: some new message" # ✅ this won't fail
```
![image](https://github.com/victorbadaro/automatic-conventional-commits-example/assets/9096344/20cd75a6-9f71-49fd-930d-6faf0b0c6a0d)

### Add interactivity to your `git commit` command
1. Install [commitizen](https://github.com/commitizen/cz-cli):
    ```bash
    npm install -D commitizen
    # or
    yarn add -D commitizen
    ```
2. Make your repo commitizen friendly:
    ```bash
    npx commitizen init cz-conventional-changelog --save-dev --save-exact
    # or
    yarn commitizen init cz-conventional-changelog --yarn --dev --exact
    ```
3. Add the `prepare-commit-msg` [hook](https://git-scm.com/docs/githooks#_prepare_commit_msg):
    ```bash
    npx husky add .husky/prepare-commit-msg  'exec < /dev/tty && node_modules/.bin/cz --hook || true'
    ```
https://github-production-user-asset-6210df.s3.amazonaws.com/9096344/281865977-82a54c18-9dd3-4a42-af80-056a0631fa61.mp4