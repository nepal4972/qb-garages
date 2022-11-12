Discord For Help : https://discord.gg/PaDuyF9w76
ATENTION:



THIS SCRIPT USES THE LATEST VERSION OF THE RADIALMENU AND QB-CORE

This is a qb-garages script that uses the radialmenu to retrieve and park vehicles. Almost everything is fully customizable to the last bit!


Dependencies:

  1. qb-radialmenu
  2. qb-core


Installation:

Drag 'n Drop replace for qb-garages.

  1. Delete qb-garages.
  2. Drag the downloaded qb-garages folder into the [qb] folder.
  3. If you want to use the latest features, apply patch1.sql to your DB


Features:

  1. Public Garages
  2. House Garages
  3. Gang Garages
  4. Job Garages
  5. Depot Garages
  6. Blips and names
  7. Custom DrawText
  8. Water Garages
  9. Aircraft Garages








Config Example:


--Dont Use This This is only for Professionals--


 --No need to use this this will create error--


 -- GARAGE CONFIGURATION EXAMPLE :
 
 
 
    ['somegarage'] = {
        ['Zone'] = {
            ['Shape'] = { -- Create a polyzone by using '/pzcreate poly', '/pzadd' and '/pzfinish' or '/pzcancel' to cancel it. the newly created polyzone will be in txData/QBCoreFramework_******.base/polyzone_created_zones.txt
            vector2(-1030.4713134766, -3016.3388671875),
            vector2(-970.09686279296, -2914.7397460938),
            vector2(-948.322265625, -2927.9030761718),
            vector2(-950.47174072266, -2941.6584472656),
            vector2(-949.04180908204, -2953.9467773438),
            vector2(-940.78369140625, -2957.2941894532),
            vector2(-943.88732910156, -2964.5512695312),
            vector2(-897.61529541016, -2990.0505371094),
            vector2(-930.01025390625, -3046.0695800782),
            vector2(-942.36407470704, -3044.7858886718),
            vector2(-952.97467041016, -3056.5122070312),
            vector2(-957.11712646484, -3057.0900878906)
            },
            ['minZ'] = 12.5,  -- min height of the parking zone, cannot be the same as maxZ, and must be smaller than maxZ
            ['maxZ'] = 20.0,  -- max height of the parking zone
            -- VERY IMPORTANT: Make sure the parking zone is high enough - higher than the tallest vehicle and LOW ENOUGH / touches the ground (turn on debug to see)
        },
        label = 'Hangar', -- label displayed on phone
        type = 'public', -- 'public', 'job', 'depot' or 'gang'
        showBlip = true, -- optional, when not defined, defaults to false
        blipName = 'Police', -- otional
        blipNumber = 90, -- optional, numbers can be found here: https://docs.fivem.net/docs/game-references/blips/
        blipColor = 69, -- optional, defaults to 3 (Blue), numbers can be found here: https://docs.fivem.net/docs/game-references/blips/
        blipcoords = vector3(-972.66, -3005.4, 13.32), -- blip coordinates
        job = 'police', -- optional, everyone can use it when not defined
        vehicleCategories = {'helicopter', 'plane'}, -- categories defined in VehicleCategories
        drawText = 'Hangar', -- the drawtext text, shown when entering the polyzone of that garage
        ParkingDistance = 10.0 -- Optional ParkingDistance, to override the global ParkingDistance
        SpawnDistance = 5.0 -- Optional SpawnDistance, to override the global SpawnDistance
        debug = false -- Optional, will show the polyzone and the parking spots, helpful when creating new garages. If too many garages are set to debug, it will not show all parking lots
        ExitWarpLocations: { -- Optional, Used for e.g. Boat parking, to teleport the player out of the boat to the closest location defined in the list. 
            vector3(-807.15, -1496.86, 1.6),
            vector3(-800.17, -1494.87, 1.6),
            vector3(-792.92, -1492.18, 1.6),
            vector3(-787.58, -1508.59, 1.6),
            vector3(-794.89, -1511.16, 1.6),
            vector3(-800.21, -1513.05, 1.6),
        } 
    },
    
    
    
    
    
 parking vehicle using target
 
 
 
 --Dont Use This This is only for Professionals--
 
 
 
 --No need to use this this will create error--
    
    
    
    
    
    
    local garageName = 'pdgarage'
    exports['qb-target']:AddBoxZone(garageName, vector3(469.51, -992.35, 26.27), 0.2, 0.2, {
        name = garageName,
        debugPoly = true,
        minZ = 26.80,
        maxZ = 27.10,
    }, {
        options = {
            {
                type = "client",
                action = function ()
                    TriggerEvent('qb-garages:client:ParkLastVehicle', garageName)
                end,
                icon = 'parking',
                label = 'Park Vehicle',
            },
        },
        distance = 3
    })
    
    
    
    
    
    
  --improved phone tracking--
  
  
    

EDIT THIS: 
    
    
    
     RegisterNUICallback('track-vehicle', function(data, cb)
    local veh = data.veh
    if veh.state == 'In' then
        if veh.parkingspot then
            SetNewWaypoint(veh.parkingspot.x, veh.parkingspot.y)
            QBCore.Functions.Notify("Your vehicle has been marked", "success")
        end
    elseif veh.state == 'Out' and findVehFromPlateAndLocate(veh.plate) then
        QBCore.Functions.Notify("Your vehicle has been marked", "success")
    else
        QBCore.Functions.Notify("This vehicle cannot be located", "error")
    end
    cb("ok")
    end)
    
    
--ONLY FOR loaf_housing--   
    
    
    
    
     exports('HasHouseKey', function(propertyId)
    local stringId = tostring(propertyId)
    local data = cache.ownedHouses[stringId] or cache.houses[stringId]
    return exports['loaf_keysystem']:HasKey(GetKeyName(propertyId, data.id))
end)
   





   
   
   

 
 

