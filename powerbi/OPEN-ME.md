# Opening the Power BI report

`NYCNoise.pbip` is a Power BI Project: the report (`NYCNoise.Report`, PBIR format) and the semantic model (`NYCNoise.SemanticModel`, TMDL) saved as text, so the repo can show every change. Power BI Desktop opens it like a `.pbix`.

## What you need

- Power BI Desktop for Windows, a recent version (2026). If Desktop is older than about mid 2025, turn on **File, Options and settings, Options, Preview features, Power BI Project (.pbip) save option** and **Store reports using enhanced metadata format (PBIR)**, then restart Desktop.
- The repo folder on the Windows machine. In Parallels the Mac home folder is usually shared as `\\Mac\Home`.

## Open it

1. In Windows, go to the repo's `powerbi` folder and double-click `NYCNoise.pbip`.
2. The visuals are empty the first time. Select **Refresh** on the Home ribbon.
   - By default the data is read from the repo's public copy on GitHub (`DataFolder` is `https://raw.githubusercontent.com/cjmuldoon/plotlay-nyc-noise/main/data/`). If Desktop asks how to connect, choose **Anonymous** and then **Connect**.
   - To read the files from disk instead, go to **Home, Transform data, Edit parameters** and set `DataFolder` to the full path of the repo's `data` folder, **ending with a backslash**. Then select **OK** and **Apply changes**.
   - If Desktop warns about privacy levels, choose **Ignore privacy levels** (all the sources are public open data).
3. Check the numbers (below).

If the report was updated while open, close Power BI and reopen the .pbip rather than using Apply external changes.

## Check the numbers after Refresh

After **Refresh**:

| Page | Card | Should read |
|---|---|---|
| The average week | Reports in an average week | 11,737 |
| Hexagons by hour (Saturday 23:00, as it opens) | Across the city, hour picked | 325.37 |

Pick **Tue 05:00** on the second page and the card reads 18.90. The matrix's darkest cells are Saturday 22:00 and 23:00 and Sunday 00:00; the README's busiest hour is Saturday 11 pm (325). The table on **Districts** starts with the district with most reports a week.

## The model

- **AverageWeek**: one row per hour of the week (`data/tables/average_week.csv`): the city's reports in that hour of an average week, in all and by complaint type. `weekday` sorts by `day_order`. Measures: `Reports a week`, `Heat colour` (the matrix cell colour, the same classes as the heat map on the page).
- **Hexagons**: one row per 1 km hexagon and hour of the week (`hexagons_by_hour.csv`), keyed by `key` as in the map file. `hour_of_week` sorts by `period_order`. Measures: `Reports in the hour picked` (the hour picked, or Saturday 23:00 when none is: one hour at a time).
- **Districts** (`community_districts.csv`) and **Types** (`types.csv`).

## The map

- **Shape Map** (page 2). The custom map, `data/geometry/hexagons.topojson`, is saved inside the report, with the counties round the city (US Census TIGERweb, public domain) in a pale ground tone. If the map shows the United States instead (an older Desktop can ignore a saved map): select it, then **Format visual**, **Visual**, **Map settings**, **Map type: Custom map**, **Add map type**, and choose `..\data\geometry\hexagons.topojson`. If the Shape Map is not in the Visualizations pane, turn it on in **File, Options and settings, Options, Preview features, Shape map visual** and restart Desktop.
- If it comes up empty, drag the fields back: Location `Hexagons[key]`, Color saturation `[Reports in the hour picked]`.

Then save with **File, Save**, and if you like **File, Save as** a `.pbix`, which includes the data.
