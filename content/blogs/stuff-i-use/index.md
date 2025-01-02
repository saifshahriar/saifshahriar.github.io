+++
title="Programs that I use on a daily basis"
author="Saif Shahriar"
date="2024-10-19"
mathjax=true
+++

## Intro
I have a sorta' minimal setup. I am biased and I mostly use what works for me.
I, for the most part try to adhere to the **UNIX Philosophy:**
> Do one thing and do it right.

Also, influenced by the **[Suckless Phylosophy](https://suckless.org/philosophy/)**.
So, I am basically DOOMED! hehe.

```text
 ________________________________
/ An idiot admires complexity,   \
| A genius admires simplicity... |
\                   —Terry Davis /
 --------------------------------
   \
    \
               |    .
           .   |L  /|
       _ . |\ _| \--+._/| .
      / ||\| Y J  )   / |/| ./
     J  |)'( |        ` F`.'/
   -<|  F         __     .-<
     | /       .-'. `.  /-. L___
     J \      <    \  | | O\|.-'
   _J \  .-    \/ O | | \  |F
  '-F  -<_.     \   .-'  `-' L__
 __J  _   _.     >-'  )._.   |-'
`-|.'   /_.           \_|   F
   /.-   .                _.<
  /'    /.'             .'  `\
   /L  /'   |/      _.-'-\
  /'J       ___.---'\|
    |\  .--' V  | `. `
    |/`. `-.     `._)
       / .-.\
 VK    \ (  `\
        `.\
```

## Setups
- **Operating System:** I use [Void Linux](https://voidlinux.org/). Which is an
  independent distribution. I am a fan of `xbps` package manager. It's fast and
  doesn't break as much as Artix (or Arch) does, which I had been using for the
  past 5 years. Also, it does not use *SystemD*.

  As for my home server (yes, I have a small home server), I use OpenBSD. It's
  simple, comes bundled with sane default tools.

  As for my toy (read *research*) *Operating System*, I use
  [Plan9](https://p9f.org/). And my remark is-
  > Such an elegant piece of art.
- **Window Manager:**
  [Dynamic Window Manager - DWM](https://github.com/saifshahriar/dwm-saif). It's
  fast, hackable, easier to understand source code, doesn't consume a lot of
  memory. I have my own build, pretty minimal with just some sane patches
  applied.
- **Terminal Emulator:**
  [Simple Terminal - st](https://github.com/saifshahriar/st) (Luke Smith's Build)
  Same principle as DWM. Luke's build is almost perfect that I didn't bother
  having my own build.
- **Shell:** [fish](https://github.com/fish-shell/fish-shell) the *Friendly
  Interactive Shell**. I have used `zsh` for a long time. Fish provides me the
  customization I have to make in order for zsh to work. Yet, it's slow in my
  experience. I don't care about POSIX in my day to life inside shell, I am not
  writing scripts in fish. I just use it as a *default user shell* to get my job
  done.
- **Editor/IDE:** Vim. Vim. Vim. It's less of a text editor and more of a
  lifestyle for me. I can't think of using any other text editor except vim.
  But, the motion, I use it everywhere I can. Nowadays, I use Neovim
  (technically the same thing or not). It's a bit faster. But, I do feel
  overwhelmed by the lua api. Hehe.

  NO, I donot use many plugins. Just a few of them that makes my life easier.

## GUI Programs
- **Browser:** [Brave Browser](https://brave.com/) with an insane amount of
  extensions.

  >Why not a minimal web browser?

  The web is bloated and broken and requires a 'modern' (read
  *bloated*) web browser. I really like the design philosophy
  of minimal web browsers like, [surf](https://surf.suckless.org/),
  [qutebrowser](https://www.qutebrowser.org/),
  [nyxt](https://nyxt-browser.com/), [vieb](https://vieb.dev/)
  and so on. But, they are far from usable. The most success I could get with is
  [qutebrowser](https://www.qutebrowser.org/).

  >Why not Firefox?

  Don't get me wrong. I love Firefox. I just don't have a good hardware to run
  the Gecko Engine.[^1]

  See the [browser extensions](#browser-extensions) section to about my
  day-to-day most used
  extensions.
- **File Manager:** I for the most part donot use or need a file manager. `cd`
  is enough. If I must have to use a file manager, it's
  [lf](https://github.com/gokcehan/lf) or for GUI it's
  [PCManFM](https://wiki.archlinux.org/title/PCManFM).
- **Image Viewer:** [Sxiv](https://github.com/xyb3rt/sxiv). Why not? Suckless,
  fast, extensible.
- **Video & Audio:** [mpv](https://mpv.io/) is THE BEST video player ever
  created. Lol.

## Tools
- [Dmenu](https://github.com/saifshahriar/dmenu) - A suckless menu literally
  has the power to be anything.<br/>
- [Slock](https://tools.suckless.org/sent/) - A suckless screenlock.
- [Xmenu](https://github.com/phillbush/xmenu) - A window manager agnostic
  suckless context menu.
- [farbfeld](https://tools.suckless.org/farbfeld/) - A lossless image format.
- [sent](https://tools.suckless.org/sent/) - A presentation tool. Focus more on
  the content rather than silly animation and colours.

- [$L^{A}T_{E}X$](https://www.latex-project.org/) - A bloated document
  preparation system. Use groff(1) instead.
- [groff](https://www.gnu.org/software/groff/) - Front-end for the groff(1)
  document formatting system.
- [pandoc](https://pandoc.org/) - A general markup converter.

- [eza](https://github.com/eza-community/eza)  - A better ls(1) & successor of
  [exa](https://the.exa.website/).
- [bat](https://github.com/sharkdp/bat) - A better cat(1).
- [delta](https://github.com/dandavison/delta) - A better diff(1).

## Browser Extensions
This part is so bloated. Stay away...
- **General:**
    - [Dark Reader](https://darkreader.org/): Heals your eyes by turning every
    webpage dark.
    - [Scrollbar Customizer](https://chromewebstore.google.com/detail/scrollbar-customizer/flffekjijpabhjgpoapooggncnmcjopa):
    Hides ugly scrollbar in chromium and saves spaces.
    - [Vimium C](https://github.com/gdh1995/vimium-c): Makes me a hackerrr while
    I am using my browser. Power of VI
      navigation within the browser.
    - [Firenvim](https://github.com/glacambre/firenvim): Turns any text field
    into a (neo)vim buffer.
- **Privacy:**
    - [uBlock Origin](https://ublockorigin.com/): Unfortunately dead in the
      chormium side. :(
    - [User Agent Switcher](https://github.com/ray-lothian/UserAgent-Switcher)
- **Competitive Programming:** I do Competitive Programming. :D
    - [Carrot](): Rating predictor for Codeforces.
    - [CF Analytics](): Analyse Codeforces profiles.
    - [CF World Standings](): Filters the standings for a given contest on
    Codeforces to show only active competitors of a specific country.
    - [Codeforces Enhancer](): Multiple ratings graph, colorizes standings,
    adds "Hide/Show solved problems" link.
    - [Codeforces Practice Tracker](): Track practice progress on Codeforces.
    - [Competitive Companion](): Parses competitive programming problems and
    sends them to various tools like CP Editor and CPH. I use it with a CP
    plugin in Neovim.

## My dots
You can find them here:
[https://github.com/saifshahriar/dotfiles](https://github.com/saifshahriar/dotfiles)

## **See also**
- Stuff that sucks: [https://suckless.org/rocks/](https://suckless.org/rocks/)
- Stuff that rocks: [https://suckless.org/rocks/](https://suckless.org/rocks/)
- List of harmful software: [https://harmful.cat-v.org/software/](https://harmful.cat-v.org/software/)
- The web is a bloat: [https://suckless.org/sucks/web/](https://suckless.org/sucks/web/)
- Tons of awesome terminal and TUI programmes everyday: [https://terminaltrove.com/new/](https://terminaltrove.com/new/)

[^1]: Firefox is slow on older hardware. I might write an article and update
    this section later.
