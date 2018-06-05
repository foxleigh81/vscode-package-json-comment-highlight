VSCODE-JSON-COMMENTS-HIGHLIGHT
===

[![License: MIT](https://img.shields.io/badge/License-MIT-brightgreen.svg)](https://opensource.org/licenses/MIT) [![Build Status]

Highlight `\\` key comments in JSON files:

e.g.

```json
{
    "\\": "This is a good way to add a comment"
}
```

*NOTICE*

Credit for the base of this package goes to github user [wayou](https://github.com/wayou) as it is forked from his [TODO highlighter package](https://github.com/wayou/vscode-todo-highlight)


### Config- TODO: REWRITE THE BELOW

`TODO:`,`FIXME:` are built-in keywords. You can override the look by customizing the setting.

To customize the keywords and other stuff, <kbd>command</kbd> + <kbd>,</kbd> (Windows / Linux: File -> Preferences -> User Settings) open the vscode file `settings.json`.

| | type | default | description |
|---|---|---|---|
| todohighlight.isEnable | boolean | true | Toggle the highlight, default is true. |
| todohighlight.isCaseSensitive  | boolean | true | Whether the keywords are case sensitive or not. |
| todohighlight.keywords | array | N/A | An array of keywords that will be hilighted. You can also specify the style for each keywords here. See example below for more infomation. |
| todohighlight.keywordsPattern  | string | N/A | Specify keywords via RegExp instead of `todohighlight.keywords` one by one. NOTE that if this presents, `todohighlight.keywords` will be ignored. And REMEMBER to escapse the back slash if there's any in your regexp (using \\ instead of signle back slash). |
| todohighlight.defaultStyle | object | N/A | Specify the default style for custom keywords, if not specified, build in default style will be applied. [See all available properties on VSCode doc DecorationRenderOptions section](https://code.visualstudio.com/docs/extensionAPI/vscode-api) |
| todohighlight.include | array | [<br>`"**/*.js"`,<br>`"**/*.jsx"`,<br>`"**/*.ts"`,<br>`"**/*.tsx",`<br>`"**/*.html"`,<br>`"**/*.php"`,<br>`"**/*.css",`<br>`"**/*.scss"`<br>] | Glob patterns that defines the files to search for. Only include files you need, DO NOT USE `{**/*.*}` for both permormance and avoiding binary files reason. <br> For backwards compatability, a string combine all the patterns is also valid `"{**/*.js,**/*.jsx,**/*.ts,**/*.tsx,**/*.html,**/*.php,**/*.css,**/*.scss}"` |
| todohighlight.exclude | array | [<br>`"**/node_modules/**"`,<br>`"**/dist/**",`<br>`"**/bower_components/**"`,<br>`"**/build/**",`<br>`"**/.vscode/**"`,<br>`"**/.github/**"`,<br>`"**/_output/**"`,<br>`"**/*.min.*"`,<br>`"**/*.map"`<br>] | Glob pattern that defines files and folders to exclude while listing annotations. <br> For backwards compatability, a string combine all the patterns is also valid `"{**/node_modules/**,**/bower_components/**,**/dist/**,**/build/**,**/.vscode/**,**/_output/**,**/*.min.*,**/*.map}"` |
| todohighlight.maxFilesForSearch | number | 5120 | Max files for searching, mostly you don't need to configure this. |
| todohighlight.toggleURI | boolean | false | If the file path within the output channel not clickable, set this to true to toggle the path patten between `<path>#<line>` and `<path>:<line>:<column>`. |


an example of customizing configuration:

```js
{
    "todohighlight.isEnable": true,
    "todohighlight.isCaseSensitive": true,
    "todohighlight.keywords": [
        "DEBUG:",
        "REVIEW:",
        {
            "text": "NOTE:",
            "color": "#ff0000",
            "backgroundColor": "yellow",
            "overviewRulerColor": "grey"
        },
        {
            "text": "HACK:",
            "color": "#000",
            "isWholeLine": false,
        },
        {
            "text": "TODO:",
            "color": "red",
            "border": "1px solid red",
            "borderRadius": "2px", //NOTE: using borderRadius along with `border` or you will see nothing change
            "backgroundColor": "rgba(0,0,0,.2)",
            //other styling properties goes here ... 
        }
    ],
    "todohighlight.keywordsPattern": "TODO:|FIXME:|\\(([^)]+)\\)", //highlight `TODO:`,`FIXME:` or content between parentheses
    "todohighlight.defaultStyle": {
        "color": "red",
        "backgroundColor": "#ffab00",
        "overviewRulerColor": "#ffab00",
        "cursor": "pointer",
        "border": "1px solid #eee",
        "borderRadius": "2px",
        "isWholeLine": true,
        //other styling properties goes here ... 
    },
    "todohighlight.include": [
        "**/*.js",
        "**/*.jsx",
        "**/*.ts",
        "**/*.tsx",
        "**/*.html",
        "**/*.php",
        "**/*.css",
        "**/*.scss"
    ],
    "todohighlight.exclude": [
        "**/node_modules/**",
        "**/bower_components/**",
        "**/dist/**",
        "**/build/**",
        "**/.vscode/**",
        "**/.github/**",
        "**/_output/**",
        "**/*.min.*",
        "**/*.map",
        "**/.next/**"
    ],
    "todohighlight.maxFilesForSearch": 5120,
    "todohighlight.toggleURI": false
}
```

### Commands

This extension contributes the following commands to the Command palette.

- `Toggle highlight` : turn on/off the highlight
![](https://github.com/wayou/vscode-todo-highlight/raw/master/assets/toggle-highlight.gif)
- `List highlighted annotations` : list annotations and reveal from corresponding file
![](https://github.com/wayou/vscode-todo-highlight/raw/master/assets/list-annotations.gif)


### Known issue

 The clickable file pattern within the output channel differs from OS platform(`<path>#<line>` for Mac/Windows and `<path>:<line>:<column>` for Linux, for details see this [issue](https://github.com/Microsoft/vscode/issues/586) ). 

 Basically the extension auto detects the OS platform.

 If you find that the file path is not clickable, set `todohighlight.toggleURI` to `true` to toggle the file pattern.
  
