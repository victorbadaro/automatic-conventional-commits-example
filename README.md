# automatic-conventional-commits-example
An example of how to set a repo to use conventional commits automatically

1. Create a `package.json` file:
    ```bash
    yarn init -y
    ```
---
2. Install the [commitlint](https://github.com/conventional-changelog/commitlint) dependencies:
    ```bash
    yarn add -D @commitlint/config-conventional @commitlint/cli
    ```
3. Configure commitlint to use conventional config:
    ```bash
    echo "module.exports = { extends: ['@commitlint/config-conventional'] };" > commitlint.config.js
    ```
4. Install [husky](https://github.com/typicode/husky):
    ```bash
    yarn add -D husky
    ```
5. Activate [git hooks](https://git-scm.com/docs/githooks):
    ```bash
    yarn husky install
    ```
6. Add the `commit-msg` [hook](https://git-scm.com/docs/githooks#_commit_msg):
    ```bash
    npx husky add .husky/commit-msg  'npx --no -- commitlint --edit ${1}'
    ```
---
7. Install [commitizen](https://github.com/commitizen/cz-cli):
    ```bash
    yarn add -D commitizen
    ```
8. Make your repo Commitizen friendly:
    ```bash
    yarn commitizen init cz-conventional-changelog --yarn --dev --exact
    ```
9. Add the `prepare-commit-msg` [hook](https://git-scm.com/docs/githooks#_prepare_commit_msg):
    ```bash
    npx husky add .husky/prepare-commit-msg  'exec < /dev/tty && node_modules/.bin/cz --hook || true'
    ```