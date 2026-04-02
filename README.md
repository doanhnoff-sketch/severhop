local TeleportService = game:GetService("TeleportService")
local HttpService = game:GetService("HttpService")
local Players = game:GetService("Players")

local PlaceID = game.PlaceId
local JobID = game.JobId

while true do
    task.wait(600)

    local url = "https://games.roblox.com/v1/games/"..PlaceID.."/servers/Public?sortOrder=Desc&limit=100"
    local servers = HttpService:JSONDecode(game:HttpGet(url))

    for _, v in pairs(servers.data) do
        if v.playing < v.maxPlayers and v.id ~= JobID then
            TeleportService:TeleportToPlaceInstance(PlaceID, v.id, Players.LocalPlayer)
            break
        end
    end
end
