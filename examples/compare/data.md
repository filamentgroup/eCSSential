# Performance testing CSS loading: separate native links vs. one concatenated CSS vs.  eCSSential

These demo pages load the same CSS files in 3 different ways to compare performance.

- Demo using native `link` elements to reference CSS via 8 files: http://filamentgroup.github.com/eCSSential/examples/compare/native.html
- Demo using eCSSential to reference those same 8 files in 2 dynamically concatenated requests: http://filamentgroup.github.com/eCSSential/examples/compare/ecssential.html
- Demo using a native `link` element to one giant CSS file containing all CSS: http://filamentgroup.github.com/eCSSential/examples/compare/concat.html


Notes and explanation:
- The CSS files for both demos are padded with 100+ lines of CSS to make them represent a realistic responsive design (total line numbers are still low compared to popular responsive sites on the web)
- CSS files are broken out by min-width media query breakpoints in attempt to load only the CSS that is necessary up-front, and load the rest in parallel. Both eCSSential and newer webkit builds perform this optimization by default, in different ways.
- Tests were run in Chrome 21 on a Mac
- The tests were performed on a fast wifi connection (connection speed: 9.3mbps download), then repeated on a fast 4G mobile connection (connection speed: .85mbps download).
- request counts come from Chrome Dev Tools and include ALL assets that are downloaded, which are 1 HTML file and up to 8 CSS files.
- tests were performed at 2 window widths to demonstrate the differences in performance when CSS is fetched all in serial vs. both in serial and parallel. At wide widths, the eCSSential demo makes 1 CSS request instead of 2 because it needs all breakpoints at load, so they all come in the first concatenated request.
- HTTP request counts and filesizes are smaller in the ecssential.html demos because eCSSential.js is able to make dynamic requests to concatenated CSS files, which makes for 1 or 2 total requests regardless of the number of CSS files in play, and also allows the CSS to compress smaller in transfer size, as GZIP compression can apply across many files at once when concatenation is used.



## Results

### On wifi

#### At window width > 62.5em:

http://filamentgroup.github.com/eCSSential/examples/compare/native.html

- 9 requests  ❘  19.33KB transferred  ❘  276ms (onload: 279ms, DOMContentLoaded: 143ms)
- 9 requests  ❘  19.33KB transferred  ❘  511ms (onload: 513ms, DOMContentLoaded: 120ms)
- 9 requests  ❘  19.33KB transferred  ❘  311ms (onload: 315ms, DOMContentLoaded: 118ms)
- 9 requests  ❘  19.33KB transferred  ❘  472ms (onload: 474ms, DOMContentLoaded: 141ms)
- 9 requests  ❘  19.33KB transferred  ❘  303ms (onload: 306ms, DOMContentLoaded: 134ms)
- ** Avg: 9 requests  ❘  19.33KB transferred  ❘  375ms (onload: 377ms, DOMContentLoaded: 131ms)**

http://filamentgroup.github.com/eCSSential/examples/compare/ecssential.html

- 2 requests  ❘  15.10KB transferred  ❘  260ms (onload: 271ms, DOMContentLoaded: 162ms)
- 2 requests  ❘  15.10KB transferred  ❘  227ms (onload: 240ms, DOMContentLoaded: 134ms)
- 2 requests  ❘  15.10KB transferred  ❘  270ms (onload: 283ms, DOMContentLoaded: 175ms)
- 2 requests  ❘  15.10KB transferred  ❘  283ms (onload: 295ms, DOMContentLoaded: 185ms)
- 2 requests  ❘  15.10KB transferred  ❘  267ms (onload: 278ms, DOMContentLoaded: 166ms)
- ** Avg: 2 requests  ❘  15.10KB transferred  ❘  261ms (onload: 273ms, DOMContentLoaded: 164ms)**

http://filamentgroup.github.com/eCSSential/examples/compare/concat.html

- 2 requests  ❘  13.79KB transferred  ❘  224ms (onload: 234ms, DOMContentLoaded: 125ms)
- 2 requests  ❘  13.79KB transferred  ❘  213ms (onload: 226ms, DOMContentLoaded: 115ms)
- 2 requests  ❘  13.79KB transferred  ❘  268ms (onload: 280ms, DOMContentLoaded: 124ms)
- 2 requests  ❘  13.79KB transferred  ❘  270ms (onload: 282ms, DOMContentLoaded: 172ms)
- 2 requests  ❘  13.79KB transferred  ❘  267ms (onload: 277ms, DOMContentLoaded: 170ms)
- ** Avg: 2 requests  ❘  13.79KB transferred  ❘  248ms (onload: 260ms, DOMContentLoaded: 141ms)**

#### At window width ~30em

http://filamentgroup.github.com/eCSSential/examples/compare/native.html

- 9 requests  ❘  19.33KB transferred  ❘  544ms (onload: 547ms, DOMContentLoaded: 116ms)
- 9 requests  ❘  19.33KB transferred  ❘  537ms (onload: 546ms, DOMContentLoaded: 138ms)
- 9 requests  ❘  19.33KB transferred  ❘  593ms (onload: 595ms, DOMContentLoaded: 110ms)
- 9 requests  ❘  19.33KB transferred  ❘  606ms (onload: 608ms, DOMContentLoaded: 113ms)
- 9 requests  ❘  19.33KB transferred  ❘  579ms (onload: 584ms, DOMContentLoaded: 117ms)
- ** Avg: 9 requests  ❘  19.33KB transferred  ❘  572ms (onload: 576ms, DOMContentLoaded: 119ms)**

http://filamentgroup.github.com/eCSSential/examples/compare/ecssential.html

- 3 requests  ❘  16.21KB transferred  ❘  201ms (onload: 208ms, DOMContentLoaded: 111ms)
- 3 requests  ❘  16.21KB transferred  ❘  238ms (onload: 247ms, DOMContentLoaded: 135ms)
- 3 requests  ❘  16.21KB transferred  ❘  229ms (onload: 236ms, DOMContentLoaded: 137ms)
- 3 requests  ❘  16.21KB transferred  ❘  223ms (onload: 229ms, DOMContentLoaded: 127ms)
- 3 requests  ❘  16.21KB transferred  ❘  228ms (onload: 235ms, DOMContentLoaded: 134ms)
- ** Avg: 3 requests  ❘  16.21KB transferred  ❘  224ms (onload: 231ms, DOMContentLoaded: 129ms)**

http://filamentgroup.github.com/eCSSential/examples/compare/concat.html

- 2 requests  ❘  13.79KB transferred  ❘  212ms (onload: 223ms, DOMContentLoaded: 129ms)
- 2 requests  ❘  13.79KB transferred  ❘  299ms (onload: 310ms, DOMContentLoaded: 189ms)
- 2 requests  ❘  13.79KB transferred  ❘  302ms (onload: 313ms, DOMContentLoaded: 191ms)
- 2 requests  ❘  13.79KB transferred  ❘  289ms (onload: 305ms, DOMContentLoaded: 168ms)
- 2 requests  ❘  13.79KB transferred  ❘  206ms (onload: 217ms, DOMContentLoaded: 103ms)
- ** Avg: 2 requests  ❘  13.79KB transferred  ❘  262ms (onload: 217ms, DOMContentLoaded: 156ms)**

### On 4G connection 

#### At window width > 62.5em:

http://filamentgroup.github.com/eCSSential/examples/compare/native.html

- 9 requests  ❘  19.33KB transferred  ❘  1.33s (onload: 1.34s, DOMContentLoaded: 204ms)
- 9 requests  ❘  19.33KB transferred  ❘  1.30s (onload: 1.31s, DOMContentLoaded: 308ms)
- 9 requests  ❘  19.33KB transferred  ❘  590ms (onload: 592ms, DOMContentLoaded: 188ms)
- 9 requests  ❘  19.33KB transferred  ❘  1.17s (onload: 1.17s, DOMContentLoaded: 178ms)
- 9 requests  ❘  19.33KB transferred  ❘  752ms (onload: 755ms, DOMContentLoaded: 314ms)
- ** Avg: 9 requests  ❘  19.33KB transferred  ❘  1.03s (onload: 1.03s, DOMContentLoaded: 238ms)**

http://filamentgroup.github.com/eCSSential/examples/compare/ecssential.html

- 2 requests  ❘  15.10KB transferred  ❘  612ms (onload: 624ms, DOMContentLoaded: 189ms)
- 2 requests  ❘  15.10KB transferred  ❘  737ms (onload: 748ms, DOMContentLoaded: 311ms)
- 2 requests  ❘  15.10KB transferred  ❘  727ms (onload: 739ms, DOMContentLoaded: 307ms)
- 2 requests  ❘  15.10KB transferred  ❘  733ms (onload: 745ms, DOMContentLoaded: 310ms)
- 2 requests  ❘  15.10KB transferred  ❘  740ms (onload: 750ms, DOMContentLoaded: 323ms)
- ** Avg: 2 requests  ❘  15.10KB transferred  ❘  710ms (onload: 721ms, DOMContentLoaded: 288ms)**

http://filamentgroup.github.com/eCSSential/examples/compare/concat.html

- 2 requests  ❘  13.79KB transferred  ❘  527ms (onload: 540ms, DOMContentLoaded: 191ms)
- 2 requests  ❘  13.79KB transferred  ❘  588ms (onload: 598ms, DOMContentLoaded: 175ms)
- 2 requests  ❘  13.79KB transferred  ❘  502ms (onload: 514ms, DOMContentLoaded: 178ms)
- 2 requests  ❘  13.79KB transferred  ❘  519ms (onload: 530ms, DOMContentLoaded: 171ms)
- 2 requests  ❘  13.79KB transferred  ❘  845ms (onload: 856ms, DOMContentLoaded: 173ms)
- ** Avg: 2 requests  ❘  13.79KB transferred  ❘  596ms (onload: 608ms, DOMContentLoaded: 178ms)**

#### At window width ~30em

http://filamentgroup.github.com/eCSSential/examples/compare/native.html

- 9 requests  ❘  19.33KB transferred  ❘  1.12s (onload: 1.12s, DOMContentLoaded: 174ms)
- 9 requests  ❘  19.33KB transferred  ❘  2.77s (onload: 2.77s, DOMContentLoaded: 191ms)
- 9 requests  ❘  19.33KB transferred  ❘  1.38s (onload: 1.38s, DOMContentLoaded: 301ms)
- 9 requests  ❘  19.33KB transferred  ❘  1.84s (onload: 1.84s, DOMContentLoaded: 331ms)
- 9 requests  ❘  19.33KB transferred  ❘  1.25s (onload: 1.25s, DOMContentLoaded: 176ms)
- ** Avg: 9 requests  ❘  19.33KB transferred  ❘  1.12s (onload: 1.12s, DOMContentLoaded: 235ms)**


http://filamentgroup.github.com/eCSSential/examples/compare/ecssential.html

- 3 requests  ❘  16.21KB transferred  ❘  663ms (onload: 669ms, DOMContentLoaded: 192ms)
- 3 requests  ❘  16.21KB transferred  ❘  652ms (onload: 658ms, DOMContentLoaded: 203ms)
- 3 requests  ❘  16.21KB transferred  ❘  796ms (onload: 803ms, DOMContentLoaded: 329ms)
- 3 requests  ❘  16.21KB transferred  ❘  681ms (onload: 688ms, DOMContentLoaded: 201ms)
- 3 requests  ❘  16.21KB transferred  ❘  752ms (onload: 759ms, DOMContentLoaded: 193ms)
- ** Avg: 3 requests  ❘  16.21KB transferred  ❘  709ms (onload: 715ms, DOMContentLoaded: 224ms)**

http://filamentgroup.github.com/eCSSential/examples/compare/concat.html

- 2 requests  ❘  13.79KB transferred  ❘  735ms (onload: 747ms, DOMContentLoaded: 176ms)
- 2 requests  ❘  13.79KB transferred  ❘  743ms (onload: 754ms, DOMContentLoaded: 190ms)
- 2 requests  ❘  13.79KB transferred  ❘  1.39s (onload: 1.40s, DOMContentLoaded: 186ms)
- 2 requests  ❘  13.79KB transferred  ❘  607ms (onload: 617ms, DOMContentLoaded: 192ms)
- 2 requests  ❘  13.79KB transferred  ❘  724ms (onload: 735ms, DOMContentLoaded: 305ms)
- ** Avg: 2 requests  ❘  13.79KB transferred  ❘  840ms (onload: 850ms, DOMContentLoaded: 176ms)**

