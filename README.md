# Prettier Plugin: Sort imports

A prettier plugin that sorts import statements by either their length or alphabetically.

Example:
![](./images/transform.png)

## Installation

```sh
npm install --save-dev prettier-plugin-sort-imports
```

## Usage

The plugin will be loaded by Prettier automatically. No configuration needed. It will sort by import statement length by default.

### Options:

-   `sortingMethod`: `'alphabetical' | 'lineLength' (default)` - What to sort the individual lines by. `alphabetical` sorts by the import path and `lineLength` sorts by the length of the import. Note that alphabetical sorting looks at the **whole** import path, so imports starting with `../` are ranked lower.
-   `sortingOrder`: `'ascending' | 'descending' (default)` -  Determines the order of imports. If set to 'ascending', imports will be sorted in ascending order, whereas if set to 'descending', they will be sorted in descending order
-   `stripNewlines`: `true | false (default)`. Determines whether newlines between blocks of imports are stripped. If the only thing between two blocks is whitespace or comments, the whitespace will be stripped and the blocks are sorted as one big one. The comment sticks to whichever import it was above initially.
-   `importTypeOrder`: `('NPMPackages' | 'localImportsValue' | 'localImportsType' | 'localImports' | 'all')[]`. An array that determines the order in which different import types are sorted. The default is `['all']`, which does no sorting of different import types. Import type are sorted according to the order in which they appear in this array. Note that, other than the `'all'` type, you can not specify an imcomplete array. See different types for which other types they can be combined with. Explanations of different types:
    -   `'NPMPackages'`: All NPM packges that are listed in your `package.json` fall into this category. If you have multiple `package.json` files you can specify them using the `packageJSONFiles` option. Can only be used with one of the other local import types (either `'localImportsValue', 'localImportsType' `or` 'localImports'`)
    -   `'localImportsValue'`: All local imports that are declared with a value `import foo from './foo'` falls into this category. Can only be used if `NPMPackages` is also specified and if `localImportsType` is also specified.
    -   `'localImportsType'`: All local imports that are imported as a type. `import type foo from './foo'` falls into this category. Only available in typecript. Can only be used if `NPMPackages` is also specified and if `localImportsValue` is also specified.
    -   `'localImports'`: All local imports that are declared with a value or a type. `import foo from './foo'` and `import type foo from './foo'` both fall into this category. Can only be used if `NPMPackages` is also specified.
    -   `'all'`: All imports fall into this category.
-   `packageJSONFiles`: `string[]`. Set to `['package.json']` by default. Lists the `package.json` files to be used for the `'NPMPackages'` import type. Note that if you specified `['all']` for the `importTypeOrder` option (or specified none at all), this is not used.
-   `newlineBetweenTypes`: `boolean`. Set to `false` by default. Determines whether a newline should be inserted between different import types.

Files containing the string `// sort-imports-ignore` are skipped. You can also ignore sections by using `// sort-imports-begin-ignore` and `// sort-imports-end-ignore`.

## Changelog

### 1.7.1

-   Move the `typescript` dependency to peer dependencies

### 1.7.0

-   Rewrite newline re-ordering to be more robust
