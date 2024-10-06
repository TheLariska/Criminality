--criminality

local Fluent = loadstring(game:HttpGet("https://github.com/dawid-scripts/Fluent/releases/latest/download/main.lua"))()
local SaveManager = loadstring(game:HttpGet("https://raw.githubusercontent.com/dawid-scripts/Fluent/master/Addons/SaveManager.lua"))()
local InterfaceManager = loadstring(game:HttpGet("https://raw.githubusercontent.com/dawid-scripts/Fluent/master/Addons/InterfaceManager.lua"))()

local Window = Fluent:CreateWindow({
    Title = "Criminality Scripts " .. Fluent.Version,
    SubTitle = "by TheMeetly [CRIMINALITY]",
    TabWidth = 160,
    Size = UDim2.fromOffset(580, 460),
    Acrylic = true, -- The blur may be detectable, setting this to false disables blur entirely
    Theme = "Rose",
    MinimizeKey = Enum.KeyCode.LeftAlt-- Used when theres no MinimizeKeybind
})

--Fluent provides Lucide Icons https://lucide.dev/icons/ for the tabs, icons are optional
local Tabs = {
    Main = Window:AddTab({ Title = "Main", Icon = "" }),
    Visual = Window:AddTab({ Title = "Visual", Icon = "" }),
    Updates = Window:AddTab({ Title = "Updates", Icon = "" }),
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
        Title = "AimBot UI",
        Description = "AimBot Criminality",
        Callback = function()
			loadstring(game:HttpGet('https://raw.githubusercontent.com/Mick-gordon/Hyper-Escape/main/DeleteMobCheatEngine.lua'))()
        end
    })

	Tabs.Visual:AddButton({
        Title = "ESP",
        Description = "Esp",
        Callback = function(esp)
			loadstring(game:HttpGet('https://raw.githubusercontent.com/Lucasfin000/SpaceHub/main/UESP'))()
        end
    })

    local Toggle = Tabs.Visual:AddToggle("Chams", {Title = "Chams", Default = false })

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
    local RunService = game:GetService("RunService")
    
    local Slider = Tabs.Visual:AddSlider("Slider", {
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
    
    
    RunService.RenderStepped:Connect(function()
        
        if Camera.FieldOfView ~= Slider.Value then
            Camera.FieldOfView = Slider.Value
        end
    end)

    Tabs.Visual:AddButton({
        Title = "FullBright",
        Description = "FullBright",
        Callback = function(esp)
			pcall(function()
                local lighting = game:GetService("Lighting");
                lighting.Ambient = Color3.fromRGB(255, 255, 255);
                lighting.Brightness = 1;
                lighting.FogEnd = 1e10;
                for i, v in pairs(lighting:GetDescendants()) do
                    if v:IsA("BloomEffect") or v:IsA("BlurEffect") or v:IsA("ColorCorrectionEffect") or v:IsA("SunRaysEffect") then
                        v.Enabled = false;
                    end;
                end;
                lighting.Changed:Connect(function()
                    lighting.Ambient = Color3.fromRGB(255, 255, 255);
                    lighting.Brightness = 1;
                    lighting.FogEnd = 1e10;
                end);
                spawn(function()
                    local character = game:GetService("Players").LocalPlayer.Character;
                    while wait() do
                        repeat wait() until character ~= nil;
                        if not character.HumanoidRootPart:FindFirstChildWhichIsA("PointLight") then
                            local headlight = Instance.new("PointLight", character.HumanoidRootPart);
                            headlight.Brightness = 1;
                            headlight.Range = 60;
                        end;
                    end;
                end);
            end)
        end
    })

    Tabs.Visual:AddButton({
        Title = "Show Chat",
        Description = "Show Chat",
        Callback = function()
		-- // Services
local Players = game:GetService("Players")

-- // Vars
local ChatFrame = Players.LocalPlayer.PlayerGui.Chat.Frame

-- //
ChatFrame.ChatChannelParentFrame.Visible = true
ChatFrame.ChatBarParentFrame.Position = UDim2.new(0, 0, 1, -42)	
        end
    })

    Tabs.Visual:AddButton({
        Title = "KeyStrokes",
        Description = "KeyStrokes",
        Callback = function(esp)
			getgenv().k1 = "W"
getgenv().k2 = "A"
getgenv().k3 =  "S"
getgenv().k4 = "D"

getgenv().backdrop = false -- only if you want the shadow bg.
getgenv().showms = true -- only if you want to have your ms shown.
getgenv().showfps = true -- only if you want to have your fps shown.
getgenv().showkps = true -- only if you want to have your kps shown.
getgenv().animated = true -- only if you want the GUI to have the animated shadow.
getgenv().showarrows = false -- only if you want arrow keys to be shown.
getgenv().keydrag = false -- only if you want the keys to be draggable, can also be buggy, will be worked on in the future.

loadstring(game:HttpGet("https://raw.githubusercontent.com/Zirmith/Util-Tools/main/keyStrokes.lua"))()

        end
    })

    Tabs.Visual:AddButton({
        Title = "Free-cam",
        Description = "toggel shift + p",
        Callback = function()
			function sandbox(var,func)
                local env = getfenv(func)
                local newenv = setmetatable({},{
                __index = function(self,k)
                if k=="script" then
                return var
                else
                return env[k]
                end
                end,
                })
                setfenv(func,newenv)
                return func
                end
                cors = {}
                mas = Instance.new("Model",game:GetService("Lighting"))
                LocalScript0 = Instance.new("LocalScript")
                LocalScript0.Name = "FreeCamera"
                LocalScript0.Parent = mas
                table.insert(cors,sandbox(LocalScript0,function()
                
                local pi    = math.pi
                local abs   = math.abs
                local clamp = math.clamp
                local exp   = math.exp
                local rad   = math.rad
                local sign  = math.sign
                local sqrt  = math.sqrt
                local tan   = math.tan
                
                local ContextActionService = game:GetService("ContextActionService")
                local Players = game:GetService("Players")
                local RunService = game:GetService("RunService")
                local StarterGui = game:GetService("StarterGui")
                local UserInputService = game:GetService("UserInputService")
                
                local LocalPlayer = Players.LocalPlayer
                if not LocalPlayer then
                Players:GetPropertyChangedSignal("LocalPlayer"):Wait()
                LocalPlayer = Players.LocalPlayer
                end
                
                local Camera = workspace.CurrentCamera
                workspace:GetPropertyChangedSignal("CurrentCamera"):Connect(function()
                local newCamera = workspace.CurrentCamera
                if newCamera then
                Camera = newCamera
                end
                end)
                
                ------------------------------------------------------------------------
                
                local TOGGLE_INPUT_PRIORITY = Enum.ContextActionPriority.Low.Value
                local INPUT_PRIORITY = Enum.ContextActionPriority.High.Value
                local FREECAM_MACRO_KB = {Enum.KeyCode.LeftShift, Enum.KeyCode.P}
                
                local NAV_GAIN = Vector3.new(1, 1, 1)*64
                local PAN_GAIN = Vector2.new(0.75, 1)*8
                local FOV_GAIN = 300
                
                local PITCH_LIMIT = rad(90)
                
                local VEL_STIFFNESS = 1.5
                local PAN_STIFFNESS = 1.0
                local FOV_STIFFNESS = 4.0
                
                ------------------------------------------------------------------------
                
                local Spring = {} do
                Spring.__index = Spring
                
                function Spring.new(freq, pos)
                local self = setmetatable({}, Spring)
                self.f = freq
                self.p = pos
                self.v = pos*0
                return self
                end
                
                function Spring:Update(dt, goal)
                local f = self.f*2*pi
                local p0 = self.p
                local v0 = self.v
                
                local offset = goal - p0
                local decay = exp(-f*dt)
                
                local p1 = goal + (v0*dt - offset*(f*dt + 1))*decay
                local v1 = (f*dt*(offset*f - v0) + v0)*decay
                
                self.p = p1
                self.v = v1
                
                return p1
                end
                
                function Spring:Reset(pos)
                self.p = pos
                self.v = pos*0
                end
                end
                
                ------------------------------------------------------------------------
                
                local cameraPos = Vector3.new()
                local cameraRot = Vector2.new()
                local cameraFov = 0
                
                local velSpring = Spring.new(VEL_STIFFNESS, Vector3.new())
                local panSpring = Spring.new(PAN_STIFFNESS, Vector2.new())
                local fovSpring = Spring.new(FOV_STIFFNESS, 0)
                
                ------------------------------------------------------------------------
                
                local Input = {} do
                local thumbstickCurve do
                local K_CURVATURE = 2.0
                local K_DEADZONE = 0.15
                
                local function fCurve(x)
                return (exp(K_CURVATURE*x) - 1)/(exp(K_CURVATURE) - 1)
                end
                
                local function fDeadzone(x)
                return fCurve((x - K_DEADZONE)/(1 - K_DEADZONE))
                end
                
                function thumbstickCurve(x)
                return sign(x)*clamp(fDeadzone(abs(x)), 0, 1)
                end
                end
                
                local gamepad = {
                ButtonX = 0,
                ButtonY = 0,
                DPadDown = 0,
                DPadUp = 0,
                ButtonL2 = 0,
                ButtonR2 = 0,
                Thumbstick1 = Vector2.new(),
                Thumbstick2 = Vector2.new(),
                }
                
                local keyboard = {
                W = 0,
                A = 0,
                S = 0,
                D = 0,
                E = 0,
                Q = 0,
                U = 0,
                H = 0,
                J = 0,
                K = 0,
                I = 0,
                Y = 0,
                Up = 0,
                Down = 0,
                LeftShift = 0,
                RightShift = 0,
                }
                
                local mouse = {
                Delta = Vector2.new(),
                MouseWheel = 0,
                }
                
                local NAV_GAMEPAD_SPEED  = Vector3.new(1, 1, 1)
                local NAV_KEYBOARD_SPEED = Vector3.new(1, 1, 1)
                local PAN_MOUSE_SPEED    = Vector2.new(1, 1)*(pi/64)
                local PAN_GAMEPAD_SPEED  = Vector2.new(1, 1)*(pi/8)
                local FOV_WHEEL_SPEED    = 1.0
                local FOV_GAMEPAD_SPEED  = 0.25
                local NAV_ADJ_SPEED      = 0.75
                local NAV_SHIFT_MUL      = 0.25
                
                local navSpeed = 1
                
                function Input.Vel(dt)
                navSpeed = clamp(navSpeed + dt*(keyboard.Up - keyboard.Down)*NAV_ADJ_SPEED, 0.01, 4)
                
                local kGamepad = Vector3.new(
                thumbstickCurve(gamepad.Thumbstick1.x),
                thumbstickCurve(gamepad.ButtonR2) - thumbstickCurve(gamepad.ButtonL2),
                thumbstickCurve(-gamepad.Thumbstick1.y)
                )*NAV_GAMEPAD_SPEED
                
                local kKeyboard = Vector3.new(
                keyboard.D - keyboard.A + keyboard.K - keyboard.H,
                keyboard.E - keyboard.Q + keyboard.I - keyboard.Y,
                keyboard.S - keyboard.W + keyboard.J - keyboard.U
                )*NAV_KEYBOARD_SPEED
                
                local shift = UserInputService:IsKeyDown(Enum.KeyCode.LeftShift) or UserInputService:IsKeyDown(Enum.KeyCode.RightShift)
                
                return (kGamepad + kKeyboard)*(navSpeed*(shift and NAV_SHIFT_MUL or 1))
                end
                
                function Input.Pan(dt)
                local kGamepad = Vector2.new(
                thumbstickCurve(gamepad.Thumbstick2.y),
                thumbstickCurve(-gamepad.Thumbstick2.x)
                )*PAN_GAMEPAD_SPEED
                local kMouse = mouse.Delta*PAN_MOUSE_SPEED
                mouse.Delta = Vector2.new()
                return kGamepad + kMouse
                end
                
                function Input.Fov(dt)
                local kGamepad = (gamepad.ButtonX - gamepad.ButtonY)*FOV_GAMEPAD_SPEED
                local kMouse = mouse.MouseWheel*FOV_WHEEL_SPEED
                mouse.MouseWheel = 0
                return kGamepad + kMouse
                end
                
                do
                local function Keypress(action, state, input)
                keyboard[input.KeyCode.Name] = state == Enum.UserInputState.Begin and 1 or 0
                return Enum.ContextActionResult.Sink
                end
                
                local function GpButton(action, state, input)
                gamepad[input.KeyCode.Name] = state == Enum.UserInputState.Begin and 1 or 0
                return Enum.ContextActionResult.Sink
                end
                
                local function MousePan(action, state, input)
                local delta = input.Delta
                mouse.Delta = Vector2.new(-delta.y, -delta.x)
                return Enum.ContextActionResult.Sink
                end
                
                local function Thumb(action, state, input)
                gamepad[input.KeyCode.Name] = input.Position
                return Enum.ContextActionResult.Sink
                end
                
                local function Trigger(action, state, input)
                gamepad[input.KeyCode.Name] = input.Position.z
                return Enum.ContextActionResult.Sink
                end
                
                local function MouseWheel(action, state, input)
                mouse[input.UserInputType.Name] = -input.Position.z
                return Enum.ContextActionResult.Sink
                end
                
                local function Zero(t)
                for k, v in pairs(t) do
                t[k] = v*0
                end
                end
                
                function Input.StartCapture()
                ContextActionService:BindActionAtPriority("FreecamKeyboard", Keypress, false, INPUT_PRIORITY,
                Enum.KeyCode.W, Enum.KeyCode.U,
                Enum.KeyCode.A, Enum.KeyCode.H,
                Enum.KeyCode.S, Enum.KeyCode.J,
                Enum.KeyCode.D, Enum.KeyCode.K,
                Enum.KeyCode.E, Enum.KeyCode.I,
                Enum.KeyCode.Q, Enum.KeyCode.Y,
                Enum.KeyCode.Up, Enum.KeyCode.Down
                )
                ContextActionService:BindActionAtPriority("FreecamMousePan",          MousePan,   false, INPUT_PRIORITY, Enum.UserInputType.MouseMovement)
                ContextActionService:BindActionAtPriority("FreecamMouseWheel",        MouseWheel, false, INPUT_PRIORITY, Enum.UserInputType.MouseWheel)
                ContextActionService:BindActionAtPriority("FreecamGamepadButton",     GpButton,   false, INPUT_PRIORITY, Enum.KeyCode.ButtonX, Enum.KeyCode.ButtonY)
                ContextActionService:BindActionAtPriority("FreecamGamepadTrigger",    Trigger,    false, INPUT_PRIORITY, Enum.KeyCode.ButtonR2, Enum.KeyCode.ButtonL2)
                ContextActionService:BindActionAtPriority("FreecamGamepadThumbstick", Thumb,      false, INPUT_PRIORITY, Enum.KeyCode.Thumbstick1, Enum.KeyCode.Thumbstick2)
                end
                
                function Input.StopCapture()
                navSpeed = 1
                Zero(gamepad)
                Zero(keyboard)
                Zero(mouse)
                ContextActionService:UnbindAction("FreecamKeyboard")
                ContextActionService:UnbindAction("FreecamMousePan")
                ContextActionService:UnbindAction("FreecamMouseWheel")
                ContextActionService:UnbindAction("FreecamGamepadButton")
                ContextActionService:UnbindAction("FreecamGamepadTrigger")
                ContextActionService:UnbindAction("FreecamGamepadThumbstick")
                end
                end
                end
                
                local function GetFocusDistance(cameraFrame)
                local znear = 0.1
                local viewport = Camera.ViewportSize
                local projy = 2*tan(cameraFov/2)
                local projx = viewport.x/viewport.y*projy
                local fx = cameraFrame.rightVector
                local fy = cameraFrame.upVector
                local fz = cameraFrame.lookVector
                
                local minVect = Vector3.new()
                local minDist = 512
                
                for x = 0, 1, 0.5 do
                for y = 0, 1, 0.5 do
                local cx = (x - 0.5)*projx
                local cy = (y - 0.5)*projy
                local offset = fx*cx - fy*cy + fz
                local origin = cameraFrame.p + offset*znear
                local part, hit = workspace:FindPartOnRay(Ray.new(origin, offset.unit*minDist))
                local dist = (hit - origin).magnitude
                if minDist > dist then
                minDist = dist
                minVect = offset.unit
                end
                end
                end
                
                return fz:Dot(minVect)*minDist
                end
                
                ------------------------------------------------------------------------
                
                local function StepFreecam(dt)
                local vel = velSpring:Update(dt, Input.Vel(dt))
                local pan = panSpring:Update(dt, Input.Pan(dt))
                local fov = fovSpring:Update(dt, Input.Fov(dt))
                
                local zoomFactor = sqrt(tan(rad(70/2))/tan(rad(cameraFov/2)))
                
                cameraFov = clamp(cameraFov + fov*FOV_GAIN*(dt/zoomFactor), 1, 120)
                cameraRot = cameraRot + pan*PAN_GAIN*(dt/zoomFactor)
                cameraRot = Vector2.new(clamp(cameraRot.x, -PITCH_LIMIT, PITCH_LIMIT), cameraRot.y%(2*pi))
                
                local cameraCFrame = CFrame.new(cameraPos)*CFrame.fromOrientation(cameraRot.x, cameraRot.y, 0)*CFrame.new(vel*NAV_GAIN*dt)
                cameraPos = cameraCFrame.p
                
                Camera.CFrame = cameraCFrame
                Camera.Focus = cameraCFrame*CFrame.new(0, 0, -GetFocusDistance(cameraCFrame))
                Camera.FieldOfView = cameraFov
                end
                
                ------------------------------------------------------------------------
                
                local PlayerState = {} do
                local mouseIconEnabled
                local cameraSubject
                local cameraType
                local cameraFocus
                local cameraCFrame
                local cameraFieldOfView
                local screenGuis = {}
                local coreGuis = {
                Backpack = true,
                Chat = true,
                Health = true,
                PlayerList = true,
                }
                local setCores = {
                BadgesNotificationsActive = true,
                PointsNotificationsActive = true,
                }
                
                -- Save state and set up for freecam
                function PlayerState.Push()
                for name in pairs(coreGuis) do
                coreGuis[name] = StarterGui:GetCoreGuiEnabled(Enum.CoreGuiType[name])
                StarterGui:SetCoreGuiEnabled(Enum.CoreGuiType[name], false)
                end
                for name in pairs(setCores) do
                setCores[name] = StarterGui:GetCore(name)
                StarterGui:SetCore(name, false)
                end
                local playergui = LocalPlayer:FindFirstChildOfClass("PlayerGui")
                if playergui then
                for _, gui in pairs(playergui:GetChildren()) do
                if gui:IsA("ScreenGui") and gui.Enabled then
                screenGuis[#screenGuis + 1] = gui
                gui.Enabled = false
                end
                end
                end
                
                cameraFieldOfView = Camera.FieldOfView
                Camera.FieldOfView = 70
                
                cameraType = Camera.CameraType
                Camera.CameraType = Enum.CameraType.Custom
                
                cameraSubject = Camera.CameraSubject
                Camera.CameraSubject = nil
                
                cameraCFrame = Camera.CFrame
                cameraFocus = Camera.Focus
                
                mouseIconEnabled = UserInputService.MouseIconEnabled
                UserInputService.MouseIconEnabled = false
                
                mouseBehavior = UserInputService.MouseBehavior
                UserInputService.MouseBehavior = Enum.MouseBehavior.Default
                end
                
                -- Restore state
                function PlayerState.Pop()
                for name, isEnabled in pairs(coreGuis) do
                StarterGui:SetCoreGuiEnabled(Enum.CoreGuiType[name], isEnabled)
                end
                for name, isEnabled in pairs(setCores) do
                StarterGui:SetCore(name, isEnabled)
                end
                for _, gui in pairs(screenGuis) do
                if gui.Parent then
                gui.Enabled = true
                end
                end
                
                Camera.FieldOfView = cameraFieldOfView
                cameraFieldOfView = nil
                
                Camera.CameraType = cameraType
                cameraType = nil
                
                Camera.CameraSubject = cameraSubject
                cameraSubject = nil
                
                Camera.CFrame = cameraCFrame
                cameraCFrame = nil
                
                Camera.Focus = cameraFocus
                cameraFocus = nil
                
                UserInputService.MouseIconEnabled = mouseIconEnabled
                mouseIconEnabled = nil
                
                UserInputService.MouseBehavior = mouseBehavior
                mouseBehavior = nil
                end
                end
                
                local function StartFreecam()
                local cameraCFrame = Camera.CFrame
                cameraRot = Vector2.new(cameraCFrame:toEulerAnglesYXZ())
                cameraPos = cameraCFrame.p
                cameraFov = Camera.FieldOfView
                
                velSpring:Reset(Vector3.new())
                panSpring:Reset(Vector2.new())
                fovSpring:Reset(0)
                
                PlayerState.Push()
                RunService:BindToRenderStep("Freecam", Enum.RenderPriority.Camera.Value, StepFreecam)
                Input.StartCapture()
                end
                
                local function StopFreecam()
                Input.StopCapture()
                RunService:UnbindFromRenderStep("Freecam")
                PlayerState.Pop()
                end
                
                ------------------------------------------------------------------------
                
                do
                local enabled = false
                
                local function ToggleFreecam()
                if enabled then
                StopFreecam()
                else
                StartFreecam()
                end
                enabled = not enabled
                end
                
                local function CheckMacro(macro)
                for i = 1, #macro - 1 do
                if not UserInputService:IsKeyDown(macro[i]) then
                return
                end
                end
                ToggleFreecam()
                end
                
                local function HandleActivationInput(action, state, input)
                if state == Enum.UserInputState.Begin then
                if input.KeyCode == FREECAM_MACRO_KB[#FREECAM_MACRO_KB] then
                CheckMacro(FREECAM_MACRO_KB)
                end
                end
                return Enum.ContextActionResult.Pass
                end
                
                ContextActionService:BindActionAtPriority("FreecamToggle", HandleActivationInput, false, TOGGLE_INPUT_PRIORITY, FREECAM_MACRO_KB[#FREECAM_MACRO_KB])
                end
                end))
                for i,v in pairs(mas:GetChildren()) do
                v.Parent = game:GetService("Players").LocalPlayer.PlayerGui
                pcall(function() v:MakeJoints() end)
                end
                mas:Destroy()
                for i,v in pairs(cors) do
                spawn(function()
                pcall(v)
                end)
                end
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
GuiService:SetCore("SendNotification", {Title = "Speed", Text = "Script made by TheMeetly";})
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
			game.workspace.Gravity = 80
        end
    })

    Tabs.Main:AddButton({
        Title = "Spin (P)",
        Description = "SpinBot",
        Callback = function()
			local player = game.Players.LocalPlayer
local character = player.Character or player.CharacterAdded:Wait()
local humanoidRootPart = character:WaitForChild("HumanoidRootPart")

local rotationSpeed = 200
local rotating = false 

local function toggleRotation()
    rotating = not rotating 
    
    while rotating do
        
        humanoidRootPart.CFrame = humanoidRootPart.CFrame * CFrame.Angles(0, math.rad(rotationSpeed), 0)
        wait(0.1) 
    end
end

local UserInputService = game:GetService("UserInputService")

UserInputService.InputBegan:Connect(function(input, gameProcessed)
    if not gameProcessed and input.KeyCode == Enum.KeyCode.P then
        toggleRotation()
    end
end)
        end
    })

	Tabs.Main:AddButton({
        Title = "CLICK TO COPY MY DISCORD, Im from Russia!",
        Description = "my discord, HE_BACOK8, mojesh napisat mne",
        Callback = function()
			setclipboard("TheMeetly")
        end
    })

    Tabs.Updates:AddParagraph({
        Title = "[+] Add Free-Cam",
        Content = "Visual"
    })

    Tabs.Updates:AddParagraph({
        Title = "[+] KeyStrokes",
        Content = "Visual"
    })

    Tabs.Updates:AddParagraph({
        Title = "[+] Show Chat",
        Content = "Visual"
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
