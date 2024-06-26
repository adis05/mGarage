# mGarage

* Create garages/impounds in-game or in the Config file
* Garage action: Target/TextUI
* Multilanguage
* Garages for jobs
* Vehicle search in the garage interface
* Custom vehicle garages
* Obtain an item key if necessary
* Mark vehicles outside the garage
* Share vehicles with companions
* Save vehicles with fake license plates (using the 'fakeplate' item from mVehicle)
* Impound with societies
* Functions to integrate the garage into any housing system
* Function to impound vehicles
* * The impound can establish a society account
* * Set a recovery date
* * Function to remove time from a plate vehicle

## Functions 

### OpenGarage![168956591-43462c40-e7c2-41af-8282-b2d9b6716771](https://github.com/adis05/mGarage/assets/102389489/2fbc5c6e-c073-431a-b284-3be18bbe4b41)

![detail](https://github.com/adis05/mGarage/assets/102389489/215a7648-32f8-4679-81b4-28083a8eadb1)
![banner-connecting](https://github.com/adis05/mGarage/assets/102389489/68a3dc09-3726-4525-a4a9-19ac27c49fad)


* **exports.mGarage:OpenGarage()**

```lua

exports.mGarage:OpenGarage({
    name = 'GARAGE ID/NAME',
    garagetype = 'garage',              
    intocar = true,                     
    carType = { 'automobile', 'bike' }, 
    spawnpos = {  vec4(0, 0, 0, 0) }
})
```
 
### SaveCar 
* **exports.mGarage:SaveCar()**
```lua
    exports.mGarage:SaveCar({
        name = 'GARAGE ID/NAME',
        garagetype = 'garage',              
        entity = vehicleEntity or false to getVehiclePedIsIn,            
        carType = { 'automobile', 'bike' }, 
    })
```

### impound Vehicle
```lua
    exports.mGarage:ImpoundVehicle({ 
        vehicle = Vehicle entity, 
        impoundName = 'Impound Name' 
    })
```

### Remove time for recovery vehicle
```lua
  -- open input to set plate 
    exports.mGarage:UnpoundVehicle()
  -- or direct plate
     exports.mGarage:UnpoundVehicle(plate)
```
### Example 

```lua
RegisterCommand('mGarage:opengarage', function(source, args, raw)
    local ped = PlayerPedId()
    local coords, heading = GetEntityCoords(ped), GetEntityHeading(ped)
    exports.mGarage:OpenGarage({
        name = 'Pillbox Hill',
        garagetype = 'garage',              
        intocar = true,                     
        carType = { 'automobile', 'bike' }, 
        spawnpos = {
            vec4(coords.x, coords.y, coords.z, heading),
        }
    })
end)

RegisterCommand('mGarage:savecar', function(source, args, raw)
    local ped = PlayerPedId()
    local vehicleEntity = GetVehiclePedIsIn(ped, false)
    if DoesEntityExist(vehicleEntity) then
        exports.mGarage:SaveCar({
            name = 'Pillbox Hill',
            garagetype = 'garage',             
            entity = vehicleEntity,             
            carType = { 'automobile', 'bike' }, 
        })
    else
        print('No Vehicle')
    end
end)

RegisterCommand('mGarage:impound', function(source, args, raw)
    local ped = PlayerPedId()
    local vehicleEntity = GetVehiclePedIsIn(ped, false)
    if DoesEntityExist(vehicleEntity) then
     ImpoundVehicle({
        vehicle = vehicleEntity,
        impoundName = 'Impound'
    })
    else
        print('No Vehicle')
    end
end)
![banner-connecting](https://github.com/adis05/mGarage/assets/102389489/f5940f41-12a8-47dc-82d9-36cca209a208)

![detail](https://github.com/adis05/mGarage/assets/102389489/91e14d25-afe4-41f9-87d7-45a8daa33613)



RegisterCommand('mGarage:unpound', function(source, args, raw)
    UnpoundVehicle()
    -- or UnpoundVehicle('MONO 420')
end)
```
