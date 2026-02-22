-- [[ CONFIGURATION ]] --
local Settings = {
    CurrentFog = "None",
    Visible = true,
    HideKey = Enum.KeyCode.X
}

-- [[ FOG PRESETS ]] --
local FogPresets = {
    ["Neon Pink"] = {Color = Color3.fromRGB(255, 20, 147), Density = 0.45},
    ["Neon Blue"] = {Color = Color3.fromRGB(0, 170, 255), Density = 0.46},
    ["Neon Purple"] = {Color = Color3.fromRGB(170, 0, 255), Density = 0.46},
    ["Neon Orange"] = {Color = Color3.fromRGB(255, 102, 0), Density = 0.45},
    ["Neon Red"] = {Color = Color3.fromRGB(255, 0, 60), Density = 0.54},
    ["Neon Green"] = {Color = Color3.fromRGB(57, 255, 20), Density = 0.52},
    ["Pastel Pink"] = {Color = Color3.fromRGB(255, 179, 223), Density = 0.55},
    ["Pastel Blue"] = {Color = Color3.fromRGB(173, 216, 255), Density = 0.52},
    ["Pastel Purple"] = {Color = Color3.fromRGB(216, 191, 255), Density = 0.55},
    ["Pastel Orange"] = {Color = Color3.fromRGB(255, 223, 186), Density = 0.49},
    ["Pastel Red"] = {Color = Color3.fromRGB(255, 179, 186), Density = 0.52},
    ["Pastel Green"] = {Color = Color3.fromRGB(186, 255, 201), Density = 0.43}
}

local Order = {
    "Neon Pink","Neon Blue","Neon Purple","Neon Orange","Neon Red","Neon Green",
    "Pastel Pink","Pastel Blue","Pastel Purple","Pastel Orange","Pastel Red","Pastel Green"
}

-- [[ ORIGINAL STATE ]] --
local Lighting = game:GetService("Lighting")
local OrigFogStart, OrigFogEnd, OrigFogColor = Lighting.FogStart, Lighting.FogEnd, Lighting.FogColor
local OrigAtmosphere = Lighting:FindFirstChildOfClass("Atmosphere") and Lighting:FindFirstChildOfClass("Atmosphere"):Clone() or nil

local UIS = game:GetService("UserInputService")
local TweenService = game:GetService("TweenService")

-- [[ ATMOSPHERE FUNCTIONS ]] --
local function CleanAtmosphere()
    for _, atm in ipairs(Lighting:GetChildren()) do
        if atm:IsA("Atmosphere") then atm:Destroy() end
    end
end

local function ApplyFog(preset)
    CleanAtmosphere()
    local atm = Instance.new("Atmosphere")
    atm.Name = "CustomFog"
    atm.Color = preset.Color
    atm.Decay = preset.Color
    atm.Density = preset.Density
    atm.Haze = 4
    atm.Parent = Lighting

    Lighting.FogStart = 30
    Lighting.FogEnd = 200
end

local function RestoreOriginal()
    CleanAtmosphere()
    if OrigAtmosphere then
        OrigAtmosphere:Clone().Parent = Lighting
    end
    Lighting.FogStart = OrigFogStart
    Lighting.FogEnd = OrigFogEnd
    Lighting.FogColor = OrigFogColor
end

-- [[ GUI CREATION - SMALL PREMIUM STYLE ]] --
local ScreenGui = Instance.new("ScreenGui", game.CoreGui)
ScreenGui.Name = "AtmosphereGUI"

-- Main Panel (smaller)
local Main = Instance.new("Frame", ScreenGui)
Main.Size = UDim2.new(0, 200, 0, 320) -- smaller frame
Main.Position = UDim2.new(0.5, -100, 0.5, -160)
Main.BackgroundColor3 = Color3.fromRGB(20,20,20)
Main.BackgroundTransparency = 0.4
Main.BorderSizePixel = 0
Main.Active = true
Main.Draggable = true
local MainCorner = Instance.new("UICorner", Main)
MainCorner.CornerRadius = UDim.new(0, 16)

-- Title Bar (glass, smaller)
local Title = Instance.new("Frame", Main)
Title.Size = UDim2.new(1, -20, 0, 40)
Title.Position = UDim2.new(0,10,0,10)
Title.BackgroundColor3 = Color3.fromRGB(40,40,40)
Title.BackgroundTransparency = 0.3
local TitleCorner = Instance.new("UICorner", Title)
TitleCorner.CornerRadius = UDim.new(0,12)

-- Title stroke glow
local TitleStroke = Instance.new("UIStroke", Title)
TitleStroke.Color = Color3.fromRGB(255,255,255)
TitleStroke.Thickness = 1
TitleStroke.Transparency = 0.7

-- Centered Text Label (smaller)
local TitleLabel = Instance.new("TextLabel", Title)
TitleLabel.Size = UDim2.new(1,0,1,0)
TitleLabel.BackgroundTransparency = 1
TitleLabel.Text = "bitethelip"
TitleLabel.TextColor3 = Color3.fromRGB(255,255,255)
TitleLabel.Font = Enum.Font.GothamBold
TitleLabel.TextSize = 16 -- smaller text
TitleLabel.TextScaled = true
TitleLabel.TextWrapped = true
TitleLabel.TextXAlignment = Enum.TextXAlignment.Center
TitleLabel.TextYAlignment = Enum.TextYAlignment.Center

-- Scroll Frame for Buttons (smaller)
local Scroll = Instance.new("ScrollingFrame", Main)
Scroll.Size = UDim2.new(1, -20, 1, -80)
Scroll.Position = UDim2.new(0,10,0,60)
Scroll.BackgroundTransparency = 1
Scroll.BorderSizePixel = 0
Scroll.ScrollBarThickness = 5

local Layout = Instance.new("UIListLayout", Scroll)
Layout.Padding = UDim.new(0,8)
Layout.SortOrder = Enum.SortOrder.LayoutOrder

-- Hide Hint
local Hint = Instance.new("TextLabel", Main)
Hint.Size = UDim2.new(1,0,0,25)
Hint.Position = UDim2.new(0,0,1,-25)
Hint.Text = "Press [X] to Toggle UI"
Hint.TextColor3 = Color3.fromRGB(220,220,220)
Hint.Font = Enum.Font.Gotham
Hint.TextSize = 10
Hint.BackgroundTransparency = 1

-- [[ CREATE PREMIUM PILL BUTTON FUNCTION (smaller) ]] --
local function CreateButton(name, preset, isRestore)
    local btn = Instance.new("TextButton", Scroll)
    btn.Size = UDim2.new(0.95,0,0,35) -- smaller buttons
    btn.BackgroundColor3 = Color3.fromRGB(60,60,60)
    btn.BackgroundTransparency = 0.2
    btn.Text = name:upper()
    btn.Font = Enum.Font.GothamSemibold
    btn.TextSize = 10 -- smaller text
    btn.TextColor3 = Color3.fromRGB(255,255,255)
    btn.AutoButtonColor = false

    local corner = Instance.new("UICorner", btn)
    corner.CornerRadius = UDim.new(0,18)

    local stroke = Instance.new("UIStroke", btn)
    stroke.Thickness = 2
    stroke.Color = Color3.fromRGB(180,180,180)
    stroke.Transparency = 0.5

    btn.MouseEnter:Connect(function()
        TweenService:Create(stroke, TweenInfo.new(0.25), {Color = isRestore and Color3.fromRGB(255,255,255) or preset.Color}):Play()
        TweenService:Create(btn, TweenInfo.new(0.25), {BackgroundTransparency = 0.1}):Play()
    end)
    btn.MouseLeave:Connect(function()
        if Settings.CurrentFog ~= name then
            TweenService:Create(stroke, TweenInfo.new(0.25), {Color = Color3.fromRGB(180,180,180)}):Play()
            TweenService:Create(btn, TweenInfo.new(0.25), {BackgroundTransparency = 0.2}):Play()
        end
    end)

    btn.MouseButton1Click:Connect(function()
        if isRestore then
            RestoreOriginal()
            Settings.CurrentFog = "None"
        else
            Settings.CurrentFog = name
            ApplyFog(preset)
        end
        for _, v in ipairs(Scroll:GetChildren()) do
            if v:IsA("TextButton") then
                v:FindFirstChildOfClass("UIStroke").Color = Color3.fromRGB(180,180,180)
            end
        end
        stroke.Color = isRestore and Color3.fromRGB(255,255,255) or preset.Color
    end)
end

-- [[ CREATE ALL BUTTONS ]] --
for _, name in ipairs(Order) do
    CreateButton(name, FogPresets[name], false)
end
CreateButton("Restore Original Fog", nil, true)

-- [[ HIDE KEY TOGGLE ]] --
UIS.InputBegan:Connect(function(input,gpe)
    if not gpe and input.KeyCode == Settings.HideKey then
        Settings.Visible = not Settings.Visible
        Main.Visible = Settings.Visible
    end
end)

-- [[ AUTO RESIZE SCROLL ]] --
Layout:GetPropertyChangedSignal("AbsoluteContentSize"):Connect(function()
    Scroll.CanvasSize = UDim2.new(0,0,0,Layout.AbsoluteContentSize.Y + 10)
end)
