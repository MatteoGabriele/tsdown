# Customizing Rolldown Options

`tsdown` uses [Rolldown](https://rolldown.rs) as its core bundling engine. This allows you to easily pass or override options directly to Rolldown, giving you fine-grained control over the bundling process.

For a full list of available Rolldown options, refer to the [Rolldown Config Options](https://rolldown.rs/reference/config-options) documentation.

## Overriding `inputOptions`

You can override the `inputOptions` generated by `tsdown` to customize how Rolldown processes your input files. There are two ways to do this:

### Using an Object

You can directly pass an object to override specific `inputOptions`:

```ts [tsdown.config.ts]
import { defineConfig } from 'tsdown'

export default defineConfig({
  inputOptions: {
    cwd: './custom-directory',
  },
})
```

In this example, the `cwd` (current working directory) option is set to `./custom-directory`.

### Using a Function

Alternatively, you can use a function to dynamically modify the `inputOptions`. The function receives the generated `inputOptions` and the current `format` as arguments:

```ts [tsdown.config.ts]
import { defineConfig } from 'tsdown'

export default defineConfig({
  inputOptions(inputOptions, format) {
    inputOptions.cwd = './custom-directory'
    return inputOptions
  },
})
```

This approach is useful when you need to customize options based on the output format or other dynamic conditions.

## Overriding `outputOptions`

The `outputOptions` can be customized in the same way as `inputOptions`. For example:

### Using an Object

You can directly pass an object to override specific `outputOptions`:

```ts [tsdown.config.ts]
import { defineConfig } from 'tsdown'

export default defineConfig({
  outputOptions: {
    comments: 'preserve-legal',
  },
})
```

In this example, the `comments: 'preserve-legal'` option ensures that legal comments (e.g., license headers) are preserved in the output files.

### Using a Function

You can also use a function to dynamically modify the `outputOptions`. The function receives the generated `outputOptions` and the current `format` as arguments:

```ts [tsdown.config.ts]
import { defineConfig } from 'tsdown'

export default defineConfig({
  outputOptions(outputOptions, format) {
    if (format === 'esm') {
      outputOptions.comments = 'preserve-legal'
    }
    return outputOptions
  },
})
```

This ensures that legal comments are preserved only for the `esm` format.

## When to Use Custom Options

While `tsdown` exposes many common options directly, there may be cases where certain Rolldown options are not exposed. In such cases, you can use the `inputOptions` and `outputOptions` overrides to directly set these options in Rolldown.

> [!TIP]
> Using `inputOptions` and `outputOptions` gives you full access to Rolldown's powerful configuration system, allowing you to customize your build process beyond what `tsdown` exposes directly.
