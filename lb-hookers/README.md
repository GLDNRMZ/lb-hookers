# LB-Hookers
ESX to QBCore. Originally converted by [M4RFY](https://github.com/M4RFY)

# Additions

* ps-dispatch alerts 
* qb-target
* Stress releif
* Disabled movement
* Whislte to hooker
* Optimizations 


# Dependencies | ps-dispatch

* Add to ps-dispatch:client:events

```

local function SuspiciousActivity()
    local currentPos = GetEntityCoords(PlayerPedId())
    local locationInfo = getStreetandZone(currentPos)
    local gender = GetPedGender()
    TriggerServerEvent("dispatch:server:notify", {
        dispatchcodename = "susactivity", -- has to match the codes in sv_dispatchcodes.lua so that it generates the right blip
        dispatchCode = "10-66",
        firstStreet = locationInfo,
        gender = gender,
        model = nil,
        plate = nil,
        priority = 2, -- priority
        firstColor = nil,
        automaticGunfire = false,
        origin = {
            x = currentPos.x,
            y = currentPos.y,
            z = currentPos.z
        },
        dispatchMessage = _U('susactivity'), -- message
        job = { "police" } -- jobs that will get the alerts
    })
end

exports('SuspiciousActivity', SuspiciousActivity)

local function SuspiciousActivity2(vehicle)
    local vehdata = vehicleData(vehicle)
    local currentPos = GetEntityCoords(PlayerPedId())
    local locationInfo = getStreetandZone(currentPos)
    local heading = getCardinalDirectionFromHeading()
    TriggerServerEvent("dispatch:server:notify", {
        dispatchcodename = "susactivity2", -- has to match the codes in sv_dispatchcodes.lua so that it generates the right blip
        dispatchCode = "10-66",
        firstStreet = locationInfo,
        model = vehdata.name, -- vehicle name
        plate = vehdata.plate, -- vehicle plate
        priority = 2,
        firstColor = vehdata.colour, -- vehicle color
        heading = heading,
        automaticGunfire = false,
        origin = {
            x = currentPos.x,
            y = currentPos.y,
            z = currentPos.z
        },
        dispatchMessage = _U('susactivity2'),
        job = { "police" }
    })
end

exports('SuspiciousActivity2', SuspiciousActivity2)
```
* Add to ps-dispatch:server:dispatchcodes

```
["susactivity"] =  {displayCode = '10-66', description = "Suspicious Activity", radius = 120.0, recipientList = {'police'}, blipSprite = 469, blipColour = 52, blipScale = 0, blipLength = 0.75, sound = "Lose_1st", sound2 = "GTAO_FM_Events_Soundset", offset = "true", blipflash = "false"},

["susactivity2"] =  {displayCode = '10-66', description = "Solicitation", radius = 0, recipientList = {'police'}, blipSprite = 279, blipColour = 48, blipScale = 1.0, blipLength = 0.75, sound = "Lose_1st", sound2 = "GTAO_FM_Events_Soundset", offset = "false", blipflash = "false"},
```
* Add to ps-dispatch:locales

```
['susactivity'] = "Suspicious Activity",

['susactivity2'] = "Solicitation in Progress",
```
