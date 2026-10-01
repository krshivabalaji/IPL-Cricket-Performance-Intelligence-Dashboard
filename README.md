# IPL-Cricket-Performance-Intelligence-Dashboard
Interactive IPL Cricket Performance Intelligence Dashboard built using Power BI, Excel and DAX.

An interactive Dashboard developed to analyse IPL matches, team performance, player achievements and season-wise championship insights. The project demonstrates how multiple source files can be transformed into a structured analytical model and presented through an interactive three-page Power BI dashboard.

---

## Project Objective

To build an interactive analytical dashboard that transforms multiple IPL datasets into meaningful insights on:

- Match performance
- Team performance
- Player achievements
- Season-wise awards
- IPL championship history

The project also demonstrates data preparation, data modelling, DAX-based calculations, interactive filtering, navigation and dynamic image integration.

---

## Project Overview

| Area | Details |
|---|---|
| Seasons | 2008–2026 |
| Source Files | Multiple Excel datasets |
| Dashboard Pages | 3 |
| Primary Tool | Power BI |
| Calculation | DAX |
| Data Preparation | Excel / Power Query |

---

# Dashboard Pages

## 1) Match Intelligence

The first page provides an overview of IPL match-level information.

### Key features

- Total Matches KPI
- Season analysis
- Venue and City analysis
- Match result analysis
- Top venue insights
- Toss decision analysis
- Interactive slicers
- Match type filtering
- City filtering
- Page navigation

<img width="842" height="484" alt="Screenshot 2026-09-29 115506" src="https://github.com/user-attachments/assets/60d53a64-1405-4151-aaa5-237e007892cd" />

---

## 2) Team Performance

The second page focuses on team-level performance using prepared team summary data.

### Key features

- Home Wins
- Away Wins
- Home Matches
- Away Matches
- Home Win Percentage
- Away Win Percentage
- Home City
- State
- Trophy Winner information
- Team-level filtering
- Map-based analysis

<img width="852" height="488" alt="Team Analysis" src="https://github.com/user-attachments/assets/e876c351-7ef0-45a3-98c4-f8bc4221990f" />

---

## 3) Player & Season Intelligence

The third page provides season-driven player and championship insights.

### Key features

### Orange Cap

Displays the Orange Cap winner based on the selected season, including:

- Player
- Team
- Runs
- Strike Rate
- Average
- Highest Score
- 50s / 100s
- 4s / 6s

### Purple Cap

Displays the Purple Cap winner based on the selected season, including:

- Player
- Team
- Matches
- Wickets

### Season Awards

- Player of the Tournament
- Final Man of the Match

### IPL Championship

- Champion
- Runner-up
- Winning Captain
- Final Venue

<img width="857" height="491" alt="Player Stats" src="https://github.com/user-attachments/assets/fde256f7-850b-4cdc-be32-efea328636cc" />

---

# Data Sources

The project uses multiple IPL-related source files.

### Match Data

Contains match-level information such as:

- Season
- City
- Date
- Match Type
- Teams
- Toss
- Winner
- Result
- Venue
- Result Margin

### Team Performance Data

Contains:

- Team
- Home Wins
- Away Wins
- Home Matches
- Away Matches
- Home Win %
- Away Win %
- Home City
- State
- Short Name
- Trophy Winner

### IPL Winners & Runners

Contains:

- Season
- Winner
- Runner-up
- Winning Captain
- Final Man of the Match
- Player of the Tournament
- Venue

### Orange Cap History

Contains season-wise Orange Cap statistics including:

- Player
- Team
- Innings
- Runs
- Highest Score
- Average
- Strike Rate
- 50s
- 100s
- 4s
- 6s

### Purple Cap History

Contains:

- Season
- Player
- Team
- Matches
- Wickets

---

# Data Preparation & Modelling

Multiple source files were imported into Power BI and prepared for analysis.

### Key steps

1. Imported multiple Excel source files.
2. Standardised team names.
3. Selected relevant columns.
4. Created supporting/reference tables.
5. Created a `DimSeason` table for season-based analysis.
6. Established relationships between relevant tables.
7. Created DAX measures for dynamic KPIs.
8. Connected slicers with report visuals.
9. Implemented page navigation and bookmarks.
10. Integrated image URLs for player/team visuals.

---

# Data Model

A dedicated `DimSeason` table was used to provide a consistent season selection for the player and championship analysis.

The model separates different levels of information rather than forcing unrelated source tables into a single dataset.

### Example

```text
                 DimSeason
                     │
        ┌────────────┼────────────┐
        │            │            │
     Winners     Orange Cap   Purple Cap
    & Runners
```
---

# DAX & Analytical Logic

DAX was used to create dynamic measures and retrieve season-specific values based on user selections.

### Selected Season

```DAX
Selected Season =
SELECTEDVALUE(DimSeason[Season])
```
Used to identify the season selected through the slicer.

### Orange Cap Player

```
Orange Cap Player =
SELECTEDVALUE('IPL ORANGE CAP WINNERS HISTORY'[Winners])
```
Returns the Orange Cap winner for the selected season.

### Purple Cap Player
```
Purple Cap Player =
SELECTEDVALUE(
    'IPL PURPLE CAP WINNERS HISTORY'[Player])
```
Returns the Purple Cap winner for the selected season.

### Champion
```
Champion =
SELECTEDVALUE(
    'IPL Winners & Runners List'[Winner])
```
Returns the IPL Champion for the selected season.

### Runner-up
```
Runner Up =
SELECTEDVALUE(
    'IPL Winners & Runners List'[Runner Up])
```
Returns the Runner-up for the selected season.

### Winning Captain
```
Winning Captain =
SELECTEDVALUE(
    'IPL Winners & Runners List'[Winning Captain])
```
Returns the Winning Captain for the selected season.

### Championship Title
```
Championship Title =
"IPL CHAMPIONSHIP — " &
SELECTEDVALUE(
    DimSeason[Season],
    "Select Season")
```
Creates a dynamic championship heading based on the selected season.

---
# Dynamic Image Integration

Player and team images were integrated using Image URLs rather than storing image files directly inside the Power BI report.

### Implementation Flow
```
Excel Source
     │
     ▼
Image_URL Column
     │
     ▼
Power BI Data Refresh
     │
     ▼
Data Category → Image URL
     │
     ▼
Image / Card Visual
     │
     ▼
Dynamic Player / Team Image
```
### Example
Season | Player | Image_URL
-------|--------|-----------------------------
2008   | Player | https://example.com/image.jpg
2009   | Player | https://example.com/image.jpg

The image URL is associated with the corresponding player or team and can be displayed dynamically when the selected season changes.

### Applications
- Orange Cap player image
- Purple Cap player image
- Player of the Tournament image
- Final Man of the Match image
- Champion team logo
- Runner-up team logo

This approach keeps the report lightweight while allowing visuals to respond dynamically to the selected season.

---
# UI & Dashboard Integration

A consistent visual design system was implemented across all three dashboard pages.

### Navigation

A reusable left-side navigation panel was created and replicated across:

- Page 1 → Match Intelligence
- Page 2 → Team Performance
- Page 3 → Player & Season Intelligence

The navigation provides a consistent user experience while allowing users to move between report pages.

### Slicers & Filters

Interactive slicers were implemented to allow users to filter the dashboard based on relevant dimensions such as:

- Season
- City
- Match Type
- Team
- State

The slicers are connected to the appropriate visuals to provide dynamic filtering.

### Bookmarks

Bookmarks were used for report interactions such as:

- Reset Filters
- Navigation states
- Selected visual states

### UI Principles
- Consistent alignment
- Reusable side panel
- Consistent spacing
- KPI hierarchy
- Clear section headings
- Interactive navigation
- Consistent colour usage
- Minimal visual clutter
---
# Dashboard Interaction Flow

The overall user interaction follows:
```
User selects Season
        │
        ▼
Season Slicer
        │
        ▼
DimSeason
        │
        ▼
Related Tables
        │
        ▼
DAX Measures
        │
        ▼
Dynamic KPIs / Visuals
        │
        ▼
Player / Team / Championship Insights
```
This allows the dashboard to function as an interactive analytical report rather than a collection of static charts.

---
# Data Refresh & Portability

The dashboard was designed to work with external Excel source files.

### Refresh Flow
```
Update Excel Data
       │
       ▼
Save Source File
       │
       ▼
Power BI Refresh
       │
       ▼
Power Query Updates
       │
       ▼
DAX Recalculates
       │
       ▼
Dashboard Updates
```
The separation between source data and the Power BI report allows the underlying datasets to be updated without rebuilding the dashboard from scratch.

---

# Key Technical Features and Learnings

The project demonstrates practical implementation of:

- Multiple Excel source files
- Power Query data preparation
- Data modelling
- Table relationships
- Reference / dimension tables
- DAX measures
- SELECTEDVALUE()
- Dynamic KPIs
- Interactive slicers
- Bookmark-based interactions
- Page navigation
- Map visualisation
- Image URL integration
- Dynamic player profiles
- Team and championship analysis
- Consistent dashboard UI
---

#  Future Enhancements

Potential future improvements include:

- Ball-by-ball player performance analysis
- Advanced player comparison
- Additional team performance metrics
- More detailed geographic analysis
- Automated data refresh
- Additional IPL seasons
- More player and team image integration
- Advanced interactive tooltips
- Drill-through pages for detailed player/team analysis
---

## Author

# Shivabalaji K R

Technical Business Analyst and Solution Engineer
Power BI • DAX • SQL • Data Analysis
