# Contributing to TrashMD Plugins

This repository is the library that TrashMD's
in-program Plugin Browser reads from, so additions go through pull requests against
the `main` branch.

## Submitting a plugin

1. **Create a folder** named after your plugin id, e.g. `my_plugin/`.
2. **Add the entry script**. Place your plugin code in
   `my_plugin/__main__.tmdplugin`. The script must start with an `@plugin`
   header block (see below).
3. **(Optional) Add a preview** — include a thumbnail image in the same folder
   and reference it from the registry entry.
4. **Register it**. Add an entry to [`registry.json`](registry.json) in the
   `plugins` array.
5. **Open a pull request** against `main`.

### Plugin header block

Every `__main__.tmdplugin` starts with a metadata block that declares the
permissions it needs:

```js
/*
@plugin
name: My Plugin
description: A short, one-line description.
version: 1.0.0
author: your-name
permissions: core, commands, context, filesystem
*/
```

Request only the permissions your plugin actually uses. For the full scripting
API, lifecycle (`register` / `unregister`), and permission reference, see the
[Plugin Guide](https://github.com/TrashBash/Trash-MD/blob/main/docs/guide.md)
in the main TrashMD repository.

### Example registry entry

```json
{
  "id": "my_plugin",
  "name": "My Plugin",
  "description": "A short, one-line description.",
  "version": "1.0.0",
  "author": "your-name",
  "download_path": "my_plugin/__main__.tmdplugin",
  "image": "my_plugin/preview.png"
}
```

See the [Registry format](README.md#registry-format) section of the README for
the full field reference.

## Checklist

Before opening your PR, confirm:

- [ ] `id` is unique and matches the folder name.
- [ ] The entry script is named `__main__.tmdplugin` and has a `@plugin` header.
- [ ] The header `name` / `version` / `author` match the `registry.json` entry.
- [ ] The plugin requests only the permissions it needs.
- [ ] `download_path` (and `image`, if present) use correct repo-relative paths
      with forward slashes.
- [ ] `registry.json` is still valid JSON (no trailing commas).
- [ ] The plugin is yours to share, or appropriately licensed for redistribution.

## Reporting a problem

If a plugin fails to download or misbehaves, open an issue using the
**Plugin issue** template.
