# EAST 370 - Chinese Traditional Literature and Thought

## Romanization Rule (MASTER RULE)

**Use Pinyin in all original writing.** Birch's *Anthology of Chinese Literature* uses Wade-Giles romanization (e.g., T'ao Ch'ien, Juan Chi, Chang Heng). When writing analytical text, glossary entries, study guide prose, or any content not directly quoting Birch, use **standard Pinyin** instead:

| Birch (Wade-Giles) | Use This (Pinyin) |
|---|---|
| T'ao Ch'ien | Tao Yuanming (陶淵明) |
| Juan Chi | Ruan Ji (阮籍) |
| Chang Heng | Zhang Heng (張衡) |
| Chuang Tzu | Zhuangzi (莊子) |
| Hsien-yang | Xianyang |
| Hsu Yu | Xu You |

**When directly referencing Birch** (e.g., poem titles as they appear in the anthology, page citations, translator credits), keep Birch's romanization so students can find the passage in their copy.

**Pattern:** "Ruan Ji (Juan Chi in Birch) wrote eighty-two poems..." or just use Pinyin and let the glossary handle the cross-reference.

---

## RULE ZERO: Every Page Connects to the Index

**No page exists in isolation.** Every lesson page must be linked from https://omatty123.github.io/east370-site/ (index.html). This is not a "nice to have." It is the first thing I do after creating a page, before git push.

Specifically:
1. **Update the Literature grid** in index.html: replace `<span class="coming">Title</span>` with `<a href="lessons/filename.html">Title</a>`.
2. **Update the Thematic Studies** section if the page fits there.
3. **Cross-link from related pages** (e.g., a new Tang prose page should link from tang-poets.html and vice versa).
4. **Verify the link works** by checking the href path.

If I forget this step, the page is not done. Period.

---

## CANONICAL TEMPLATE — HARD RULE

**Every new lesson page MUST be built by copying the structure and CSS from `lessons/lu-ji-wen-fu.html`.** This is not a guideline. This is a template. Copy the HTML skeleton, copy the full `<style>` block, then replace the content.

**The file**: `~/east370-site/lessons/lu-ji-wen-fu.html`
**Live reference**: https://omatty123.github.io/east370-site/lessons/lu-ji-wen-fu.html

If a new page looks different from lu-ji-wen-fu.html, it is wrong. Fix it.

### How to Build a New Page

1. **Copy the entire `<style>` block** from lu-ji-wen-fu.html verbatim. Do not rewrite CSS. Do not invent new class names. Use the existing ones.
2. **Copy the HTML skeleton** (header, nav, sections, footer) and replace content.
3. **Add topic-specific accent colors** to `:root` if needed (e.g., `--tang: #8a3030;`) but NEVER remove or change the base palette.
4. **Use the existing component patterns** (cards, blockquotes, timelines, genre grids, structure lists, key-themes boxes, source cards). Do not invent new patterns when an existing one fits.

### Required Page Skeleton (from lu-ji-wen-fu.html)

```html
<!-- 1. Page Header: dark bar, back link, Chinese title, English title, metadata -->
<header class="page-header">
    <a href="../index.html" class="back">&larr; EAST 370</a>
    <div class="page-title">
        <span class="ch">中文標題</span>
        <span class="en">English Title</span>
        <span class="meta">Author, dates</span>
    </div>
</header>

<!-- 2. Sticky Nav: dark bar with section anchors -->
<nav class="nav">
    <a href="#section1">Section 1</a>
    <a href="#section2">Section 2</a>
    ...
</nav>

<!-- 3. Content Sections: alternating backgrounds -->
<section class="content-section" id="section1">
    <div class="section-label"><span class="chinese">漢字</span> SECTION TITLE</div>
    <div class="content-grid">
        <div class="card">
            <div class="card-head"><span class="chinese">漢字</span> Card Title <span class="meta">dates/pages</span></div>
            <div class="card-body">...</div>
        </div>
    </div>
</section>

<section class="content-section alt" id="section2">
    <!-- .alt gives the darker alternating background -->
</section>

<!-- 4. Sources Section -->
<section class="sources" id="sources">
    <div class="section-label">Sources &amp; Further Reading</div>
    <div class="sources-grid">
        <div class="source-card">
            <h4>Category</h4>
            <a href="..." target="_blank" rel="noopener">Source description</a>
        </div>
    </div>
</section>

<!-- 5. Footer: dark bar, centered (only place centering is allowed) -->
<footer>
    <div class="foot-chinese">中國文學與思想</div>
    <div class="foot-title">EAST 370 &middot; Chinese Traditional Literature and Thought</div>
    <div class="foot-term">WINTER 2026</div>
</footer>
```

### Available Component Patterns (from lu-ji-wen-fu.html)

| Component | Class | Use For |
|-----------|-------|---------|
| Content grid | `.content-grid` | 2-column card layouts (minmax 320px) |
| Three-col grid | `.content-grid.three-col` | 3-column layouts (minmax 240px) |
| Card | `.card` > `.card-head` + `.card-body` | All content blocks |
| Blockquote | `blockquote` with `cite` | Quoted passages (MUST have page number) |
| Timeline | `.mini-timeline` > `.timeline-item` | Chronological events |
| Genre grid | `.genre-grid` > `.genre-item` | Categorized items with Chinese + English + description |
| Structure list | `.structure-list` > `.structure-item` | Numbered/ordered breakdowns |
| Key themes box | `.key-themes` | Highlighted analysis boxes with gold gradient |
| Section label | `.section-label` > `.chinese` | Every section header |
| Source card | `.source-card` | Bibliography/links |

### Card Count Rule — NO ORPHAN CARDS

**Never put an odd number of cards in a `.content-grid` or a number that doesn't divide evenly into the column count.** The default grid (`minmax(320px, 1fr)`) creates 2 or 3 columns depending on viewport width. If you have 4 cards, on a 3-column screen one card orphans on a second row with dead space beside it. This looks terrible.

Rules:
- **2 cards per grid** is the default and almost always correct. This is what lu-ji-wen-fu.html does.
- **3 cards** only with `.content-grid.three-col` (e.g., discussion questions).
- **4 cards?** Consolidate into 2. Combine related content using `<h4>` sub-headers within a single card-body.
- **Never 1 card alone** in a grid. Use full-width (`grid-template-columns: 1fr`) or just skip the grid wrapper.
- If a section has both an image card and content cards, put the image + stats in one 2-col row, then narrative in a separate full-width row below.

## Page-Building Spec (MANDATORY for all new lesson pages)

Every time I'm asked to take a reading, research it, and build a webpage, I follow ALL of these rules. No exceptions, no shortcuts.

### 1. DESIGN SYSTEM

#### CSS Variables (use these, don't invent new ones)
```css
--ink: #1a1a1a;
--ink-light: #4a4a4a;
--ink-faint: #8a8a8a;
--paper: #fafaf8;
--paper-dark: #f0ede8;
--gold: #b8860b;
--gold-light: #daa520;
--teal: #2d5a5a;
```
Topic-specific accent colors are allowed (e.g., --wang, --li, --du for Tang poets) but must complement the base palette.

#### Fonts
- **Body**: `'Inter', -apple-system, sans-serif`
- **Chinese text**: `'Noto Sans SC'` (default) or `'Noto Serif SC'` (for poetry/literary passages)
- Load via Google Fonts. Always include `preconnect` tags.

#### Layout Rules
- **Left-aligned text. Multi-column grids. Asymmetric layouts.**
- NO `text-align: center` on body content (footer is the one exception).
- Use CSS Grid (`grid-template-columns: repeat(auto-fit, minmax(Xpx, 1fr))`) for card layouts.
- Responsive breakpoints at 900px and 600px.

#### Page Structure (every page must have ALL of these)

1. **Page header** (`.page-header`): Dark bar (`background: var(--ink)`). Contains:
   - Back link: `← EAST 370` linking to `../index.html`
   - Chinese title (gold, Noto Sans/Serif SC)
   - English title (white)
   - Metadata: Birch page range, period label
2. **Sticky nav** (`.nav` or `.nav-strip`): Section anchors. Dark background or white with border.
3. **Content sections**: Alternating `var(--paper)` and `var(--paper-dark)` backgrounds.
4. **Section labels**: Small uppercase with Chinese character: `<div class="section-label"><span class="chinese">討論</span> Discussion Questions</div>`
5. **Footer**: Dark bar with Chinese title, English course name, "WINTER 2026", and back link to home.

#### Card Pattern
```
.card > .card-head (dark, with Chinese + English title) > .card-body (content)
```
Cards use `border-radius: 6px`, `box-shadow: 0 2px 8px rgba(0,0,0,0.04)`, white background.

### 2. CONTENT RULES

#### What Goes on Every Page
- **Executive Summary / Overview**: What is this reading? What period? What's the argument?
- **Text Analysis**: Cards or sections breaking down each text/author/poem in the reading.
- **Discussion Questions**: Numbered, substantive, tied to the reading. Not generic. Each question should reference specific passages, figures, or arguments.
- **Sources Section**: Primary text citation + verified external links.

#### Content Sourcing (HARD RULES)
- **Primary text is ALWAYS Birch** unless the user specifies otherwise. Cite as: `Birch, *Anthology of Chinese Literature* (Grove Press, 1965), pp. X–Y.`
- **Only use authors, readings, and materials explicitly in the syllabus or the assigned reading.** Never invent content.
- **Page range discipline**: If given "pp. 157–169", cover ONLY pp. 157–169. Do not drift into adjacent readings.
- **Translator credit**: Always name the translator for each piece. Birch's anthology uses multiple translators (Waley, Watson, Hightower, Graham, Acker, Kwock & McHugh, etc.). Name them.

#### Quotes
- Every blockquote needs an **exact page number** (not a year, not "p. 1839").
- Format: `<blockquote>"Quote text."<cite>— p. 163</cite></blockquote>`
- If quoting Birch's editorial commentary, say so: `— Birch, p. X`
- **Never fabricate quotes.** If uncertain, flag with `[verify]` rather than guessing.

### 3. SOURCING & LINKING

#### External Links (MANDATORY verification)
Every external link must be:
1. **Searched** (WebSearch) to find the real URL
2. **Verified** (WebFetch) to confirm it loads
3. Only then added to the document

**Never guess URLs.** This is a hard block.

#### Approved External Sources (prefer these)
| Source | Use For | Base URL |
|---|---|---|
| Stanford Encyclopedia of Philosophy | Philosophy entries | `https://plato.stanford.edu/entries/` |
| Chinese Text Project | Classical Chinese texts | `https://ctext.org/` |
| Britannica | Biographical entries | `https://www.britannica.com/` |
| 讀古詩詞網 | Chinese originals | `https://fanti.dugushici.com/` |

Other scholarly sources are fine, but verify them.

#### Internal Links
- Every page links back to `../index.html` (header + footer).
- Cross-link to related lesson pages where relevant (e.g., on-seclusion links to recluse-poetry).
- After creating a new page, **update index.html** to link to it (replace `<span class="coming">` with an `<a>` tag if applicable).

#### Chinese Original Texts
When including Chinese originals, use the collapsible pattern:
```html
<details class="chinese-original">
  <summary>Chinese Original <span class="ch-label">原文</span></summary>
  <div class="original-text">...</div>
  <span class="source-link">Source: <a href="VERIFIED_URL" target="_blank">Source Name</a></span>
</details>
```
- Source the Chinese text from a reputable digital library (ctext.org, dugushici.com, etc.).
- **Verify the source URL loads.**

### 4. RESEARCH PROCESS

When asked "take this reading and make a page," follow this sequence:

1. **Confirm scope**: What pages? What's the reading? Ask if unclear.
2. **Read the actual text** (if available as PDF/file) or work from the user's description.
3. **Research context**: Use WebSearch for historical/philosophical background. Stick to verified scholarly sources.
4. **Find Chinese originals**: Search dugushici.com or ctext.org. Verify URLs.
5. **Find external reference links**: SEP, Britannica, etc. Verify every URL.
6. **Build the page**: Follow the design system above.
7. **Update index.html**: Add/update the link to the new page.
8. **Git push**: Commit, push, and open the live site.

### 5. QUALITY CHECKS (before pushing)

- [ ] All external links verified (WebFetch or WebSearch)?
- [ ] Page range matches what was assigned?
- [ ] Romanization follows the master rule (Pinyin primary, Wade-Giles for Birch references)?
- [ ] Chinese characters included for all proper names on first mention?
- [ ] Every blockquote has a page number?
- [ ] Discussion questions reference specific texts/passages?
- [ ] index.html updated?
- [ ] Back link works (← EAST 370)?
- [ ] Footer has course info?
- [ ] Responsive design tested (cards stack on mobile)?

### 6. WHAT NOT TO DO

- **Don't center text.** Left-align everything except the footer.
- **Don't invent readings.** If it's not in Birch or the syllabus, don't add it.
- **Don't use em dashes excessively.** One per paragraph max. Use periods, commas, colons.
- **Don't skip translator credits.** Every translated passage needs attribution.
- **Don't link to unverified URLs.** Search first. Fetch first. Then link.
- **Don't make generic discussion questions.** "What do you think about X?" is lazy. Tie questions to specific textual evidence and philosophical problems.
