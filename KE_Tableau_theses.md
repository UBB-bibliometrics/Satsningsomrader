# Energiomstilling

String to use against an export from BORA to identify master and PhD theses related to energy transitions (energiomstilling). Exported from BORA via API. 

Search string and terms discussed with director for KE (KGF) january 2024. 

The string covers the following groups:
- Ammonia
- Bioenergy/biofuels/biogas
- CCS
- Energy systems/transition/mix
- Energy security/policy/justice
- Energy efficiency
- Geothermal
- Hydrogen
- Hydropower
- Nuclear
- Ocean/wave energy
- Power grid/batteries
- Renewable energy
- Solar
- Transport (decarbonised, green, electric)
- Wind power (all)
- Offshore wind (subset of "wind power (all)")
- Zero emissions

## Search string
Some terms are combined with other terms (e.g. energy, renewable) to avoid noise. Some are not but seem to work ok on this limited dataset - they would likely be problematic in other, larger datasets (e.g. "ammonia"). 

### Ammonia
```py
IF
  (CONTAINS(LOWER([Abstract]), "ammonia")
  OR CONTAINS(LOWER([Subject]), "ammonia")
  OR CONTAINS(LOWER([Name]), "ammonia"))
  AND NOT
  (CONTAINS(LOWER([Abstract]), "aquaculture")
  OR CONTAINS(LOWER([Subject]), "aquaculture")
  OR CONTAINS(LOWER([Name]), "aquaculture")
  OR CONTAINS(LOWER([Abstract]), "akvakult")
  OR CONTAINS(LOWER([Subject]), "akvakult")
  OR CONTAINS(LOWER([Name]), "akvakult")
  OR REGEXP_MATCH(LOWER([Abstract]), "\bfish")
  OR REGEXP_MATCH(LOWER([Subject]), "\bfish")
  OR REGEXP_MATCH(LOWER([Name]), "\bfish"))
THEN "Ammonia"
END
```
### Bioenergy/fuel/gas
```py
IF CONTAINS(LOWER([Abstract]), "bioenergy")
OR CONTAINS(LOWER([Subject]), "bioenergy")
OR CONTAINS(LOWER([Name]), "bioenergy")
OR CONTAINS(LOWER([Abstract]), "bioenergi")
OR CONTAINS(LOWER([Subject]), "bioenergi")
OR CONTAINS(LOWER([Name]), "bioenergi")
OR CONTAINS(LOWER([Abstract]), "bio-oil")
OR CONTAINS(LOWER([Subject]), "bio-oil")
OR CONTAINS(LOWER([Name]), "bio-oil")
OR CONTAINS(LOWER([Abstract]), "bioolje")
OR CONTAINS(LOWER([Subject]), "bioolje")
OR CONTAINS(LOWER([Name]), "bioolje")
OR CONTAINS(LOWER([Abstract]), "bio-fuel")
OR CONTAINS(LOWER([Subject]), "bio-fuel")
OR CONTAINS(LOWER([Name]), "bio-fuel")
OR CONTAINS(LOWER([Abstract]), "biofuel")
OR CONTAINS(LOWER([Subject]), "biofuel")
OR CONTAINS(LOWER([Name]), "biofuel")
OR CONTAINS(LOWER([Abstract]), "bio fuel")
OR CONTAINS(LOWER([Subject]), "bio fuel")
OR CONTAINS(LOWER([Name]), "bio fuel")
OR CONTAINS(LOWER([Abstract]), "biodrivstoff")
OR CONTAINS(LOWER([Subject]), "biodrivstoff")
OR CONTAINS(LOWER([Name]), "biodrivstoff")
OR CONTAINS(LOWER([Abstract]), "biogas")
OR CONTAINS(LOWER([Subject]), "biogas")
OR CONTAINS(LOWER([Name]), "biogas")
THEN "Bioenergy/fuel/gas"
END
```
### CCS
```py
IF
  ((REGEXP_MATCH(([Subject]), "\bCCS\b")
  OR REGEXP_MATCH(([Name]), "\bCCS\b"))
  AND NOT CONTAINS(lower([Name]), "closed containment system")
  )
OR CONTAINS(([Abstract]), "CCUS")
OR CONTAINS(([Subject]), "CCUS")
OR CONTAINS(([Name]), "CCUS")
OR CONTAINS(LOWER([Abstract]), "carbon capture and storage")
OR CONTAINS(LOWER([Subject]), "carbon capture and storage")
OR CONTAINS(LOWER([Name]), "carbon capture and storage")
OR CONTAINS(LOWER([Abstract]), "karbonfangst")
OR CONTAINS(LOWER([Subject]), "karbonfangst")
OR CONTAINS(LOWER([Name]), "karbonfangst")
OR CONTAINS(LOWER([Abstract]), "co2 capture")
OR CONTAINS(LOWER([Subject]), "co2 capture")
OR CONTAINS(LOWER([Name]), "co2 capture")
OR CONTAINS(LOWER([Abstract]), "co2-fangst")
OR CONTAINS(LOWER([Subject]), "co2-fangst")
OR CONTAINS(LOWER([Name]), "co2-fangst")
OR CONTAINS(LOWER([Abstract]), "co2 storage")
OR CONTAINS(LOWER([Subject]), "co2 storage")
OR CONTAINS(LOWER([Name]), "co2 storage")
OR CONTAINS(LOWER([Abstract]), "co2-lagring")
OR CONTAINS(LOWER([Subject]), "co2-lagring")
OR CONTAINS(LOWER([Name]), "co2-lagring")
THEN "Carbon capture and storage"
END
```
### Energy system/transformation/mix
```py
IF CONTAINS(LOWER([Abstract]), "energy system")
OR CONTAINS(LOWER([Subject]), "energy system")
OR CONTAINS(LOWER([Name]), "energy system")
OR CONTAINS(LOWER([Abstract]), "energisystem")
OR CONTAINS(LOWER([Subject]), "energisystem")
OR CONTAINS(LOWER([Name]), "energisystem")
OR CONTAINS(LOWER([Abstract]), "kraftsystem")
OR CONTAINS(LOWER([Subject]), "kraftsystem")
OR CONTAINS(LOWER([Name]), "kraftsystem")

OR CONTAINS(LOWER([Abstract]), "local energy")
OR CONTAINS(LOWER([Subject]), "local energy")
OR CONTAINS(LOWER([Name]), "local energy")
OR CONTAINS(LOWER([Abstract]), "community energy")
OR CONTAINS(LOWER([Subject]), "community energy")
OR CONTAINS(LOWER([Name]), "community energy")
OR CONTAINS(LOWER([Abstract]), "lokal energi")
OR CONTAINS(LOWER([Subject]), "lokal energi")
OR CONTAINS(LOWER([Name]), "lokal energi")
OR CONTAINS(LOWER([Abstract]), "energy coop")
OR CONTAINS(LOWER([Subject]), "energy coop")
OR CONTAINS(LOWER([Name]), "energy coop")
OR CONTAINS(LOWER([Abstract]), "off-grid")
OR CONTAINS(LOWER([Subject]), "off-grid")
OR CONTAINS(LOWER([Name]), "off-grid")

OR CONTAINS(LOWER([Abstract]), "energiomstilling")
OR CONTAINS(LOWER([Subject]), "energiomstilling")
OR CONTAINS(LOWER([Name]), "energiomstilling")
OR CONTAINS(LOWER([Abstract]), "energy transition")
OR CONTAINS(LOWER([Subject]), "energy transition")
OR CONTAINS(LOWER([Name]), "energy transition")
OR CONTAINS(LOWER([Abstract]), "energy transformation")
OR CONTAINS(LOWER([Subject]), "energy transformation")
OR CONTAINS(LOWER([Name]), "energy transformation")

OR CONTAINS(LOWER([Abstract]), "energy mix")
OR CONTAINS(LOWER([Subject]), "energy mix")
OR CONTAINS(LOWER([Name]), "energy mix")
OR CONTAINS(LOWER([Abstract]), "energimiks")
OR CONTAINS(LOWER([Subject]), "energimiks")
OR CONTAINS(LOWER([Name]), "energimiks")
OR
  ((
  CONTAINS(LOWER([Name]), "klimapolitikk")
  OR CONTAINS(LOWER([Subject]), "klimapolitikk")
  OR CONTAINS(LOWER([Abstract]), "klimapolitikk")
  OR CONTAINS(LOWER([Name]), "climate poli")
  OR CONTAINS(LOWER([Subject]), "climate poli")
  OR CONTAINS(LOWER([Abstract]), "climate poli")
  OR CONTAINS(LOWER([Name]), "grønt skifte")
  OR CONTAINS(LOWER([Subject]), "grønt skifte")
  OR CONTAINS(LOWER([Abstract]), "grønt skifte")
  OR CONTAINS(LOWER([Name]), "grønne skifte")
  OR CONTAINS(LOWER([Subject]), "grønne skifte")
  OR CONTAINS(LOWER([Abstract]), "grønne skifte")
  OR CONTAINS(LOWER([Name]), "green trans")
  OR CONTAINS(LOWER([Subject]), "green trans")
  OR CONTAINS(LOWER([Abstract]), "green trans")
  )
  AND 
  (CONTAINS(LOWER([Name]), "energy")
  OR CONTAINS(LOWER([Subject]), "energy")
  OR CONTAINS(LOWER([Abstract]), "energy")
  OR CONTAINS(LOWER([Name]), "energi")
  OR CONTAINS(LOWER([Subject]), "energi")
  OR CONTAINS(LOWER([Abstract]), "energi")
  OR CONTAINS(LOWER([Name]), "fornybar")
  OR CONTAINS(LOWER([Subject]), "fornybar")
  OR CONTAINS(LOWER([Abstract]), "fornybar")
  OR CONTAINS(LOWER([Name]), "renewable")
  OR CONTAINS(LOWER([Subject]), "renewable")
  OR CONTAINS(LOWER([Abstract]), "renewable")
  ))
THEN "Energy system/transition/mix"
END
```
### Energy security/policy/justice
```py
IF CONTAINS(LOWER([Abstract]), "energy democracy")
OR CONTAINS(LOWER([Subject]), "energy democracy")
OR CONTAINS(LOWER([Name]), "energy democracy")
OR CONTAINS(LOWER([Abstract]), "energy justice")
OR CONTAINS(LOWER([Subject]), "energy justice")
OR CONTAINS(LOWER([Name]), "energy justice")
OR CONTAINS(LOWER([Abstract]), "energy law")
OR CONTAINS(LOWER([Subject]), "energy law")
OR CONTAINS(LOWER([Name]), "energy law")
OR CONTAINS(LOWER([Abstract]), "energy polic")
OR CONTAINS(LOWER([Subject]), "energy polic")
OR CONTAINS(LOWER([Name]), "energy polic")
OR CONTAINS(LOWER([Abstract]), "energipoli")
OR CONTAINS(LOWER([Subject]), "energipoli")
OR CONTAINS(LOWER([Name]), "energipoli")
OR CONTAINS(LOWER([Abstract]), "energy inequit")
OR CONTAINS(LOWER([Subject]), "energy inequit")
OR CONTAINS(LOWER([Name]), "energy inequit")
OR CONTAINS(LOWER([Abstract]), "energy law")
OR CONTAINS(LOWER([Subject]), "energy law")
OR CONTAINS(LOWER([Name]), "energy law")
OR CONTAINS(LOWER([Abstract]), "energy poverty")
OR CONTAINS(LOWER([Subject]), "energy poverty")
OR CONTAINS(LOWER([Name]), "energy poverty")
OR CONTAINS(LOWER([Abstract]), "fuel poverty")
OR CONTAINS(LOWER([Subject]), "fuel poverty")
OR CONTAINS(LOWER([Name]), "fuel poverty")
OR CONTAINS(LOWER([Abstract]), "energy vulnerab")
OR CONTAINS(LOWER([Subject]), "energy vulnerab")
OR CONTAINS(LOWER([Name]), "energy vulnerab")
OR CONTAINS(LOWER([Abstract]), "energy security")
OR CONTAINS(LOWER([Subject]), "energy security")
OR CONTAINS(LOWER([Name]), "energy security")
OR CONTAINS(LOWER([Abstract]), "energy insecurity")
OR CONTAINS(LOWER([Subject]), "energy insecurity")
OR CONTAINS(LOWER([Name]), "energy insecurity")
OR
  ((CONTAINS(LOWER([Subject]), "energ")
  OR CONTAINS(LOWER([Name]), "energ"))
  AND
  (CONTAINS(LOWER([Subject]), "rettigheter")
  OR CONTAINS(LOWER([Name]), "rettigheter")
  OR CONTAINS(LOWER([Subject]), "rettferdig")
  OR CONTAINS(LOWER([Name]), "rettferdig")
  OR CONTAINS(LOWER([Subject]), "rights")
  OR CONTAINS(LOWER([Name]), "rights")
  OR CONTAINS(LOWER([Subject]), "poverty")
  OR CONTAINS(LOWER([Name]), "poverty")
  OR CONTAINS(LOWER([Subject]), "fattigdom")
  OR CONTAINS(LOWER([Name]), "fattigdom")
  OR CONTAINS(LOWER([Subject]), "arealbruk")
  OR CONTAINS(LOWER([Name]), "arealbruk")
  OR CONTAINS(LOWER([Abstract]), "arealbruk")
  OR CONTAINS(LOWER([Subject]), "land use")
  OR CONTAINS(LOWER([Name]), "land use")
  OR CONTAINS(LOWER([Abstract]), "land use")
  OR CONTAINS(LOWER([Subject]), "urfolk")
  OR CONTAINS(LOWER([Name]), "urfolk")
  OR CONTAINS(LOWER([Abstract]), "urfolk")
  ))
THEN "Energy security/policy/justice"
END
```
### Energy efficiency
```py
IF CONTAINS(LOWER([Abstract]), "energy efficien")
OR CONTAINS(LOWER([Subject]), "energy efficien")
OR CONTAINS(LOWER([Name]), "energy efficien")
OR CONTAINS(LOWER([Abstract]), "energieffektiv")
OR CONTAINS(LOWER([Subject]), "energieffektiv")
OR CONTAINS(LOWER([Name]), "energieffektiv")
OR CONTAINS(LOWER([Abstract]), "energy saving")
OR CONTAINS(LOWER([Subject]), "energy saving")
OR CONTAINS(LOWER([Name]), "energy saving")
OR CONTAINS(LOWER([Abstract]), "energisparing")
OR CONTAINS(LOWER([Subject]), "energisparing")
OR CONTAINS(LOWER([Name]), "energisparing")
OR CONTAINS(LOWER([Abstract]), "energy consumption")
OR CONTAINS(LOWER([Subject]), "energy consumption")
OR CONTAINS(LOWER([Name]), "energy consumption")
OR CONTAINS(LOWER([Abstract]), "energiforbruk")
OR CONTAINS(LOWER([Subject]), "energiforbruk")
OR CONTAINS(LOWER([Name]), "energiforbruk")
OR CONTAINS(LOWER([Abstract]), "energy suffici")
OR CONTAINS(LOWER([Subject]), "energy suffici")
OR CONTAINS(LOWER([Name]), "energy suffici")
THEN "Energy efficiency"
END
```
### Geothermal energy
```py
IF CONTAINS(LOWER([Name]), "geotermi")
OR CONTAINS(LOWER([Name]), "geothermal reservoir")
OR CONTAINS(LOWER([Abstract]), "geothermal energy")
OR CONTAINS(LOWER([Abstract]), "geotermisk energi")
OR
  ((CONTAINS(LOWER([Subject]), "geotherm")
  OR CONTAINS(LOWER([Name]), "geotherm"))
  AND 
  (CONTAINS(LOWER([Name]), "energ")
  OR CONTAINS(LOWER([Subject]), "energ"))
  )
THEN "Geothermal energy"
END
```
### Hydrogen
```py
IF CONTAINS(LOWER([Name]), "hydrogenprosjekt")
OR CONTAINS(LOWER([Subject]), "hydrogenprosjekt")
OR CONTAINS(LOWER([Abstract]), "hydrogenprosjekt")
OR CONTAINS(LOWER([Name]), "liquid hydrogen")
OR CONTAINS(LOWER([Subject]), "liquid hydrogen")
OR CONTAINS(LOWER([Abstract]), "liquid hydrogen")
OR
  ((CONTAINS(LOWER([Name]), "hydrogen")
  OR CONTAINS(LOWER([Subject]), "hydrogen")
  OR CONTAINS(LOWER([Abstract]), "hydrogen"))
  AND
  (CONTAINS(LOWER([Name]), "energ")
  OR CONTAINS(LOWER([Subject]), "energ")
  OR CONTAINS(LOWER([Abstract]), "energy system")
  OR CONTAINS(LOWER([Abstract]), "energy transition")
  OR CONTAINS(LOWER([Abstract]), "energisystem")
  OR CONTAINS(LOWER([Abstract]), "energiomstilling")
  OR CONTAINS(LOWER([Name]), "power")
  OR CONTAINS(LOWER([Subject]), "power")
  OR CONTAINS(LOWER([Abstract]), "power")
  OR CONTAINS(LOWER([Name]), "nuclear fusion")
  OR CONTAINS(LOWER([Subject]), "nuclear fusion")
  OR CONTAINS(LOWER([Abstract]), "nuclear fusion")
  OR CONTAINS(LOWER([Name]), "carbon")
  OR CONTAINS(LOWER([Subject]), "carbon")
  OR CONTAINS(LOWER([Abstract]), "carbon")
  OR CONTAINS(LOWER([Name]), "storage")
  OR CONTAINS(LOWER([Subject]), "storage")
  OR CONTAINS(LOWER([Name]), "lagring")
  OR CONTAINS(LOWER([Subject]), "lagring")
  OR CONTAINS(LOWER([Name]), "production")
  OR CONTAINS(LOWER([Subject]), "production")
  OR CONTAINS(LOWER([Abstract]), "production")
  OR CONTAINS(LOWER([Name]), "fuel")
  OR CONTAINS(LOWER([Subject]), "fuel")
  OR CONTAINS(LOWER([Abstract]), "fuel")
  OR CONTAINS(LOWER([Name]), "drivstoff")
  OR CONTAINS(LOWER([Subject]), "drivstoff")
  OR CONTAINS(LOWER([Abstract]), "drivstoff")
  OR REGEXP_MATCH(LOWER([Name]), "\bship")
  OR REGEXP_MATCH(LOWER([Subject]), "\bship")
  OR REGEXP_MATCH(LOWER([Abstract]), "\bship")
  OR CONTAINS(LOWER([Name]), "maritim")
  OR CONTAINS(LOWER([Subject]), "maritim")
  OR CONTAINS(LOWER([Abstract]), "maritim")
  OR CONTAINS(LOWER([Name]), "renewable")
  OR CONTAINS(LOWER([Subject]), "renewable")
  OR CONTAINS(LOWER([Abstract]), "renewable")
  OR CONTAINS(LOWER([Name]), "fornybar")
  OR CONTAINS(LOWER([Subject]), "fornybar")
  OR CONTAINS(LOWER([Abstract]), "fornybar")
  OR CONTAINS(LOWER([Name]), "seismic")
  OR CONTAINS(LOWER([Subject]), "seismic")
  OR CONTAINS(LOWER([Abstract]), "seismic")
  OR CONTAINS(LOWER([Name]), "geolog")
  OR CONTAINS(LOWER([Subject]), "geolog")
  OR CONTAINS(LOWER([Abstract]), "geolog")
  OR CONTAINS(LOWER([Name]), "combust")
  OR CONTAINS(LOWER([Subject]), "combust")
  OR CONTAINS(LOWER([Abstract]), "combust")
  OR CONTAINS(LOWER([Name]), "burning")
  OR CONTAINS(LOWER([Subject]), "burning")
  OR CONTAINS(LOWER([Abstract]), "burning")
  OR CONTAINS(LOWER([Name]), "igniti")
  OR CONTAINS(LOWER([Subject]), "igniti")
  OR CONTAINS(LOWER([Abstract]), "igniti")
  OR CONTAINS(LOWER([Name]), "forbrenn")
  OR CONTAINS(LOWER([Subject]), "forbrenn")
  OR CONTAINS(LOWER([Abstract]), "forbrenn")
  OR CONTAINS(LOWER([Name]), "safety stud")
  OR CONTAINS(LOWER([Subject]), "safety stud")
  OR CONTAINS(LOWER([Abstract]), "safety stud")
  OR CONTAINS(LOWER([Name]), "fuel cell")
  OR CONTAINS(LOWER([Subject]), "fuel cell")
  OR CONTAINS(LOWER([Abstract]), "fuel cell"))
  AND NOT 
  (CONTAINS(LOWER([Abstract]), "hydrate")
  OR CONTAINS(LOWER([Name]), "hydrate")
  OR CONTAINS(LOWER([Abstract]), "hydrogen peroxide")
  OR CONTAINS(LOWER([Name]), "hydrogen peroxide")
  )
)
THEN "Hydrogen"
END
```
### Hydropower
```py
IF CONTAINS(LOWER([Abstract]), "vannkraft")
OR CONTAINS(LOWER([Subject]), "vannkraft")
OR CONTAINS(LOWER([Name]), "vannkraft")
OR CONTAINS(LOWER([Abstract]), "vasskraft")
OR CONTAINS(LOWER([Subject]), "vasskraft")
OR CONTAINS(LOWER([Name]), "vasskraft")
OR CONTAINS(LOWER([Abstract]), "hydropower")
OR CONTAINS(LOWER([Subject]), "hydropower")
OR CONTAINS(LOWER([Name]), "hydropower")
OR CONTAINS(LOWER([Abstract]), "hydro-power")
OR CONTAINS(LOWER([Subject]), "hydro-power")
OR CONTAINS(LOWER([Name]), "hydro-power")
OR CONTAINS(LOWER([Abstract]), "hydroelectric")
OR CONTAINS(LOWER([Subject]), "hydroelectric")
OR CONTAINS(LOWER([Name]), "hydroelectric")
THEN "Hydropower"
END
```
### Nuclear power
```py
IF CONTAINS(LOWER([Abstract]), "nuclear power")
OR CONTAINS(LOWER([Subject]), "nuclear power")
OR CONTAINS(LOWER([Name]), "nuclear power")
OR CONTAINS(LOWER([Abstract]), "nuclear reactor")
OR CONTAINS(LOWER([Subject]), "nuclear reactor")
OR CONTAINS(LOWER([Name]), "nuclear reactor")
OR CONTAINS(LOWER([Abstract]), "kjernekraft")
OR CONTAINS(LOWER([Subject]), "kjernekraft")
OR CONTAINS(LOWER([Name]), "kjernekraft")
OR CONTAINS(LOWER([Abstract]), "nuclear fusion")
OR CONTAINS(LOWER([Subject]), "nuclear fusion")
OR CONTAINS(LOWER([Name]), "nuclear fusion")
THEN "Nuclear"
END
```
### Ocean/wave energy
```py
IF CONTAINS(LOWER([Abstract]), "ocean energy")
OR CONTAINS(LOWER([Subject]), "ocean energy")
OR CONTAINS(LOWER([Name]), "ocean energy")
OR CONTAINS(LOWER([Abstract]), "havenergi")
OR CONTAINS(LOWER([Subject]), "havenergi")
OR CONTAINS(LOWER([Name]), "havenergi")
OR CONTAINS(LOWER([Abstract]), "bølgekraft")
OR CONTAINS(LOWER([Name]), "bølgekraft")
OR CONTAINS(LOWER([Subject]), "bølgekraft")
OR 
  ((CONTAINS(LOWER([Name]), "wave energy")
  OR CONTAINS(LOWER([Subject]), "wave energy")
  OR CONTAINS(LOWER([Abstract]), "wave energy"))
  AND (CONTAINS(LOWER([Name]), "power")
  OR CONTAINS(LOWER([Subject]), "power")
  OR CONTAINS(LOWER([Abstract]), "power")))
THEN "Ocean/wave energy"
END
```
### Power grid/energy storage
```py
IF CONTAINS(LOWER([Abstract]), "power grid")
OR CONTAINS(LOWER([Subject]), "power grid")
OR CONTAINS(LOWER([Name]), "power grid")
OR CONTAINS(LOWER([Abstract]), "kraftlinj")
OR CONTAINS(LOWER([Subject]), "kraftlinj")
OR CONTAINS(LOWER([Name]), "kraftlinj")
OR CONTAINS(LOWER([Abstract]), "strømkabler")
OR CONTAINS(LOWER([Subject]), "strømkabler")
OR CONTAINS(LOWER([Name]), "strømkabler")
OR CONTAINS(LOWER([Abstract]), "mikrogrid")
OR CONTAINS(LOWER([Subject]), "mikrogrid")
OR CONTAINS(LOWER([Name]), "mikrogrid")
OR CONTAINS(LOWER([Abstract]), "microgrid")
OR CONTAINS(LOWER([Subject]), "microgrid")
OR CONTAINS(LOWER([Name]), "microgrid")
OR CONTAINS(LOWER([Abstract]), "DC-grid")
OR CONTAINS(LOWER([Subject]), "DC-grid")
OR CONTAINS(LOWER([Name]), "DC-grid")
OR CONTAINS(LOWER([Abstract]), "energy storage device")
OR CONTAINS(LOWER([Subject]), "energy storage device")
OR CONTAINS(LOWER([Name]), "energy storage device")
OR CONTAINS(LOWER([Abstract]), "batterier")
OR CONTAINS(LOWER([Subject]), "batterier")
OR CONTAINS(LOWER([Name]), "batterier")
OR CONTAINS(LOWER([Abstract]), "batteries")
OR CONTAINS(LOWER([Subject]), "batteries")
OR CONTAINS(LOWER([Name]), "batteries")
OR CONTAINS(LOWER([Abstract]), "fuel cell")
OR CONTAINS(LOWER([Subject]), "fuel cell")
OR CONTAINS(LOWER([Name]), "fuel cell")
THEN "Power grid/batteries"
END
```
### Renewable energy
```py
IF
  ((CONTAINS(LOWER([Subject]), "renewable")
  OR CONTAINS(LOWER([Name]), "renewable")
  OR CONTAINS(LOWER([Subject]), "fornybar")
  OR CONTAINS(LOWER([Name]), "fornybar"))
  AND 
  (CONTAINS(LOWER([Name]), "energ")
  OR CONTAINS(LOWER([Subject]), "energ")
  OR CONTAINS(LOWER([Name]), "kraft")
  OR CONTAINS(LOWER([Subject]), "kraft"))
  )
OR CONTAINS(LOWER([Abstract]), "renewable energ")
OR CONTAINS(LOWER([Abstract]), "fornybar energi")
OR CONTAINS(LOWER([Abstract]), "fornybar kraft")
OR CONTAINS(LOWER([Subject]), "green energy")
OR CONTAINS(LOWER([Name]), "green energy")
OR CONTAINS(LOWER([Abstract]), "green energy")
OR CONTAINS(LOWER([Subject]), "grønn energi")
OR CONTAINS(LOWER([Name]), "grønn energi")
OR CONTAINS(LOWER([Abstract]), "grønn energi")
THEN "Renewable energy"
END
```
### Solar power
```py
IF
  ((CONTAINS(LOWER([Subject]), "solar")
  OR CONTAINS(LOWER([Name]), "solar"))
  AND 
  (CONTAINS(LOWER([Name]), "energ")
  OR CONTAINS(LOWER([Subject]), "energ")
  OR CONTAINS(LOWER([Name]), "panel")
  OR CONTAINS(LOWER([Subject]), "panel")
  OR CONTAINS(LOWER([Name]), "pv")
  OR CONTAINS(LOWER([Subject]), "pv")
  OR CONTAINS(LOWER([Name]), "photovolta")
  OR CONTAINS(LOWER([Subject]), "photovolta")
  OR CONTAINS(LOWER([Name]), "collector")
  OR CONTAINS(LOWER([Subject]), "collector"))
  )
OR CONTAINS(LOWER([Abstract]), "solcell")
OR CONTAINS(LOWER([Abstract]), "solar panel")
OR CONTAINS(LOWER([Abstract]), "solar pv")
OR CONTAINS(LOWER([Abstract]), "solar collector")
OR CONTAINS(LOWER([Abstract]), "solfanger")
OR CONTAINS(LOWER([Name]), "solfanger")
OR CONTAINS(LOWER([Subject]), "solfanger")
OR CONTAINS(LOWER([Abstract]), "solar cell")
OR CONTAINS(LOWER([Name]), "solar cell")
OR CONTAINS(LOWER([Subject]), "solar cell")
THEN "Solar"
END
```
### Transport
```py
IF CONTAINS(LOWER([Abstract]), "electric car")
OR CONTAINS(LOWER([Subject]), "electric car")
OR CONTAINS(LOWER([Name]), "electric car")
OR REGEXP_MATCH(LOWER([Abstract]), "\belbil")
OR REGEXP_MATCH(LOWER([Subject]), "\belbil")
OR REGEXP_MATCH(LOWER([Name]), "\belbil")
OR REGEXP_MATCH(LOWER([Abstract]), "\bel-bil")
OR REGEXP_MATCH(LOWER([Subject]), "\bel-bil")
OR REGEXP_MATCH(LOWER([Name]), "\bel-bil")
OR CONTAINS(LOWER([Abstract]), "electric vehicle")
OR CONTAINS(LOWER([Subject]), "electric vehicle")
OR CONTAINS(LOWER([Name]), "electric vehicle")
OR CONTAINS(LOWER([Abstract]), "electric bus")
OR CONTAINS(LOWER([Subject]), "electric bus")
OR CONTAINS(LOWER([Name]), "electric bus")
OR CONTAINS(LOWER([Abstract]), "green shipping")
OR CONTAINS(LOWER([Subject]), "green shipping")
OR CONTAINS(LOWER([Name]), "green shipping")
OR CONTAINS(LOWER([Abstract]), "green aviation")
OR CONTAINS(LOWER([Subject]), "green aviation")
OR CONTAINS(LOWER([Name]), "green aviation")
OR CONTAINS(LOWER([Abstract]), "green transport")
OR CONTAINS(LOWER([Subject]), "green transport")
OR CONTAINS(LOWER([Name]), "green transport")
OR CONTAINS(LOWER([Abstract]), "grønne transport")
OR CONTAINS(LOWER([Subject]), "grønne transport")
OR CONTAINS(LOWER([Name]), "grønne transport")
OR CONTAINS(LOWER([Abstract]), "sustainable transport")
OR CONTAINS(LOWER([Subject]), "sustainable transport")
OR CONTAINS(LOWER([Name]), "sustainable transport")
OR CONTAINS(LOWER([Abstract]), "sustainable ship")
OR CONTAINS(LOWER([Subject]), "sustainable ship")
OR CONTAINS(LOWER([Name]), "sustainable ship")
OR CONTAINS(LOWER([Abstract]), "sustainable aviation")
OR CONTAINS(LOWER([Subject]), "sustainable aviation")
OR CONTAINS(LOWER([Name]), "sustainable aviation")
OR
  ((CONTAINS(LOWER([Abstract]), "transport")
  OR CONTAINS(LOWER([Subject]), "transport")
  OR CONTAINS(LOWER([Name]), "transport")
  OR CONTAINS(LOWER([Abstract]), "aviation")
  OR CONTAINS(LOWER([Subject]), "aviation")
  OR CONTAINS(LOWER([Name]), "aviation")
  OR REGEXP_MATCH(LOWER([Abstract]), "\bship")
  OR REGEXP_MATCH(LOWER([Subject]), "\bship")
  OR REGEXP_MATCH(LOWER([Name]), "\bship"))
  AND
  (CONTAINS(LOWER([Abstract]), "decarbon")
  OR CONTAINS(LOWER([Subject]), "decarbon")
  OR CONTAINS(LOWER([Name]), "decarbon"))
  )
THEN "Transport"
END
```
### Wind energy (all)
```py
IF CONTAINS(LOWER([Abstract]), "wind energy")
OR CONTAINS(LOWER([Subject]), "wind energy")
OR CONTAINS(LOWER([Name]), "wind energy")
OR CONTAINS(LOWER([Abstract]), "wind power")
OR CONTAINS(LOWER([Subject]), "wind power")
OR CONTAINS(LOWER([Name]), "wind power")
OR CONTAINS(LOWER([Abstract]), "vindkraft")
OR CONTAINS(LOWER([Subject]), "vindkraft")
OR CONTAINS(LOWER([Name]), "vindkraft")
OR CONTAINS(LOWER([Abstract]), "wind turbine")
OR CONTAINS(LOWER([Subject]), "wind turbine")
OR CONTAINS(LOWER([Name]), "wind turbine")
OR CONTAINS(LOWER([Abstract]), "vindturbin")
OR CONTAINS(LOWER([Subject]), "vindturbin")
OR CONTAINS(LOWER([Name]), "vindturbin")
OR CONTAINS(LOWER([Abstract]), "wind farm")
OR CONTAINS(LOWER([Subject]), "wind farm")
OR CONTAINS(LOWER([Name]), "wind farm")
OR CONTAINS(LOWER([Abstract]), "offshore wind")
OR CONTAINS(LOWER([Subject]), "offshore wind")
OR CONTAINS(LOWER([Name]), "offshore wind")
OR CONTAINS([Abstract], "havvind")
OR CONTAINS(LOWER([Subject]), "havvind")
OR CONTAINS(LOWER([Name]), "havvind")
THEN "Wind energy (all)"
END
```
### Offshore wind
```py
IF CONTAINS(LOWER([Abstract]), "offshore wind")
OR CONTAINS(LOWER([Subject]), "offshore wind")
OR CONTAINS(LOWER([Name]), "offshore wind")
OR CONTAINS([Abstract], "havvind")
OR CONTAINS(LOWER([Subject]), "havvind")
OR CONTAINS(LOWER([Name]), "havvind")
OR
  ((CONTAINS(LOWER([Abstract]), "offshore")
  OR CONTAINS(LOWER([Subject]), "offshore")
  OR CONTAINS(LOWER([Name]), "offshore")
  OR CONTAINS(LOWER([Abstract]), "floating")
  OR CONTAINS(LOWER([Subject]), "floating")
  OR CONTAINS(LOWER([Name]), "floating")
  OR CONTAINS(LOWER([Abstract]), "flytende")
  OR CONTAINS(LOWER([Subject]), "flytende")
  OR CONTAINS(LOWER([Name]), "flytende")
  )
  AND
  (CONTAINS(LOWER([Abstract]), "wind energy")
  OR CONTAINS(LOWER([Subject]), "wind energy")
  OR CONTAINS(LOWER([Name]), "wind energy")
  OR CONTAINS(LOWER([Abstract]), "wind power")
  OR CONTAINS(LOWER([Subject]), "wind power")
  OR CONTAINS(LOWER([Name]), "wind power")
  OR CONTAINS(LOWER([Abstract]), "vindkraft")
  OR CONTAINS(LOWER([Subject]), "vindkraft")
  OR CONTAINS(LOWER([Name]), "vindkraft")
  OR CONTAINS(LOWER([Abstract]), "wind turbine")
  OR CONTAINS(LOWER([Subject]), "wind turbine")
  OR CONTAINS(LOWER([Name]), "wind turbine")
  OR CONTAINS(LOWER([Abstract]), "vindturbin")
  OR CONTAINS(LOWER([Subject]), "vindturbin")
  OR CONTAINS(LOWER([Name]), "vindturbin")
  OR CONTAINS(LOWER([Abstract]), "wind farm")
  OR CONTAINS(LOWER([Subject]), "wind farm")
  OR CONTAINS(LOWER([Name]), "wind farm"))
  )
THEN "Offshore wind"
END
```
### Zero emission
```py
IF CONTAINS(LOWER([Abstract]), "zero emission")
OR CONTAINS(LOWER([Subject]), "zero emission")
OR CONTAINS(LOWER([Name]), "zero emission")
OR CONTAINS(LOWER([Abstract]), "zero-emission")
OR CONTAINS(LOWER([Subject]), "zero-emission")
OR CONTAINS(LOWER([Name]), "zero-emission")
OR CONTAINS(LOWER([Abstract]), "null utslipp")
OR CONTAINS(LOWER([Subject]), "null utslipp")
OR CONTAINS(LOWER([Name]), "null utslipp")
OR CONTAINS(LOWER([Abstract]), "nullutslipp")
OR CONTAINS(LOWER([Subject]), "nullutslipp")
OR CONTAINS(LOWER([Name]), "nullutslipp")
THEN "Zero emission"
END
```
