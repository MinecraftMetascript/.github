<p align="center">
  <a href="https://minecraftmetascript.github.io/mms/">
    <picture>
      <source media="(prefers-color-scheme: dark)" srcset="assets/logo-dark.svg">
      <img src="assets/logo-light.svg" alt="MMS Metascript" height="96">
    </picture>
  </a>
</p>

<p align="center">
  <b>A small language that compiles to Minecraft data packs.</b><br>
  One <code>.mms</code> file stands in for the dozens of JSON and <code>.mcfunction</code> files a feature needs.
</p>

<p align="center">
  <a href="https://minecraftmetascript.github.io/mms/"><b>Open the editor</b></a> ·
  <a href="https://minecraftmetascript.github.io/mms/docs">Docs</a> ·
  <a href="https://github.com/MinecraftMetascript/mms/releases/latest">Download</a> ·
  <a href="https://github.com/MinecraftMetascript/mms">Source</a>
</p>

---

Minecraft Metascript (MMS) covers the whole data pack: world generation (noise, density functions, surface rules, biomes, structures), loot tables, recipes, tags, predicates, advancements and functions. Functions get helpers for globals, variables and scoreboards, so you can write `found[@s] += 1` instead of a `scoreboard players` command. The checker knows every field of every resource in Minecraft Java Edition 26.3, so mistakes show up while you type instead of in the game log.

```
/** Gems that drop from the gem chest. */
ItemTag gems = [diamond, emerald, amethyst_shard]

LootTable chests/gems {
  pools = [Pool(1..3, #gems)]
}

Recipe gem_block = Shaped(["GG", "GG"], { G = #gems }, emerald_block)

Objective found = dummy

Function find {
  found[@s] += 1
  /loot give @s loot gems:chests/gems
  /tellraw @s "You have found ${found[@s]} gem chests"
}
```

`mms build` turns that into eight files (a tag, a loot table, a recipe, the functions and the scoreboard setup), ready to drop into a world.

### Get started

| | |
| --- | --- |
| 🌐 **Web editor** | [minecraftmetascript.github.io/mms](https://minecraftmetascript.github.io/mms/). Nothing to install. Live 2D and 3D terrain previews, examples to start from, and **Download pack** for a ready zip. |
| 📖 **Docs** | [Getting started](https://minecraftmetascript.github.io/mms/docs), a [custom dimension tutorial](https://github.com/MinecraftMetascript/mms/blob/main/docs/tutorial-dimension.md), and a reference for every kind and helper. |
| ⌨️ **Command line** | `mms` for Linux, macOS and Windows from the [latest release](https://github.com/MinecraftMetascript/mms/releases/latest), or `go install github.com/minecraftmetascript/mms/engine/cmd/mms@latest`. `mms build -world <save>` installs straight into a world. |
| 🧩 **VS Code** | The `.vsix` on the [latest release](https://github.com/MinecraftMetascript/mms/releases/latest): completion, hover docs, quick fixes, formatting and terrain previews. |
| ⚡ **Zed** | [`editors/zed`](https://github.com/MinecraftMetascript/mms/tree/main/editors/zed#readme), with tree-sitter highlighting and the same language server. |

Already have a data pack? `mms import pack.zip my_project` turns it into MMS.

### Contributing

Everything lives in [MinecraftMetascript/mms](https://github.com/MinecraftMetascript/mms): the Go compiler and language server, the web editor, the editor extensions and the docs. Bug reports, especially packs that fail to load in game, are very welcome in [issues](https://github.com/MinecraftMetascript/mms/issues).
