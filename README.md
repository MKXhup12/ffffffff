_G.Key = 

local ClientId = game:GetService("RbxAnalyticsService"):GetClientId()
local Hwid = {
    [1] = "0650vsd9559-df1b5dfb9-d1f8bdfbdf",--Hwid You
    ["0650vsd9559-df1b5dfb9-d1f8bdfbdf"] = 1,--Hwid You
    [2] = "0650vsd9559-df1b5dfb9-d1f8bdfbdf",--Hwid You
    ["0650vsd9559-df1b5dfb9-d1f8bdfbdf"] = 2,--Hwid You
}
local Key = {
    [1] = "MAMA-70001",--Custom Key
}

local KeyNumber = Hwid[ClientId]
if Hwid[KeyNumber] == ClientId then
if Key[KeyNumber] == _G.Key then
print("Successfully whitelisted!")
loadstring(game:HttpGet("https://raw.githubusercontent.com/MAMAhub1/Mmahub/main/README.md"))()
else
    print("Not Have Key")
function Randomkey(v)
        local GenKey = ""
        for i = 1,v do
            GenKey = GenKey ..string.char(math.random(80,90))
        end
        return GenKey
end
setclipboard("Hwid : "..ClientId.."Key : HUB YOU-"..Randomkey(2)..Randomkey(5))
end
else
    print("Not Have Hwid")
function Randomkey(v)
        local GenKey = ""
        for i = 1,v do
            GenKey = GenKey ..string.char(math.random(80,90))
        end
        return GenKey
end
setclipboard("Hwid : "..ClientId.." Key : HUB YOU-"..Randomkey(2)..Randomkey(5))
end
