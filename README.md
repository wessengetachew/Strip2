# Strip Arithmetic II — Slope, Width & the Singular Series

**Live:** https://wessengetachew.github.io/Strips2/

Part II of the strip series. Part I is
[The Goldbach Diagonal](https://wessengetachew.github.io/Partition/); both extend the
[C(n) block-coprime density suite](https://wessengetachew.github.io/smith/).

Single-file interactive page. No build step, no dependencies to install.

---

## The claim

One counting rule produces both the `min(n+1, p)` inside block-coprime density and the
Goldbach correction factor `∏(p−1)/(p−2)`.

For a finite set of integer offsets `ℋ` and a prime `p`, let

```
ν_p(ℋ) = number of distinct residue classes ℋ occupies mod p
```

**The block.** `ℋ = {0, 1, …, n}` — consecutive integers, so by pigeonhole
`ν_p = min(n+1, p)`. Every class is hit once `p ≤ n+1`, which is the saturation
mechanism: the local factor freezes at `1 − 1/p` and stops moving. This is the
`min(n+1, p)` in

```
D(n) = ∏ₚ (1 − min(n+1, p) / p²),    C(n) = ζ(2)·D(n)
```

**The Goldbach pair.** `ℋ = {0, N}`, since `r` and `N−r` must both be prime. So
`ν_p = 2` — unless `p | N`, when the two offsets collide and `ν_p = 1`.

Feed `ν_p` into the Hardy–Littlewood singular series
`𝔖 = ∏ₚ (1 − ν_p/p) / (1 − 1/p)²` and the `{0, N}` case collapses to

```
𝔖(N) = 2·C₂ · ∏_{p | N, p > 2} (p−1)/(p−2),    C₂ ≈ 0.6601618158
```

`p = 2` always collides and supplies the leading 2; every odd prime dividing `N`
supplies one `(p−1)/(p−2)`. Nothing was added — the correction **is** the collision
count, read off the same rule that gives `min(n+1, p)`.

### Does the correction do real work?

Even numbers of near-identical size, very different radicals:

| N | rad(N) | r(N) | 𝔖(N) | with 𝔖 | without |
|---|---|---|---|---|---|
| 299990 | 299990 | 4024 | 1.782 | 0.982 | 1.325 |
| 299998 | 299998 | 2996 | 1.343 | 0.969 | 0.986 |
| 300000 | 30 | 7830 | 3.521 | 0.967 | **2.578** |
| 300002 | 300002 | 2927 | 1.320 | 0.964 | 0.964 |
| 300006 | 100002 | 7096 | 3.170 | 0.973 | **2.336** |
| 300030 | 300030 | 8080 | 3.597 | 0.976 | **2.660** |

`with 𝔖` is `r(N) / (𝔖(N)·li₂(N))`; `without` replaces `𝔖(N)` by the bare `2C₂`.
Drop the correction and the prediction is off by a factor of 2.7 on smooth `N`.
Keep it and all six land in 0.963–0.982. Across every even `N ≥ 1000` in range the
standard deviation of the ratio falls from 0.552 to 0.040 — about 14× tighter.

---

## Strips and bands

Most of the page is one walk over a **strip**: lattice points `(r, M)` with

```
s ≤ b·r − a·M < s + w
```

for slope `a/b`, offset `s`, width `w`. Three familiar objects are three settings:

| Slope | Width | What it is | Exact |
|---|---|---|---|
| `+1` | `1` | Gap diagonal `r − M = g` | density `φ(g)/g` |
| `+1` | `1`, `s = 0` | Main diagonal `r = M` | exactly one coprime cell, at (1,1) |
| `−1` | `1` | Goldbach anti-diagonal `r + M = N` | exactly `φ(N)` points |
| `a/b` | `1` | Farey sector ray | Stern–Brocot mediant structure |

**The block is the exception, and it is easy to get wrong.** `C(n)` is *not* the coprime
density inside a diagonal strip. The block `{M, …, M+n}` runs along `M` and the condition
is a **conjunction**:

```
gcd(r, M+j) = 1   for all j = 0…n
```

A vertical band of `n+1` columns with an AND across it, not an average within a strip.
Measured as an AND it converges to `D(n)`; measured as a strip average it converges to
something roughly three times larger at `n = 5`. Band mode measures the first. This is the
same condition Strip Arithmetic I applies in its *block n* control, walked over the whole
lattice here instead of along a single strip.

---

## What's on the page

- **Lattice plate** — strips at any slope/offset/width, or block bands, over a `G×G`
  coprimality lattice up to `G = 10,000`
- **Live identity check** — measured strip density against the exact `φ(g)/g` or `φ(N)`,
  recomputed on every parameter change
- **The Goldbach comet** — `r(N)` for all even `N` up to 300,000, with a `𝔖(N)`
  normalisation toggle and spread statistics computed live
- **gcd colouring** — by value, smallest or largest prime factor, `ω(g)`, `Ω(g)`, or banded
- **gcd distribution** — measured counts against the exact form: over `[1,n]²` the number
  of pairs with `gcd = d` is exactly `Φ(⌊n/d⌋)` where `Φ(m) = 2·Σφ(k) − 1`, with the
  partition identity `Σ_d Φ(⌊n/d⌋) = n²` checked live
- **Magnifier** — 1–500× true magnification, corner-pinnable, with six label modes
  including the strip coordinates `v = b·r − a·M`
- **Self test** — 16 claims, run on load, each recomputed by a route independent of the
  one the page uses
- **Exports** — 2K/4K/8K PNG carrying parameters, counts and verdict; CSV for the strip,
  the comet and the gcd distribution

### Controls

Every numeric parameter has a stepper: previous prime, −, type a value, +, next prime.
A teal **prime** tag lights when a parameter sits on one. Presets cover the gap diagonal,
`C(n)` blocks, smooth vs rough Goldbach `N`, and Farey rays.

Keyboard: `←`/`→` offset ±1 (`Shift` for ±10), `↑`/`↓` width, `P` next prime offset
(`Shift+P` previous), `D` diagonal, `G` Goldbach, `R` reset, `L` toggle lens.

---

## Performance

- Coprimality is a **bitset**, not a byte array. `G = 10,000` is 10⁸ cells in 12.5 MB;
  the same as `Uint8Array` is 100 MB and will be killed on a phone.
- It is built by **clearing, not testing**. For each prime `p ≤ G`, clear every `(r, M)`
  with `p|r` and `p|M` — that is `G²·Σₚ p⁻² ≈ 0.4522·G²` writes, about 4.5×10⁷ at
  `G = 10,000`, versus 10⁸ gcd calls. Chunked at 24 ms per frame.
- Nothing draws per cell. The base layer is one `ImageData` pass at canvas resolution;
  when `G` exceeds the canvas each pixel aggregates its block and shades by density.
- The base layer is cached by `(G, size, colour mode)`. Slope, offset and width changes
  redraw only the overlay — `O(strip length)`, never `O(G²)`.
- `r(N)` is computed by **convolving the prime set** (for each pair `p+q ≤ N`, bump a
  counter), an order of magnitude cheaper than testing each `N` separately.

**Note on the gcd colour modes:** a gcd cannot be averaged, so unlike the binary and
density modes these *sample* each block's representative cell when `G` exceeds the canvas.
They are not exact at `G = 10,000` — the magnifier is, since it re-reads the bitset.

---

## Verification

The page runs its own test battery 1.2 s after load, so a broken build is visible without
anyone pressing anything. The rule is that the two sides of a test must not share an
implementation:

- coprimality bitset against direct `gcd` on every cell
- `Φ(n)` closed form against direct pair enumeration
- `Σ_d Φ(⌊n/d⌋) = n²` exactly
- `Φ(n)/n² → 6/π²`
- anti-diagonal count against `φ(N)`; diagonal density against `φ(g)/g`
- `ν_p = min(n+1,p)` and `ν_p ∈ {1,2}` by direct residue enumeration
- the `𝔖` Euler product against its closed form
- `C₂` against [A005597](https://oeis.org/A005597)
- `li₂` against a 400,000-step Simpson reference
- the prime convolution against published `r(N)` values
- band AND-density against `D(n)`, with tolerance `0.005 + 4(n+1)/G` — the finite-`G`
  bias is structural, since a band of `n+1` columns loses its last `n` at the edge

---

## What is and isn't established

- **Exact.** `φ(g)/g` on the `+1` diagonal and `φ(N)` on the `−1` anti-diagonal, checked
  by direct enumeration rather than asymptotics.
- **Exact.** `ν_p = min(n+1,p)` for consecutive blocks and `ν_p ∈ {1,2}` for `{0,N}`.
- **Exact.** The algebraic collapse of `∏ (1−ν_p/p)/(1−1/p)²` to `2C₂∏(p−1)/(p−2)`.
- **Heuristic.** That `𝔖(N)·li₂(N)` approximates `r(N)`. This is the Hardy–Littlewood
  conjecture. It is unproven. The comet shows it fits; fitting is not proof.
- **Not claimed.** Any progress on Goldbach's conjecture. The lattice sees coprimality;
  primality is strictly harder and nothing here bridges that.

**Normalisation.** `C(n)` uses local factors `1 − ν_p/p²` because it averages over block
anchors — it is a density of integers. The singular series uses `(1 − ν_p/p)/(1 − 1/p)²`
because it compares against a prime-density baseline. Different normalisations of the same
`ν_p`. Conflating them would be an error; the shared object is the residue count, not the
Euler factor.

---

## Tech

Single-file HTML/CSS/JS. MathJax for typeset formulas, Canvas 2D for every plate.
Typography is Cinzel / Spectral / JetBrains Mono; colour language is gold / teal / coral,
matching the rest of the project.

Open `index.html` directly in a browser, or serve the folder:

```bash
python3 -m http.server 8000
# then visit http://localhost:8000
```

Some features (PNG and CSV export) hit browser restrictions on `file://` URLs, so a local
server is easier.

---

## Credits

Hardy & Littlewood, *Partitio Numerorum III* (1923), for the singular series and the
`ν_p(ℋ)` formulation. Euler for `ζ(2)` and the totient. Mertens for the decomposition
`C(n) = ζ(2)·∏_{p≤n}(1−1/p)·∏_{p>n}(1−(n+1)/p²)`.

`C(n)`, its generalisations `C(n₁,…,n_k)` and `C_χ(n)`, the block-coprimality framing and
the strip construction are original work. The classical results they build on are credited
page by page across the suite.

## Author

Wessen Getachew — 2026
