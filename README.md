# Was 2000 the best year in gaming?

An interactive scrollytelling page about 250 top-rated games, and why critic scores from different eras can't be compared directly.

View the page here: https://jamie-jamieson.com/how-would-games-rank-if-each-one-were-rated-as-if-no-previous-game-had-come-before-it/ 

As you scroll, one chart reshapes itself through eight steps:

1. **The list:** the top 250 games on Metacritic as dots, by release year and Metascore.
2. **The obvious answer:** the top 100 stacked by year. 2000 wins with eight games.
3. **The catch:** critics score against the games they've just played, so the ruler moves. Remasters show it: Ocarina of Time went from 99 (1998) to 94 (3DS, 2011).
4. **Measuring the drift:** six original-to-remaster pairs give about 0.18 points per year.
5. **The upweight:** every game gets that credit for each year after 1996. 31 games enter the top 100.
6. **The recount:** the best year moves to 2023.
7. **Your turn:** sliders for drift and reference year, a scores/counts toggle, and live readouts.
8. **Caveats:** what the method can't tell you.

## Run it

It's a single self-contained file with no dependencies, build step or network requests.

```sh
open index.html          # macOS; or just double-click the file
python3 -m http.server   # or serve the folder and visit http://localhost:8000
```

## How it works

- **Data:** the first 250 entries of Metacritic's "Best games of all time" list, sorted by Metascore, retrieved on 19 November 2026. The data is embedded in `index.html` as one array of `[title, release year, Metascore]`.
- **Release years** are Metacritic's own for each entry, so remasters and ports count in their own year.
- **Drift:** a least-squares line through the origin, fitted to six original-to-remaster pairs (Ocarina of Time twice, Metroid Prime, Breath of the Wild, Tears of the Kingdom and The Last of Us). It comes to 266/1463, about 0.182 points per year.
- **Adjusted score** = raw score + drift × (release year − reference year). The reference year changes what the numbers mean but never the ranking.
- **Rendering:** plain JavaScript and SVG, with scroll steps driven by `IntersectionObserver`. It follows your light or dark setting and respects reduced-motion.

## Caveats

This is a thought experiment, not a ranking to trust.

- Six pairs is a thin base. A bootstrap puts the drift between 0.14 and 0.38, and dropping any one pair moves it between 0.16 and 0.23.
- Remasters may be marked down for being remasters, which would overstate the drift.
- Remasters of old games are lifted by their release year even though the design is old.
- Only 250 games are included, so a game just below the 91 cutoff can never move in.
- Counts near the top-100 cutoff are sensitive to ties, so a tiny change in drift can move one game in or out.
- Positions 1 to 50 came from a scrape I couldn't verify against the raw page text. Treat GTA VI at #1 and the 2026 Ocarina of Time re-release with extra caution.
- It measures how the ruler moves, not who influenced whom.

## Credits

Built with Claude. Scores and titles are from Metacritic, which isn't affiliated with this project. No licence has been added yet.
