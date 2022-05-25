# WSL 配置前端开发环境

#basic

>使用debian系统

### 安装aptitude
```
sudo apt-get update
sudo apt-get install aptitude
```
### 安装git
```
sudo aptitude install git
```
配置git
```
git config --global user.name "Your Name"
git config --global email "you@your-domain.com"
git config --global alias.lg "log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit"
```

### 安装nvm
```
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.2/install.sh | bash
```
最新的发行版本号参考https://github.com/nvm-sh/nvm/releases

### 安装node
```
nvm install node
```
### 安装nrm
```
npm install -g nrm
```
### 安装starship
https://starship.rs/zh-CN/

### 安装vscode
https://code.visualstudio.com/Download

### 安装vscode插件
```
Remote-SSH
Remote-Containers
Remote-WSL
Remote-Development
Night Owl
GitLens
Better Comments
Import Cost
Auto Rename Tag
Auto Close Tag
ES7+ React/Redux/React-Native snippets
VSCode React Refactor
Live Server
Path Intellisense
Prettier ESLint
Todo Tree
dependency cruiser extension
foam
markdown all in one
```

JSON setting
```json
{
    "files.eol": "\n",
    "[markdown]": {
        "editor.quickSuggestions": true
    },
    "workbench.list.smoothScrolling": true,
    "editor.smoothScrolling": true,
    "todo-tree.general.tags": [
        "BUG",
        "HACK",
        "FIXME",
        "TODO",
        "FEAT",
        "[ ]",
        "[x]"
    ],
    "todo-tree.regex.regex": "(//|#|<!--|;|/\\*|^|^\\s*(-|\\d+.))\\s*($TAGS)",
    "todo-tree.highlights.useColourScheme": true,
    "explorer.confirmDelete": false,
    "emmet.triggerExpansionOnTab": true,
    "editor.tabSize": 2,
    "javascript.updateImportsOnFileMove.enabled": "always",
    "editor.renderControlCharacters": true,
    "emmet.syntaxProfiles": {
        "vue-html": "html",
        "vue": "html"
    },
    "emmet.includeLanguages": {
        "javascript": "javascriptreact",
        "wxml": "html"
    },
    "typescript.updateImportsOnFileMove.enabled": "always",
    "search.followSymlinks": false,
    "files.exclude": {
        // 是否显示这些文件(夹)
        "**/.git": true,
        "**/.svn": true,
        "**/.hg": true,
        "**/CVS": true,
        "**/.DS_Store": true,
        "**/tmp": true,
        // "**/node_modules": true,
        "**/bower_components": true
        // "**/dist": true
    },
    "search.exclude": {
        // 搜索的时候排除的文件夹，视情况开启
        // "**/node_modules": false,
    },
    "files.watcherExclude": {
        "**/.git/objects/**": true,
        "**/.git/subtree-cache/**": true,
        "**/node_modules/**": true,
        "**/tmp/**": true,
        "**/bower_components/**": true,
        "**/dist/**": true
    },
    "files.autoSave": "onFocusChange",
    "js/ts.implicitProjectConfig.experimentalDecorators": true,
    "workbench.iconTheme": "material-icon-theme",
    "workbench.settings.editor": "json",
    "window.zoomLevel": 1,
    "diffEditor.ignoreTrimWhitespace": false,
    "security.workspace.trust.untrustedFiles": "open",
    "gitlens.hovers.currentLine.over": "line",
    "liveServer.settings.donotShowInfoMsg": true,
    "editor.fontFamily": "Noto Sans Mono",
    "files.trimTrailingWhitespace": true,
    "workbench.colorTheme": "Night Owl",
    "workbench.startupEditor": "none",
    "workbench.statusBar.visible": true,
    "workbench.editor.restoreViewState": true,
    "editor.fontSize": 14,
    "editor.insertSpaces": true,
    "editor.detectIndentation": false,
    "editor.renderWhitespace": "none",
    "editor.scrollBeyondLastLine": true,
    "editor.minimap.enabled": false,
    "editor.find.seedSearchStringFromSelection": "never",
    // syntax highlighting
    "files.associations": {
        ".env*": "makefile"
    },
    "editor.formatOnSave": false,
    "[javascript]": {
        "editor.formatOnSave": true,
        "editor.defaultFormatter": "rvest.vs-code-prettier-eslint"
    },
    "[javascriptreact]": {
        "editor.formatOnSave": true,
        "editor.defaultFormatter": "rvest.vs-code-prettier-eslint"
    },
    "[typescript]": {
        "editor.formatOnSave": true,
        "editor.defaultFormatter": "rvest.vs-code-prettier-eslint"
    },
    "[typescriptreact]": {
        "editor.formatOnSave": true,
        "editor.defaultFormatter": "rvest.vs-code-prettier-eslint"
    },
    // eslint
    "editor.codeActionsOnSave": {
        "source.fixAll.eslint": true
    },
    // auto generated
    "explorer.confirmDragAndDrop": false,
    "js/ts.implicitProjectConfig.checkJs": true
}
```
### 安装edge
edge扩展
```
AdBlock — 最佳广告拦截工具
Allow CORS: Access-Control-Allow-Origin
Chrono Download Manager
Dark Reader
Gitako - GitHub file tree
RSSHub Radar
User-Agent Switcher and Manager
Vue.js devtools
沙拉查词-聚合词典划词翻译
React Developer Tools
Unsplash Instant
XSwitch
tweak: mock and modify HTTP requests
```
### 安装graphviz
```
sudo aptitude install graphviz
```