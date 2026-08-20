# FantasqueSansMNoLigNerdFont

A modified build of [Fantasque Sans Mono](https://github.com/belluzj/fantasque-sans) for terminal and coding use, with fixes for optical size and the lowercase "f", patched as a Nerd Font.

The family is named **FantasqueSansMNoLig Nerd Font** so it installs cleanly alongside the official Fantasque and official Nerd Fonts "FantasqueSansM" builds without any name conflicts.

## Base font

The letterforms correspond to **v1.8.1** of [spinda/fantasque-sans-ligatures](https://github.com/spinda/fantasque-sans-ligatures), a ligature-free fork built from upstream Fantasque master (which contains unreleased fixes beyond the last tagged v1.8.0 release, including revised tilde, backtick, ©/®, curly quotes, and comma-accent letters). The `FantasqueSansMono-LargeLineHeight-NoLoopK` variant is used:

- **No-loop `k`** — the straight-leg `k` is the default (the looped form remains available via stylistic set `ss01`).
- **Large line height** — extra vertical room, mainly for accented capitals.
- **No ligatures** — the `calt` coding-ligature feature is absent, so sequences like `->` and `!=` always render as literal characters.

## Modifications relative to upstream

Applied in this order:

1. **Lowercase "f" gap fix.** In the original design, the hook of the `f` terminates ~130 font units (~6% of em) above the crossbar, which collapses to about one pixel at typical text sizes and makes the hook appear to touch the crossbar. The hook's terminal end-cap was raised — by 70 units in Regular and Bold, 50 in Bold Italic, and 40 in Italic (which already had more clearance) — with the adjacent curve control points eased proportionally so the hook stays smooth. The crossbar itself, its x-height alignment (shared with `t`), and the hook's apex are unchanged.

2. **Nerd Font patch.** Patched with the official [Nerd Fonts](https://github.com/ryanoasis/nerd-fonts) `font-patcher` **v3.4.0** using `--mono --complete`, adding ~4,200 icon glyphs (Powerline, Devicons, Font Awesome, Material Design, Codicons, Octicons, Font Logos, Weather, and more), all fitted to the single monospace cell width. This also normalizes the symbol alignment used by prompt tools such as Starship and Oh-My-Posh, and includes the Powerline position/size refinements from Nerd Fonts 3.2–3.4.

3. **Optical size correction ("upscaled 1.10").** Upstream Fantasque draws small on its em: x-height is only 0.497 of the em square, versus ~0.53–0.55 for the proportional fonts it gets mixed with in browsers (DejaVu Sans 0.547, Liberation Sans 0.528), so inline code visibly shrank next to body text. All outlines and metrics were scaled by **1.10×** using fontTools `scale_upem`, then the em size was restored to 2048, making every glyph render ~10% larger at the same nominal point size. After the fix, the x-height ratio is **0.547 — matching DejaVu Sans exactly** — with cap height at 0.688 (matching Liberation Sans). Because outlines, advance widths, and vertical metrics all scaled together, monospace cell proportions, icon alignment, and line spacing relative to glyph size are unchanged.

4. **Re-hinted.** Rescaling invalidates TrueType bytecode hinting (instruction constants don't scale), so the original hinting was stripped entirely and the text glyphs were re-hinted with **ttfautohint 1.8.4** (`--stem-width-mode=nnn`, Latin). Icon glyphs intentionally carry no hint bytecode (hinting only benefits text at small sizes), which keeps file sizes reasonable. Stale `DSIG`/`FFTM`/`PfEd` tables were removed and a fresh `gasp` table written.

## Version identification

The name table records `Version 1.8.1;Nerd Fonts 3.4.0;f-gap-fix;upscaled 1.10` with font revision 2.0, so font caches distinguish this build from both upstream and earlier builds of this repo.

## Notes

- The fonts are strictly monospaced (single advance width, `isFixedPitch` set, PANOSE monospace). There is intentionally no kerning — pair-dependent spacing would break terminal/grid alignment. Any airiness after letters like `f` or `t` is the letterform's shape inside its fixed cell, inherited from the original design.
- Styles included: Regular, Bold, Italic, Bold Italic.

## License

Fantasque Sans Mono is © Jany Belluz, licensed under the [SIL Open Font License 1.1](LICENSE.md). This modified build is distributed under the same license.
