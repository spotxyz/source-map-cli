# Fork changes

You can customize the HTTP request made when retrieving remote files. If `~/.source-map-cli.json` exists and contains a key matching the origin of the URL then you can add headers to the request.

Example:

```json
{
  "https://example.com": {
    "headers": {
      "Cookie": "session=0123456789abcdef"
    }
  }
}
```

Other changes:

- Automatically adds `.map` to the path/URL if missing.
- Line and column information can be passed in the same argument as the URL (common stacktrace format), e.g. `https://example.com/js/main.js.map:1:22012`

Install fork with:

```
npm install -g git+https://github.com/spotxyz/source-map-cli.git
```

Verify you are using the new version:

```
$ source-map --version
1.0.2
```

# Source-map CLI

Command-line interface to the [`source-map`](https://github.com/mozilla/source-map) module.

```bash
npm install --global source-map-cli
```

## Usage

The tool accepts [`source-map`](https://github.com/mozilla/source-map) commands to operate with source maps.

### `resolve [options] <uri> <line> <column>`

The `resolve` command accepts a source map (either a path or a URL), a line and column and returns the original source file name, line and column, along with a context (usually the name of the variable or function).

```
$ source-map resolve bundle.js.map 1 28
Maps to source.js:2:10 (baz)

   return baz(bar);
          ^
```

#### Context

Additional lines of context can be shown by including the `--context [num]` option.

#### Column marker

It is possible to prevent the column marker to be shown with the `--no-marker` option.
