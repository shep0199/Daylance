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