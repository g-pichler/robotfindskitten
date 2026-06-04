# robotfindskitten

In 1997, Peter A. Peterson II held a contest for his now-defunct Nerth Pork magazine.
The goal: come up with the best piece of art entitled "robotfindskitten".
Leonard Richardson submitted the winning (read: only) entry, a [Zen Simulation](https://stackoverflow.com/questions/10140069/what-in-the-world-is-a-zen-simulator/15147633#15147633).

```
┌──────────────────────────────────────────────────────────────────────┐
│                                                                      │
│       c                         a                                    │
│               yn                      [                              │
│                                                                     _│
│                                  #                                   │
│                            a                           p             │
│                                                                      │
│                               .                       Y              │
│ u                                                      N             │
│|                                   i                                 │
│                           M                       H               g  │
│        )                      P                                      │
│                                                                      │
│                                      w                           8   │
└──────────────────────────────────────────────────────────────────────┘
```

## Obtaining

robotfindskitten is available from most Unix distributions.

  * `sudo apt install robotfindskitten`  # [Debian](https://packages.debian.org/stable/robotfindskitten), Ubuntu, etc
  * `sudo dnf install robotfindskitten`  # Fedora, etc
  * `sudo pkg install robotfindskitten`  # [FreeBSD](https://www.freshports.org/games/robotfindskitten)
  * `sudo port install robotfindskitten`  # [macOS MacPorts](https://ports.macports.org/port/robotfindskitten/)
  * `brew install robotfindskitten`  # [macOS Homebrew](https://formulae.brew.sh/formula/robotfindskitten)
  * `guix install robotfindskitten`  # GNU Guix

As of this writing, [Finnix](https://www.finnix.org/) is the only distribution to carry robotfindskitten pre-installed.

If your distribution does not have robotfindskitten, contact them and politely ask them to distribute it.
It's in their best interest.

## Building from source

To build robotfindskitten from source, you will need GNU and TeX tools.
On Debian-based systems, the following build dependencies will be sufficient:

```
sudo apt install build-essential gnulib libncurses-dev texinfo texlive-latex-recommended
```

Generate/update autoconf/automake scripts.
This is required when building from git source, but is recommended for releases too.

```
autoreconf -ifv
```

Configure, make, install.

```
./configure
make
sudo make install
```

## Translations

**Note:** both translations below — German *and* Spanish — are
machine-generated (produced by a large language model) and have not been fully
reviewed by a human translator. Some wordings, puns, or cultural adaptations
may be awkward or wrong. Corrections are welcome.

This tree ships translated editions of the game alongside the English
original. The normal `make` / `sudo make install` builds and installs all of
them:

| Language | Binary                 | Item file         | Data directory                        |
|----------|------------------------|-------------------|---------------------------------------|
| English  | `robotfindskitten`     | `nki/vanilla.nki` | `$(datadir)/games/robotfindskitten`    |
| German   | `robotfindskitten-de`  | `nki/deutsch.nki` | `$(datadir)/games/robotfindskitten-de` |
| Spanish  | `robotfindskitten-es`  | `nki/espanol.nki` | `$(datadir)/games/robotfindskitten-es` |

Each translated binary carries all of its on-screen text (instructions, win
and error messages) in its language, and the ~700 Non Kitten Items have been
localized and adapted rather than translated word-for-word: English puns and
US-cultural references have been re-created so they land for the target
audience. Each binary reads its items from its own data directory, so the
languages never mix once installed.

### Playing in a translated language

After `sudo make install`, run the chosen binary from anywhere outside the
source tree:

```
robotfindskitten-de      # German
robotfindskitten-es      # Spanish
```

To play a translation straight from the build tree, point it at the single
matching item file — the tree's `nki/` directory holds *all* languages, and
the game would otherwise merge them:

```
src/robotfindskitten-de -f nki/deutsch.nki
src/robotfindskitten-es -f nki/espanol.nki
```

Note: the translated text uses non-ASCII UTF-8 characters (umlauts, accents,
`¡`, `¿`, …), so a UTF-8 locale (e.g. `de_DE.UTF-8` or `es_ES.UTF-8`) must be
active. The translated binaries call `setlocale(LC_ALL, "")` so that (n)curses
renders these correctly instead of as blank cells; if you see blanks, check
that `locale charmap` reports `UTF-8`.

### Adding another language

The translated editions follow a fixed pattern, so a new language `xx` is
additive — no existing files change:

  1. `nki/<lang>.nki` — translate the items (copy `nki/vanilla.nki` as a base).
  2. `src/robotfindskitten.xx.c` — copy `src/robotfindskitten.c`, translate the
     handful of UI string literals, and add `setlocale(LC_ALL, "")` in `main()`.
  3. `src/Makefile.am` — add `robotfindskitten-xx` to `execgames_PROGRAMS` with
     its `_SOURCES` and a `_CPPFLAGS` pointing `SYSTEM_NKI_DIR` at its own dir.
  4. `nki/Makefile.am` — add an `nkixxdir` / `nkixx_DATA` install pair and list
     the file in `EXTRA_DIST`.
  5. `.gitignore` — add `src/robotfindskitten-xx`.
