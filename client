local QBCore = exports['qb-core']:GetCoreObject()
--------------------------------------------------------------------------------------

RegisterNetEvent('spwanBike:client:spawncycel')
AddEventHandler('spwanBike:client:spawncycel', function()    local ped = PlayerPedId()
  QBCore.Functions.Progressbar('spawn_bike', 'renting bike...', 2000, false, true, { -- Name | Label | Time | useWhileDead | canCancel
      disableMovement = true,
      disableCarMovement = true,
      disableMouse = false,
      disableCombat = true,
  }, {
      animDict = '',
      anim = '',
      flags = 2,
      TriggerEvent('animations:client:EmoteCommandStart', {"keyfob"})
  }, {}, {}, function() -- Play When Done
    local hash = GetHashKey('bmx')
    if not IsModelInCdimage(hash) then return end
    RequestModel(hash)
    while not HasModelLoaded(hash) do Wait(10) end
    local vehicle = CreateVehicle(hash, GetEntityCoords(ped), GetEntityHeading(ped), true, false)
    TaskWarpPedIntoVehicle(ped, vehicle, -1)
    SetModelAsNoLongerNeeded(vehicle)
    TriggerEvent("vehiclekeys:client:SetOwner", GetVehicleNumberPlateText(vehicle))
    QBCore.Functions.Notify('you got bike', 'success', 2000)
      IsDrilling = false
      TriggerEvent('animations:client:EmoteCommandStart', {"c"})
      print('spwan')
  end, function() -- Play When Cancel
      QBCore.Functions.Notify('cancel', 'error', 5000)
      TriggerEvent('animations:client:EmoteCommandStart', {"c"})
      print('cancel')
    end)
end)
-----------------------------------------------------------------
RegisterNetEvent('spwanBike:client:delbike')
AddEventHandler('spwanBike:client:delbike', function()    local ped = PlayerPedId()
QBCore.Functions.Progressbar('store_bike', 'store the bike...', 2000, false, true, { -- Name | Label | Time | useWhileDead | canCancel
    disableMovement = true,
    disableCarMovement = true,
    disableMouse = true,
    disableCombat = true,
}, {
    animDict = '',
    anim = '',
    TriggerEvent('animations:client:EmoteCommandStart', {"kneel2"})
}, {}, {}, function() -- Play When Done
    local ped = PlayerPedId()
    local veh = GetVehiclePedIsUsing(ped)
    if veh ~= 0 then
        SetEntityAsMissionEntity(veh, true, true)
        DeleteVehicle(veh)
    else
        local pcoords = GetEntityCoords(ped)
        local vehicles = GetGamePool('CVehicle')
        for k, v in pairs(vehicles) do
            if #(pcoords - GetEntityCoords(v)) <= 5.0 then
                SetEntityAsMissionEntity(v, true, true)
                DeleteVehicle(v)
            end
        end
    end
    IsDrilling = true
    QBCore.Functions.Notify('bike got store', 'success', 5000)
    TriggerEvent('animations:client:EmoteCommandStart', {"c"})
    print('done')
end, function() -- Play When Cancel
    QBCore.Functions.Notify('cancel', 'error', 5000)
    TriggerEvent('animations:client:EmoteCommandStart', {"c"})
    print('cancel')
   end)
end)
---------------------------------------------------------------
RegisterNetEvent('spwanBike:client:rentmenu')
AddEventHandler('spwanBike:client:rentmenu', function()
    exports['qb-menu']:openMenu({
        {
            header = "🚲 rent menu",
            isMenuHeader = true
        },
        {
            header = "< rent bike 🚲",
            txt = "",
            params = {
                event = "spwanBike:client:spawncycel"
            }
        },
        {
            header = "< store the bike 🅿",
            txt = "",
            params = {
                event = "spwanBike:client:delbike"
            }
        },
    })
end)
