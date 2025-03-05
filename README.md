local Fluent = loadstring(game:HttpGet("https://github.com/dawid-scripts/Fluent/releases/latest/download/main.lua"))()
local SaveManager = loadstring(game:HttpGet("https://raw.githubusercontent.com/dawid-scripts/Fluent/master/Addons/SaveManager.lua"))()
local InterfaceManager = loadstring(game:HttpGet("https://raw.githubusercontent.com/dawid-scripts/Fluent/master/Addons/InterfaceManager.lua"))()

local Window = Fluent:CreateWindow({
	Title = "Data Test Auto Mission  | Last Update 2/27/25 | ".. Fluent.Version,
	SubTitle = "	|	By Snowman	|	",
	TabWidth = 100,
	Size = UDim2.fromOffset(600, 350),
    Acrylic = true,
    Theme = "Normal Theme",
    MinimizeKey = Enum.KeyCode.Equals
})

local Tabs = {
	MainTab = Window:AddTab({ Title = "Main", Icon = "scroll"}),
	Farm = Window:AddTab({ Title = "Farm", Icon = "bomb"}),
	Settings = Window:AddTab({ Title = "Settings", Icon = "settings" }),
}

Fluent:Notify({
    Title = "Kuy Kub Hub",
    Content = "Loading...",
    Duration = 5
})

local AllMissions = {
	"Crab",
	"Boar",
	"Freddy",
	"Gunner Captain",
	"Bucky",
	"Angry Bob",
	"Bruno",
	"Thug",
	"Bandit",
	"Cave Demon",
	"Gunslinger",
	"Thief",
	"Vokun",
	"buster"
}

local NotDoMission = {}

local MissionAliases = {
	["Freddy"] = {"Frued","Freyd","Fredde","Friedrich","Freddi","Fred","Freddy"},
	["Angry Bob"] = {"Angry Bobby","Angry Bobbi","Angry Bobb","Angry Bobber"}
}

Tabs.MainTab:AddToggle("Toggle", {
    Title = "Anti-AFK",
    Description = "Activates an Anti Afk for you, you will never be kicked for standing still for too long!",
    Default = false,
    Callback = function(state)
        if state then
            local vu = game:GetService("VirtualUser")
            game:GetService("Players").LocalPlayer.Idled:Connect(function()
                vu:Button2Down(Vector2.new(0,0), workspace.CurrentCamera.CFrame)
                wait(1)
                vu:Button2Up(Vector2.new(0,0), workspace.CurrentCamera.CFrame)
            end)

            Fluent:Notify({
                Title = "Anti-AFK Activated",
                Content = "Made by Plug 愛",
                Duration = 5
            })

        else
            Fluent:Notify({
                Title = "Anti-AFK Desactivated",
                Content = "Made by Plug 愛",
                Duration = 5
            })
        end
    end
})

local VirtualInputManager = game:GetService("VirtualInputManager")

local function GetAbsolutePosition(guiObject)
    if guiObject and guiObject:IsA("GuiObject") then
        local screenSize = game:GetService("Workspace").CurrentCamera.ViewportSize
        local absPos = Vector2.new(
            (guiObject.AbsolutePosition.X),
            (guiObject.AbsolutePosition.Y)
        )
        return absPos
    end
    return nil
end

local VirtualInputManager = game:GetService("VirtualInputManager")
local Camera = game:GetService("Workspace").CurrentCamera

local function GetButtonPosition(guiObject)
    if guiObject and guiObject:IsA("GuiObject") then
        local absPos = guiObject.AbsolutePosition
        local absSize = guiObject.AbsoluteSize
        return Vector2.new(absPos.X + absSize.X / 2, absPos.Y + absSize.Y / 2 + 70)
    end
    return nil
end

Tabs.MainTab:AddToggle("Toggle", {
    Title = "Auto Spawn",
    Description = "Automatically Respawn Your Character",
    Default = false,
    Callback = function(spawns)
        print("🔄 Auto Spawn Toggle:", spawns)
        _G.AutoSpawnCharacter = spawns
		if spawns then
            Fluent:Notify({
                Title = "Auto Spawn Activated",
                Content = "Auto respawn feature is now enabled.",
                Duration = 5
            })
        else
            Fluent:Notify({
                Title = "Auto Spawn Deactivated",
                Content = "Auto respawn feature has been disabled.",
                Duration = 5
            })
        end
        while _G.AutoSpawnCharacter do
            task.wait(1)

            pcall(function()
                local player = game.Players.LocalPlayer
                local playerGui = player:FindFirstChild("PlayerGui")

                if playerGui then
                    local loadGui = playerGui:FindFirstChild("Load")
                    if loadGui then
                        local loadFrame = loadGui:FindFirstChild("Frame")
                        if loadFrame then
                            local loadButton = loadFrame:FindFirstChild("Load")

                            while _G.AutoSpawnCharacter 
                                and loadFrame 
                                and loadFrame.Visible 
                                and loadButton 
                                and loadButton:IsA("TextButton") 
                                and loadButton.Visible do
								
								task.wait(1)
									Fluent:Notify({
                						Title = "Spawn In 5",
                						Content = "Before Auto Spawn",
                						Duration = 3
            						})
								task.wait(1)
									Fluent:Notify({
                						Title = "Spawn In 4",
                						Content = "Before Auto Spawn",
                						Duration = 3
            						})
								task.wait(1)
									Fluent:Notify({
                						Title = "Spawn In 3",
                						Content = "Before Auto Spawn",
                						Duration = 3
            						})
								task.wait(1)
									Fluent:Notify({
                						Title = "Spawn In 2",
                						Content = "Before Auto Spawn",
                						Duration = 3
            						})
								task.wait(1)
									Fluent:Notify({
                						Title = "Spawn In 1",
                						Content = "Before Auto Spawn",
                						Duration = 3
            						})
                                
                                local buttonPosition = GetButtonPosition(loadButton)
                                
                                if buttonPosition then

                                    VirtualInputManager:SendMouseButtonEvent(buttonPosition.X, buttonPosition.Y, 0, true, game, 0)
                                    task.wait(0.1)
                                    VirtualInputManager:SendMouseButtonEvent(buttonPosition.X, buttonPosition.Y, 0, false, game, 0)

                                    task.wait(0.5)
									Fluent:Notify({
                						Title = "Spawn Complete",
                						Content = "Auto spawn made by  | Snowman and Chat gpt |",
                						Duration = 3
            						})
                                else
                                    break
                                end
                            end
                        end
                    end
                end
            end)
        end
    end
})

Tabs.MainTab:AddToggle("Toggle", {
    Title = "Auto Challenges",
    Description = "Automatically claim challenges for you!",
    Default = false,
    Callback = function(ACLL)
		_G.autoclaim = ACLL
	end    
})

spawn(function()
    while wait(0) do
        pcall(function()
            if _G.autoclaim then
local A_1 = "Claim"
local A_2 = "Daily1"
    local Event = game:GetService("Workspace").UserData["User_"..game.Players.LocalPlayer.UserId].ChallengesRemote
    Event:FireServer(A_1,A_2)
wait(.8)
local A_1 = "Claim"
local A_2 = "Daily2"
    local Event = game:GetService("Workspace").UserData["User_"..game.Players.LocalPlayer.UserId].ChallengesRemote
    Event:FireServer(A_1,A_2)
wait(.8)
local A_1 = "Claim"
local A_2 = "Daily3"
    local Event = game:GetService("Workspace").UserData["User_"..game.Players.LocalPlayer.UserId].ChallengesRemote
    Event:FireServer(A_1,A_2)
wait(.8)
local A_1 = "Claim"
local A_2 = "Daily4"
    local Event = game:GetService("Workspace").UserData["User_"..game.Players.LocalPlayer.UserId].ChallengesRemote
    Event:FireServer(A_1,A_2)
wait(.8)
            end
        end)
    end
end)

spawn(function()
    while wait(0) do
        pcall(function()
            if _G.autoclaim then
local A_1 = "Claim"
local A_2 = "Weekly1"
    local Event = game:GetService("Workspace").UserData["User_"..game.Players.LocalPlayer.UserId].ChallengesRemote
    Event:FireServer(A_1,A_2)
wait(.8)
local A_1 = "Claim"
local A_2 = "Weekly2"
    local Event = game:GetService("Workspace").UserData["User_"..game.Players.LocalPlayer.UserId].ChallengesRemote
    Event:FireServer(A_1,A_2)
wait(.8)
local A_1 = "Claim"
local A_2 = "Weekly3"
    local Event = game:GetService("Workspace").UserData["User_"..game.Players.LocalPlayer.UserId].ChallengesRemote
    Event:FireServer(A_1,A_2)
wait(.8)
            end
        end)
    end
end)

spawn(function()
    while wait(0) do
        pcall(function()
            if _G.autoclaim then
local A_1 = "Claim"
local A_2 = "Monthly1"
    local Event = game:GetService("Workspace").UserData["User_"..game.Players.LocalPlayer.UserId].ChallengesRemote
    Event:FireServer(A_1,A_2)
wait(.8)
local A_1 = "Claim"
local A_2 = "Monthly2"
    local Event = game:GetService("Workspace").UserData["User_"..game.Players.LocalPlayer.UserId].ChallengesRemote
    Event:FireServer(A_1,A_2)
wait(.8)
            end
        end)
    end
end)

spawn(function()
    while wait(0) do
        pcall(function()
            if _G.autoclaim then
local A_1 = "Claim"
local A_2 = "Challenge1"
    local Event = game:GetService("Workspace").UserData["User_"..game.Players.LocalPlayer.UserId].ChallengesRemote
    Event:FireServer(A_1,A_2)
wait(.8)
local A_1 = "Claim"
local A_2 = "Challenge2"
    local Event = game:GetService("Workspace").UserData["User_"..game.Players.LocalPlayer.UserId].ChallengesRemote
    Event:FireServer(A_1,A_2)
wait(.8)
local A_1 = "Claim"
local A_2 = "Challenge3"
    local Event = game:GetService("Workspace").UserData["User_"..game.Players.LocalPlayer.UserId].ChallengesRemote
    Event:FireServer(A_1,A_2)
wait(.8)
local A_1 = "Claim"
local A_2 = "Challenge4"
    local Event = game:GetService("Workspace").UserData["User_"..game.Players.LocalPlayer.UserId].ChallengesRemote
    Event:FireServer(A_1,A_2)
wait(.8)
local A_1 = "Claim"
local A_2 = "Challenge5"
    local Event = game:GetService("Workspace").UserData["User_"..game.Players.LocalPlayer.UserId].ChallengesRemote
    Event:FireServer(A_1,A_2)
wait(.8)
local A_1 = "Claim"
local A_2 = "Challenge6"
    local Event = game:GetService("Workspace").UserData["User_"..game.Players.LocalPlayer.UserId].ChallengesRemote
    Event:FireServer(A_1,A_2)
wait(.8)
local A_1 = "Claim"
local A_2 = "Challenge7"
    local Event = game:GetService("Workspace").UserData["User_"..game.Players.LocalPlayer.UserId].ChallengesRemote
    Event:FireServer(A_1,A_2)
wait(.8)
local A_1 = "Claim"
local A_2 = "Challenge8"
    local Event = game:GetService("Workspace").UserData["User_"..game.Players.LocalPlayer.UserId].ChallengesRemote
    Event:FireServer(A_1,A_2)
wait(.8)
local A_1 = "Claim"
local A_2 = "Challenge9"
    local Event = game:GetService("Workspace").UserData["User_"..game.Players.LocalPlayer.UserId].ChallengesRemote
    Event:FireServer(A_1,A_2)
wait(.8)
local A_1 = "Claim"
local A_2 = "Challenge10"
    local Event = game:GetService("Workspace").UserData["User_"..game.Players.LocalPlayer.UserId].ChallengesRemote
    Event:FireServer(A_1,A_2)
wait(.8)
local A_1 = "Claim"
local A_2 = "Challenge11"
    local Event = game:GetService("Workspace").UserData["User_"..game.Players.LocalPlayer.UserId].ChallengesRemote
    Event:FireServer(A_1,A_2)
wait(.8)
local A_1 = "Claim"
local A_2 = "Challenge12"
    local Event = game:GetService("Workspace").UserData["User_"..game.Players.LocalPlayer.UserId].ChallengesRemote
    Event:FireServer(A_1,A_2)
wait(.8)
local A_1 = "Claim"
local A_2 = "Challenge13"
    local Event = game:GetService("Workspace").UserData["User_"..game.Players.LocalPlayer.UserId].ChallengesRemote
    Event:FireServer(A_1,A_2)
wait(.8)
local A_1 = "Claim"
local A_2 = "Challenge14"
    local Event = game:GetService("Workspace").UserData["User_"..game.Players.LocalPlayer.UserId].ChallengesRemote
    Event:FireServer(A_1,A_2)
wait(.8)
            end
        end)
    end
end)

local Section = Tabs.MainTab:AddSection("Auto Reroll Affinities")

local Toggle
local isRunning1 = false

Tabs.MainTab:AddToggle("Toggly",{
	Title = "Auto 2.0 Affinities	| Gems |",
	Description = "This will roll your gems affinities untill it all 2.0",
	Default = false,
	Callback = function(rollgems)
		isRunning1 = rollgems
		if isRunning1 then
			spawn(function()
				while isRunning1 do
					wait(8)
					local player = game.Players.LocalPlayer
					local playerId = player.UserId
					local userDataName = game.workspace.UserData["User_"..playerId]


					local AffMelee1 = userDataName.Data.DFT1Melee.Value
					local AffSniper1 = userDataName.Data.DFT1Sniper.Value
					local AffDefense1 = userDataName.Data.DFT1Defense.Value
					local AffSword1 = userDataName.Data.DFT1Sword.Value

					local AffMelee2 = userDataName.Data.DFT2Melee.Value
					local AffSniper2 = userDataName.Data.DFT2Sniper.Value
					local AffDefense2 = userDataName.Data.DFT2Defense.Value
					local AffSword2 = userDataName.Data.DFT2Sword.Value

					if AffSniper1 == 2 and AffSword1 == 2 and AffMelee1 == 2 and AffDefense1 == 2 then
						script.Parent:Destroy()
					end

					if AffSniper2 == 2 and AffSWord2 == 2 and AffMelee2 == 2 and AffDefense2 == 2 then
						script.Parent:Destroy()
					end

					local args1 = {
						[1] = "DFT1",
						[2] = false, --defense
						[3] = false, --melee
						[4] = false, --sniper
						[5] = false, --sword
						[6] = "Gems"
					}

					local args2 = {
						[1] = "DFT2",
						[2] = false, --defense
						[3] = false, --melee
						[4] = false, --sniper
						[5] = false, --sword
						[6] = "Gems"
					}

					if AffDefense1 == 2 then
						args1[2] = 0/0
					end

					if AffMelee1 == 2 then
						args1[3] = 0/0
					end

					if AffSniper1 == 2 then
						args1[4] = 0/0
					end

					if AffSword1 == 2 then
						args1[5] = 0/0
					end

					if AffDefense2 == 2 then
						args2[2] = 0/0
					end

					if AffMelee2 == 2 then
						args2[3] = 0/0
					end

					if AffSniper2 == 2 then
						args2[4] = 0/0
					end

					if AffSword2 == 2 then
						args2[5] = 0/0
					end

					workspace:WaitForChild("Merchants"):WaitForChild("AffinityMerchant"):WaitForChild("Clickable"):WaitForChild("Retum"):FireServer(unpack(args1))
					workspace:WaitForChild("Merchants"):WaitForChild("AffinityMerchant"):WaitForChild("Clickable"):WaitForChild("Retum"):FireServer(unpack(args2))
				end
			end)
		end
	end
})

local ToggleBeri
local isRunning2 = false

Tabs.MainTab:AddToggle("Toggle", {
    Title = "Auto 2.0 Affinities | Beri |",
    Description = "This will roll your beri affinity until it is all 2.0!",
    Default = false,
    Callback = function(Value)
        isRunning2 = Value
        if isRunning2 then
            spawn(function()
                while isRunning2 do
                    wait(8)
                    local player = game.Players.LocalPlayer
                    local playerId = player.UserId
                    local userDataName = game.Workspace.UserData["User_" .. playerId]

                    local AffMelee1 = userDataName.Data.DFT1Melee.Value
                    local AffSniper1 = userDataName.Data.DFT1Sniper.Value
                    local AffDefense1 = userDataName.Data.DFT1Defense.Value
                    local AffSword1 = userDataName.Data.DFT1Sword.Value

                    -- DFT2 Variables
                    local AffMelee2 = userDataName.Data.DFT2Melee.Value
                    local AffSniper2 = userDataName.Data.DFT2Sniper.Value
                    local AffDefense2 = userDataName.Data.DFT2Defense.Value
                    local AffSword2 = userDataName.Data.DFT2Sword.Value

                    if AffSniper1 == 2 and AffSword1 == 2 and AffMelee1 == 2 and AffDefense1 == 2 then
                        script.Parent:Destroy()
                    end

                    if AffSniper2 == 2 and AffSword2 == 2 and AffMelee2 == 2 and AffDefense2 == 2 then
                        script.Parent:Destroy()
                    end

                    local args1 = {
                        [1] = "DFT1",
                        [2] = false, -- defense
                        [3] = false, -- melee
                        [4] = false, -- sniper
                        [5] = false, -- sword
                        [6] = "Cash"
                    }

                    local args2 = {
                        [1] = "DFT2",
                        [2] = false, -- defense
                        [3] = false, -- melee
                        [4] = false, -- sniper
                        [5] = false, -- sword
                        [6] = "Cash"
                    }

                    if AffDefense1 == 2 then
                        args1[2] = 0 / 0
                    end

                    if AffMelee1 == 2 then
                        args1[3] = 0 / 0
                    end

                    if AffSniper1 == 2 then
                        args1[4] = 0 / 0
                    end

                    if AffSword1 == 2 then
                        args1[5] = 0 / 0
                    end

                    if AffDefense2 == 2 then
                        args2[2] = 0 / 0
                    end

                    if AffMelee2 == 2 then
                        args2[3] = 0 / 0
                    end

                    if AffSniper2 == 2 then
                        args2[4] = 0 / 0
                    end

                    if AffSword2 == 2 then
                        args2[5] = 0 / 0
                    end

                    workspace:WaitForChild("Merchants"):WaitForChild("AffinityMerchant"):WaitForChild("Clickable"):WaitForChild("Retum"):FireServer(unpack(args1))
                    workspace:WaitForChild("Merchants"):WaitForChild("AffinityMerchant"):WaitForChild("Clickable"):WaitForChild("Retum"):FireServer(unpack(args2))
                end
            end)
        end
    end,
})

local Section = Tabs.Farm:AddSection("Auto Do Mission")

Tabs.Farm:AddToggle("Toggle",{
	Title = "Auto Claim Mission",
	Description = "Automatically Claim Your Mission",
	Default = false,
	Callback = function(AMS)
		AutoMission = AMS
	end
})

spawn(function()
	while task.wait(1) do
		if AutoMission then
			pcall(function()
				workspace.Merchants.ExpertiseMerchant.Clickable.Retum:FireServer()
			end)
		end
	end
end)

local MultiDropdown = Tabs.Farm:AddDropdown("MultiDropdown", {
    Title = "Do Not This Mission",
    Description = "Select missions to disable",
    Values = AllMissions,
    Multi = true,
    Default = {},
    Callback = function(selectedMissions)
        NotDoMission = {}
        for _, mission in pairs(selectedMissions) do
            NotDoMission[mission] = true
        end
    end
})

function IsMissionDisabled(mission)
	for disabledMission, _ in pairs(NotDoMission) do
        if string.match(mission, disabledMission) then
            return true
        end
    end
    for missionName, aliasList in pairs(MissionAliases) do
		if NotDoMission[missionName] then
			for _, alias in ipairs(aliasList) do
				if string.match(mission, alias) and NotDoMission[missionName] then
					return true
				end
			end
		end
	end
    return false
end

Tabs.Farm:AddToggle("Toggle",{
	Title = "Auto Mission",
	Description = "Automatically Do Your Mission",
	Default = false,
	Callback = function(ADAM)
		AutoDoAllMission = ADAM
		if ADAM then
			CheckAndStartMission()
		end
	end
})

function CheckAndStartMission()
	local playerData = game:GetService("Workspace").UserData["User_"..game.Players.LocalPlayer.UserId].Data
	local missionType = playerData.MissionObjective.Value
	local currentMission = playerData.MissionObjectiveTarget.Value

	if missionType ~= "None" and not IsMissionDisabled(currentMission) then
		AutoDoAllMission = true
		MissionInProgress = missionType
	else
		AutoDoAllMission = false
		MissionInProgress = "None"
	end
end

spawn(function()
	while true do  
		local currentTime = os.date("*t")
		if currentTime.min == 1 and currentTime.sec == 0 then
			print("🔄 รีเฟรช Mission ณ เวลา", os.date("%X"))
			CheckAndStartMission()
		end
		wait(1)
	end
end)

function ActivateHaki(state)
    pcall(function()
        if state then
            game.workspace.UserData["User_" .. game.Players.LocalPlayer.UserId].UpdateHaki:FireServer()
        else
            game.workspace.UserData["User_" .. game.Players.LocalPlayer.UserId].UpdateHaki:FireServer()
        end
    end)
end

local DamageMission = false
local KillMission = false
local QuestsMission = false
local EliteKillMission = false

spawn(function()
	while task.wait(1) do
		pcall(function()
		local playerData = game:GetService("Workspace").UserData["User_"..game.Players.LocalPlayer.UserId].Data
		local missionType = playerData.MissionObjective.Value
		local currentMission = playerData.MissionObjectiveTarget.Value
			if missionType == "None" then
                MissionInProgress = "None"
                AutoDoAllMission = false
            elseif missionType == "Kill" then
                MissionInProgress = "Kill"
                KillMission = true
                DamageMission = false
                QuestsMission = false
                EliteKillMission = false
            elseif missionType == "Damage" or missionType == "Money" then
                MissionInProgress = "DamageAndMoney"
                DamageMission = AutoDoAllMission
                KillMission = false
                DamageMission = true
                QuestsMission = false
                EliteKillMission = false
            elseif missionType == "Quests" then
                MissionInProgress = "Quests"
                QuestsMission = false
                KillMission = false
                DamageMission = false
                QuestsMission = true
                EliteKillMission = false
            elseif missionType == "Elite Kill" then
                MissionInProgress = "Kill"
                KillMission = false
                DamageMission = false
                QuestsMission = false
                EliteKillMission = true
            end
			if DamageMission then
				if DamageMission and MissionInProgress == "DamageAndMoney" then
					wait(0.5)
					ActivateHaki(true)
                	for _, v in pairs(game.Workspace.Enemies:GetChildren()) do
                    	if (string.find(v.Name, " Boar") or string.find(v.Name, "Crab") or 
                        	string.find(v.Name, "Angry") or string.find(v.Name, "Bandit") or 
                        	string.find(v.Name, "Thief") or string.find(v.Name, "Vokun") or 
                        	string.find(v.Name, "Buster") or string.find(v.Name, "Freddy") or 
                        	string.find(v.Name, "Bruno") or string.find(v.Name, "Thug") or 
                        	string.find(v.Name, "Gunslinger") or string.find(v.Name, "Gunner") or 
                        	string.find(v.Name, "Cave") or string.find(v.Name, "Bucky")) and v:FindFirstChild("HumanoidRootPart") then
                        	v.HumanoidRootPart.CanCollide = false
                        	v.HumanoidRootPart.Size = Vector3.new(10, 10, 10)
                        	v.HumanoidRootPart.Anchored = true
                        	v.HumanoidRootPart.CFrame = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame * CFrame.new(0, 4, -15)
                        	if v.Humanoid.Health == 0 then
                            	v.HumanoidRootPart.Size = Vector3.new(0, 0, 0)
                            	v:Destroy()
                        	end
                    	end
                	end
				end
			end
			if (KillMission or EliteKillMission) and MissionInProgress == "Kill" then
				if IsMissionDisabled(currentMission) then
					Fluent:Notify({
						Title = "Mission Cancelled",
						Content = "Canceled kill name : "..currentMission,
						Duration = 5 
					})
				else
					wait(0.5)
					ActivateHaki(true)
					for _, v in pairs(game.Workspace.Enemies:GetChildren()) do
						if v:FindFirstChild("HumanoidRootPart") and v.Name:match(currentMission) then 
							v.HumanoidRootPart.CanCollide = false
							v.HumanoidRootPart.Size = Vector3.new(10, 10, 10)
							v.HumanoidRootPart.Anchored = true
							v.HumanoidRootPart.CFrame = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame * CFrame.new(0, 4, -15)
							if v.Humanoid.Health == 0 then
								v.HumanoidRootPart.Size = Vector3.new(0, 0, 0)
								v:Destroy()
							end
						end
					end
					ActivateHaki(false)
				end
			end
		end)
	end
end)

local ActiveMission = false

spawn(function()
	while task.wait(1) do
		pcall(function()
			local Plr = game.Players.LocalPlayer
			local toolname = "Cannon Ball"
			if (KillMission or DamageMission or EliteKillMission) and MissionInProgress ~="None" then
				ActiveMission = true
				if Plr.Backpack:FindFirstChild(toolname) and not Plr.Character:FindFirstChild(toolname) and not Plr.Character:FindFirstChildOfClass("Tool") then
					Plr.Character.Humanoid:EquipTool(Plr.Backpack:FindFirstChild(toolname))
				end
				local cannon = Plr.Character:FindFirstChild(toolname)
				if cannon then
					local args = {
						[1] = CFrame.new(Vector3.new(Plr.Character.HumanoidRootPart.Position))
					}
					cannon.RemoteEvent:FireServer(unpack(args))
				end
			else
				ActiveMission = false
				return
			end
		end)
	end
end)

spawn(function()
	while task.wait(1) do
		pcall(function()
			if (KillMission or DamageMission or EliteKillMission) and MissionInProgress ~="None" then
				ActiveMission = true
				for _, v in pairs(game.workspace.ResourceHolder["Resources_" .. game.Players.LocalPlayer.UserId]:GetChildren()) do
					if v.Name == "CannonBall" then
						v.CFrame = game.Players.LocalPlayer.Character.Head.CFrame * CFrame.new(0, 2, -15)
						v.CanCollide = false
						if not v:FindFirstChild("BodyClip") then
							local Noclip = Instance.new("BodyVelocity")
							Noclip.Name = "BodyClip"
							Noclip.Parent = v
							Noclip.MaxForce = Vector3.new(100000,100000,100000)
							Noclip.Velocity = Vector3.new(0,20,0)
						end
					end
				end
			else
				ActiveMission = false
				return
			end
		end)
	end
end)

local hasTeleported = false

spawn(function()
	while task.wait(1) do
		pcall(function()
			if QuestsMission and MissionInProgress == "Quests" then
				workspace:WaitForChild("Merchants")
					:WaitForChild("QuestFishMerchant")
					:WaitForChild("Clickable")
					:WaitForChild("Retum")
					:FireServer()
				wait(2)
				hasTeleported = false
			end
		end)
	end
end)
function StartMissionLoop()
    spawn(function()
        while task.wait(1) do
            pcall(function()
                if QuestsMission and MissionInProgress == "Quests" then
                    local player = game.Players.LocalPlayer
                    local character = player.Character
                    local backpack = player.Backpack
                    if backpack:FindFirstChild("Package") and not character:FindFirstChild("Package") then
                        backpack:FindFirstChild("Package").Parent = character
                        character.Humanoid.Sit = true
                    elseif character:FindFirstChild("Package") and QuestsMission then
                        for _, v in pairs(game.Workspace.Merchants:GetChildren()) do
                            if v:FindFirstChild("HumanoidRootPart") then
                                local merchantName = v.Name
                                if string.find(merchantName, "Aff") or string.find(merchantName, "Heavy") or string.find(merchantName, "Drink") 
                                or string.find(merchantName, "Boat") or string.find(merchantName, "Emote") or string.find(merchantName, "Exp") 
                                or string.find(merchantName, "Fish") or string.find(merchantName, "Flail") or string.find(merchantName, "Krizma") 
                                or string.find(merchantName, "QuestFish") or string.find(merchantName, "QuestMe") or string.find(merchantName, "Friend") 
                                or string.find(merchantName, "Sniper") or string.find(merchantName, "Sword") then
                                    character.HumanoidRootPart.CFrame = v.HumanoidRootPart.CFrame + Vector3.new(1, 0, 0)
                                    wait(0.3)
                                end
                            end
                        end
                        character.Package:Activate()
                    elseif not backpack:FindFirstChild("Package") and not character:FindFirstChild("Compass") then
                        if not hasTeleported then
                            character.HumanoidRootPart.CFrame = CFrame.new(118.400009, 305, 4946.99951)
                            character.Humanoid.Sit = false
                            hasTeleported = true
                        end
                    end
                end
            end)
        end
    end)
end

StartMissionLoop()

SaveManager:SetLibrary(Fluent)
InterfaceManager:SetLibrary(Fluent)
SaveManager:IgnoreThemeSettings()
SaveManager:SetIgnoreIndexes({})

InterfaceManager:SetFolder("AscendedScriptHub")
SaveManager:SetFolder("AscendedScriptHub/OPL")

InterfaceManager:BuildInterfaceSection(Tabs.Settings)
SaveManager:BuildConfigSection(Tabs.Settings)


Window:SelectTab(1)

Fluent:Notify({
    Title = "Ascended Hub",
    Content = "The script has been loaded.",
    Duration = 8
})

-- You can use the SaveManager:LoadAutoloadConfig() to load a config
-- which has been marked to be one that auto loads!
SaveManager:LoadAutoloadConfig()
Fluent:SetTheme("Normal Theme")
setfflag("TaskSchedulerTargetFps", "1000")
setfpscap(60)
while task.wait(0) do
    if game:GetService("Workspace").DistributedGameTime % 1 * 60 > 30 then
    	if getfpscap() ~= 60 then
        	setfpscap(60)
    	end
	end
end
