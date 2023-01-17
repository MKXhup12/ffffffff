local LocalPlayer = game:GetService('Players').LocalPlayer
local PlayerGui = LocalPlayer:WaitForChild('PlayerGui')
local MainScreen = PlayerGui:WaitForChild('Main')
local AwakeningToggler = MainScreen:WaitForChild('AwakeningToggler')
local HttpService = game:GetService('HttpService')
local PostionXCount = 0;
local ItemRange = 0; 
local PositionYCount = 0;
local PostionXCountFruit = 800;
local ItemRangeFruit = 0; 
local ItemMaxFruit = 2;
local PositionYCountFruit = 113;
local RequestGetInvertory;
_G.MythicalCut = true
_G.LegendaryCut = true
_G.RareCut = false
_G.UncommonCut = false
_G.CommonCut = false
_G.MaxCountItem = 10
_G.ShowMasteryCut = true
 _G.LevelMasteryCut = 300
local __Config = {
	['Rarity'] = {
		__Mythical = _G.MythicalCut,
		__Legendary = _G.LegendaryCut,
		__Rare = _G.RareCut, 
		__Uncommon = _G.UncommonCut, 
		__Common = _G.CommonCut
	},
	['MaxLength'] = _G.MaxCountItem,
	['ShowMastery'] = _G.ShowMasteryCut,
	['LevelShowMastery'] = _G.LevelMasteryCut,
};
local MaleeList = {};
local ItemMax = __Config['MaxLength'];
local Requirement = {
    ['Mythical'] = {},
    ['Legendary'] = {},
    ['Rare'] = {},
    ['Uncommon'] = {},
    ['Common'] = {}
}
local ViewportSize = workspace.CurrentCamera.ViewportSize
local IconModule = require(game.Players.LocalPlayer.PlayerGui.Main.UIController.Inventory.Spritesheets)
if game.CoreGui:FindFirstChild('CreateItem') then 
	game.CoreGui:FindFirstChild('CreateItem'):Destroy()
end
function OffsetXToSacle(offset)
	return offset / ViewportSize.X
end
function OffsetYToSacle(offset)
	return offset / ViewportSize.Y
end
function SacleXToOffeset(offset)
	return offset / ViewportSize.X
end
function SacleYToOffeset(offset)
	return offset / ViewportSize.Y
end
function queryData(ItemName)
   	local v1 = ItemName:gsub("'", ""):gsub(":", "") .. "1.png";
	local v2 = ItemName:gsub("'", ""):gsub(":", "") .. "2.png";
	for i, _ in pairs(IconModule) do 
        for v, __ in pairs(_) do 
            if v == v1 then 
                local j = __
                local q = i
                	return {
                	    ['Name'] = q, 
                	    ['Value'] = __
                	}
            end    
        end
	end

end
function formatNumber(nb) 
   local i, k, j = tostring(nb):match("(%-?%d?)(%d*)(%.?.*)")
   return i..k:reverse():gsub("(%d%d%d)", "%1,"):reverse()..j

end
	local CreateItemScreen = Instance.new("ScreenGui")
	local CreateItems = Instance.new('Frame')
	local CreateItemFruit = Instance.new('Frame')
	
    CreateItemScreen.Name = 'CreateItem'
    CreateItemScreen.Parent = game.CoreGui
    
    CreateItems.Name = HttpService:GenerateGUID()
    CreateItems.Parent = CreateItemScreen
    CreateItems.Size = UDim2.new(1,0,1,0)
    CreateItems.BackgroundTransparency = 1.000
    CreateItemFruit.Name = HttpService:GenerateGUID()
    CreateItemFruit.Parent = CreateItemScreen
    CreateItemFruit.Size = UDim2.new(1,0,1,0)
    CreateItemFruit.BackgroundTransparency = 1.000
	local Fragments = Instance.new("TextLabel")
	Fragments.Name = HttpService:GenerateGUID()
	Fragments.Parent = CreateItemScreen
	Fragments.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
	Fragments.BackgroundTransparency = 1.000
	Fragments.Position = UDim2.new(0, 6, 0.65, 0);
	Fragments.Size = UDim2.new(0.150000006, 0, 0.0599999987, 5)
	Fragments.ZIndex = -9
	Fragments.Font = Enum.Font.SourceSansBold
	Fragments.Text =  'ƒ' .. formatNumber(game:GetService("Players").LocalPlayer.Data.Fragments.Value)
	Fragments.TextColor3 = Color3.fromRGB(177, 121, 255)
	Fragments.TextScaled = true
	Fragments.TextSize = 36.000
	Fragments.TextStrokeTransparency = 0.000
	Fragments.TextWrapped = true
	Fragments.TextXAlignment = Enum.TextXAlignment.Left
	game:GetService("Players").LocalPlayer.PlayerGui.Main.MenuButton.Position = UDim2.new(0, 10, 0.6, 0)
function CreateItemFruit(ItemType, ItemNames, ItemIcon, ImageRectSize, ItemRectOffset, ItemBackgroundColor, ExtraData, Data)
	local _1 = Instance.new("Frame")
	local ItemLine2 = Instance.new("TextLabel")
	local ItemName = Instance.new("TextLabel")
	local Background = Instance.new("ImageLabel")
	local UICorner = Instance.new("UICorner")
	local UIGradient = Instance.new("UIGradient")
	local Icon = Instance.new("ImageLabel")
	if ItemRangeFruit >= ItemMaxFruit then 
		PositionYCountFruit = PositionYCountFruit + 105;
		ItemRangeFruit = 0 ;
		PostionXCountFruit = 800; 
	end
	_1.Name = HttpService:GenerateGUID()
	_1.Parent = CreateItems
	_1.BackgroundColor3 = Color3.fromRGB(255, 0, 4)
	_1.BackgroundTransparency = 1.000
	_1.LayoutOrder = 1
	_1.Size = UDim2.new(0, 100, 0, 100)
	_1.Position = UDim2.new(OffsetXToSacle(PostionXCountFruit),0,OffsetYToSacle(PositionYCountFruit),0)
	PostionXCountFruit = PostionXCountFruit + 101; 
	ItemRangeFruit = ItemRangeFruit + 1;
	
	ItemLine2.Name = HttpService:GenerateGUID()
	ItemLine2.Parent = _1
	ItemLine2.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
	ItemLine2.BackgroundTransparency = 1.000
	ItemLine2.Position = UDim2.new(0.0799999982, 0, 0.0199999996, 0)
	ItemLine2.Size = UDim2.new(0.699999988, 0, 0.150000006, 0)
	ItemLine2.ZIndex = 5
	ItemLine2.Font = Enum.Font.SourceSansItalic
	ItemLine2.Text = ItemType
	ItemLine2.TextColor3 = Color3.fromRGB(255, 255, 255)
	ItemLine2.TextScaled = true
	ItemLine2.TextSize = 14.000
	ItemLine2.TextStrokeTransparency = 0.600
	ItemLine2.TextWrapped = true
	ItemLine2.TextXAlignment = Enum.TextXAlignment.Left
	ItemLine2.TextYAlignment = Enum.TextYAlignment.Top

	ItemName.Name = HttpService:GenerateGUID()
	ItemName.Parent = _1
	ItemName.AnchorPoint = Vector2.new(1, 1)
	ItemName.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
	ItemName.BackgroundTransparency = 1.000
	ItemName.Position = UDim2.new(0.959999979, 0, 0.980000019, 0)
	ItemName.Size = UDim2.new(0.600000024, 0, 0.319999993, 0)
	ItemName.ZIndex = 5
	ItemName.Font = Enum.Font.SourceSansSemibold
	ItemName.Text = ItemNames
	ItemName.TextColor3 = Color3.fromRGB(255, 255, 255)
	ItemName.TextScaled = true
	ItemName.TextSize = 14.000
	ItemName.TextStrokeTransparency = 0.600
	ItemName.TextWrapped = true
	ItemName.TextXAlignment = Enum.TextXAlignment.Right
	ItemName.TextYAlignment = Enum.TextYAlignment.Bottom

	Background.Name = HttpService:GenerateGUID()
	Background.Parent = _1
	Background.BackgroundColor3 = ItemBackgroundColor
	Background.BorderSizePixel = 0
	Background.Size = UDim2.new(1, 0, 1, 0)
	Background.ZIndex = 3
	Background.Image = "http://www.roblox.com/asset/?id=9944431153"
	Background.ImageColor3 = Color3.fromRGB(0, 0, 0)
	Background.ImageTransparency = 1.000

	UICorner.CornerRadius = UDim.new(0.0700000003, 0)
	UICorner.Parent = Background

	UIGradient.Color = ColorSequence.new{ColorSequenceKeypoint.new(0.00, Color3.fromRGB(172, 172, 172)), ColorSequenceKeypoint.new(1.00, Color3.fromRGB(225, 225, 225))}
	UIGradient.Rotation = 90
	UIGradient.Parent = Background

	Icon.Name = HttpService:GenerateGUID()
	Icon.Parent = _1
	Icon.AnchorPoint = Vector2.new(0.5, 0.5)
	Icon.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
	Icon.BackgroundTransparency = 1.000
	Icon.Position = UDim2.new(0.5, 0, 0.5, 0)
	Icon.Size = UDim2.new(0.899999976, 0, 0.899999976, 0)
	Icon.Visible = true
	Icon.ZIndex = 4
	Icon.Image = ItemIcon
	Icon.ScaleType = Enum.ScaleType.Fit
	Icon.ImageRectSize = ItemRectOffset
	Icon.ImageRectOffset = ImageRectSize
	if ExtraData then 
		local ItemLine1 = Instance.new("TextLabel")
		ItemLine1.Name = HttpService:GenerateGUID()
		ItemLine1.Parent = _1
		ItemLine1.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
		ItemLine1.BackgroundTransparency = 1.000
		ItemLine1.Position = UDim2.new(0.0799999982, 0, 0.140000001, 0)
		ItemLine1.Size = UDim2.new(0.699999988, 0, 0.150000006, 0)
		ItemLine1.Visible = true
		ItemLine1.ZIndex = 5
		ItemLine1.Font = Enum.Font.SourceSansSemibold
		ItemLine1.Text = Data
		ItemLine1.TextColor3 = Color3.fromRGB(255, 255, 255)
		ItemLine1.TextScaled = true
		ItemLine1.TextSize = 14.000
		ItemLine1.TextStrokeTransparency = 0.600
		ItemLine1.TextWrapped = true
		ItemLine1.TextXAlignment = Enum.TextXAlignment.Left
		ItemLine1.TextYAlignment = Enum.TextYAlignment.Top
	end
end
function CreateItem(ItemType, ItemNames, ItemIcon, ImageRectSize, ItemRectOffset, ItemBackgroundColor, ExtraData, Data)
	local _1 = Instance.new("Frame")
	local ItemLine2 = Instance.new("TextLabel")
	local ItemName = Instance.new("TextLabel")
	local Background = Instance.new("ImageLabel")
	local UICorner = Instance.new("UICorner")
	local UIGradient = Instance.new("UIGradient")
	local Icon = Instance.new("ImageLabel")
	if ItemRange >= ItemMax then 
		PositionYCount = PositionYCount + 101;
		ItemRange = 0 ;
		PostionXCount = 0; 
	end
	_1.Name = HttpService:GenerateGUID()
	_1.Parent = CreateItems
	_1.BackgroundColor3 = Color3.fromRGB(255, 0, 4)
	_1.BackgroundTransparency = 1.000
	_1.LayoutOrder = 1
	_1.Size = UDim2.new(0, 100, 0, 100)
	_1.Position = UDim2.new(0,PostionXCount,0,PositionYCount)
	PostionXCount = PostionXCount + 101; 
	ItemRange = ItemRange + 1;
	
	ItemLine2.Name = HttpService:GenerateGUID()
	ItemLine2.Parent = _1
	ItemLine2.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
	ItemLine2.BackgroundTransparency = 1.000
	ItemLine2.Position = UDim2.new(0.0799999982, 0, 0.0199999996, 0)
	ItemLine2.Size = UDim2.new(0.699999988, 0, 0.150000006, 0)
	ItemLine2.ZIndex = 5
	ItemLine2.Font = Enum.Font.SourceSansItalic
	ItemLine2.Text = ItemType
	ItemLine2.TextColor3 = Color3.fromRGB(255, 255, 255)
	ItemLine2.TextScaled = true
	ItemLine2.TextSize = 14.000
	ItemLine2.TextStrokeTransparency = 0.600
	ItemLine2.TextWrapped = true
	ItemLine2.TextXAlignment = Enum.TextXAlignment.Left
	ItemLine2.TextYAlignment = Enum.TextYAlignment.Top

	ItemName.Name = HttpService:GenerateGUID()
	ItemName.Parent = _1
	ItemName.AnchorPoint = Vector2.new(1, 1)
	ItemName.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
	ItemName.BackgroundTransparency = 1.000
	ItemName.Position = UDim2.new(0.959999979, 0, 0.980000019, 0)
	ItemName.Size = UDim2.new(0.600000024, 0, 0.319999993, 0)
	ItemName.ZIndex = 5
	ItemName.Font = Enum.Font.SourceSansSemibold
	ItemName.Text = ItemNames
	ItemName.TextColor3 = Color3.fromRGB(255, 255, 255)
	ItemName.TextScaled = true
	ItemName.TextSize = 14.000
	ItemName.TextStrokeTransparency = 0.600
	ItemName.TextWrapped = true
	ItemName.TextXAlignment = Enum.TextXAlignment.Right
	ItemName.TextYAlignment = Enum.TextYAlignment.Bottom

	Background.Name = HttpService:GenerateGUID()
	Background.Parent = _1
	Background.BackgroundColor3 = ItemBackgroundColor
	Background.BorderSizePixel = 0
	Background.Size = UDim2.new(1, 0, 1, 0)
	Background.ZIndex = 3
	Background.Image = "http://www.roblox.com/asset/?id=9944431153"
	Background.ImageColor3 = Color3.fromRGB(0, 0, 0)
	Background.ImageTransparency = 1.000

	UICorner.CornerRadius = UDim.new(0.0700000003, 0)
	UICorner.Parent = Background

	UIGradient.Color = ColorSequence.new{ColorSequenceKeypoint.new(0.00, Color3.fromRGB(172, 172, 172)), ColorSequenceKeypoint.new(1.00, Color3.fromRGB(225, 225, 225))}
	UIGradient.Rotation = 90
	UIGradient.Parent = Background

	Icon.Name = HttpService:GenerateGUID()
	Icon.Parent = _1
	Icon.AnchorPoint = Vector2.new(0.5, 0.5)
	Icon.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
	Icon.BackgroundTransparency = 1.000
	Icon.Position = UDim2.new(0.5, 0, 0.5, 0)
	Icon.Size = UDim2.new(0.899999976, 0, 0.899999976, 0)
	Icon.Visible = true
	Icon.ZIndex = 4
	Icon.Image = ItemIcon
	Icon.ScaleType = Enum.ScaleType.Fit
	Icon.ImageRectSize = ItemRectOffset
	Icon.ImageRectOffset = ImageRectSize
	if ExtraData then 
		local ItemLine1 = Instance.new("TextLabel")
		ItemLine1.Name = HttpService:GenerateGUID()
		ItemLine1.Parent = _1
		ItemLine1.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
		ItemLine1.BackgroundTransparency = 1.000
		ItemLine1.Position = UDim2.new(0.0799999982, 0, 0.140000001, 0)
		ItemLine1.Size = UDim2.new(0.699999988, 0, 0.150000006, 0)
		ItemLine1.Visible = true
		ItemLine1.ZIndex = 5
		ItemLine1.Font = Enum.Font.SourceSansSemibold
		ItemLine1.Text = Data
		ItemLine1.TextColor3 = Color3.fromRGB(255, 255, 255)
		ItemLine1.TextScaled = true
		ItemLine1.TextSize = 14.000
		ItemLine1.TextStrokeTransparency = 0.600
		ItemLine1.TextWrapped = true
		ItemLine1.TextXAlignment = Enum.TextXAlignment.Left
		ItemLine1.TextYAlignment = Enum.TextYAlignment.Top
	end
end
RequestGetInvertory = game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("getInventory")


function getBackgroundColor(Rarity) 
    if Rarity == 0 then 
        return Color3.fromRGB(179, 179, 179)    
    elseif Rarity == 1 then
        return Color3.fromRGB(92, 140, 211)
    elseif Rarity == 2 then
        return Color3.fromRGB(140, 82, 255)
    elseif Rarity == 3 then 
        return Color3.fromRGB(213, 43, 228)
    elseif Rarity == 4 then 
        return Color3.fromRGB(238,47,50)
    end
end

for _, __ in pairs(RequestGetInvertory) do 
    if __['Rarity'] == 4 then
		if __Config['Rarity']['__Mythical'] then 
			table.insert(Requirement['Mythical'], __)
		end
    end
    if __['Rarity'] == 3 then
		if __Config['Rarity']['__Legendary'] then 
			table.insert(Requirement['Legendary'], __)
		end
    end
    if __['Rarity'] == 2 then
		if __Config['Rarity']['__Rare'] then 
			table.insert(Requirement['Rare'], __)
		end
    end
    if __['Rarity'] == 1 then
		if __Config['Rarity']['__Uncommon'] then 
			table.insert(Requirement['Uncommon'], __)
		end
    end
    if __['Rarity'] == 0 then
		if __Config['Rarity']['__Common'] then 
			table.insert(Requirement['Common'], __)
		end
    end
end

function SortItemSword(itemType)
		for i ,__  in pairs(Requirement['Mythical']) do
			if __['Type'] == itemType then
				local IconData = queryData(__['Name'])
				local Offset = Vector2.new(IconData['Value'][3], IconData['Value'][4])
				local Size = Vector2.new(IconData['Value'][1], IconData['Value'][2])
				if __['Mastery'] >= __Config['LevelShowMastery'] and __Config['ShowMastery'] then 
					CreateItem('Sword', __['Name'], IconData['Name'], Size, Offset, getBackgroundColor(__['Rarity']), true, "Mastery - " .. tostring(__['Mastery']))
				else
					CreateItem('Sword', __['Name'], IconData['Name'], Size, Offset, getBackgroundColor(__['Rarity']), false, "")
				end
			end		
		end
	for i ,__  in pairs(Requirement['Legendary']) do
			if __['Type'] == itemType then
				local IconData = queryData(__['Name'])
				local Offset = Vector2.new(IconData['Value'][3], IconData['Value'][4])
				local Size = Vector2.new(IconData['Value'][1], IconData['Value'][2])
				if __['Mastery'] >= __Config['LevelShowMastery'] and __Config['ShowMastery'] then 
					CreateItem('Sword', __['Name'], IconData['Name'], Size, Offset, getBackgroundColor(__['Rarity']), true, "Mastery - " .. tostring(__['Mastery']))
				else
					CreateItem('Sword', __['Name'], IconData['Name'], Size, Offset, getBackgroundColor(__['Rarity']), false, "")
				end
			end		
	end
	for i ,__  in pairs(Requirement['Rare']) do
			if __['Type'] == itemType then
				local IconData = queryData(__['Name'])
				local Offset = Vector2.new(IconData['Value'][3], IconData['Value'][4])
				local Size = Vector2.new(IconData['Value'][1], IconData['Value'][2])
				if __['Mastery'] >= __Config['LevelShowMastery'] and __Config['ShowMastery'] then 
					CreateItem('Sword', __['Name'], IconData['Name'], Size, Offset, getBackgroundColor(__['Rarity']), true, "Mastery - " .. tostring(__['Mastery']))
				else
					CreateItem('Sword', __['Name'], IconData['Name'], Size, Offset, getBackgroundColor(__['Rarity']), false, "")
				end
			end		
	end
	for i ,__  in pairs(Requirement['Uncommon']) do
			if __['Type'] == itemType then
				local IconData = queryData(__['Name'])
				local Offset = Vector2.new(IconData['Value'][3], IconData['Value'][4])
				local Size = Vector2.new(IconData['Value'][1], IconData['Value'][2])
				if __['Mastery'] >= __Config['LevelShowMastery'] and __Config['ShowMastery'] then 
					CreateItem('Sword', __['Name'], IconData['Name'], Size, Offset, getBackgroundColor(__['Rarity']), true, "Mastery - " .. tostring(__['Mastery']))
				else
					CreateItem('Sword', __['Name'], IconData['Name'], Size, Offset, getBackgroundColor(__['Rarity']), false, "")
				end
			end		
	end
	for i ,__  in pairs(Requirement['Common']) do
			if __['Type'] == itemType then
				local IconData = queryData(__['Name'])
				local Offset = Vector2.new(IconData['Value'][3], IconData['Value'][4])
				local Size = Vector2.new(IconData['Value'][1], IconData['Value'][2])
				if __['Mastery'] >= __Config['LevelShowMastery'] and __Config['ShowMastery'] then 
					CreateItem('Sword', __['Name'], IconData['Name'], Size, Offset, getBackgroundColor(__['Rarity']), true, "Mastery - " .. tostring(__['Mastery']))
				else
					CreateItem('Sword', __['Name'], IconData['Name'], Size, Offset, getBackgroundColor(__['Rarity']), false, "")
				end
			end		
	end
	ItemRange = ItemMax
end
SortItemSword('Sword')
function SortItemBloxFruit(itemType)
		for i ,__  in pairs(Requirement['Mythical']) do
			if __['Type'] == itemType then
				local IconData = queryData(__['Name'])
				local Offset = Vector2.new(IconData['Value'][3], IconData['Value'][4])
				local Size = Vector2.new(IconData['Value'][1], IconData['Value'][2])
            CreateItemFruit( __['Type'], __['Name'], IconData['Name'], Size, Offset, getBackgroundColor(__['Rarity']), true, "x" .. __['Count'])
			end		
		end
	for i ,__  in pairs(Requirement['Legendary']) do
			if __['Type'] == itemType then
				local IconData = queryData(__['Name'])
				local Offset = Vector2.new(IconData['Value'][3], IconData['Value'][4])
				local Size = Vector2.new(IconData['Value'][1], IconData['Value'][2])
            CreateItemFruit( __['Type'], __['Name'], IconData['Name'], Size, Offset, getBackgroundColor(__['Rarity']), true, "x" .. __['Count'])
			end		
	end
	for i ,__  in pairs(Requirement['Rare']) do
			if __['Type'] == itemType then
				local IconData = queryData(__['Name'])
				local Offset = Vector2.new(IconData['Value'][3], IconData['Value'][4])
				local Size = Vector2.new(IconData['Value'][1], IconData['Value'][2])
            CreateItemFruit( __['Type'], __['Name'], IconData['Name'], Size, Offset, getBackgroundColor(__['Rarity']), true, "x" .. __['Count'])
			end		
	end
	for i ,__  in pairs(Requirement['Uncommon']) do
			if __['Type'] == itemType then
				local IconData = queryData(__['Name'])
				local Offset = Vector2.new(IconData['Value'][3], IconData['Value'][4])
				local Size = Vector2.new(IconData['Value'][1], IconData['Value'][2])
            CreateItemFruit( __['Type'], __['Name'], IconData['Name'], Size, Offset, getBackgroundColor(__['Rarity']), true, "x" .. __['Count'])
			end		
	end
	for i ,__  in pairs(Requirement['Common']) do
			if __['Type'] == itemType then
				local IconData = queryData(__['Name'])
				local Offset = Vector2.new(IconData['Value'][3], IconData['Value'][4])
				local Size = Vector2.new(IconData['Value'][1], IconData['Value'][2])
            CreateItemFruit( __['Type'], __['Name'], IconData['Name'], Size, Offset, getBackgroundColor(__['Rarity']), true, "x" .. __['Count'])
			end		
	end
	ItemRange = ItemMax
end
SortItemBloxFruit("Blox Fruit")
function SortItemWear(itemType)
		for i ,__  in pairs(Requirement['Mythical']) do
			if __['Type'] == itemType then
				local IconData = queryData(__['Name'])
				local Offset = Vector2.new(IconData['Value'][3], IconData['Value'][4])
				local Size = Vector2.new(IconData['Value'][1], IconData['Value'][2])
            	CreateItem('Accessory', __['Name'], IconData['Name'], Size, Offset, getBackgroundColor(__['Rarity']), false, "")
			end		
		end
	for i ,__  in pairs(Requirement['Legendary']) do
			if __['Type'] == itemType then
				local IconData = queryData(__['Name'])
				local Offset = Vector2.new(IconData['Value'][3], IconData['Value'][4])
				local Size = Vector2.new(IconData['Value'][1], IconData['Value'][2])
            	CreateItem('Accessory', __['Name'], IconData['Name'], Size, Offset, getBackgroundColor(__['Rarity']), false, "")
			end		
	end
	for i ,__  in pairs(Requirement['Rare']) do
			if __['Type'] == itemType then
				local IconData = queryData(__['Name'])
				local Offset = Vector2.new(IconData['Value'][3], IconData['Value'][4])
				local Size = Vector2.new(IconData['Value'][1], IconData['Value'][2])
            	CreateItem('Accessory', __['Name'], IconData['Name'], Size, Offset, getBackgroundColor(__['Rarity']), false, "")
			end		
	end
	for i ,__  in pairs(Requirement['Uncommon']) do
			if __['Type'] == itemType then
				local IconData = queryData(__['Name'])
				local Offset = Vector2.new(IconData['Value'][3], IconData['Value'][4])
				local Size = Vector2.new(IconData['Value'][1], IconData['Value'][2])
            	CreateItem('Accessory', __['Name'], IconData['Name'], Size, Offset, getBackgroundColor(__['Rarity']), false, "")
			end		
	end
	for i ,__  in pairs(Requirement['Common']) do
			if __['Type'] == itemType then
				local IconData = queryData(__['Name'])
				local Offset = Vector2.new(IconData['Value'][3], IconData['Value'][4])
				local Size = Vector2.new(IconData['Value'][1], IconData['Value'][2])
            	CreateItem('Accessory', __['Name'], IconData['Name'], Size, Offset, getBackgroundColor(__['Rarity']), false, "")
			end		
	end
	ItemRange = ItemMax
end
function SortItemGun(itemType)
		for i ,__  in pairs(Requirement['Mythical']) do
			if __['Type'] == itemType then
				local IconData = queryData(__['Name'])
				local Offset = Vector2.new(IconData['Value'][3], IconData['Value'][4])
				local Size = Vector2.new(IconData['Value'][1], IconData['Value'][2])
				CreateItem('Gun', __['Name'], IconData['Name'], Size, Offset, getBackgroundColor(__['Rarity']), false, "")
			end		
		end
	for i ,__  in pairs(Requirement['Legendary']) do
			if __['Type'] == itemType then
				local IconData = queryData(__['Name'])
				local Offset = Vector2.new(IconData['Value'][3], IconData['Value'][4])
				local Size = Vector2.new(IconData['Value'][1], IconData['Value'][2])
				CreateItem('Gun', __['Name'], IconData['Name'], Size, Offset, getBackgroundColor(__['Rarity']), false, "")
			end		
	end
	for i ,__  in pairs(Requirement['Rare']) do
			if __['Type'] == itemType then
				local IconData = queryData(__['Name'])
				local Offset = Vector2.new(IconData['Value'][3], IconData['Value'][4])
				local Size = Vector2.new(IconData['Value'][1], IconData['Value'][2])
				CreateItem('Gun', __['Name'], IconData['Name'], Size, Offset, getBackgroundColor(__['Rarity']), false, "")
			end		
	end
	for i ,__  in pairs(Requirement['Uncommon']) do
			if __['Type'] == itemType then
				local IconData = queryData(__['Name'])
				local Offset = Vector2.new(IconData['Value'][3], IconData['Value'][4])
				local Size = Vector2.new(IconData['Value'][1], IconData['Value'][2])
				CreateItem('Gun', __['Name'], IconData['Name'], Size, Offset, getBackgroundColor(__['Rarity']), false, "")
			end		
	end
	for i ,__  in pairs(Requirement['Common']) do
			if __['Type'] == itemType then
				local IconData = queryData(__['Name'])
				local Offset = Vector2.new(IconData['Value'][3], IconData['Value'][4])
				local Size = Vector2.new(IconData['Value'][1], IconData['Value'][2])
				CreateItem('Gun', __['Name'], IconData['Name'], Size, Offset, getBackgroundColor(__['Rarity']), false, "")
			end		
	end
	ItemRange = ItemMax
end
SortItemGun('Gun')
SortItemWear('Wear')
function SortItemMaterial(itemType)
		for i ,__  in pairs(Requirement['Mythical']) do
			if __['Type'] == itemType then
				local IconData = queryData(__['Name'])
				local Offset = Vector2.new(IconData['Value'][3], IconData['Value'][4])
				local Size = Vector2.new(IconData['Value'][1], IconData['Value'][2])
            CreateItem('Material', __['Name'], IconData['Name'], Size, Offset, getBackgroundColor(__['Rarity']), true, "x" .. __['Count'])
			end		
		end
	for i ,__  in pairs(Requirement['Legendary']) do
			if __['Type'] == itemType then
				local IconData = queryData(__['Name'])
				local Offset = Vector2.new(IconData['Value'][3], IconData['Value'][4])
				local Size = Vector2.new(IconData['Value'][1], IconData['Value'][2])
            CreateItem('Material', __['Name'], IconData['Name'], Size, Offset, getBackgroundColor(__['Rarity']), true, "x" .. __['Count'])
			end		
	end
	for i ,__  in pairs(Requirement['Rare']) do
			if __['Type'] == itemType then
				local IconData = queryData(__['Name'])
				local Offset = Vector2.new(IconData['Value'][3], IconData['Value'][4])
				local Size = Vector2.new(IconData['Value'][1], IconData['Value'][2])
            CreateItem('Material', __['Name'], IconData['Name'], Size, Offset, getBackgroundColor(__['Rarity']), true, "x" .. __['Count'])
			end		
	end
	for i ,__  in pairs(Requirement['Uncommon']) do
			if __['Type'] == itemType then
				local IconData = queryData(__['Name'])
				local Offset = Vector2.new(IconData['Value'][3], IconData['Value'][4])
				local Size = Vector2.new(IconData['Value'][1], IconData['Value'][2])
            CreateItem('Material', __['Name'], IconData['Name'], Size, Offset, getBackgroundColor(__['Rarity']), true, "x" .. __['Count'])
			end		
	end
	for i ,__  in pairs(Requirement['Common']) do
			if __['Type'] == itemType then
				local IconData = queryData(__['Name'])
				local Offset = Vector2.new(IconData['Value'][3], IconData['Value'][4])
				local Size = Vector2.new(IconData['Value'][1], IconData['Value'][2])
            	CreateItem('Material', __['Name'], IconData['Name'], Size, Offset, getBackgroundColor(__['Rarity']), true, "x" .. __['Count'])
			end		
	end
	ItemRange = ItemMax
end
SortItemMaterial('Material')
local MaleeY = 0.0922693312; 
function CreateItemMalee(ImageId)
    local ImageLabel = Instance.new("ImageLabel")

    ImageLabel.Parent = CreateItemScreen
    ImageLabel.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
    ImageLabel.BackgroundTransparency = 1.000
    ImageLabel.BorderColor3 = Color3.fromRGB(27, 42, 53)
    ImageLabel.BorderSizePixel = 0
    ImageLabel.Position = UDim2.new(0.915300548, 0, MaleeY, 0)
    ImageLabel.Size = UDim2.new(0, 100, 0, 100)
    ImageLabel.Image = ImageId
    MaleeY = MaleeY + OffsetYToSacle(102)
end
RequestGodhuman = game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyGodhuman", true)
if RequestGodhuman == 1 then 
    table.insert(MaleeList, "http://www.roblox.com/asset/?id=10338473987")
end
RquestSuperhuman = game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuySuperhuman", true)

if RquestSuperhuman == 1 then 
    table.insert(MaleeList, "http://www.roblox.com/asset/?id=4831781711")
end
RequestSharkMan = game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuySharkmanKarate", true)

if RequestSharkMan == 1 then 
    table.insert(MaleeList, "http://www.roblox.com/asset/?id=6525157144")
end


RequestDeathStep = game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyDeathStep", true)

if RequestDeathStep == 1 then 
    table.insert(MaleeList, "http://www.roblox.com/asset/?id=6085350468")
end

RequestElectricClaw = game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyElectricClaw", true)

if RequestElectricClaw == 1 then 
    table.insert(MaleeList, "http://www.roblox.com/asset/?id=6866994470"
    )
end

RequestDragonTalon = game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyDragonTalon", true)

if RequestDragonTalon == 1 then 
table.insert(MaleeList, "http://www.roblox.com/asset/?id=7831677967")
end
for i, v in pairs(MaleeList) do 
    CreateItemMalee(v)
end
for i, v in pairs(AwakeningToggler:GetChildren()) do 
	if v:IsA('Frame') or v:IsA('TextLabel') then 
		v.Visible = false
	end
end

AwakeningToggler.Visible = true
wait(4 * math.random(0.5, 2.5))
local AwakeningTogglerMain = AwakeningToggler:Clone()
AwakeningTogglerMain.Name = HttpService:GenerateGUID()
AwakeningTogglerMain.Parent = CreateItemScreen
AwakeningTogglerMain.Position = UDim2.new(0.5, 0, 0.800000012, 2)
AwakeningTogglerMain.Size = UDim2.new(1, 0, 0.300000012, 0)
for i, v in pairs(AwakeningTogglerMain:GetDescendants()) do 
	v.Name = HttpService:GenerateGUID()
	if v:IsA('Frame') or v:IsA('TextLabel') then 
		v.Visible = true
	end
end
AwakeningToggler.Visible = false
for i, v in pairs(AwakeningToggler:GetChildren()) do 
	if v:IsA('Frame') or v:IsA('TextLabel') then 
		v.Visible = true
	end
end
