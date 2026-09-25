# caracara.games

The Caracara studio site. Static HTML and CSS for GitHub Pages, with no build step.
`DESIGN.md` is Claude Design's handoff: every colour, size and shape the pages use.

## Structure
- `index.html` and `styles.css`: the studio page, in the logo's style (cream, ink, orange, cut shapes).
- `games/hex-and-hearth/`: the game page, in the game's parchment style (`game.css`).
- To add a game, copy `games/hex-and-hearth/`, then duplicate the `<li class="game-item">` on the studio page.

## Still to swap
- The capsule: a still from the game stands in (`assets/img/hex-and-hearth-capsule*.jpg`). Replace it with the
  Steam main capsule at 616×353 and 1232×706.
- The trailer: a still stands in (`hex-and-hearth-still*.jpg`). The embed snippets are in a comment on the game page.
- Social links: only Steam is live. The rest are commented out in the footer of `index.html`.
- `hello@caracara.games` must receive mail before anyone writes to it.

## Deploy
GitHub Pages serves `main` from the root. `CNAME` holds `caracara.games` and `.nojekyll` turns Jekyll off.
