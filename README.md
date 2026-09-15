# adityapratapyadav.netlify.app

Portfolio site for **Aditya Pratap Yadav**, Graduate Business Analyst, Birmingham.

Live at **https://adityapratapyadav.netlify.app** and mirrored at
**https://aditya-p-yadav.github.io**.

## What it is

One `index.html` and one `assets/` folder. Plain HTML, CSS and vanilla JavaScript. No
framework, no build step, no dependencies, no backend. The page is 66 KB and loads in under
a second.

The hero is a scroll-scrubbed video: it plays forward as you scroll down and backward as you
scroll up, so you are moving through the footage rather than watching it.

## Things in here worth a look if you write code

**Two cuts of the same film.** A 16:9 video cover-cropped into a portrait phone shows only
its middle quarter, so there is a second, natively vertical cut. The gate picks one before
any fetch starts, and a visitor only ever downloads the one that fits their screen. Rotating
a tablet aborts the in-flight fetch, revokes the old object URL and loads the other cut.

**The video is fetched as a Blob, not streamed.** Plenty of static hosts lack HTTP Range
support, and without it every seek clamps to zero, so scrubbing silently does nothing in
production while working perfectly on localhost. Fetching the whole file and playing an
object URL works everywhere. It streams behind a progress ring with a watchdog that aborts
after 20 seconds of no progress and falls back to a still image.

**Scroll position is never written straight to `currentTime`.** It is eased toward, in a
`requestAnimationFrame` loop that stops when it converges and when the hero leaves the
screen. The smoothing is normalised against a 60fps reference so a 120Hz display converges at
the same speed rather than twice as fast.

**Seeks are gated.** Writing `currentTime` while a previous seek is in flight piles them up,
which is most of the difference between smooth and choppy in Chrome. Requests coalesce to
the newest target and the busy flag resets on `error`, so the gate cannot deadlock.

**Text over moving footage is measured, not eyeballed.** Every caption band was audited by
hiding the glyphs, screenshotting the real composited page at that scroll position, and
finding the lightest pixel inside the text's bounding box. All five bands clear 3.5:1 against
the actual video frames.

**Reduced motion is honoured live, in both directions.** Turning it on mid-session pins every
scroll-drawn element to its finished state and stops the drives. Turning it back off re-arms
them rather than leaving the page stuck.

## Structure

```
index.html     the entire site
assets/        two video cuts, their posters, the dashboards, a CV
```

## The interactive bit

Scroll to the project section and press and hold "Hold to resolve". Ninety four inconsistent
spellings of one workshop title collapse into a single canonical title while a counter runs
94 down to 1. Releasing early eases it back rather than snapping. It is a real thing that
happened on the capstone project, made into something you can do with your thumb.

## Contact

apy270602@gmail.com / [LinkedIn](https://www.linkedin.com/in/aditya-pratap-yadav-6505742a5/)
