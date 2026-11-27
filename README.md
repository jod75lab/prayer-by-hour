# Prayer by Hour

A small static site that shows one prayer intention for each hour. It follows the visitor's local clock and displays the current hour at the top and in the list.

## Edit the intentions

The site reads `data/intentions.csv` directly. To edit a prayer, find its `weekday` and `hour` (0–23), then edit the `intention` for the desired season.

- Weekly rows have a blank `celebration`. A blank `natural_season` or `church_season` matches any value in that column. If both are blank, the prayer is used year-round.
- General always selects `Ordinary Time` for the Church-season lookup. Catholic selects the current Church season. Both calendars use the visitor's natural season. Keep exactly one matching row for each weekday, hour and combination of seasons.
- `psalter_anchor` supplies the Catholic label for the hour.
- Catholic Sunday Gospel rows have a `celebration`, a `gospel` reference and an original prayer in `intention`. The `lectionary_year` column takes A, B or C, or stays blank for a reading shared across the cycle. These rows supply the noon intention. Keep one matching Gospel row per celebration and cycle.
- The eight optional sunrise and sunset reflections use `Sunrise` or `Sunset` in the hour column and a natural season. They are appended when the visitor enables local sun times.

## Calendar behavior

- Hour and date use the visitor's local browser time.
- Each weekday, including Sunday, has 24 hourly intentions. The same weekday repeats the following week while the seasons stay the same. The page updates automatically when the local hour or day changes.
- Each four-hour window has one slot that follows the natural season in General and the Church season in Catholic during Advent, Christmas, Lent, Holy Week, and Easter. The other three slots share their prayers across both calendars. Some have natural-season variants for school, family care, and work on the land. For example, a summer morning can remember teachers resting or children missing their friends. Both calendars use the same natural-season variants, including when Christmas falls in summer.
- Catholic Sundays have one exception to the weekly timetable. At noon the prayer follows the Sunday Gospel, including in Advent and Lent. The A/B/C cycle changes on the first Sunday of Advent. The app uses the daytime Mass on the General Roman Calendar, keeping Epiphany on January 6 and Ascension and Corpus Christi on Thursday. Palm Sunday uses the Passion. Where alternatives are permitted, the displayed reference identifies the chosen reading.
- Reading references follow the [Liturgy Office Sunday lectionary tables](https://www.liturgyoffice.org.uk/Calendar/Sunday/index.shtml). The [USCCB lectionary guide](https://www.usccb.org/faq/questions-about-lectionary) explains the three-year cycle.
- Catholic is the default. Choosing a calendar saves a first-party preference cookie for one year. If cookies are blocked, the choice still works on the open page.
- Calendar seasons use meteorological months for the selected hemisphere. The default `Auto` setting makes a best-effort guess from the browser's time-zone region; visitors can choose Northern or Southern manually. That choice is saved in the current browser. Northern seasons are spring March to May, summer June to August, autumn September to November, and winter December to February. Southern seasons are reversed.
- Liturgical season uses Gregorian Easter computus. Holy Week takes precedence over Lent from Palm Sunday through Holy Saturday. Easter includes Pentecost Sunday.
- Christmas is treated as December 25 through the Baptism of the Lord, calculated as the Sunday after January 6. Advent begins on the Sunday on or before December 3 and runs through December 24. Ordinary Time is the default.
- Local calendars can transfer Epiphany or other observances. The first version does not account for local feast transfers or the evening start of liturgical days.
- The `psalter_anchor` is a devotional guide to the rhythm of the day, not a claim that every civil hour is an appointed canonical hour.
- Time-zone region is only a rough clue to hemisphere, so use the selector if the automatic choice is wrong. Sunrise and sunset are calculated only after a visitor selects **Show my sunrise & sunset** and grants location access. Coordinates stay in page memory and are not saved or sent anywhere; the displayed times are estimates.

## Publish with GitHub Pages

In the repository, open **Settings → Pages**. Choose **Deploy from a branch**, select `main` and the root folder, then save. GitHub Pages can serve these files directly; GitHub Actions is not needed.

For a local preview, serve the repository folder over HTTP (for example, `python -m http.server 8000`) and open `http://localhost:8000`. The browser cannot load the CSV through a `file://` URL.
