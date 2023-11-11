# automatic-conventional-commits-example
[![image](https://img.shields.io/badge/EN-blue)](./README.md)
[![image](https://img.shields.io/badge/PT-blue)](./LEIAME.md)

Este repositório serve como um exemplo para implementar o [conventional commits](https://www.conventionalcommits.org/) automaticamente em um projeto. Ele demonstra como otimizar a formatação e estrutura das mensagens de commit para uma melhor legibilidade e versionamento automatizado.

## Pré-requisitos

Antes de começar, certifique-se de atender aos seguintes requisitos:

1. Você criou um arquivo `package.json` para o seu projeto. Se ainda não o fez, você pode inicializar um novo arquivo `package.json` usando um dos seguintes comandos:
    ```bash
    npm init -y
    # or
    yarn init -y
    ```
2. Você tem o Git instalado. Se não tiver, você pode baixá-lo [aqui](https://git-scm.com/downloads).
3. Você inicializou um repositório Git local. Se ainda não o fez, você pode fazê-lo executando o seguinte comando no diretório do seu projeto:
    ```bash
    git init
    ```

## Configuração
Você pode aderir a uma convenção de commit e também (se desejar) adicionar interatividade ao seu comando `git commit`.

### Aderir a uma convenção de commit
Aqui, você precisará de algumas dependências ([commitlint](https://github.com/conventional-changelog/commitlint) e [husky](https://github.com/typicode/husky)), configure-as e adicione o [hook](https://git-scm.com/docs/githooks#_commit_msg) `commit-msg`.

1. Instale as dependências do commitlint:
    ```bash
    npm install -D @commitlint/config-conventional @commitlint/cli
    # or
    yarn add -D @commitlint/config-conventional @commitlint/cli
    ```
2. Configure o commitlint para usar a configuração convencional:
    ```bash
    echo "module.exports = { extends: ['@commitlint/config-conventional'] };" > commitlint.config.js
    ```
3. Instale o husky:
    ```bash
    npm install -D husky
    # or
    yarn add -D husky
    ```
4. Ative os [git hooks](https://git-scm.com/docs/githooks):
    ```bash
    npx husky install
    # or
    yarn husky install
    ```
5. Adicione o hook `commit-msg`:
    ```bash
    npx husky add .husky/commit-msg  'npx --no -- commitlint --edit ${1}'
    ```
Se você não quiser executar o passo 4 (`npx husky install` ou `yarn husky install`) toda vez que clonar o seu repositório, inclua o script `prepare` no seu `package.json` e ele será executado automaticamente toda vez que você executar o comando para instalar as dependências do seu projeto (por exemplo: `npm install` ou `yarn`):
```json
"scripts": {
  "prepare": "husky install" 
}
```

Se você estiver enfrentando algum erro de configuração, verifique o [guia do commitlint](https://commitlint.js.org/#/guides-local-setup).<br/>
Está pronto! Agora você pode tentar commitar algumas novas alterações (você pode querer verificar a especificação do _conventional commits_ [aqui](https://www.conventionalcommits.org/)):
```bash
git commit -m "some new message" # ❌ falhará
git commit -m "foo: some new message" # ❌ falhará
git commit -m "feat: some new message" # ✅ não falhará
```
![image](https://github.com/victorbadaro/automatic-conventional-commits-example/assets/9096344/20cd75a6-9f71-49fd-930d-6faf0b0c6a0d)

### Adicione interatividade ao teu comando `git commit`:
1. Instale o [commitizen](https://github.com/commitizen/cz-cli):
    ```bash
    npm install -D commitizen
    # or
    yarn add -D commitizen
    ```
2. Torne o seu repositório _commitizen friendly_:
    ```bash
    npx commitizen init cz-conventional-changelog --save-dev --save-exact
    # or
    yarn commitizen init cz-conventional-changelog --yarn --dev --exact
    ```
3. Adicione o [hook](https://git-scm.com/docs/githooks#_prepare_commit_msg) `prepare-commit-msg`:
    ```bash
    npx husky add .husky/prepare-commit-msg  'exec < /dev/tty && node_modules/.bin/cz --hook || true'
    ```
https://github-production-user-asset-6210df.s3.amazonaws.com/9096344/281865977-82a54c18-9dd3-4a42-af80-056a0631fa61.mp4