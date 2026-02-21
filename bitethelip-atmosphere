-- [[ CONFIGURATION ]] --
local Settings = {
    CurrentFog = "None",
    Visible = true,
    HideKey = Enum.KeyCode.X
}

-- [[ FOG PRESETS ]] --
local FogPresets = {

    -- Neon Colors
    ["Neon Pink"] = {
        Color = Color3.fromRGB(255, 20, 147),
        Density = 0.45
    },
    ["Neon Blue"] = {
        Color = Color3.fromRGB(0, 170, 255),
        Density = 0.46
    },
    ["Neon Purple"] = {
        Color = Color3.fromRGB(170, 0, 255),
        Density = 0.46
    },
    ["Neon Orange"] = {
        Color = Color3.fromRGB(255, 102, 0),
        Density = 0.45
    },
    ["Neon Red"] = {
        Color = Color3.fromRGB(255, 0, 60),
        Density = 0.54
    },
    ["Neon Green"] = {
        Color = Color3.fromRGB(57, 255, 20),
        Density = 0.52
    },

    -- Pastel Colors
    ["Pastel Pink"] = {
        Color = Color3.fromRGB(255, 179, 223), 
        Density = 0.55
    },
    ["Pastel Blue"] = {
        Color = Color3.fromRGB(173, 216, 255), 
        Density = 0.52
    },
    ["Pastel Purple"] = {
        Color = Color3.fromRGB(216, 191, 255), 
        Density = 0.55
    },
    ["Pastel Orange"] = {
        Color = Color3.fromRGB(255, 223, 186), 
        Density = 0.49
    },
    ["Pastel Red"] = {
        Color = Color3.fromRGB(255, 179, 186), 
        Density = 0.52
    },
    ["Pastel Green"] = {
        Color = Color3.fromRGB(186, 255, 201), 
        Density = 0.43
    }
}

-- [[ FIXED BUTTON ORDER ]] --
local Order = {
    "Neon Pink",
    "Neon Blue",
    "Neon Purple",
    "Neon Orange",
    "Neon Red",
    "Neon Green",
    "Pastel Pink",
    "Pastel Blue",
    "Pastel Purple",
    "Pastel Orange",
    "Pastel Red",
    "Pastel Green"
}

-- [[ CAPTURE ORIGINAL GAME STATE ]] --
local Lighting = game:GetService("Lighting")
local OrigFogStart = Lighting.FogStart
local OrigFogEnd = Lighting.FogEnd
local OrigFogColor = Lighting.FogColor
local OrigAtmosphere = Lighting:FindFirstChildOfClass("Atmosphere") and Lighting:FindFirstChildOfClass("Atmosphere"):Clone() or nil

-- [[ SERVICES ]] --
local UIS = game:GetService("UserInputService")
local TweenService = game:GetService("TweenService")

-- [[ UI CONSTRUCT ]] --
local ScreenGui = Instance.new("ScreenGui", game.CoreGui)
local Main = Instance.new("Frame", ScreenGui)
local Corner = Instance.new("UICorner", Main)
local Glow = Instance.new("UIStroke", Main)

Main.Name = "bitethelip Atmosphere"
Main.Size = UDim2.new(0, 240, 0, 350)
Main.Position = UDim2.new(0.5, -120, 0.5, -175)
Main.BackgroundColor3 = Color3.fromRGB(10, 10, 10)
Main.BorderSizePixel = 0
Main.Active = true
Main.Draggable = true

Corner.CornerRadius = UDim.new(0, 10)
Glow.Color = Color3.fromRGB(255, 196, 228)
Glow.Thickness = 2
Glow.ApplyStrokeMode = Enum.ApplyStrokeMode.Border

local Title = Instance.new("TextLabel", Main)
Title.Size = UDim2.new(1, 0, 0, 45)
Title.Text = "bitethelip Atmosphere"
Title.BackgroundTransparency = 1
Title.TextColor3 = Color3.fromRGB(255, 255, 255)
Title.Font = Enum.Font.GothamBold
Title.TextSize = 14

local AccentLine = Instance.new("Frame", Main)
AccentLine.Size = UDim2.new(0.8, 0, 0, 2)
AccentLine.Position = UDim2.fromScale(0.1, 0.15)
AccentLine.BackgroundColor3 = Color3.fromRGB(255, 179, 223)
AccentLine.BorderSizePixel = 0

local Scroll = Instance.new("ScrollingFrame", Main)
Scroll.Size = UDim2.new(1, -20, 1, -110)
Scroll.Position = UDim2.new(0, 10, 0, 60)
Scroll.BackgroundTransparency = 1
Scroll.BorderSizePixel = 0
Scroll.ScrollBarThickness = 2

local Layout = Instance.new("UIListLayout", Scroll)
Layout.Padding = UDim.new(0, 8)

local Hint = Instance.new("TextLabel", Main)
Hint.Size = UDim2.new(1, 0, 0, 30)
Hint.Position = UDim2.new(0, 0, 1, -30)
Hint.BackgroundTransparency = 1
Hint.Text = "Press [X] to Hide UI"
Hint.TextColor3 = Color3.fromRGB(100, 100, 100)
Hint.Font = Enum.Font.Gotham
Hint.TextSize = 11

-- [[ CORE LOGIC ]] --

local function CleanAtmosphere()
    for _, v in ipairs(Lighting:GetChildren()) do
        if v:IsA("Atmosphere") then
            v:Destroy()
        end
    end
end

local function ApplySkyFog(preset)
    CleanAtmosphere()

    local atm = Instance.new("Atmosphere")
    atm.Name = "bitethelip"
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

local function CreateButton(name, data, isReset)
    local btn = Instance.new("TextButton", Scroll)
    btn.Size = UDim2.new(0.95, 0, 0, 38)
    btn.BackgroundColor3 = Color3.fromRGB(20, 20, 20)
    btn.Text = name:upper()
    btn.Font = Enum.Font.GothamSemibold
    btn.TextColor3 = Color3.fromRGB(200, 200, 200)
    btn.TextSize = 11
    btn.AutoButtonColor = false

    Instance.new("UICorner", btn)

    local stroke = Instance.new("UIStroke", btn)
    stroke.Color = Color3.fromRGB(40, 40, 40)

    local targetColor = isReset and Color3.new(1,1,1) or data.Color

    btn.MouseEnter:Connect(function()
        TweenService:Create(stroke, TweenInfo.new(0.2), {Color = targetColor}):Play()
    end)

    btn.MouseLeave:Connect(function()
        if Settings.CurrentFog ~= name then
            TweenService:Create(stroke, TweenInfo.new(0.2), {Color = Color3.fromRGB(40,40,40)}):Play()
        end
    end)

    btn.MouseButton1Click:Connect(function()
        if isReset then
            RestoreOriginal()
            Settings.CurrentFog = "None"
        else
            Settings.CurrentFog = name
            ApplySkyFog(data)
        end

        for _, v in ipairs(Scroll:GetChildren()) do
            if v:IsA("TextButton") then
                v:FindFirstChildOfClass("UIStroke").Color = Color3.fromRGB(40,40,40)
            end
        end

        stroke.Color = targetColor
    end)
end

-- [[ CREATE BUTTONS IN FIXED ORDER ]] --
for _, name in ipairs(Order) do
    CreateButton(name, FogPresets[name], false)
end

CreateButton("Restore Game Fog", nil, true)

-- [[ HIDE KEY ]] --
UIS.InputBegan:Connect(function(input, gpe)
    if not gpe and input.KeyCode == Settings.HideKey then
        Settings.Visible = not Settings.Visible
        Main.Visible = Settings.Visible
    end
end)

-- Auto resize scroll
Layout:GetPropertyChangedSignal("AbsoluteContentSize"):Connect(function()
    Scroll.CanvasSize = UDim2.new(0, 0, 0, Layout.AbsoluteContentSize.Y + 10)
end)
