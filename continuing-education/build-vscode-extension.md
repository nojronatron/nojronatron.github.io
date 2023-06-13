# Build VSCode Extension

This document will store my experiences learning about, and interacting with the process of building a VSCode Extension.

## Goals

At the end of this experience, I hope to have learned the following:

1. Minimum requirements to build an extension.
2. About the development process.
3. How to test the extension.
4. Extension publication.
5. Supporting the extension going forward.

In addition, I am challenging myself to complete the following:

1. Build an extension that I will use.
2. Develop short videos and/or sequenced screenshots demonstrating its use.
3. Publish the extension to VSCode Marketplace.
4. Add this to my portfolio.

## Planning

- [x] Read up on how Extensions are built.
- [x] Create an exploratory project to experiment with.
- [x] Develop the MVP feature target.
- [x] Develop functions that implement the features.
- [ ] Implement tests to validation functionality for MVP.
- [ ] Design walk-throughs and pix/video for publication.
- [ ] Design stellar documentation.
- [ ] Consider ongoing support and/or feedback options for user-driven improvement.

## Learning How To Build Extensions

### New Project

Yeoman: Aka "yo". VSCode Extension Generator. Enables creating new:

- JS or TS Extension.
- Color Theme.
- Language Support.
- Code Snippets.
- Keymapping.
- Extension Pack.
- Language Pack (Localization).
- Web Extension (TS).
- Notebook Renderer (TS).

Yeoman supports NPM, Yarn, and PNPM.

1. Set up dependencies: `npm install -g yo generator-code`.
2. Set up the project: `yo code`
3. Respond to questions.
4. CD to the new project.
5. Update package.json (see below).
6. Start coding!

Update Package.json:

- Name.
- Display Name.
- Project description.
- Version (as updates are made).

### Debug in Special VSCode Instance

1. Save changes.
2. Press [F5]. This launches the Extension Development Host.
3. Open a file or target folder location if necessary.
4. Open the Command Palette (Press CTRL + SHIFT + P).
5. Type the name of the command as indicated in Package.json as the Command Title.

### Reloading After Making Code Changes

1. Launch the Extension Development Host.
2. Make changes to your code in the VS Code instance that is in "Run and Debug" mode.
3. Save code changes.
4. Open the Command Palette in Ext Dev Host.
5. Type 'Developer: Reload Window'.

Newly saved code is now running.

### Notes While Learning

Build Development Host is a live build+run version of VSCode using the Extension code in the parent VSCode instance from 'Run Extension' (F5) command.

Naming a Command requires editing package.json: 'contributes:commands:command:' and 'contributes:commands:title'. This is different than naming the Extension Project (top of Package.json 'name' and 'displayName' KVPs).

VSCode Commands follow a disposable pattern:

1. Code within the `activate(context: vscode.ExtensionContext)` method.
2. Create a variable as a result of `vscode.commands.registerCommand()` with the package.json command name followed by a lambda that executes a function or code block.
3. At the end of the `activate()` function, call `context.subscriptions.push(disposable_variable_from_step2)`.

Live Debugging is supported! Use breakpoints and view in-execution variable values just like any other code.

Async-Await and Promises are supported [example code source](https://github.com/microsoft/vscode-extension-samples/blob/main/notebook-serializer-sample/src/extension.ts).

```typescript
// the following code was copied on 7-June-23 from github.com/microsoft/vscode-extension-samples
import * as vscode from 'vscode';
import { SampleKernel } from './controller';
import { SampleContentSerializer } from './serializer';

const NOTEBOOK_TYPE = 'test-notebook-serializer';

export function activate(context: vscode.ExtensionContext) {
  context.subscriptions.push(
    vscode.commands.registerCommand(
      'notebook-serializer-sample.createJsonNotebook',
      // ASYNC
      async () => {
        const language = 'json';
        const defaultValue = `{ "hello_world": 123 }`;
        const cell = new vscode.NotebookCellData(
          vscode.NotebookCellKind.Code,
          defaultValue,
          language
        );
        const data = new vscode.NotebookData([cell]);
        data.metadata = {
          custom: {
            cells: [],
            metadata: {
              orig_nbformat: 4,
            },
            nbformat: 4,
            nbformat_minor: 2,
          },
        };
        const doc = await vscode.workspace.openNotebookDocument(
          NOTEBOOK_TYPE,
          data
        );
        // AWAIT
        await vscode.window.showNotebookDocument(doc);
      }
    )
  );

  context.subscriptions.push(
    vscode.workspace.registerNotebookSerializer(
      NOTEBOOK_TYPE,
      new SampleContentSerializer(),
      { transientOutputs: true }
    ),
    new SampleKernel()
  );
}
```

Cancellation Tokens: The last parameter of a function call (optional). Use `isCancellationRequested` to check if canceled, or register for notifications via `onCancellationRequested`. A Cancellation Token will be valid on events that cause an API call to become obsolete. For example: During an API Call the user types more characters, so a new API call could be made with more up-to-date context and data.

Events are exposed as Functions. Use the Listener Pattern (example below) to subscribe to Events. Return a Disposable so the Event Listener can be removed. From [vscode api patterns documentation](https://code.visualstudio.com/api/references/vscode-api#api-patterns): '...an event fired when the active text editor (noun) has been (onDid) changed (verb)'

```typescript
// Event Listener Pattern from code.visualstudio.com
var listener = function (event) {
  console.log('It happened', event);
};

// start listening using 'onWillVerbNoun' and 'onDidVerbNoun' terminology
var subscription = fsWatcher.onDidDelete(listener);

// do stuff
// ...

// stop listening
subscription.dispose();
```

### Command WHEN and ENABLEMENT

Commands can be hidden until a `when clause` returns true, for example: Only show the command when the editor language is markdown:

```json
{
  "contributes": {
    "menus": {
      "commandPallete": [
        {
          "command": "markdowntocer:markdownTOCer",
          "title": "Markdown TOCer",
          "when": "editorLangId == markdown"
        }
      ]
    }
  }
}
```

When a command is showing (when clause returns true), the `enablement` allows use of the command, perhaps when a cursor is over a line of text.

Example (from API Guides) of storing a value to use with a `when` clause to check if number of cool open things is greater than 2:

```typescript
vscode.commands.executeCommand('setContext', 'myExtension.showMyCommand', true);
vscode.commands.executeCommand(
  'setContext',
  'myExtension.numberOfCoolOpenThings',
  4
);
```

### Localization

Namespace for localization-related functionality is `l10n` and must be definied in Extension Manifest and have `bundle.l10n.json` files included. Does not apply to built-in Extensions like GitHub Authentication, Git, some Language Features, etc.

### Extension Anatomy

- Action Event: Registers command so Extension becomes active when command is called. Example: `onCommand:helloworld.helloWorld`
- Contribution Point: Static declarations from Package.json that make commands available to the Command Palette. Example `contribues.commands`.
- VS Code API: JS APIs enabling invokation of custom (extension) code. Binds function to registered command ID. Example `commands.regsiterCommand` and `helloworld.helloWorld`.
- package.json: The Extension Manifest. There is a full [reference](https://code.visualstudio.com/api/references/extension-manifest) to all the possible fields.
- Activate method: This is called when VSCode activates your Extension successfully from the Manifest.
- Deactivate method: Add 'cleanup' code here that must be executed before the Extension is unloaded by VSCode. Also used to 'disable' or 'uninstall' the Extension.
- VSCode API Extension definitions e.g. `@types/vscode`: See Package.json, 'engines:vscode'. These provide IntelliSense and commands like 'Go to definition', etc to the Extension code.

Check out [Extension Anatomy Documentation](https://code.visualstudio.com/api/get-started/extension-anatomy) for up-to-date info.

### Language Server

Program analyzes project to provide dynamic features.

Example: `typescript-language-features` utilizes TS Language Service to offer features like Hover Info, Auto Completion, Formatting, etc.

LSP: Language Server Protocol

- A static code analysis tool.
- Allows writing one code analysis program that will apply to multiple editors (VSCode, Aton, etc).

[Language Server Extension Guide](https://code.visualstudio.com/api/language-extensions/language-server-extension-guide)

### Providers

- Code Action: The little light-bulb that appears when a cursor is placed on a line that has an associated action. Asks the user to select 'Quick Fix' or 'More Actions' and applies the suggested action.

### Testing Extensions

VSCode Documentation on [Testing Extensions](https://code.visualstudio.com/api/working-with-extensions/testing-extension).

Requirements:

- Environment variables.
- Special Import(s).
- Test Runner Script.
- Use VSCode Insiders Version (else integration tests could throw a show-stopping error).

Capabilities:

- Continuous Integration e.g. Azure DevOps!

### Electron

[Electron](https://code.visualstudio.com/api/working-with-extensions/testing-extension#migrating-from-vscode) is going to be the way to test VSCode Extensions going forward.

- Replaces `vscode` dependency.
- Instead of `engines.vscode: 1.3`, install `'@types/vscode': '^1.30.0'` to package.json dependencies.
- No longer requires `'postinstall': 'node ./node_modules/vscode/bin/install'` in package.json.
- If using TypeScript: Point `test` script in package.json to the compiled output of `runTest.ts`.
- A [test runner script](https://github.com/microsoft/vscode-extension-samples/blob/main/helloworld-test-sample/src/test/suite/index.ts) will be needed as a starting point.
- `mocha@4` and `glob` will need to be in devDependencies if the above steps were taken.

### Testing Extension in GitHub Actions

When targeting Linux in YAML, ensure `Xvfb` enabled environment is targeted, otherwise test will fail.

See GitHub Actions subsection in [Working With Extensions](https://code.visualstudio.com/api/working-with-extensions/continuous-integration).

### Publication via GitHub Actions

See GitHub Actions Automated Publishing subsection in [Working With Extensions](https://code.visualstudio.com/api/working-with-extensions/continuous-integration)

### Publishing

Define the `publisher` property in order to enable managing an Extension.

Publishing can be done 2 ways:

- Publish via CS Vode Extension Marketplace.
- Package into a VSIX format to share with other users.

Packaging tool: `vsce` the Visual Studio Code Extensions packaing and publishing tool.

1. Update the README.MD file (make it yours, make it stellar).
1. Run `npm install -g vsce` at the root of the project.
1. Open a MSFT account using Azure DevOps.
1. Create an Org in Azure DevOps.
1. Get Personal Access Token(s).
1. Set "All accessible organizations".
1. Set show all scopes and select "Marketplace: Manage".
1. Copy the Personal Access Token to a safe place.
1. Click Create.
1. Create a publisher using Manage Publishers & Extensions page in visualstudio.com.
1. Add name and ID and Create to make a new publisher. This must be unique in the Marketplace.
1. Login as the Publisher using `vsce login {publister_name_from_step_11}` and the Publisher Token captured previously.
1. Specify the Git Repository field in teh package.json.
1. Specify the publisher field in the root of package.json: `{ ..., "publisher": "{publisher_name_created_previously}", ...}`.
1. Publish the extension using `vsce publish`.

## References

[VSCode Extension Samples](https://github.com/microsoft/vscode-extension-samples)

[VSCode Extensions API](https://code.visualstudio.com/api/)

## Footer

Return to [Conted Index](./conted-index.html).

Return to [Root README](../README.html).
