# Strip Arithmetic II — Slope, Width & the Singular Series

**Live demo:** https://wessengetachew.github.io/Strip2/

An interactive page that draws the triangle of cells $(r, M)$ in several views and counts the coprime cells along a strip of any slope, width and offset. Those counts lead to the block-coprime density $C(n)$ and to the Goldbach singular series.

Part II of the Strip series. Part I is
[The Goldbach Diagonal](https://wessengetachew.github.io/Partition/). Both pieces extend the
[C(n) block-coprime density suite](https://wessengetachew.github.io/smith/page2.html).

Wessen Getachew, 2026. The whole page is one `index.html` file. It has no build step and needs no server, so you can open it in any modern browser.

This page draws one object and then looks at it in many ways. The object is the triangle of cells $(r, M)$ with $1 \le r \le M \le G$. Every picture, overlay and exported sheet is a different reading of that triangle, and each reading rests on a classical result. We do not claim anything here as a new theorem. The exact counts are computed in your browser, and anything that is only observed is labelled as observed in the Status section of the page.

The page has three layers, and you meet them in this order. The **intro** is a timed animation that you can scrub and play with. The **opener** is the welcome panel, with a small sieve game and live previews. The **main page** is the full workbench. The intro draws up to 512 rings, the opener's sieve game goes up to $G = 1024$, and the main page goes up to $G = 10{,}000$. The intro plays on your first visit and skips itself afterwards. It also skips itself whenever the link carries a saved state (`#s=...`).

---

## The object and its formulas

A cell $(r, M)$ is called coprime when

$$\gcd(r, M) = 1.$$

Among all cells, the share that are coprime tends to

$$\frac{1}{\zeta(2)} = \frac{6}{\pi^2} \approx 0.6079.$$

The number of coprime cells on ring $M$ is $\varphi(M)$, Euler's totient, so the page counts the new points that each ring adds with $\varphi(M)$.

### The block sieve

The sieve depth is $n$. A cell survives to depth $n$ when $r$ is coprime to every one of the integers $M, M+1, \dots, M+n$. The code kills a cell when some prime $p$ divides $r$ and also divides $M + j$ for some $j$ between $0$ and $n$. In symbols, a cell survives when

$$\gcd(r,\, M+j) = 1 \quad \text{for every } j = 0, 1, \dots, n.$$

A prime $p \le n+1$ removes every cell with $p \mid r$, because $n+1$ consecutive integers always contain a multiple of $p$. A prime $p > n+1$ removes only a fraction $(n+1)/p^2$ of the cells. The Chinese remainder theorem lets the primes act independently, so the raw density of survivors is

$$D(n) = \prod_{p} \left(1 - \frac{\min(n+1,\, p)}{p^2}\right).$$

We normalise it so that depth zero gives exactly one:

$$C(n) = \zeta(2)\, D(n) = \prod_{p} \frac{1 - \min(n+1,\, p)/p^2}{1 - 1/p^2}.$$

This gives $C(0) = 1$, $C(1) \approx 0.5307$ and $C(2) \approx 0.4128$. For large $n$ the decay follows Mertens' third theorem, which is quoted rather than proved on the page:

$$C(n) \sim \frac{\zeta(2)\, e^{-\gamma}}{\ln n}.$$

At a finite $G$ the page compares its own exact count with the prediction. The total number of cells is $G(G+1)/2$, so the expected number of survivors is

$$\text{expected} = \frac{G(G+1)}{2}\, D(n).$$

### Strips, slopes and the block

A strip is the set of cells that satisfy

$$s \le b\,r - a\,M < s + w,$$

where $a/b$ is the slope, $s$ is the offset and $w$ is the width. At slope $+1$ with width $n+1$, read as a block, the strip gives the block-coprime density $C(n)$. Along a single diagonal $M - r = g$ the share of coprime cells is

$$\frac{\varphi(g)}{g}.$$

At slope $-1$ with width $1$ the strip is the Goldbach anti-diagonal

$$r + M = N.$$

On this page we take $N = E = 2(G+1)$. A Goldbach pair is a point $(g,\, E - g)$ where both $g$ and $E - g$ are prime.

### Goldbach and the singular series

The Hardy and Littlewood singular series for an even $N$ is

$$\mathfrak{S}(N) = 2\, C_2 \prod_{\substack{p \mid N \\ p > 2}} \frac{p-1}{p-2}, \qquad C_2 = \prod_{p > 2} \left(1 - \frac{1}{(p-1)^2}\right) \approx 0.6602.$$

The heuristic count of ordered prime pairs summing to $N$ is

$$r(N) \approx \mathfrak{S}(N)\, \mathrm{li}_2(N), \qquad \mathrm{li}_2(N) = \int_2^N \frac{dt}{(\ln t)^2}.$$

The comet section plots $r(N)$ against $N$ and then divides by $\mathfrak{S}(N)$ so that the bands merge. Be aware that the page uses the single-log form of $\mathrm{li}_2$ as a stand-in. The natural density of the pair $(a, N-a)$ is $1/(\ln a \,\ln(N-a))$, so the two forms differ at relative order $1/\ln N$. That is the most likely reason the "with $\mathfrak{S}$" column sits near $0.95$ to $0.97$ and not at $1.00$.

---

## The four views

The views are presentation only. No count depends on which one you choose. Each view places the same cell $(r, M)$ in a different way.

**Grid.** The Grid is a square lattice with $M$ across and $r$ up. Cell $(r, M)$ sits at

$$x = \frac{M - \tfrac12}{G}, \qquad y = \frac{r - \tfrac12}{G}.$$

**Ring.** Ring $M$ sits at a radius that depends on the hole setting $h$, and cell $r$ sits at an angle $\theta$. With plate radius $R$ and $G_Z$ the largest ring that sets the scale, the radius is

$$\rho_{\text{ring}}(M) = R\left(h + (1 - h)\,\frac{M - \tfrac12}{G_Z}\right).$$

At $h = 0$ the rings fill the plate. At $h = 1$ every ring collapses onto one circle. Ring $M$ holds the fractions $r/M$, which is the Farey structure.

**Cayley.** We place the ring point in the complex plane as $z = \rho\, e^{i\theta}$ with $\rho = \rho_0 + \rho_D\, M/G$, and then apply the Möbius map

$$\Gamma(z) = \frac{z - 1}{z + 1}.$$

The result is drawn on the Riemann sphere, which you can tilt about the $x$, $y$ and $z$ axes.

**Helix.** The Helix takes the ring point and lifts it to a height proportional to the unwrapped angle. With $\kappa = \max(\tfrac12, k/2)$, the point is

$$\bigl(X, Y, Z\bigr) = \left(\rho_{\text{ring}}\cos\theta,\ \rho_{\text{ring}}\sin\theta,\ \frac{\theta}{2\pi\kappa}\,(0.9R) - 0.45R\right),$$

and it is then turned by your $z$, $x$ and $y$ angles and drawn orthographically.

### The angle

The angle scale is $k$, and the angle mode decides how $r$ turns into $\theta$. All three modes carry the factor $k/2$:

$$\theta = \frac{k}{2}\,\Theta(r, M).$$

In **clamp** mode, which is the default, the angle is

$$\Theta = 2\pi \min\!\left(\frac{r}{M},\, 1\right).$$

Cells with $r \ge M$ are pinned at the limit, so you get one turn. In **wrap** mode the angle is unbounded,

$$\Theta = \frac{2\pi\, r}{M},$$

so cells with $r > M$ lap the ring and the page draws the full $G \times G$ square. On the Helix this extra length is the tail. In **unit** mode the angle is budgeted by $G$ and not by $M$,

$$\Theta = \frac{2\pi\, r}{G},$$

which gives straight radial spokes. With $k = 2$ the factor $k/2$ is one and you see the plain formulas above.

---

## Sectors and overlays

### Sectors

Sector $S_s$ is the set of cells where the integer part of $M/r$ equals $s$. This is the first step of the Euclidean algorithm. The sector is a wedge of the triangle,

$$S_s = \left\{ (r, M) : \frac{1}{s+1} < \frac{r}{M} \le \frac{1}{s} \right\},$$

and on the Ring the boundary between sector $s$ and sector $s+1$ is the ray at angle $\theta = \tfrac{k}{2}\cdot 2\pi/(s+1)$. At finite $G$ the page compares each sector's exact count with the prediction

$$\frac{G(G+1)}{2} \cdot \frac{D(n)}{s(s+1)}.$$

The intro's **sectors** button cycles through $4$, $8$, $16$ and all of them, and $16$ is the default. Every sector that is drawn gets its own colour. Sectors $1$ to $8$ keep the original palette, further sectors get hues spread evenly around the colour wheel, and anything past the last drawn sector is pooled in grey. The sector names $s=1, 2, \dots$ are written on their own wedges. Names from $s = 6$ on are smaller, and each label shrinks and fades with the room its wedge has, so neighbours never overlap.

### The prime spiral and its mirror

For a prime $p$ the column $r = p$ is coprime to $M$ unless $p \mid M$, and the ring $M = p$ is the dropout ring. On ring $M > p$ the angle is $2\pi p / M$ and the radius grows with $M$, so the product $\rho\theta$ is constant. That makes the spiral a classical hyperbolic spiral. Its mirror is the map

$$\sigma(r) = M - r,$$

which works because $\gcd(r, M) = \gcd(M - r, M)$. On the Ring this mirror is complex conjugation.

### The $\pm n$ path

The $\pm n$ path is the set of solutions of $2r \equiv \pm n \pmod M$, so

$$r = \frac{M \pm n}{2}.$$

The **Connect** option joins the spiral and the path at the rings they share. When $n$ goes to $n+1$ the lines only change when $n + 2$ is prime, and the lines that are about to be cut are drawn in red.

### Block patterns

The block control changes which integers a cell is tested against. The default is $M, M+1, \dots, M+n$. A step $k$ tests $M, M+k, \dots, M+nk$, and a custom list tests exactly the offsets $o_j$ you give it. The only change to the sieve is the local count $\nu_p$, which is the number of distinct residues of the offsets modulo $p$. A prime then removes a fraction $\nu_p / p^2$ of the cells.

### The circle method set-up

In the Ring's hole the page can draw the Farey dissection into major arcs, together with the prime exponential sum

$$S(\alpha) = \sum_{p \le N} e^{2\pi i\, p\, \alpha}.$$

This illustrates the dissection and does not prove anything.

### The slope band locked to a Goldbach pair

For $E = 2(G+1)$ and a pair $(g, s)$ with $g + s = E$, the marker sits on ring $M = s$ at column $r = g$. The locked band runs along the line

$$\frac{r}{M} = \frac{g}{s},$$

reduced by the gcd of $g$ and $s$.

---

## 1. The intro

The intro is a full-screen animation on a timeline that you can scrub. The clock starts at $-30$ s. During the first ten seconds, from $-30$ s to $-20$ s, $M$ grows from $1$ to $512$ on a log scale while $k$ unwinds from $2$ towards $0$ on the Helix. While $M$ is $7$ or less, every point is labelled with its $r$. The sector rays then draw themselves outward one after another and settle into faint lines.

The title carries a restart mark, and the slider at the top scrubs the timeline. The **Enter** button takes you on to the opener. Wheel or pinch zooms the plate, a drag pans it, and a double click resets it. The **fit tail** button sets the zoom and pan so that the whole Helix, tail included, is in the plate, and it keeps your current $x$, $y$ and $z$ turn.

The **controls** drawer holds the following groups.

The **Ring** group has the $M$ slider with its step arrows, a play button that runs $M$ from $1$ to $512$ and back, the angle mode, $k$, the hole slider, the $x$, $y$ and $z$ turns with their presets, the Cayley radii $\rho_0$ and $\rho_D$, the point size, the colour switch, and the sectors button. The **Prime spiral** group picks $p$ or scans through the primes. The **Goldbach** group steps through the pairs. The **Slope band** group sets $a$, $b$, the offset and the width, can grow the band one line on each side per step, and can lock the band to the Goldbach pair on screen. The **Sieve** group sets the depth $n$ from $0$ to $255$ and can play it up and back. The **Record** group captures every parameter change for up to 256 seconds, and you can replay the recording and save it as a video. The **formula** button keeps the top corner tables and shows the equation that is playing at that moment, with the live numbers put in. The **math sheet** button opens the sheet described below. The two arrow buttons send the exact picture on to the opener or all the way to the main page, and the last button saves a 1080 by 1920 PNG.

One detail is worth knowing. When you zoom out in Cayley, the intro normally adds rings so that the new space fills with points. With Goldbach on it does not, because $E = 2(G+1)$ and the locked pair would otherwise change with every zoom step.

## 2. The opener

The opener is the welcome panel, titled *The Opener · Strip Arithmetic II*. It has a music button, which plays *Riemann Zeta Function* by Vince Rubinetti and starts on your first click or key press. It also has a share-link button that reopens the opener with exactly your current settings.

**Level 1** is a small game. A cell is crossed out when a prime you pick divides $\gcd(r, M)$. Your goal is to cross out 99 percent of the cells that share a factor, using as few primes as you can. The par is the best greedy order. A hint shows you the best next prime but caps your stars at two. Teal cells are coprime and never crossed out, dark cells are crossed out, and coral cells share a factor and are still in play. The **Enter Level 2** button takes you to the main page.

The text below the game explains that this is the foundational layer, which is the $G$ lattice in Grid, Ring and Cayley form, its colouring and its lift dynamics. Strip II builds its slope, offset and width dynamic on top of that layer. The gap presets cover the gaps $1$, $2$ (twin), $4$ (cousin), $6$ (sexy), $8$, $10$ and $12$, with buttons to step to the previous or next prime pair. The strip presets are the diagonal, the blocks $n = 1$, $n = 2$ and $n = 4$, the Goldbach line, and the slope one half strip that is the page's default.

The live preview lets you choose Grid, Ring, Cayley, Helix or all three together, and showing one view at a time redraws faster. It has the hole and circle-method controls, the angle mode, $k$, and a lock that pins the canvases to the top while you scroll the controls. It can print a small label at every point while $G$ is small, and it has switches for the corner statistics: the share of coprime cells, the sectors, the sieve and the primes. You can also preview the math sheet, or just the sieve, as a pop-up.

## 3. The main page

The main page is called *Slope, Width, and the Singular Series* and has five folds.

**Section 0, the Guide,** explains everything above in classical terms. It ends with a table that pairs each control with the classical result behind it and says whether that result is a theorem, an elementary proof, a quoted asymptotic, or only an observation.

**Section 1, Setup,** covers blocks, strips and the residue count. It states the rule underneath, the two normalisations and where they part company, the branch for $\mathfrak{S}$ at slope $-1$, and the branch for $D$ in the block.

**Section 2, the lattice,** is the workbench. The plate has zoom buttons, a lens, point size and shape, and the Cayley guide curves. The number $G$ can be typed from $2$ to $10{,}000$, stepped by one, or stepped to the previous or next prime, and it has a play button with speed control and presets from $2$ up to $10{,}000$. The slope $a/b$ has presets for the $+1$ diagonal, for Goldbach lines, and for Farey rays. The page can lock the strip to prime pairs, and it can show which $r$ are kept or removed by sector. The block presets include $n = 1$, $n = 5$ and $n = 29$, and a walk setting switches between a strip and a band.

**Section 3, the comet,** plots the Goldbach comet with the $\mathfrak{S}$ normalisation described above. Its $N$ can go up to $300{,}000$.

**Section 4, Status,** says which register each statement belongs to: elementary and classical, one classical theorem, one classical evaluation, and one conjecture that is still open. It also says what the page does not claim.

## 4. The sheets

The math sheet and the sieve-only sheet export the state that is on screen. They open as a page that you can print to PDF. The math sheet has ten parts: the three views of the same cells, the legend and definitions, the state at this moment, the sectors, the kept ratio against $G$ around the target $D(n)$, the prime columns $r = p$, the births $\varphi(M)$ per ring, the values $D(n)$ and $C(n) = \zeta(2)\,D(n)$, the slope band, and the Goldbach section with $E$, the formula, the circle method and the actual count.

The parameters table follows the live state. It reports the view and its turns, the zoom and pan, the angle mode and its formula, the colouring, how many sectors are drawn, the point size, the Goldbach pair, the strip $a/b$ with its width and offset, and the lock on the spiral prime. The Helix and Cayley plates keep the zoom and pan that you set.

## 5. Sharing and saving

The share link is the page address followed by `#s=` and the state, and it stores only what differs from the defaults. The two arrow buttons in the intro hand the exact picture, with its $G$, $n$, view, angle, hole and tilt, on to the opener or the main page. The intro recording lasts up to 256 seconds and can be saved as a video, in MP4 where the browser allows it and otherwise WebM. The intro remembers that you have seen it by setting a flag named `stripII_welcome_seen` in your browser's local storage.

## 6. Limits worth knowing

In wrap and unit mode with a large $G$, the Helix tail is about $G$ turns tall, so the fit tail button will shrink the main ring a lot. With the sectors set to all and a large $G$, there are more sectors than distinguishable hues, so some colours repeat. The per-point labels only appear while $G$ is small.

## Credits and status

Everything on the page is classical material that we restate and compute in the browser. It draws on Euclid, Euler, Bézout, Möbius inversion, the Eratosthenes and Legendre sieve, the Chinese remainder theorem, Mertens' theorems, and the Hardy and Littlewood local factors. The most accurate name for the object is an Euler-product block sieve on the coprime lattice. Full attribution, with chips that open each result on the page, is in the credits panel at the bottom of the main page. The music is *Riemann Zeta Function* by Vince Rubinetti.
