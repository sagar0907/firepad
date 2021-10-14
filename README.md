## Usage

### Public API

Firepad takes two dependencies, one **Database Adapter** and one **Editor Adapter**, with a custom configuration object like the following:

```ts
import Firepad, { IDatabaseAdapter, IEditorAdapter, IFirepadConstructorOptions } from "@sagar0907/firepad";

const databaseAdapter: IDatabaseAdapter = ...; // Database Adapter instance

const editorAdapter: IEditorAdapter = ...; // Editor Adapter instance

const options: IFirepadConstructorOptions = {
   /** Unique Identifier for current User */
  userId: ..., // string or number
  /** Unique Hexadecimal color code for current User */
  userColor: ..., // string
  /** Name/Short Name of the current User (optional) */
  userName: ..., // string
  /** Default content of Firepad (optional) */
  defaultText: ..., // string
};

const firepad = new Firepad(databaseAdapter, editorAdapter, options);
```

### Monaco as editor

If you use Monaco as an editor, we have an shorthand function `fromMonaco` to provide adapters and the binding out of the box with optional configuration object:

```ts
import { fromMonaco } from "@sagar0907/firepad";

const databaseRef: string | firebase.database.Reference = ...; // Path to Firebase Database or a Reference Object

const editor: monaco.editor.IEditor = ...; // Monaco Editor Instance

const firepad = fromMonaco(databaseRef, editor);
```

### Writing Custom Adapters

To use Firepad with any other Editor, one simply need to write an implementation of Editor Adapter interface for that editor. This can be done like this:

```ts
import { IEditorAdapter } from "@sagar0907/firepad";

class MyEditorAdapter implements IEditorAdapter {
  ...
}
```

Similar thing can be done for Database as well by implementing `IDatabaseAdapter` interface. Keep in mind, you might also need to implement event handlers and event triggers depending upon nature of the adapters.

### Dispose

After Firepad usecase is over, it is recommended to cleanup all the resources (e.g., memory, network etc.) using `dispose()` method. Note that, making any further API call after calling `dispose()` will result into error.

```ts
...

const firepad = new Firepad(databaseAdapter, editorAdapter, options);

...

firepad.dispose();
```

## Development

We have used [`yarn`](https://yarnpkg.com/) as our package manager through out the project.

We use [`webpack-dev-server`](https://webpack.js.org/configuration/dev-server/) for local development environment and [`webpack`](https://webpack.js.org/api/) for bundling. After installing all the dependencies including all the devDependencies and updating Database (Firebase) configuration, just do `yarn start` to kickoff development server. By default, the dev server opens in `localhost:9000` but this can be configured by passing additional `--port` argument to the start command.

We use [`jest`](https://jestjs.io/docs) as both test runner and test suite to write unit tests. Doing `yarn test` should run all the testcases and publish coverage report.

### Directories

1. [`examples`](examples) - All the working examples are kept and used for manual testing during development.
2. [`src`](src) - Source directory for all the modules.
3. [`test`](test) - Specs directory for all the modules.

## Changelog

See [CHANGELOG](CHANGELOG.md) for more details.

## Contributing

See [CONTRIBUTING GUIDELINES](.github/CONTRIBUTING.md) for more details.

## License

See [LICENSE](LICENSE) for more details.
