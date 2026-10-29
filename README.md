# Daylance
MTM1544 Week 7:
## Breakpoints (found by widening the browser in Chrome DevTools)

I started at 320px and widened the browser slowly, noting where the layout stopped looking right.

- **~401px:** below this, the 5 nav links wrap onto two lines. No media query needed, `flex-wrap: wrap` handles it.
- **600px (header):** below this, "Daylance" and the nav links are too crowded to sit side by side, so the header stays stacked. At 600px they fit in one row with space between.
- **600px (2 columns):** at 599px one card was over 550px wide with lots of empty space. At 600px two cards fit (~260px each) without "Upcoming Tasks" wrapping onto two lines.
- **880px (3 columns):** from 880px, three cards fit side by side without looking cramped. Recent Messages spans 2 columns so the grid has no empty gap.