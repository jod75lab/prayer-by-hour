# Prayer by Hour

A small static site that shows one prayer intention for each hour. It follows the visitor's local clock and displays the current hour at the top and in the list.

## Edit the intentions

`data/intentions.csv` is the editable source. Open it in Excel, LibreOffice, or Google Sheets, change values in the `intention` column, and save or download it as UTF-8 CSV with the same filename and headers. The site reads this file directly, so there is no build step. Commit the updated CSV and publish the branch to update the site.

Keep the `record_id`, `hour`, `calendar_season`, and `liturgical_season` values unchanged unless you are also changing the lookup scheme. The site expects one row for every hour and season combination.

## Calendar behavior

- Hour and date use the visitor's local browser time.
- Calendar seasons use meteorological months for the selected hemisphere. The default `Auto` setting makes a best-effort guess from the browser's time-zone region; visitors can choose Northern or Southern manually. That choice is saved in the current browser. Northern seasons are spring March to May, summer June to August, autumn September to November, and winter December to February. Southern seasons are reversed.
- Liturgical season uses Gregorian Easter computus. Holy Week takes precedence over Lent from Palm Sunday through Holy Saturday. Easter includes Pentecost Sunday.
- Christmas is treated as December 25 through the Baptism of the Lord, calculated as the Sunday after January 6. Advent begins on the Sunday on or before December 3 and runs through December 24. Ordinary Time is the default.
- Local calendars can transfer Epiphany or other observances. The first version does not account for local feast transfers or the evening start of liturgical days.
- The `psalter_anchor` is a devotional guide to the rhythm of the day, not a claim that every civil hour is an appointed canonical hour.
- Time-zone region is only a rough clue to hemisphere, so use the selector if the automatic choice is wrong. Sunrise and sunset are calculated only after a visitor selects **Show my sunrise & sunset** and grants location access. Coordinates stay in page memory and are not saved or sent anywhere; the displayed times are estimates.

## Publish with GitHub Pages

In the repository, open **Settings → Pages**. Choose **Deploy from a branch**, select `main` and the root folder, then save. GitHub Pages can serve these files directly; GitHub Actions is not needed.

For a local preview, serve the repository folder over HTTP (for example, `python -m http.server 8000`) and open `http://localhost:8000`. The browser cannot load the CSV through a `file://` URL.
