# DAX Measures

## Selected Season Used to identify the season selected by the user.

```DAX
Selected Season =
SELECTEDVALUE(DimSeason[Season])

## Returns the Orange Cap winner for the selected season.

Orange Cap Player =
SELECTEDVALUE('IPL ORANGE CAP WINNERS HISTORY'[Winners])

## Returns the Purple Cap winner for the selected season.

Purple Cap Player =
SELECTEDVALUE('IPL PURPLE CAP WINNERS HISTORY'[Player])

## Returns the IPL champion for the selected season.

Champion =
SELECTEDVALUE('IPL Winners & Runners List'[Winner])

## Returns the runner-up for the selected season.

Runner Up =
SELECTEDVALUE('IPL Winners & Runners List'[Runner Up])
