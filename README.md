--Criminality

local Fluent = loadstring(game:HttpGet("https://github.com/dawid-scripts/Fluent/releases/latest/download/main.lua"))()
local SaveManager = loadstring(game:HttpGet("https://raw.githubusercontent.com/dawid-scripts/Fluent/master/Addons/SaveManager.lua"))()
local InterfaceManager = loadstring(game:HttpGet("https://raw.githubusercontent.com/dawid-scripts/Fluent/master/Addons/InterfaceManager.lua"))()

local Window = Fluent:CreateWindow({
    Title = "Criminality " .. Fluent.Version,
    SubTitle = "by TheMeetly",
    TabWidth = 160,
    Size = UDim2.fromOffset(580, 460),
    Acrylic = true, -- The blur may be detectable, setting this to false disables blur entirely
    Theme = "Rose",
    MinimizeKey = Enum.KeyCode.LeftAlt-- Used when theres no MinimizeKeybind
})

--Fluent provides Lucide Icons https://lucide.dev/icons/ for the tabs, icons are optional
local Tabs = {
    Main = Window:AddTab({ Title = "Main", Icon = "" }),
    Settings = Window:AddTab({ Title = "Settings", Icon = "settings" })
}

local Options = Fluent.Options

do
    Fluent:Notify({
        Title = "CRIMINALITY",
        Content = "Script By Meetly",
        SubContent = "Ezz", -- Optional
        Duration = 5 -- Set to nil to make the notification not disappear
    })


    Tabs.Main:AddButton({
        Title = "AimBot",
        Description = "AimBot Criminality",
        Callback = function()
			loadstring(game:HttpGet('https://raw.githubusercontent.com/Mick-gordon/Hyper-Escape/main/DeleteMobCheatEngine.lua'))()
        end
    })

	Tabs.Main:AddButton({
        Title = "ESP",
        Description = "Esp",
        Callback = function(esp)
			loadstring(game:HttpGet('https://raw.githubusercontent.com/Lucasfin000/SpaceHub/main/UESP'))()
        end
    })

    local Toggle = Tabs.Main:AddToggle("Chams", {Title = "Chams", Default = false })

    Toggle:OnChanged(function(Value)
        _G.highlightEnabled = Value
    end)


    _G.highlightEnabled = false

    local function getRoleColor(plr)
        if (plr.Backpack:FindFirstChild("Knife") or plr.Character:FindFirstChild("Knife")) then
            return Color3.new(1, 0, 0)
        elseif (plr.Backpack:FindFirstChild("Gun") or plr.Character:FindFirstChild("Gun")) then
            return Color3.new(0, 0, 1)
        else
            return Color3.new(186,85,211)
        end
    end
    
    local function handleHighlight()
        while true do
            if _G.highlightEnabled then
                for _, v in pairs(game.Players:GetChildren()) do
                    if v ~= game.Players.LocalPlayer and v.Character then
                        if not v.Character:FindFirstChild("Highlight") then
                            local highlight = Instance.new("Highlight", v.Character)
                            highlight.FillTransparency = 0.5
                            highlight.OutlineTransparency = 0.5
                            highlight.FillColor = getRoleColor(v)
                        else
                            v.Character.Highlight.FillColor = getRoleColor(v)
                        end
                    end
                end
            else
                for _, v in pairs(game.Players:GetChildren()) do
                    if v ~= game.Players.LocalPlayer and v.Character and v.Character:FindFirstChild("Highlight") then
                        v.Character.Highlight:Destroy()
                    end
                end
            end
            wait(0.1)
        end
    end
    
    spawn(handleHighlight)

	local Camera = game.Workspace.CurrentCamera

	local Slider = Tabs.Main:AddSlider("Slider", {
		Title = "FOV changer",
		Description = "FOV",
		Default = 60,
		Min = 60,
		Max = 120,
		Rounding = 1,
		Callback = function(Value)
			Camera.FieldOfView = Value
		end
	})

    Tabs.Main:AddButton({
        Title = "Glide Fly",
        Description = "Flight Bind: B - Fly/Speed; U - Only Speed",
        Callback = function(esp)
			togglekey = "b"  -- fly toggle
upkey = "="      -- makes speed faster
downkey = "-"    -- makes speed slower
enablepart = "u" -- enables part fly
speed = -0.5     -- changes set speed
updown = false   -- true if you want to go up
notify = true    -- true if you want notifcations
flypart = true   -- true for part fly
local user = game:GetService("UserInputService")
local player = game:GetService("Players").LocalPlayer
local GuiService = game:GetService("StarterGui")
local mouse = game.Players.LocalPlayer:GetMouse()
local holdingWKey = false
local holdingSKey = false
local holdingAKey = false
local holdingDKey = false
local holdingSpaceKey = false
local holdingShiftKey = false
local check = false
GuiService:SetCore("SendNotification", {Title = "Speed", Text = "Script made by Zurewrath";})
mouse.KeyDown:connect(function(key)
   if key == enablepart then
       if flypart then
           flypart = false
           if notify then
               GuiService:SetCore("SendNotification", {Title = "Speed", Text = "Disabled part fly";})
           end
       else
           flypart = true
           if notify then
               GuiService:SetCore("SendNotification", {Title = "Speed", Text = "Enabled part fly";})
           end
       end
   end
end)
mouse.KeyDown:connect(function(key)
   if key == upkey then
       speed = speed + -0.1
       if notify then
           GuiService:SetCore("SendNotification", {Title = "Speed", Text = "Speed is now set to " .. speed;})
       end
   end
end)
mouse.KeyDown:connect(function(key)
   if key == downkey then
       speed = speed - -0.1
       if notify then
           GuiService:SetCore("SendNotification", {Title = "Speed", Text = "Speed is now set to " .. speed;})
       end
   end
end)
mouse.KeyDown:connect(function(key)
   if key == togglekey then
       if check  == true then
           check = false
           if notify then
               GuiService:SetCore("SendNotification", {Title = "Speed", Text = "Speed is now disabled";})
           end
           game.Workspace.fly:Destroy()
       else
           check = true
           if notify then
               GuiService:SetCore("SendNotification", {Title = "Speed", Text = "Speed is now enabled";})
           end
           if flypart then
               local brick = Instance.new("Part", workspace)
               brick.Size = Vector3.new(8, 2, 8)
               brick.CFrame = game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.CFrame + Vector3.new(0, -4, 0)
               brick.Transparency = 1 brick.Anchored = true brick.Name = "fly"
               game:GetService('RunService').Stepped:connect(function()
                   brick.CFrame = game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.CFrame + Vector3.new(0, -4, 0)
                   brick.Size = Vector3.new(8+-speed, 2, 8+-speed)
               end)
           end
       end
   end
end)
game:GetService('RunService').Stepped:connect(function()
   if check then
       if holdingWKey == true then
         game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame * CFrame.new(0,0,speed)
       end
       if holdingSKey == true then
        game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame * CFrame.new(0,0,-speed)
   end
       if holdingAKey == true then
   game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame * CFrame.new(speed,0,0)
   end
       if holdingDKey == true then
   game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame * CFrame.new(-speed,0,0)
       end
       if holdingShiftKey == true then
           game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame * CFrame.new(0,speed,0)
       end
       if updown then
           if holdingSpaceKey == true then
               game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame * CFrame.new(0,-speed,0)
           end
       end
   end
end)
user.InputBegan:Connect(function(inputObject)
   if (inputObject.KeyCode == Enum.KeyCode.W) then
       holdingWKey = true
   end
   if (inputObject.KeyCode == Enum.KeyCode.S) then
       holdingSKey = true
   end
   if (inputObject.KeyCode == Enum.KeyCode.A) then
       holdingAKey = true
   end
   if (inputObject.KeyCode == Enum.KeyCode.D) then
       holdingDKey = true
   end
   if (inputObject.KeyCode == Enum.KeyCode.LeftControl) then
       holdingShiftKey = true
   end
   if (inputObject.KeyCode == Enum.KeyCode.Space) then
       holdingSpaceKey = true
   end
end)
user.InputEnded:Connect(function(inputObject)
   if (inputObject.KeyCode == Enum.KeyCode.W) then
       holdingWKey = false
   end
   if( inputObject.KeyCode == Enum.KeyCode.S) then
       holdingSKey = false
   end
   if (inputObject.KeyCode == Enum.KeyCode.A) then
       holdingAKey = false
   end
   if (inputObject.KeyCode == Enum.KeyCode.D) then
       holdingDKey = false
   end
   if (inputObject.KeyCode == Enum.KeyCode.LeftControl) then
       holdingShiftKey = false
   end
   if (inputObject.KeyCode == Enum.KeyCode.Space) then
       holdingSpaceKey = false
   end
end)
        end
    })

    Tabs.Main:AddButton({
        Title = "Jump-Boost",
        Description = "Gravity",
        Callback = function()
			game.workspace.Gravity = 70
        end
    })

-- Addons:
-- SaveManager (Allows you to have a configuration system)
-- InterfaceManager (Allows you to have a interface managment system)

-- Hand the library over to our managers
SaveManager:SetLibrary(Fluent)
InterfaceManager:SetLibrary(Fluent)

-- Ignore keys that are used by ThemeManager.
-- (we dont want configs to save themes, do we?)
SaveManager:IgnoreThemeSettings()

-- You can add indexes of elements the save manager should ignore
SaveManager:SetIgnoreIndexes({})

-- use case for doing it this way:
-- a script hub could have themes in a global folder
-- and game configs in a separate folder per game
InterfaceManager:SetFolder("FluentScriptHub")
SaveManager:SetFolder("FluentScriptHub/specific-game")

InterfaceManager:BuildInterfaceSection(Tabs.Settings)
SaveManager:BuildConfigSection(Tabs.Settings)


Window:SelectTab(1)

Fluent:Notify({
    Title = "Fluent",
    Content = "The script has been loaded.",
    Duration = 8
})

-- You can use the SaveManager:LoadAutoloadConfig() to load a config
-- which has been marked to be one that auto loads!
SaveManager:LoadAutoloadConfig()
end
