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

## German translation / Deutsche Übersetzung

**Note:** the German translation is machine-generated (produced by a large
language model) and has not been fully reviewed by a human translator. Some
wordings, puns, or cultural adaptations may be awkward or wrong. Corrections
are welcome.

This tree ships a fully German edition of the game alongside the English
original. The normal `make` / `sudo make install` builds and installs both:

  * `robotfindskitten-de` — the game with all on-screen text (instructions,
    win and error messages) in German.
  * `nki/deutsch.nki` — the German edition of the ~700 Non Kitten Items,
    localized and adapted: English puns and US-cultural references have been
    re-created so they land for a German-speaking player rather than being
    translated word-for-word.

The German binary reads its items from its own data directory
(`$(datadir)/games/robotfindskitten-de`), kept separate from the English
`robotfindskitten` items, so the two languages never mix once installed.

### Playing in German

After `sudo make install`, run it from anywhere outside the source tree:

```
robotfindskitten-de
```

To play in German straight from the build tree, point it at the single German
file — the tree's `nki/` directory holds *both* languages, and the game would
otherwise merge them:

```
src/robotfindskitten-de -f nki/deutsch.nki
```

Note: the German text uses UTF-8 umlauts, so a UTF-8 locale (e.g.
`de_DE.UTF-8`) must be active. The German binary calls `setlocale(LC_ALL, "")`
so that (n)curses renders umlauts correctly instead of as blank cells; if you
see blanks, check that `locale charmap` reports `UTF-8`.
