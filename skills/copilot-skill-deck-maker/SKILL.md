---
name: copilot-skill-deck-maker
description: Create a self-contained HTML presentation from notes, meeting recaps, or a topic. Use for requests like make a deck, build slides, deck from these notes, create a presentation, presentation about X, turn this recap into slides, or make an HTML deck.
---
# Copilot Skill Deck Maker
You turn rough material into a polished single-file HTML deck.
This skill is for Microsoft partner consultants who need a sharp browser-based deck without cloning Johan Wallquist's full presentation framework. It distills the useful parts: brief, outline, build, polish. Keep the workflow fast. The output is one HTML file that can be sent, opened, and presented in any modern browser.
## MANDATORY outcome
Every run produces one self-contained `.html` file with:
- All CSS and JavaScript inline.
- No runtime dependencies.
- No PowerPoint requirement.
- Arrow-key navigation.
- Fullscreen with `f`.
- Hidden presenter view using `?presenter=notes`.
- Speaker notes stored in the same file, invisible to the audience.
- Partner-branded colours, fonts, and tone when a homepage URL is provided.
If the user asks for PowerPoint, explain that this skill creates the browser deck first. They can export to PDF from the browser if needed.
## Trigger phrases
Use this skill when the user says anything close to:
- Make a deck from these notes.
- Build slides about this topic.
- Turn this meeting recap into a presentation.
- Create a partner-ready HTML deck.
- Make a browser deck.
- Presentation about X.
- Slides for tomorrow.

## Phase 1: Brief

Collect only what is missing. Do not interview the user if the prompt already has enough signal.

Minimum brief:

1. Topic or source notes.
2. Audience.
3. Desired length, default to 6 to 8 slides if unknown.
4. Partner brand homepage, optional but recommended.
5. Tone, default to direct consultant-peer language.
6. Desired file name, default to a short slug from the topic.

If the user gives a meeting recap, extract:

- Decisions.
- Tensions.
- Open questions.
- Commercial implications.
- Clear next steps.

If the material is thin, build a short deck. Do not pad.

## Phase 2: Outline

Create the outline before writing HTML. Keep it visible in chat unless the user explicitly asked for direct file generation.

Use this structure:

1. Hook: why this matters now.
2. Situation: what is happening.
3. Implication: what changes for the audience.
4. Proof or example: one concrete case, demo, metric, or pattern.
5. Action: what the audience should do next.

For most decks, use 5 to 8 slides. For a quick meeting recap, use 3 to 5.

Each outline line must include:

- Slide title.
- One key idea.
- Suggested component.
- Speaker note intent.

Allowed components:

- Hero.
- Big statement.
- Two-column split.
- Card grid.
- Metric strip.
- Timeline.
- Process steps.
- Quote.
- CTA.

Do not use more than three component types in a tiny deck. Visual rhythm matters, but so does coherence.

## Phase 3: Build

Create exactly one HTML file.

Use the template below as the base. Replace the sample slides with the generated deck. Keep the runtime intact.

### Brand matching

When the user provides a partner homepage:

1. Fetch the homepage.
2. Sample 2 to 3 dominant colours from CSS variables, inline styles, logo areas, buttons, and headings.
3. Prefer one dark or neutral background, one primary accent, and one warm or cool support colour.
4. Detect font signals from CSS. If custom fonts are blocked, choose a safe pair that matches the feel.
5. Sample tone from homepage headings and short copy. Use it lightly. Do not imitate slogans.
6. Apply the result as CSS variables in `:root`.

Default typography pairs:

- Professional consulting: `Aptos Display` or `Segoe UI Semibold` for headings, `Segoe UI` for body.
- Product-led firm: `Inter` for both, stronger weight contrast.
- Engineering-heavy firm: `Segoe UI` for body, `Consolas` for code or terminal moments.
- Premium advisory: `Georgia` for display accents, `Segoe UI` for body.

Keep brand matching tasteful. If the site is visually messy, use one accent colour and a clean neutral base.

### Deck rules

Apply these rules to visible slide text and speaker notes.

- One idea per slide.
- Body text stays under 40 words per slide.
- No wall of bullets.
- No generic agenda slide for short decks.
- No final slide that only says thank you.
- End with an ask, decision, or practical next step.
- Titles should create curiosity or state a useful claim.
- Avoid orphan words in titles. Use deliberate line breaks when needed.
- Pills and labels are content-width, never stretched.
- Use the same visual motifs across the deck.
- Speaker notes must never say "on this slide" or refer to slide numbers.
- Speaker notes use `SAY:` and `DO:` blocks.
- Notes are glance-friendly. Short phrases, not paragraphs.

### Anti-AI writing rules

Run this check before final output:

- Zero em dashes.
- No `not just X, but Y` framing.
- No `not only, but also` framing.
- No reflexive rule-of-three titles.
- Avoid `Here's the thing` and similar reveal phrases.
- Avoid gerund starters such as `Leveraging`, `Building on`, or `Driving`.
- Vary sentence length.
- Vary sentence openings.
- Prefer concrete nouns, named tools, and direct asks.

If any visible text breaks these rules, rewrite it before saving.

## Phase 4: Polish

Before handing over the file:

1. Open it mentally as a presenter, not as a document.
2. Check that every slide has speaker notes.
3. Confirm keyboard navigation works in the inline script.
4. Confirm `?presenter=notes` renders presenter view.
5. Confirm there are no external assets except optional Google Fonts.
6. Confirm the final slide has a clear next step.
7. Confirm the file name is descriptive, for example `partner-kickoff-recap.html`.

If browser automation is available, open the file and walk forward and back with arrow keys. If not, inspect the runtime carefully.

## Output format

When finished, tell the user:

- File created.
- How to open presenter view: add `?presenter=notes` or press `p`.
- Navigation: arrow keys, Home, End, and `f` for fullscreen.
- That it is safe to send as a single file.

## HTML template to emit

Copy this structure and replace the content between `<!-- SLIDES -->` and `<!-- END SLIDES -->`. Keep one `<aside class="notes">` after each slide.

```html
<!doctype html>
<html lang="en">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width,initial-scale=1">
<title>{{DECK_TITLE}}</title>
<style>
:root{
  --bg:#0b1020;
  --surface:#121a2f;
  --surface-soft:#18223a;
  --fg:#f7f8fb;
  --muted:#aab3c5;
  --line:rgba(255,255,255,.14);
  --accent:#5eead4;
  --accent-2:#f59e0b;
  --accent-soft:rgba(94,234,212,.16);
  --font-display:"Segoe UI",Aptos,Arial,sans-serif;
  --font-body:"Segoe UI",Aptos,Arial,sans-serif;
  --font-mono:Consolas,"Courier New",monospace;
}
*{box-sizing:border-box}
html,body{margin:0;height:100%;background:var(--bg);color:var(--fg);font-family:var(--font-body);overflow:hidden}
body{background:radial-gradient(circle at 18% 12%,var(--accent-soft),transparent 30%),var(--bg)}
.stage{width:100vw;height:100vh;display:grid;place-items:center;overflow:hidden}
.deck{width:min(100vw,calc(100vh * 16 / 9));height:min(100vh,calc(100vw * 9 / 16));position:relative;overflow:hidden;background:var(--bg);box-shadow:0 24px 80px rgba(0,0,0,.35)}
.slide{position:absolute;inset:0;padding:6vmin 7vmin;display:flex;flex-direction:column;justify-content:center;gap:3vmin;opacity:0;transform:translateX(2%);transition:opacity .28s ease,transform .28s ease;pointer-events:none}
.slide.active{opacity:1;transform:none;pointer-events:auto}
.eyebrow{display:inline-flex;align-self:flex-start;border:1px solid var(--line);border-radius:999px;padding:.45rem .75rem;color:var(--accent);font:700 clamp(11px,1.2vmin,14px)/1 var(--font-mono);letter-spacing:.12em;text-transform:uppercase;background:rgba(255,255,255,.04)}
h1,h2{font-family:var(--font-display);letter-spacing:-.04em;line-height:.98;margin:0;text-wrap:balance}
h1{font-size:clamp(52px,8vmin,112px);max-width:12ch}
h2{font-size:clamp(36px,5.2vmin,70px);max-width:15ch}
p{font-size:clamp(18px,2.2vmin,28px);line-height:1.45;color:var(--muted);max-width:58ch;margin:0}
.lead{font-size:clamp(22px,2.7vmin,34px);color:var(--fg);max-width:42ch}
.grid{display:grid;grid-template-columns:repeat(2,minmax(0,1fr));gap:2vmin}
.card{background:linear-gradient(180deg,rgba(255,255,255,.08),rgba(255,255,255,.035));border:1px solid var(--line);border-radius:24px;padding:2.2vmin;min-height:18vmin}
.card h3{font-size:clamp(20px,2.4vmin,30px);margin:.2rem 0 .7rem;font-family:var(--font-display)}
.card p{font-size:clamp(15px,1.6vmin,21px)}
.metric{font-family:var(--font-display);font-size:clamp(56px,10vmin,130px);font-weight:800;color:var(--accent);line-height:.9}
.split{display:grid;grid-template-columns:1.05fr .95fr;gap:4vmin;align-items:center}
.quote{font-size:clamp(28px,4.2vmin,58px);line-height:1.12;font-family:var(--font-display);max-width:17ch}
.cta{display:inline-flex;align-self:flex-start;margin-top:1vmin;border-radius:999px;background:var(--accent);color:#061014;padding:1rem 1.35rem;font-weight:800;text-decoration:none;font-size:clamp(17px,1.8vmin,24px)}
.footer{position:absolute;left:7vmin;right:7vmin;bottom:4vmin;display:flex;justify-content:space-between;color:var(--muted);font:600 12px var(--font-mono);letter-spacing:.08em;text-transform:uppercase}
.progress{position:absolute;left:0;bottom:0;height:4px;background:var(--accent);width:0%;transition:width .2s ease}
.presenter{height:100vh;display:grid;grid-template-columns:1.1fr .9fr;background:#07090f;color:var(--fg)}
.preview{display:grid;place-items:center;border-right:1px solid var(--line);padding:24px}.preview iframe{width:min(90vw,960px);aspect-ratio:16/9;border:0;background:var(--bg);transform:scale(.9)}
.notes-pane{padding:32px;overflow:auto}.notes-pane h1{font-size:28px;max-width:none;margin-bottom:14px}.notes-pane pre{white-space:pre-wrap;font:20px/1.55 var(--font-body);color:var(--fg)}
.notes-meta{color:var(--accent);font:700 12px var(--font-mono);letter-spacing:.12em;text-transform:uppercase;margin-bottom:18px}
@media (max-width:800px){.slide{padding:7vmin}.grid,.split{grid-template-columns:1fr}.presenter{grid-template-columns:1fr}.preview{display:none}}
</style>
</head>
<body>
<div class="stage" id="stage"><main class="deck" id="deck">
<!-- SLIDES -->
<section class="slide active" data-title="{{SLIDE_TITLE}}">
  <span class="eyebrow">{{SECTION_LABEL}}</span>
  <h1>{{TITLE}}</h1>
  <p class="lead">{{LEAD}}</p>
  <div class="footer"><span>{{DECK_SHORT_TITLE}}</span><span>1 / {{TOTAL}}</span></div>
</section>
<aside class="notes" hidden>
DO:
- Pause before the key claim.

SAY:
{{SPEAKER_NOTES}}
</aside>
<!-- END SLIDES -->
<div class="progress" id="progress"></div>
</main></div>
<div class="presenter" id="presenter" hidden>
  <div class="preview"><iframe id="thumb" title="Current slide preview"></iframe></div>
  <section class="notes-pane"><div class="notes-meta" id="count"></div><h1 id="noteTitle"></h1><pre id="noteText"></pre></section>
</div>
<script>
(function(){
  const params = new URLSearchParams(location.search);
  const isPresenter = params.get("presenter") === "notes";
  const slides = [...document.querySelectorAll(".slide")];
  const notes = [...document.querySelectorAll(".notes")];
  const stage = document.getElementById("stage");
  const presenter = document.getElementById("presenter");
  const progress = document.getElementById("progress");
  let index = Math.max(0, Math.min(slides.length - 1, Number(params.get("slide") || 0)));
  const channelName = (document.title || "deck").toLowerCase().replace(/[^a-z0-9]+/g,"-") + "-presenter";
  const channel = "BroadcastChannel" in window ? new BroadcastChannel(channelName) : null;

  function show(i, send=true){
    index = Math.max(0, Math.min(slides.length - 1, i));
    slides.forEach((s,n)=>s.classList.toggle("active", n === index));
    if(progress) progress.style.width = ((index + 1) / slides.length * 100) + "%";
    if(isPresenter) renderNotes();
    if(send) broadcast();
  }
  function broadcast(){
    const msg = {type:"slide", index};
    if(channel) channel.postMessage(msg);
    try{localStorage.setItem(channelName, JSON.stringify({...msg, t:Date.now()}));}catch(e){}
  }
  function renderNotes(){
    stage.hidden = true; presenter.hidden = false;
    document.getElementById("count").textContent = `Slide ${index + 1} of ${slides.length}`;
    document.getElementById("noteTitle").textContent = slides[index].dataset.title || slides[index].querySelector("h1,h2")?.textContent || "Slide";
    document.getElementById("noteText").textContent = notes[index]?.textContent.trim() || "No notes.";
    const thumb = document.getElementById("thumb");
    if(thumb) thumb.src = location.pathname + "?slide=" + index;
  }
  function next(){show(index + 1)}
  function prev(){show(index - 1)}
  function openPresenter(){
    const url = location.pathname + "?presenter=notes&slide=" + index;
    const win = window.open(url, "presenter", "width=1200,height=760");
    if(!win) alert("Allow popups for presenter view, or open this file with ?presenter=notes.");
  }
  document.addEventListener("keydown", e => {
    const k = e.key.toLowerCase();
    if(["arrowright","pagedown"," "].includes(k)){e.preventDefault();next();}
    if(["arrowleft","pageup"].includes(k)){e.preventDefault();prev();}
    if(k === "home") show(0);
    if(k === "end") show(slides.length - 1);
    if(k === "f") document.documentElement.requestFullscreen?.();
    if(k === "p" && !isPresenter) openPresenter();
  });
  if(channel) channel.onmessage = e => { if(e.data?.type === "slide") show(e.data.index, false); };
  window.addEventListener("storage", e => { if(e.key === channelName){ try{ const msg = JSON.parse(e.newValue); if(msg.type === "slide") show(msg.index, false); }catch(err){} } });
  if(isPresenter) renderNotes(); else { stage.hidden = false; presenter.hidden = true; show(index, false); }
})();
</script>
</body>
</html>
```

## Slide content patterns

### Hero

Use for the opening claim. One title and one line of context.

```html
<section class="slide" data-title="The work moved">
  <span class="eyebrow">Partner briefing</span>
  <h1>The work moved.<br>The process did not.</h1>
  <p class="lead">AI changed the effort curve. Most delivery models still price like nothing happened.</p>
  <div class="footer"><span>Frontier Consultancy</span><span>1 / 6</span></div>
</section>
```

### Two-column split

Use for a choice, a tension, or a before and after. Do not overload it.

```html
<section class="slide" data-title="Where time leaks">
  <div class="split">
    <div><h2>Where time leaks</h2><p>Meeting notes become slides, actions, status updates, and follow-up emails. Each handoff costs attention.</p></div>
    <div class="card"><h3>Copilot can take the first pass</h3><p>The consultant still owns judgement. The agent removes the blank page.</p></div>
  </div>
  <div class="footer"><span>Delivery pattern</span><span>2 / 6</span></div>
</section>
```

### Card grid

Use for a small set of related ideas. Two cards is often enough.

```html
<section class="slide" data-title="What the deck needs">
  <h2>What the deck needs</h2>
  <div class="grid">
    <div class="card"><h3>One claim</h3><p>The audience should remember one useful thing.</p></div>
    <div class="card"><h3>One next step</h3><p>The close should make action obvious.</p></div>
  </div>
  <div class="footer"><span>Structure</span><span>3 / 6</span></div>
</section>
```

### CTA

Use for the final slide. Make the ask specific.

```html
<section class="slide" data-title="Start with one meeting">
  <span class="eyebrow">Next step</span>
  <h2>Start with one meeting recap.</h2>
  <p>Paste the notes. Ask for a browser deck. Edit the judgement, not the formatting.</p>
  <a class="cta" href="mailto:you@company.com?subject=Deck maker pilot">Pilot it this week</a>
  <div class="footer"><span>Action</span><span>6 / 6</span></div>
</section>
```

## Speaker notes pattern

Each slide gets one hidden notes block directly after it.

```html
<aside class="notes" hidden>
DO:
- Let the title sit for a beat.

SAY:
The point is simple. We lose time between the meeting and the next useful artifact.
That is exactly where Copilot can help.
</aside>
```

Rules for notes:

- No slide references.
- No long paragraphs.
- No filler.
- Include a pause cue only when it helps delivery.

## File naming

Use descriptive local filenames:

- `customer-kickoff-recap.html`
- `ai-readiness-briefing.html`
- `quarterly-review-deck.html`

Avoid `index.html` for generated local decks unless the user is building a hosted site.
