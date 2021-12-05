<h3>

| **Package source:** | Tarball |             Git              | Node | Gem |
| :-----------------: | :-----: | :--------------------------: | :--: | :-: |
|     **Status:**     |    -    | :heavy_check_mark: (default) | :x:  | :x: |

</h3>

- [Introduction](#introduction)
- [Install](#install)
  - [Available `pack''` invocations](#available-pack-invocations)
  - [Default Profile](#default-profile)
  - [`no-zsh-completion` Profile](#no-zsh-completion-profile)
  - [`no-dir-color-swap` Profile](#no-dir-color-swap-profile)

## Introduction

> **[?]**
> This repository not compatible with previous versions (zplugin, zinit).
>
> Please upgrade to [ZI](https://github.com/z-shell-zi)

The [trapd00r/LS_COLORS](https://github.com/jhawthorn/fzy) zsh package that can use the NPM package registry to automatically:

- get the plugin's Git repository OR release-package URL,
- get the list of the recommended ices for the plugin,
  - there can be multiple lists of ices,
  - the ice lists are stored in _profiles_; there's at least one profile, _default_,
  - the ices can be selectively overridden.

## Install

### Available `pack''` invocations

```zsh
# Download the default profile
zi pack for ls_colors

# Download the no-zsh-completion profile
zi pack"no-zsh-completion" for ls_colors

# Download the no-dir-color-swap profile
zi pack"no-dir-color-swap" for ls_colors
```

### Default Profile

Provides the LS_COLORS definitions for GNU `ls`, `ogham/exa` and also setups
zsh-completion system to use the definitions. It also edits the color for the
directory (see the details in the `no-dir-color-swap` profile section).

The ZI command executed will be equivalent to:

```zsh
zi lucid reset \
 atclone"[[ -z ${commands[dircolors]} ]] && local P=g
    \${P}sed -i '/DIR/c\DIR 38;5;63;1' LS_COLORS; \
    \${P}dircolors -b LS_COLORS > clrs.zsh" \
 atpull'%atclone' pick"clrs.zsh" nocompile'!' \
 atload'zstyle ":completion:*:default" list-colors "${(s.:.)LS_COLORS}";' for \
    trapd00r/LS_COLORS
```

### `no-zsh-completion` Profile

Provides the LS_COLORS definitions for GNU `ls`, `ogham/exa` but doesn't set up
the zsh-completion system to use them.

The ZI command executed will be equivalent to:

```zsh
zi lucid reset \
 atclone"[[ -z ${commands[dircolors]} ]] && local P=g
    \${P}sed -i '/DIR/c\DIR 38;5;63;1' LS_COLORS; \
    \${P}dircolors -b LS_COLORS > clrs.zsh" \
 atpull'%atclone' pick"clrs.zsh" nocompile'!' for \
    trapd00r/LS_COLORS
```

### `no-dir-color-swap` Profile

Provides the LS_COLORS definitions like the `default` profile, however doesn't
edit the definitions file and doesn't change the color for directories. The
color is being edited in the default profile because the author found it to be
too dark.

The ZI command executed will be equivalent to:

```zsh
zi lucid \
 atclone"[[ -z ${commands[dircolors]} ]] && local P=g
     ${P}dircolors -b LS_COLORS > clrs.zsh" \
 atpull'%atclone' pick"clrs.zsh" nocompile'!' \
 atload'zstyle ":completion:*:default" list-colors "${(s.:.)LS_COLORS}";' for \
    trapd00r/LS_COLORS
```
