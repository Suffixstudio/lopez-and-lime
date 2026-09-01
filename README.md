# Lopez & Lime booking app

A single-page booking form for Lopez & Lime, Mobile Bar + Events.
One file, no build step, no server. Deploys to Netlify as-is.

## Before you go live

Open `index.html` and find this block near the bottom (search for "EDIT THESE TWO LINES"):

```js
var MY_PHONE = "(714) 873-2402";
var MY_EMAIL = "lopezandlime@gmail.com";
```

Both are set to your real contact info now. Keep in mind what these
actually do, though: they only appear if a submission fails to send, as
a fallback so a customer is never left with no way to reach you. They
are **not** how bookings normally reach you day to day — that is the
"Turn on form notifications" step further down, which is a setting in
Netlify, not in this file. Make sure you point that at
`lopezandlime@gmail.com` too, or the two will disagree: this file's
fallback would be correct, but the address actually collecting your
real bookings would not be.

Your phone number is also shown for real in the footer of the page
itself (see "The footer phone number" below) — that is a separate line
of HTML, so if your number ever changes, update it in both places.

## Files in this project

- `index.html` — the app itself
- `logo.svg` — your logo, sized for the web. The page loads this file directly, so it must stay named `logo.svg` and sit next to `index.html`, unless you also update the `src` in the masthead.
- `lopezlimecocktail.jpg` — the small round photo next to "The Lopez & Lime" in the house menu. See "The signature drink photos" below.
- `lopezlimesignaturephoto.jpg` — the full photo shown between Add-ons and Your drinks. Same section.
- `brand/` — your original approved master logo files (full-size vector and a 6000px transparent PNG). These are your source files for print: business cards, signage, invoices. Not used by the web app itself, just kept here so they travel with the project. Keep them out of anything that needs a small file size.

## Deploy

1. Create a new repository on GitHub named `lopez-and-lime`
2. Upload `index.html`, `logo.svg`, `lopezlimecocktail.jpg`,
   `lopezlimesignaturephoto.jpg`, the `brand` folder, and this README to it
3. Go to netlify.com, sign in with GitHub
4. Choose "Add new site", then "Import an existing project"
5. Pick the `lopez-and-lime` repository
6. Leave the build command blank and the publish directory as `/`
7. Click Deploy

Netlify gives you a URL like `lopez-and-lime.netlify.app`. Change it under
Site configuration, then Change site name.

## Turn on form notifications

Netlify will not email you until you tell it where to send things.

1. In Netlify, open your site
2. Go to Forms
3. Find the form named `booking`
4. Open Settings and notifications, then Add notification
5. Choose "Email notification"
6. Enter `lopezandlime@gmail.com` and save

Send yourself a test booking to confirm it arrives.

Netlify changed its pricing in September 2025: newer accounts are on a
credit-based plan where form submissions are free and unlimited, not
capped. Older accounts on the legacy plan still get 100 submissions a
month free, which is plenty for a solo operator either way. Check your
own plan under Site configuration if you want the exact number, but you
are very unlikely to actually hit either limit.

You do not need Formspree or any other third-party form service on top
of this. The form is already wired for Netlify's own built-in handling
(that is what `data-netlify="true"` on the form, the hidden
`form-name` field, and the honeypot field are for), so turning on the
notification above is the only setup step. Adding Formspree would mean
a second service to configure, and its own free plan is more limited
than Netlify's, not less (50 submissions a month, no file uploads)
-- worth knowing only if you ever want form data that lives somewhere
other than Netlify.

## Making changes

Edit `index.html` on GitHub and commit. Netlify redeploys automatically
in about thirty seconds. The URL and the QR code never change.

## Changing the logo

Replace `logo.svg` with a new file and keep the same name, or update the
`src="logo.svg"` in the masthead (search for `class="logo-img"`) to point
at whatever you name it. Update the `alt="..."` text on that same line if
the wording on the logo changes. If you swap in a PNG or JPG instead of an
SVG, it will still work, but it won't stay sharp on very large screens.

## The footer phone number

The footer (search for `Questions? `) shows your real number, right
below your certifications and service area. "Call" and "text" are each
their own tappable link, not one link with generic phrasing -- a phone
number link can only ever do one thing when tapped, either open the
dialer or open a text, never offer a choice of both. So "Call" opens the
dialer with your number ready to go, and "text" opens a text to your
number instead, each doing exactly what it says.

It offers both rather than just one on purpose. Solo operators miss a
lot of live calls simply because they are mid-job -- setting up,
serving, or driving -- so offering text gives a customer a way to reach
you that does not depend on you being free to pick up right that
second. Call-only would be too narrow the other way: some people would
rather just call, and nothing about offering both costs you anything.

To change the number, it needs to be updated in two different formats,
each appearing twice, or the page will display one number while
actually calling or texting another:

- Search for `+17148732402` -- this is the digits-only format the
  links themselves use (`href="tel:+17148732402"` on "Call" and
  `href="sms:+17148732402"` on "text").
- Search for `873-2402` -- this is the friendly format people actually
  read: the visible text right after those two links, and the
  `MY_PHONE` fallback near the bottom of the file (see "Before you go
  live" above).

## The signature drink photos

There are two different photos of "The Lopez & Lime," used two different
ways.

**The small round one** sits next to "The Lopez & Lime" in the house menu
(search for `hp-photo`) so it stands out from the plain-text picks around
it — it is already the one drink singled out with brass-colored styling
instead of green, so the photo reinforces that rather than fighting it.
To swap it, replace `lopezlimecocktail.jpg` and keep the same name, or
update the `src="lopezlimecocktail.jpg"` next to `hp0` in the house menu
list to point at whatever you name it (see the naming note at the end of
this section first). A few things matter for it to look right at that
size:

- Crop it close and roughly square before you save it — the CSS displays
  it as a 26px circle and crops to a circle automatically, but it crops
  from the center, so anything important near the edges of a non-square
  photo gets cut off.
- Keep any text out of the photo itself (a title, an ingredient list, a
  logo baked into the image). It will be illegible at 26px regardless,
  and a circle crop will likely cut it off anyway.
- It does not need to be large. The current photo is saved at 200×200px,
  which is already more resolution than a 26px circle needs even on a
  sharp phone screen, and keeps the page fast to load. A full-resolution
  photo works too, but there is no visual benefit and it only slows down
  the page.

**The full photo** (search for `sig-photo`) runs as its own section
between Add-ons and Your drinks — the complete image, title, ingredient
list, logo and all, at up to 420px wide. To swap it, replace
`lopezlimesignaturephoto.jpg` and keep the same name, or update the
`src="lopezlimesignaturephoto.jpg"` in the `sig-photo` section to point
at whatever you name it (see the naming note below first). Unlike the
small round one, this photo is meant to be seen in full, so there is no
cropping to worry about — whatever aspect ratio you save it at is the
aspect ratio it displays at. It is still worth resizing and compressing
before you save it, though; the current photo is saved at 880px wide
(about 180KB) rather than its
original full camera resolution (which was over 10x that size), since a
screen showing it at 420px wide has no use for more pixels than that, and
the extra size would only slow the page down.

**A naming note:** both of these filenames are deliberately one run-on
word with no hyphens, spaces, or underscores. That is not a style
preference -- an earlier version used hyphens
(`lopez-lime-cocktail.jpg`), and they were silently stripped out
somewhere between downloading the file and uploading it to GitHub,
which broke both photos on the live site until it was caught. Whatever
you name a replacement photo, keep it to one unbroken word (letters and
numbers only) to sidestep that entirely.

## Adjusting the shopping list math

Search for `DRINKING_SHARE` in `index.html`:

```js
var DRINKING_SHARE = 0.75;
```

This assumes about 75% of guests actually drink, which allows for
designated drivers and non-drinkers. Raise it toward 1 to recommend
more alcohol, lower it to recommend less. This one number moves every
quantity on the list.

Search for `PROFILES` for the per-crowd-type splits. Each has a `rate`
multiplier and the liquor/beer/wine ratio.

The base formula is 2 drinks in the first hour, then 1 per hour after.
Search for `var drinks =` to change it.

**Important:** the Quick Reference table is hand-written HTML, so it
does NOT update automatically when you change these numbers. Search for
`class="ref-t"` and update the figures to match, or the table and the
live list will disagree. The current table matches the live calculation
exactly at each bracket ceiling for a 4 hour balanced event.

Ice and bottled water follow the same `weBring` switch as mixers and
garnish: customers on Bartender Only and The Mobile Bar still buy their
own (search for `weBring` inside the `shopping()` function), while
Signature Bar and Full House bring both, so their "You provide: alcohol
only" promise on the package card is actually true. The Quick Reference
table's Ice column only applies to the two packages where the customer
still buys it, and its caption says so.

## House menu picks and their extra ingredients

The house menu checkboxes (Margarita, Mojito, Moscow Mule, and so on)
mostly just tell you what the customer wants — the name gets sent to you
in the booking notification either way. But some of those drinks need an
ingredient the shopping list math above has no way to know about: mint
for a Mojito, ginger beer for a Moscow Mule, bitters for an Old
Fashioned. Search for `EXTRA_ITEMS` in `index.html`:

```js
var EXTRA_ITEMS = {
  'The Lopez & Lime':   ['Reposado tequila'],
  'Paloma':             ['Grapefruit soda (Jarritos or Squirt)'],
  'Mojito':             ['Mint'],
  'Old Fashioned':      ['Bitters', 'Simple syrup', 'Orange peel or cocktail cherries'],
  'Whiskey Sour':       ['Simple syrup'],
  'Ranch Water':        ['Topo Chico or sparkling mineral water'],
  'Moscow Mule':        ['Ginger beer'],
  'Daiquiri':           ['Simple syrup'],
  'Michelada':          ['Clamato or tomato juice', 'Hot sauce', 'Tajín or chili-lime seasoning'],
  'Sangria':            ['Brandy', 'Orange liqueur', 'Fresh fruit for the pitcher'],
  'Zero proof options': ['Extra sparkling water, juice, or NA spirits for mocktails']
};
```

When a customer checks one of these on Bartender Only or The Mobile Bar
(the two packages where they buy their own mixers), a short note appears
on their shopping list naming what to grab — no quantities, since that
depends on your real recipe and how many guests actually order that
specific drink, not the guest-count math above. On Signature Bar and
Full House, where you already bring mixers and garnish, the note is
skipped entirely; those extra ingredients are on you to bring, same as
everything else in that group.

Margarita, Cosmopolitan, and Beer & wine service are left out of this
list on purpose — they're already covered by the base spirits and
mixers above.

The Lopez & Lime is your own signature drink, and it is deliberately
**not** pre-checked. It needs reposado tequila specifically, and the
base shopping list only ever suggests blanco — so an event with no
tequila planned at all (or a vodka-only night) should not quietly
promise a tequila drink nobody bought the ingredients for. It's a
checkbox like any other on the house menu, just colored brass instead
of green so it still stands out as the signature. If the real recipe
needs more than reposado, add it to its line in `EXTRA_ITEMS` above.

## Adjusting prices

Prices live in two places per package and must match:

- `data-price` on the radio input (used for the estimate math)
- the `pkg-now` and `pkg-was` divs (what the customer sees)

Extra hours are `$70` each. Search for `* 70` and `+$70`.

Add-ons each have their own price. In the HTML, each one is a line like:

```html
<input type="checkbox" name="addon" value="Extra bartender" data-price="300">
```

`data-price` is a flat dollar amount. `data-per="4.5"` (used on the
Infused water station and the Mimosa bar) means dollars per guest
instead, and `data-price="0"` on those rows just means "no flat fee,
per-guest only." Change the number in either attribute, and update the
price shown next to it in `<span class="addon-price">` to match.

The extra bartender is priced at $300 for a 4 hour block. That assumes
paying that bartender around $40/hour yourself; the difference covers
your coordination time and the risk of representing your brand with
someone else's work. Adjust `data-price="300"` if your actual pay rate
changes.

## Setup and breakdown timing

Search for `SETUP_MIN` in `index.html`:

```js
var SETUP_MIN = 30, BREAKDOWN_MIN = 30, LAST_CALL_MIN = 15;
```

These drive the "Your day" timeline the customer sees. `SETUP_MIN` and
`BREAKDOWN_MIN` set how long before/after the booked hours you arrive
and pack up. `LAST_CALL_MIN` sets how many minutes before the bar
actually closes that last call happens. Change any of them if your
real timing is different, and the whole timeline updates automatically.

## The 11:30 PM cutoff

Search for `LATEST_CLOSE_MIN` in `index.html`:

```js
var LATEST_CLOSE_MIN = 23 * 60 + 30; // 11:30 PM
```

Closing time (start time plus booked hours) is never allowed to land
after this. A 6 or 7 hour booking simply can't start as late as a 4
hour one, so the "Bar opens at" list automatically grays out any start
time that would break the cutoff, and if a customer had already picked
a start time that no longer fits once they change the hours, it snaps
back to the latest one that still does. A short note explains why
whenever that happens. To move the cutoff, change the number of
minutes (it's written as `hour * 60 + minute` so it's easy to read) —
for example `22 * 60 + 30` for 10:30 PM, or `0` for midnight.

## Adjusting the travel fee

Search for `TRAVEL_FEE` in `index.html`. There are two lines together:

```js
var TRAVEL_FEE = 30;
var EXTENDED_CITIES = ['Canyon Lake','Chino Hills','Claremont','Lake Elsinore','Menifee','Murrieta','San Dimas','Temecula','Upland','Wildomar'];
```

Any city in that list gets the flat fee added automatically, and the
customer sees a note explaining why. Change the number, or add and
remove cities, and both the list and the math update together. Cities
not on the list (Corona, Riverside, the closer ones) never get the fee.

Picking "Somewhere else" (outside the whole service area) does not add
a fee automatically, since there is no way to price an unknown
location. Instead, the notes field becomes required so you always get
an actual place to work with, and both the estimate and the itemized
quote say plainly that the travel fee still needs to be confirmed with
you, instead of showing a total that looks final.

## No default date or start time

The event date and "Bar opens at" fields used to auto-fill (21 days
out, 5:00 PM) so the page looked ready to submit right away. That also
meant a customer could tab straight through and request a real date and
time they never actually chose. Both fields now start empty like every
other required field on the form, and `required` actually blocks
submission until a real choice is made. If you ever want a default
back, search for "No default date" and "Select a start time" in
`index.html`.

## Running the tests

There is a regression suite in `test.js`. Run it after any change:

```
npm install playwright
node test.js
```

It checks 129 things: every package price, that each hours option charges
exactly what its label promises, that each package card's own copy
matches what the form actually offers (signature cocktail count, guest
range), travel fees (including that "Somewhere else" requires a real
location before it will let you submit), add-on math, that the spirit
split adds up at every guest count from 1 to 150, that the reference
table agrees with the live list, that the quote line items sum to the
total, layout checks (no sideways scroll, badge not overlapping the
price, drink pills not reflowing, both signature-drink photos actually
loading and the full one sitting right before "Your drinks"), the
footer's call and text links (right number on each, both as the two
tappable links and in the "Something went wrong" fallback message), the
"Your day" timeline
(including the 11:30 PM cutoff, checked against every combination of
start time and hours), that booked hours survive switching packages
instead of silently changing, that ice and bottled water switch to "we
bring these" on the packages that promise "alcohol only," the
house-menu extras note (including that the signature drink can be
picked and un-picked like any other), that the event date and start
time have no default and actually block submission until chosen, form
validation, and that the page still works with JavaScript disabled.
It also checks a handful of visual details: the
estimate bar dims itself until a package is picked, the
disabled "already included" mobile-bar row stays legible instead of
fading to near-invisible, and the success screen collapses the hero
banner so "Request received" leads instead of repeating the full masthead.

It exits non-zero if anything fails, so it will not pass silently.

## Notes

- Client purchases and owns all alcohol. Do not add alcohol-inclusive
  packages without an ABC licensed catering partner.
- Prices shown are estimates. The form says a written quote follows.
