<h1 align="center">TrashMD Plugins</h1>
<p align="center"><strong>The community plugin library for <a href="https://github.com/TrashBash/Trash-MD">TrashMD</a>.</strong></p>
<p align="center">
  Installable <code>.tmdplugin</code> scripts that show up in the in-program Plugin Browser.
</p>

<p align="center">
  <a href="#what-is-this">What is this?</a> •
  <a href="#how-trashmd-uses-this-repo">How TrashMD uses it</a> •
  <a href="#repository-layout">Layout</a> •
  <a href="#registry-format">Registry format</a> •
  <a href="#included-plugins">Included plugins</a> •
  <a href="#contributing">Contributing</a>
</p>

---

## What is this?

This repository is the remote plugin library that TrashMD's **Plugin Browser**
reads from. Each plugin is a `.tmdplugin` script (Catspeak/GMLspeak) that extends
the editor with custom commands, context-menu entries, importers/exporters,
event hooks and more. Every plugin is indexed by a single [`registry.json`](registry.json)
at the repository root.

---

## How TrashMD uses this repo

TrashMD reads from this repository over the GitHub API at runtime:

- It fetches [`registry.json`](registry.json) from the **`main`** branch.
- For each plugin, it downloads the `download_path` script when the user installs
  it, and loads the optional `image` for the browser thumbnail.

Because the app reads the `main` branch, **only content merged into `main`
appears in the live Plugin Browser.** Open changes as pull requests against
`main`.

For the plugin scripting API itself (permissions, commands, lifecycle), see the
[Plugin Guide](https://github.com/TrashBash/TrashMD-MD/blob/main/docs/guide.md)
in the main TrashMD repository.

---

## Repository layout

```
.
├── registry.json                 # Index of every published plugin
└── <plugin_id>/
    ├── __main__.tmdplugin         # The plugin entry script
    └── <preview>.png              # Optional thumbnail shown in the browser
```

One directory per plugin, named after the plugin `id`. The entry script must be
named `__main__.tmdplugin`.

---

## Registry format

`registry.json` is a single object with a `version` and a `plugins` array.
Each plugin entry looks like:

```json
{
  "id": "material_clipboard",
  "name": "Material Clipboard",
  "description": "Copy material properties from one material asset and paste them onto another.",
  "version": "1.0.0",
  "author": "TrashBash",
  "download_path": "material_clipboard/__main__.tmdplugin",
  "image": "material_clipboard/preview.png"
}
```

| Field | Required | Description |
|---|:---:|---|
| `id` | ✅ | Unique identifier. Also the folder name. |
| `name` | ✅ | Display name shown in the browser. |
| `description` | ✅ | One line summary shown in the browser. |
| `version` | ✅ | Plugin version string. |
| `author` | ✅ | Who made the plugin. |
| `download_path` | ✅ | Repo-relative path to the `__main__.tmdplugin` script. |
| `image` | — | Optional repo-relative path to a preview image. |

---

## Included plugins

| Plugin | What it does |
|---|---|
| **Material Clipboard** | Copy material properties from one material asset and paste them onto another. |
| **Quick Transform** | Reset position, rotation, or scale on selected nodes. |
| **Unused Asset Cleane** | Find and report unused assets in the project. Models, materials, and textures not referenced in the scene. |

These also serve as worked examples for authoring your own plugins.

---

## Contributing

Want to publish a plugin? See [CONTRIBUTING.md](CONTRIBUTING.md) for the
submission checklist and a step-by-step walkthrough.

---

## License

Released under the [MIT License](LICENSE).
