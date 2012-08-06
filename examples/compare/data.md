# Performance testing CSS loading: separate native links vs. one concatenated CSS vs.  eCSSential

These demo pages load the same CSS files in different ways to compare performance.

- Demo using native `link` elements: http://filamentgroup.github.com/eCSSential/examples/compare/native.html
- Demo using eCSSential: http://filamentgroup.github.com/eCSSential/examples/compare/ecssential.html


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

- 9 requests  ❘  11.22KB transferred  ❘  248ms (onload: 249ms, DOMContentLoaded: 138ms)
- 9 requests  ❘  11.22KB transferred  ❘  269ms (onload: 271ms, DOMContentLoaded: 136ms)
- 9 requests  ❘  11.22KB transferred  ❘  289ms (onload: 291ms, DOMContentLoaded: 135ms)
- 9 requests  ❘  11.22KB transferred  ❘  193ms (onload: 196ms, DOMContentLoaded: 103ms)
- 9 requests  ❘  11.22KB transferred  ❘  279ms (onload: 281ms, DOMContentLoaded: 146ms)

http://filamentgroup.github.com/eCSSential/examples/compare/ecssential.html

- 2 requests  ❘  4.60KB transferred  ❘  209ms (onload: 214ms, DOMContentLoaded: 154ms)
- 2 requests  ❘  4.60KB transferred  ❘  204ms (onload: 210ms, DOMContentLoaded: 146ms)
- 2 requests  ❘  4.60KB transferred  ❘  207ms (onload: 212ms, DOMContentLoaded: 153ms)
- 2 requests  ❘  4.60KB transferred  ❘  179ms (onload: 184ms, DOMContentLoaded: 131ms)
- 2 requests  ❘  4.60KB transferred  ❘  216ms (onload: 223ms, DOMContentLoaded: 159ms)

#### At window width ~30em

http://filamentgroup.github.com/eCSSential/examples/compare/native.html

- 9 requests  ❘  11.22KB transferred  ❘  610ms (onload: 612ms, DOMContentLoaded: 148ms)
- 9 requests  ❘  11.22KB transferred  ❘  504ms (onload: 505ms, DOMContentLoaded: 95ms)
- 9 requests  ❘  11.22KB transferred  ❘  525ms (onload: 528ms, DOMContentLoaded: 126ms)
- 9 requests  ❘  11.22KB transferred  ❘  547ms (onload: 551ms, DOMContentLoaded: 95ms)
- 9 requests  ❘  11.22KB transferred  ❘  543ms (onload: 545ms, DOMContentLoaded: 94ms)

http://filamentgroup.github.com/eCSSential/examples/compare/ecssential.html

- 3 requests  ❘  5.76KB transferred  ❘  209ms (onload: 215ms, DOMContentLoaded: 142ms)
- 3 requests  ❘  5.76KB transferred  ❘  245ms (onload: 248ms, DOMContentLoaded: 143ms)
- 3 requests  ❘  5.76KB transferred  ❘  265ms (onload: 268ms, DOMContentLoaded: 161ms)
- 3 requests  ❘  5.76KB transferred  ❘  203ms (onload: 206ms, DOMContentLoaded: 107ms)
- 3 requests  ❘  5.76KB transferred  ❘  252ms (onload: 255ms, DOMContentLoaded: 103ms)


### On 4G connection 

#### At window width > 62.5em:

http://filamentgroup.github.com/eCSSential/examples/compare/native.html

- 9 requests  ❘  11.22KB transferred  ❘  992ms (onload: 994ms, DOMContentLoaded: 567ms)
- 9 requests  ❘  11.22KB transferred  ❘  880ms (onload: 883ms, DOMContentLoaded: 309ms)
- 9 requests  ❘  11.22KB transferred  ❘  765ms (onload: 767ms, DOMContentLoaded: 326ms)
- 9 requests  ❘  11.22KB transferred  ❘  747ms (onload: 749ms, DOMContentLoaded: 325ms)
- 9 requests  ❘  11.22KB transferred  ❘  747ms (onload: 748ms, DOMContentLoaded: 310ms)

http://filamentgroup.github.com/eCSSential/examples/compare/ecssential.html

- 2 requests  ❘  4.60KB transferred  ❘  588ms (onload: 598ms, DOMContentLoaded: 444ms)
- 2 requests  ❘  4.60KB transferred  ❘  620ms (onload: 661ms, DOMContentLoaded: 323ms)
- 2 requests  ❘  4.60KB transferred  ❘  364ms (onload: 370ms, DOMContentLoaded: 198ms)
- 2 requests  ❘  4.60KB transferred  ❘  334ms (onload: 340ms, DOMContentLoaded: 191ms)
- 2 requests  ❘  4.60KB transferred  ❘  453ms (onload: 460ms, DOMContentLoaded: 308ms)

#### At window width ~30em

http://filamentgroup.github.com/eCSSential/examples/compare/native.html

- 9 requests  ❘  11.22KB transferred  ❘  1.21s (onload: 1.21s, DOMContentLoaded: 324ms)
- 9 requests  ❘  11.22KB transferred  ❘  1.05s (onload: 1.05s, DOMContentLoaded: 177ms)
- 9 requests  ❘  11.22KB transferred  ❘  1.35s (onload: 1.35s, DOMContentLoaded: 317ms)
- 9 requests  ❘  11.22KB transferred  ❘  1.18s (onload: 1.18s, DOMContentLoaded: 179ms)
- 9 requests  ❘  11.22KB transferred  ❘  1.35s (onload: 1.35s, DOMContentLoaded: 326ms)

http://filamentgroup.github.com/eCSSential/examples/compare/ecssential.html

- 3 requests  ❘  5.76KB transferred  ❘  502ms (onload: 505ms, DOMContentLoaded: 338ms)
- 3 requests  ❘  5.76KB transferred  ❘  372ms (onload: 375ms, DOMContentLoaded: 221ms)
- 3 requests  ❘  5.76KB transferred  ❘  355ms (onload: 358ms, DOMContentLoaded: 191ms)
- 3 requests  ❘  5.76KB transferred  ❘  519ms (onload: 522ms, DOMContentLoaded: 213ms)
- 3 requests  ❘  5.76KB transferred  ❘  741ms (onload: 771ms, DOMContentLoaded: 456ms)



