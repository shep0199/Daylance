# Daylance
MTM1544 Week 7:
## Breakpoints (found by widening the browser in Chrome DevTools)

I started at 320px and widened the browser slowly, noting where the layout stopped looking right.

- **~401px:** below this, the 5 nav links wrap onto two lines. No media query needed, `flex-wrap: wrap` handles it.
- **600px (header):** below this, "Daylance" and the nav links are too crowded to sit side by side, so the header stays stacked. At 600px they fit in one row with space between.
- **600px (2 columns):** at 599px one card was over 550px wide with lots of empty space. At 600px two cards fit (~260px each) without "Upcoming Tasks" wrapping onto two lines.
- **880px (3 columns):** from 880px, three cards fit side by side without looking cramped. Recent Messages spans 2 columns so the grid has no empty gap.

## Container query
- `.card` is a container (`container-type: inline-size`, `container-name: card`).
- At 400px+ card width, the card's items sit side by side using Grid.
- Tested in two spots: Recent Messages spans 2 columns (wide spot), so its 4 messages sit in a row, while the other cards (narrow spots) stay stacked at the same screen width.

## Small-screen decisions (not shown in the mockup)
- **Header:** the name stacks above the nav on phones, and links wrap instead of shrinking, so all 5 pages stay easy to tap.
- **Cards:** 1 column on phones instead of a sideways scroll, keeping the same order as desktop.
- **Recent Messages:** spans 2 columns on wider screens so the grid has no empty gap.
- **Form:** fields are full width so they're easy to tap.
- **Table:** stays a table on phones. At 321px all 4 columns still fit, so no horizontal scroll was needed. Text is left-aligned to match the page.
- **100dvh:** not used, since the site has no full-screen section.

## Fluid sizing
- Site heading uses `clamp(1.75rem, 1rem + 3vw, 2.75rem)`.
- Calendar intro and form are capped at `max-width: 65ch`.
- `img { max-width: 100%; height: auto; }` applied site-wide.

## Testing
- **Real phone:** iPhone 13, Safari. Homepage and calendar page checked. Found that iOS Safari shows date/time inputs wider than other fields, so I added a fix.
- **Second browser:** Safari on Mac (I normally use Chrome).
- **Chrome DevTools:** checked every width from 320px to 1200px with no horizontal scroll.

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