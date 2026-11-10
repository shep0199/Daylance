# Daylance
MTM1544 Week 7:
## Breakpoints (found by widening the browser in Chrome DevTools)

I started at 320px and widened the browser slowly, noting where the layout stopped looking right.

- **~401px:** below this, the 5 nav links wrap onto two lines. No media query needed, `flex-wrap: wrap` handles it.
- **600px (2 columns):** at 599px one card was over 550px wide with lots of empty space. At 600px two cards fit (~260px each) without "Upcoming Tasks" wrapping onto two lines.
- **720px (header):** below this, "Daylance" and the nav links are too crowded to sit side by side, so the header stays stacked. This was 600px before styling, but once the nav links got padding they wrapped onto 2 rows next to the name from 600-699px. At 720px they fit on one row.
- **880px (3 columns):** from 880px, three cards fit side by side without looking cramped. Recent Messages becomes a tall column on the right, like my desktop mockup.

## Container query
- `.card` is a container (`container-type: inline-size`, `container-name: card`).
- At 500px+ card width, the card's items sit side by side using Grid.
- Tested in two spots: from 600-879px, Recent Messages spans 2 columns (wide spot), so its 4 messages sit in a row, while the other cards (narrow spots) stay stacked at the same screen width.

## Small-screen decisions (not shown in the mockup)
- **Header:** the name stacks above the nav on phones, and links wrap instead of shrinking, so all 5 pages stay easy to tap.
- **Cards:** 1 column on phones instead of a sideways scroll, keeping the same order as desktop. Phone cards are white with a thin border, like my phone mockup.
- **Recent Messages:** spans 2 columns from 600px so the grid has no empty gap, then becomes a tall right-hand column from 880px.
- **Form:** fields are full width so they're easy to tap. Radio options stack one per row so a label never gets split from its button.
- **Table:** stays a table on phones. At 320px all 4 columns still fit, so no horizontal scroll was needed. Text is left-aligned to match the page.
- **100dvh:** used `min-height: 100dvh` on the wrapper so the footer stays at the bottom of short pages.

## Fluid sizing
- Site heading uses `clamp(1.75rem, 1rem + 3vw, 2.75rem)`.
- Intro text and forms are capped at `max-width: 65ch`.
- `img { max-width: 100%; height: auto; }` applied site-wide.

## Testing
- **Real phone:** iPhone 13, Safari. Homepage and calendar page checked. Found that iOS Safari shows date/time inputs wider than other fields. The full fix was added in Week 8 (see Week 8 testing).
- **Second browser:** Safari on Mac (I normally use Chrome).
- **Chrome DevTools:** checked every width from 320px to 1440px with no horizontal scroll.

A freelancer organizer that keeps schedules, clients, income, content and messages in one place, because a freelancer's work is usually scattered across many apps.

## MTM1511 Midterm: Multi-Page Site

### Pages
- index.html: Home dashboard (profile avatar, welcome, mini calendar, tasks, recent messages)
- calendar.html: Add an Event form and a table of upcoming events
- messages.html: Recent client messages and a Send a Message form (the site's contact form)
- income.html: Table of client payments with a total
- content.html: Empty uploads state, upcoming posts, and content ideas
- result.html: Confirmation page that both forms submit to. It isn't in the nav because it's only reached by submitting a form.

### Departures from the plan
- The brief suggests Home, About, Projects/Work and Contact pages. Daylance follows my Week 5 site map instead, using app-style pages (Calendar, Messages, Income, Content) that suit a freelancer tool.
- The contact form lives on the Messages page ("Send a Message"), since that's where a freelancer contacts clients.
- The Content page shows an empty-state section ("No content uploaded yet") with a folder icon. In a finished version, this would only appear when a user has no uploads.
- The Home page shows a default profile avatar that users would later replace with their own photo.

### Folders and files
- images/: profile-avatar.jpeg and folder-icon.png, both credited in the footer of the page that uses them
- style.css: all styles for the site

### Image credits
- Profile avatar by WandererCreative from Pixabay: https://pixabay.com/vectors/blank-profile-picture-mystery-man-973460/
- Folder icon by janjf93 from Pixabay: https://pixabay.com/vectors/folder-flat-design-icon-symbol-2103508/

### Accessibility and validation testing (Nov 8, 2026)
- Keyboard test: PASSED on all 6 pages. Skip link appears on the first Tab, focus is visible on every link and form control, and both forms submit using only the keyboard.
- Lighthouse Accessibility: PASSED with 100% on all 6 pages.
- W3C Markup Validator: PASSED with zero errors on all 6 pages.

### Note on forms
Both forms use method="post" because they send new data that includes client details, which shouldn't appear in the URL. On GitHub Pages, submitting a form shows a "405 Not Allowed" error because static hosting can't receive POST data. The forms are built correctly and would work on a real server.

## MTM1544 Project: Styling the MTM1511 Midterm Site

- One external stylesheet (style.css) linked from all 6 pages, with `box-sizing: border-box` set globally.
- Typography: system font stack ending in `sans-serif`, all font sizes in `rem`, `line-height` 1.6 for body text and 1.2 for headings.
- Colour palette: warm whites with navy text, documented at the top of style.css with names by job (Ink, Muted, Page, Surface, Card, Brand...). Every text/background pair, plus hover and focus states, was checked with the WebAIM contrast checker and passes AA. I changed the focus outline from #f59e0b to #b45309, because the lighter amber was only about 2:1 on white and focus outlines need 3:1.
- Grid: page layout on `.wrapper` (header / main / footer), dashboard cards, upcoming posts, and forms.
- Flexbox: header, nav links, welcome section, Recent Messages rows, empty uploads box.
- Mobile-first: `min-width` queries only, at 600, 720 and 880px, each chosen from where the content broke (see Breakpoints above).

### Why Grid and Flexbox where I used them
- **Grid for the page and the dashboard:** both are two-dimensional. The wrapper needs rows that size differently (`auto 1fr auto`) so the footer stays at the bottom. The dashboard needs rows and columns at the same time, because Recent Messages spans 2 rows on the right like my mockup. Flexbox only lays things out in one direction, so it can't do that.
- **Flexbox for the nav bar:** the links are one row of items with different widths that just need to sit side by side and wrap on small screens. That's a one-dimensional problem, so Flexbox with `flex-wrap` and `gap` fits, and there are no columns to line up.

### How the palette works on a new page
The colours are named by job, so a page I haven't built (for example, a Settings or Invoice page) would use them the same way: Page for the background, Surface for panels and inputs, Card for grouped content, Ink for headings and text, Muted for helper text, Brand for the main button, and Brand tint for the selected item. No new colours would be needed, and every pair is already checked.

### Week 8 testing
- Chrome DevTools: all 6 pages checked from 320px to 1440px, no horizontal scroll.
- Real phone (iPhone 13, Safari): found the date and time fields running off the right edge of the Calendar page, because Safari's built-in date styling ignores `width: 100%`. Fixed with `appearance: none` (and `-webkit-appearance: none` for Safari) on those two fields. Re-tested: all pages fit with no layout breaks.
- W3C CSS Validator: 0 syntax errors in my own code. It flags 3 lines (`container-type`, `container-name`, `@container`) for my container query. As the Week 7 Container Queries module says, "The W3C CSS Validator has not caught up yet and will report an error here. That is the tool lagging the specification, not a problem with your code." The 1 warning is `-webkit-appearance`, which I kept on purpose because Safari on iPhone needs it to keep the date and time fields on screen.
- Lighthouse Accessibility and keyboard test re-run after styling: PASSED.