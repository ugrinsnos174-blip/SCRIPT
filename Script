--[[ GOD IS COMING — visual only, executor
     Звук: 108035501622201
     PlaybackSpeed = 0.3 — медленно, низко, слышно чётко.
     Без PitchShift (он даёт ускорение/артефакты).
]]

local Players = game:GetService("Players")
local TweenService = game:GetService("TweenService")
local Lighting = game:GetService("Lighting")
local RunService = game:GetService("RunService")
local Workspace = game:GetService("Workspace")
local CoreGui = game:GetService("CoreGui")
local SoundService = game:GetService("SoundService")
local StarterGui = game:GetService("StarterGui")

local player = Players.LocalPlayer
local TRACK_ID = "rbxassetid://108035501622201"
local TIMER = 10
local KICK_DELAY = 4
local SLOW_SPEED = 0.3 -- чем меньше, тем медленнее и ниже

-- ===== UI =====
pcall(function() StarterGui:SetCoreGuiEnabled(Enum.CoreGuiType.All, false) end)
pcall(function() StarterGui:SetCore("TopbarEnabled", false) end)
pcall(function()
    local top = CoreGui:FindFirstChild("TopBarApp")
    if top then top:Destroy() end
end)
local pg = player:FindFirstChild("PlayerGui")
if pg then
    for _, obj in ipairs(pg:GetChildren()) do
        if obj.Name ~= "GodUI" then
            pcall(function() obj.Enabled = false end)
        end
    end
end

-- ===== ЗВУКИ =====
for _, s in ipairs(SoundService:GetDescendants()) do
    if s:IsA("Sound") then
        pcall(function() s:Stop() s.Volume = 0 end)
    end
end
SoundService.DescendantAdded:Connect(function(s)
    if s:IsA("Sound") then
        pcall(function() s.Volume = 0 s:Stop() end)
    end
end)

-- ===== КАМЕРА =====
local camera = Workspace.CurrentCamera
local function lockCamera()
    if not player.Character then return end
    local root = player.Character:FindFirstChild("HumanoidRootPart")
    if not root then return end
    camera.CameraType = Enum.CameraType.Scriptable
    camera.CFrame = CFrame.new(root.Position + Vector3.new(0, 8, 12), root.Position)
end
if player.Character then lockCamera() end
player.CharacterAdded:Connect(function()
    task.wait(1)
    lockCamera()
end)
RunService.RenderStepped:Connect(function()
    local char = player.Character
    local root = char and char:FindFirstChild("HumanoidRootPart")
    if root and camera.CameraType == Enum.CameraType.Scriptable then
        local targetPos = root.Position + Vector3.new(0, 8, 12)
        camera.CFrame = camera.CFrame:Lerp(CFrame.new(targetPos, root.Position), 0.1)
    end
end)

-- ===== GUI =====
local gui = Instance.new("ScreenGui")
gui.Name = "GodUI"
gui.IgnoreGuiInset = true
gui.DisplayOrder = 2147483647
gui.ResetOnSpawn = false
gui.Parent = CoreGui

local shakeFrame = Instance.new("Frame")
shakeFrame.Size = UDim2.fromScale(1, 1)
shakeFrame.BackgroundTransparency = 1
shakeFrame.Parent = gui

local black = Instance.new("Frame")
black.Size = UDim2.fromScale(1, 1)
black.BackgroundColor3 = Color3.new()
black.BackgroundTransparency = 1
black.BorderSizePixel = 0
black.Parent = shakeFrame

local red = Instance.new("Frame")
red.Size = UDim2.fromScale(1, 1)
red.BackgroundColor3 = Color3.fromRGB(120, 0, 0)
red.BackgroundTransparency = 1
red.BorderSizePixel = 0
red.Parent = shakeFrame

local vignette = Instance.new("ImageLabel")
vignette.Size = UDim2.fromScale(1, 1)
vignette.BackgroundTransparency = 1
vignette.Image = "rbxassetid://8992230677"
vignette.ImageColor3 = Color3.fromRGB(255, 0, 0)
vignette.ImageTransparency = 1
vignette.ScaleType = Enum.ScaleType.Stretch
vignette.Parent = shakeFrame

local god = Instance.new("TextLabel")
god.Size = UDim2.new(1, 0, 0.22, 0)
god.Position = UDim2.new(0, 0, 0.28, 0)
god.BackgroundTransparency = 1
god.Text = "god is coming"
god.TextColor3 = Color3.fromRGB(255, 0, 0)
god.TextScaled = true
god.Font = Enum.Font.Arcade
god.TextTransparency = 1
god.TextStrokeTransparency = 1
god.TextStrokeColor3 = Color3.fromRGB(80, 0, 0)
god.Parent = shakeFrame

local timer = Instance.new("TextLabel")
timer.Size = UDim2.new(1, 0, 0.16, 0)
timer.Position = UDim2.new(0, 0, 0.55, 0)
timer.BackgroundTransparency = 1
timer.Text = ""
timer.TextColor3 = Color3.fromRGB(255, 60, 60)
timer.TextScaled = true
timer.Font = Enum.Font.Arcade
timer.TextTransparency = 1
timer.Parent = shakeFrame

-- ===== ЗВУК (без PitchShift, только PlaybackSpeed) =====
local sound = Instance.new("Sound")
sound.SoundId = TRACK_ID
sound.Looped = true
sound.Volume = 0
sound.PlaybackSpeed = SLOW_SPEED -- медленно и низко, слышно
sound.Parent = gui
-- лёгкий дисторшн, не глушит
local dist = Instance.new("DistortionSoundEffect", sound)
dist.Level = 0.3

-- ===== ЭФФЕКТЫ =====
local cc = Instance.new("ColorCorrectionEffect")
cc.Parent = Lighting
local blur = Instance.new("BlurEffect")
blur.Size = 0
blur.Parent = Lighting

-- ===== ТРЯСКА =====
local shakeAmt = 0
RunService.RenderStepped:Connect(function()
    if shakeAmt > 0 then
        shakeFrame.Position = UDim2.fromOffset(
            math.random(-shakeAmt, shakeAmt),
            math.random(-shakeAmt, shakeAmt)
        )
    end
end)

-- ===== СТАРТ =====
sound:Play()
TweenService:Create(sound, TweenInfo.new(2), {Volume = 0.85}):Play()

local slow = TweenInfo.new(3, Enum.EasingStyle.Quad, Enum.EasingDirection.In)
TweenService:Create(black, slow, {BackgroundTransparency = 0.55}):Play()
TweenService:Create(cc, slow, {
    TintColor = Color3.fromRGB(255, 180, 180),
    Brightness = -0.3,
    Contrast = 0.35,
    Saturation = 0.6
}):Play()
TweenService:Create(blur, slow, {Size = 6}):Play()

task.wait(3)

for _, other in ipairs(Players:GetPlayers()) do
    if other ~= player and other.Character then
        for _, part in ipairs(other.Character:GetDescendants()) do
            if part:IsA("BasePart") or part:IsA("Decal") then
                pcall(function() part.LocalTransparencyModifier = 1 end)
            end
        end
    end
end

TweenService:Create(black, TweenInfo.new(1), {BackgroundTransparency = 0.7}):Play()
TweenService:Create(red, TweenInfo.new(1), {BackgroundTransparency = 0.6}):Play()
TweenService:Create(vignette, TweenInfo.new(1), {ImageTransparency = 0.3}):Play()
TweenService:Create(blur, TweenInfo.new(1), {Size = 4}):Play()

local char = player.Character
local rootPart = char and char:FindFirstChild("HumanoidRootPart")
local playerLight = Instance.new("PointLight")
playerLight.Color = Color3.fromRGB(255, 200, 200)
playerLight.Range = 22
playerLight.Brightness = 2
playerLight.Shadows = true
playerLight.Parent = rootPart or gui

god.TextTransparency = 0
god.TextStrokeTransparency = 0.4
timer.TextTransparency = 0

local textShake
textShake = RunService.RenderStepped:Connect(function()
    god.Position = UDim2.new(0, math.random(-6, 6), 0.28, math.random(-6, 6))
    god.Rotation = math.random(-2, 2)
end)

for i = TIMER, 0, -1 do
    timer.Text = tostring(i)
    if i <= 3 then
        god.TextColor3 = Color3.fromRGB(255, math.random(0, 40), math.random(0, 40))
        red.BackgroundColor3 = Color3.fromRGB(150, math.random(0, 25), math.random(0, 25))
        -- к концу ещё медленнее
        sound.PlaybackSpeed = SLOW_SPEED - (3 - i) * 0.05
    end
    task.wait(1)
end

textShake:Disconnect()
god.Text = "RUN."
god.Position = UDim2.new(0, 0, 0.28, 0)
god.Rotation = 0
timer.Text = ""

TweenService:Create(red, TweenInfo.new(1.5), {
    BackgroundColor3 = Color3.fromRGB(255, 0, 0),
    BackgroundTransparency = 0.5
}):Play()
TweenService:Create(blur, TweenInfo.new(1.5), {Size = 8}):Play()

-- ===== СУЩЕСТВО =====
local monster = Instance.new("Model")
monster.Name = "GodMonster_Local"

local mroot = Instance.new("Part")
mroot.Name = "HumanoidRootPart"
mroot.Size = Vector3.new(2, 2, 1)
mroot.Transparency = 1
mroot.CanCollide = false
mroot.Anchored = true
mroot.Parent = monster

local blackCol = Color3.fromRGB(10, 0, 0)
local redCol   = Color3.fromRGB(255, 15, 15)

local function part(name, size, color, mat, shape)
    local p = Instance.new("Part")
    p.Name = name
    p.Size = size
    p.Color = color
    p.Material = mat or Enum.Material.Slate
    p.Anchored = true
    p.CanCollide = false
    p.TopSurface = Enum.SurfaceType.Smooth
    p.BottomSurface = Enum.SurfaceType.Smooth
    if shape then p.Shape = shape end
    p.Parent = monster
    return p
end

local torso = part("Torso", Vector3.new(2.4, 3.6, 1.1), blackCol)
torso.CFrame = CFrame.new(0, 0.4, 0)
local head = part("Head", Vector3.new(1.5, 1.9, 1.3), blackCol)
head.CFrame = CFrame.new(0, 2.9, 0)
local jaw = part("Jaw", Vector3.new(1.2, 0.5, 1.0), blackCol)
jaw.CFrame = CFrame.new(0, 2.1, -0.2)

for _, side in ipairs({-1, 1}) do
    local hornBig = part("HornBig", Vector3.new(0.35, 1.8, 0.35), blackCol, Enum.Material.Slate, Enum.PartType.Cylinder)
    hornBig.CFrame = CFrame.new(side * 0.6, 4.1, 0) * CFrame.Angles(0, 0, math.rad(side * 30))
    local hornSmall = part("HornSmall", Vector3.new(0.22, 1.0, 0.22), blackCol, Enum.Material.Slate, Enum.PartType.Cylinder)
    hornSmall.CFrame = CFrame.new(side * 0.9, 3.6, 0.3) * CFrame.Angles(math.rad(20), 0, math.rad(side * 45))
    local eye = part("Eye", Vector3.new(0.38, 0.18, 0.15), redCol, Enum.Material.Neon)
    eye.CFrame = CFrame.new(side * 0.38, 2.7, -0.66)
    local arm = part("Arm", Vector3.new(0.5, 4.2, 0.5), blackCol)
    arm.CFrame = CFrame.new(side * 1.55, -0.3, 0)
    local claw = part("Claw", Vector3.new(0.7, 0.5, 0.7), blackCol)
    claw.CFrame = CFrame.new(side * 1.55, -2.6, -0.2)
    local leg = part("Leg", Vector3.new(0.65, 3.4, 0.65), blackCol)
    leg.CFrame = CFrame.new(side * 0.65, -3.4, 0)
    local foot = part("Foot", Vector3.new(0.9, 0.4, 1.2), blackCol)
    foot.CFrame = CFrame.new(side * 0.65, -5.0, -0.2)
end

for i = 1, 8 do
    local plate = part("Tatter", Vector3.new(0.3, 1.6 + math.random() * 1.5, 0.08), blackCol)
    plate.CFrame = CFrame.new(math.random(-14, 14) / 10, -1.5 - math.random() * 1.5, 0.6)
        * CFrame.Angles(math.rad(math.random(-15, 15)), 0, math.rad(math.random(-10, 10)))
end

local light = Instance.new("PointLight")
light.Color = redCol
light.Range = 16
light.Brightness = 2.5
light.Shadows = true
light.Parent = head

monster.PrimaryPart = mroot
monster.Parent = Workspace

if rootPart then
    local spawnPos = rootPart.Position - rootPart.CFrame.LookVector * 60 + Vector3.new(0, 5, 0)
    monster:PivotTo(CFrame.new(spawnPos))
end

-- ===== ПОГОНЯ =====
local caught = false
local closeSent = false

RunService.Heartbeat:Connect(function()
    local c = player.Character
    local cur = c and c:FindFirstChild("HumanoidRootPart")
    local mcur = monster:FindFirstChild("HumanoidRootPart")
    if not (cur and mcur) then return end

    local dist = (cur.Position - mcur.Position).Magnitude

    if not caught then
        local dir = (cur.Position - mcur.Position).Unit
        mcur.CFrame = CFrame.new(mcur.Position + dir * 0.8, Vector3.new(cur.Position.X, mcur.Position.Y, cur.Position.Z))
    else
        local facePos = cur.Position + (mcur.Position - cur.Position).Unit * 3.5
        mcur.CFrame = CFrame.new(facePos, Vector3.new(cur.Position.X, facePos.Y, cur.Position.Z))
    end

    if dist < 28 and not closeSent then
        closeSent = true
        sound.Volume = 1
        shakeAmt = 14
        TweenService:Create(cc, TweenInfo.new(1), {
            Contrast = 0.9, Brightness = -0.55, TintColor = Color3.fromRGB(255, 60, 60)
        }):Play()
        TweenService:Create(blur, TweenInfo.new(1), {Size = 14}):Play()
    end

    if dist < 6 and not caught then
        caught = true
        shakeAmt = 22
        sound.PlaybackSpeed = SLOW_SPEED * 0.6 -- ещё медленнее при контакте
        sound.Volume = 1

        TweenService:Create(red, TweenInfo.new(0.5), {
            BackgroundColor3 = Color3.fromRGB(180, 0, 0), BackgroundTransparency = 0.75
        }):Play()
        TweenService:Create(vignette, TweenInfo.new(0.5), {ImageTransparency = 0.1}):Play()
        TweenService:Create(blur, TweenInfo.new(0.5), {Size = 6}):Play()
        TweenService:Create(cc, TweenInfo.new(0.5), {
            Contrast = 1, Brightness = -0.35, TintColor = Color3.fromRGB(255, 80, 80)
        }):Play()

        god.Text = "..."
        god.TextTransparency = 0.4
        timer.Text = ""

        task.delay(KICK_DELAY, function()
            pcall(function() player:Kick("GOD IS HERE.") end)
        end)
    end
end)
