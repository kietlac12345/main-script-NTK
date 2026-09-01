--[[
    NTK HUB - Horizontal Rectangle Layout
    Author: NTK HUB
]]

-- Services
local CoreGui = game:GetService("CoreGui")
local TweenService = game:GetService("TweenService")
local UserInputService = game:GetService("UserInputService")

-- Remove existing GUI
local existing = CoreGui:FindFirstChild("NTKHubMain")
if existing then existing:Destroy() end

-- Create ScreenGui
local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Name = "NTKHubMain"
ScreenGui.ResetOnSpawn = false
ScreenGui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
ScreenGui.Parent = CoreGui

-- ===== MAIN FRAME - Horizontal Rectangle =====
local MainFrame = Instance.new("Frame")
MainFrame.Name = "MainFrame"
MainFrame.Size = UDim2.new(0, 780, 0, 420)
MainFrame.Position = UDim2.new(0.5, -390, 0.5, -210)
MainFrame.BackgroundColor3 = Color3.fromRGB(16, 14, 28)
MainFrame.BorderSizePixel = 0
MainFrame.Active = true
MainFrame.Draggable = true
MainFrame.ClipsDescendants = true
MainFrame.Parent = ScreenGui

local mainCorner = Instance.new("UICorner")
mainCorner.CornerRadius = UDim.new(0, 0)
mainCorner.Parent = MainFrame

local mainStroke = Instance.new("UIStroke")
mainStroke.Color = Color3.fromRGB(160, 120, 240)
mainStroke.Thickness = 2
mainStroke.Transparency = 0.2
mainStroke.Parent = MainFrame

local glowBg = Instance.new("ImageLabel")
glowBg.Size = UDim2.new(1.6, 0, 1.6, 0)
glowBg.Position = UDim2.new(-0.3, 0, -0.3, 0)
glowBg.BackgroundTransparency = 1
glowBg.Image = "rbxassetid://5028857083"
glowBg.ImageColor3 = Color3.fromRGB(120, 80, 220)
glowBg.ImageTransparency = 0.85
glowBg.Parent = MainFrame

local gradient = Instance.new("UIGradient")
gradient.Color = ColorSequence.new({
    ColorSequenceKeypoint.new(0, Color3.fromRGB(30, 24, 55)),
    ColorSequenceKeypoint.new(0.3, Color3.fromRGB(22, 18, 42)),
    ColorSequenceKeypoint.new(0.7, Color3.fromRGB(18, 15, 35)),
    ColorSequenceKeypoint.new(1, Color3.fromRGB(14, 12, 28))
})
gradient.Rotation = 135
gradient.Parent = MainFrame

-- ===== TOP BAR =====
local TopBar = Instance.new("Frame")
TopBar.Size = UDim2.new(1, 0, 0, 50)
TopBar.BackgroundColor3 = Color3.fromRGB(35, 28, 65)
TopBar.BorderSizePixel = 0
TopBar.Parent = MainFrame

local topCorner = Instance.new("UICorner")
topCorner.CornerRadius = UDim.new(0, 0)
topCorner.Parent = TopBar

local TitleLabel = Instance.new("TextLabel")
TitleLabel.Size = UDim2.new(1, -70, 0, 24)
TitleLabel.Position = UDim2.new(0, 14, 0, 4)
TitleLabel.BackgroundTransparency = 1
TitleLabel.Text = "✦ NTK HUB ✦"
TitleLabel.TextColor3 = Color3.fromRGB(210, 190, 255)
TitleLabel.Font = Enum.Font.GothamBold
TitleLabel.TextSize = 20
TitleLabel.TextXAlignment = Enum.TextXAlignment.Left
TitleLabel.Parent = TopBar

local SubtitleLabel = Instance.new("TextLabel")
SubtitleLabel.Size = UDim2.new(1, -70, 0, 14)
SubtitleLabel.Position = UDim2.new(0, 16, 0, 30)
SubtitleLabel.BackgroundTransparency = 1
SubtitleLabel.Text = "19 scripts — Click to load"
SubtitleLabel.TextColor3 = Color3.fromRGB(170, 160, 210)
SubtitleLabel.Font = Enum.Font.Gotham
SubtitleLabel.TextSize = 11
SubtitleLabel.TextXAlignment = Enum.TextXAlignment.Left
SubtitleLabel.Parent = TopBar

local decLine = Instance.new("Frame")
decLine.Size = UDim2.new(0.92, 0, 0, 2)
decLine.Position = UDim2.new(0.04, 0, 1, -2)
decLine.BackgroundColor3 = Color3.fromRGB(160, 120, 240)
decLine.BorderSizePixel = 0
decLine.Parent = TopBar

local decGrad = Instance.new("UIGradient")
decGrad.Color = ColorSequence.new({
    ColorSequenceKeypoint.new(0, Color3.fromRGB(160, 120, 240)),
    ColorSequenceKeypoint.new(0.5, Color3.fromRGB(220, 180, 255)),
    ColorSequenceKeypoint.new(1, Color3.fromRGB(160, 120, 240))
})
decGrad.Parent = decLine

-- ===== CLOSE BUTTON =====
local CloseButton = Instance.new("TextButton")
CloseButton.Size = UDim2.new(0, 30, 0, 30)
CloseButton.Position = UDim2.new(1, -38, 0, 10)
CloseButton.BackgroundColor3 = Color3.fromRGB(200, 50, 50)
CloseButton.BorderSizePixel = 0
CloseButton.Text = "✕"
CloseButton.TextColor3 = Color3.fromRGB(255, 255, 255)
CloseButton.Font = Enum.Font.GothamBold
CloseButton.TextSize = 14
CloseButton.Parent = TopBar

local closeCorner = Instance.new("UICorner")
closeCorner.CornerRadius = UDim.new(0, 0)
closeCorner.Parent = CloseButton

CloseButton.MouseEnter:Connect(function()
    TweenService:Create(CloseButton, TweenInfo.new(0.15), {
        BackgroundColor3 = Color3.fromRGB(230, 60, 60)
    }):Play()
end)
CloseButton.MouseLeave:Connect(function()
    TweenService:Create(CloseButton, TweenInfo.new(0.15), {
        BackgroundColor3 = Color3.fromRGB(200, 50, 50)
    }):Play()
end)

CloseButton.MouseButton1Click:Connect(function()
    local tween = TweenService:Create(MainFrame, TweenInfo.new(0.3), {BackgroundTransparency = 1})
    for _, child in ipairs(MainFrame:GetDescendants()) do
        if child:IsA("TextLabel") or child:IsA("TextButton") then
            TweenService:Create(child, TweenInfo.new(0.3), {
                TextTransparency = 1,
                BackgroundTransparency = child:IsA("TextButton") and 1 or child.BackgroundTransparency
            }):Play()
        elseif child:IsA("UIStroke") then
            TweenService:Create(child, TweenInfo.new(0.3), {Transparency = 1}):Play()
        end
    end
    tween:Play()
    tween.Completed:Connect(function() ScreenGui:Destroy() end)
end)

-- ===== SCROLL FRAME =====
local ScrollFrame = Instance.new("ScrollingFrame")
ScrollFrame.Size = UDim2.new(1, -16, 1, -70)
ScrollFrame.Position = UDim2.new(0, 8, 0, 56)
ScrollFrame.BackgroundTransparency = 1
ScrollFrame.BorderSizePixel = 0
ScrollFrame.CanvasSize = UDim2.new(0, 0, 0, 0)
ScrollFrame.ScrollBarThickness = 4
ScrollFrame.ScrollBarImageColor3 = Color3.fromRGB(160, 120, 240)
ScrollFrame.ScrollBarImageTransparency = 0.3
ScrollFrame.Parent = MainFrame

local ScrollLayout = Instance.new("UIListLayout")
ScrollLayout.Padding = UDim.new(0, 6)
ScrollLayout.HorizontalAlignment = Enum.HorizontalAlignment.Center
ScrollLayout.SortOrder = Enum.SortOrder.LayoutOrder
ScrollLayout.Parent = ScrollFrame

-- ===== CATEGORY HEADER =====
local function createCategoryHeader(parent, title, order)
    local header = Instance.new("Frame")
    header.Size = UDim2.new(0.95, 0, 0, 30)
    header.BackgroundColor3 = Color3.fromRGB(45, 38, 80)
    header.BorderSizePixel = 0
    header.Parent = parent
    header.LayoutOrder = order
    
    local headerCorner = Instance.new("UICorner")
    headerCorner.CornerRadius = UDim.new(0, 0)
    headerCorner.Parent = header
    
    local headerStroke = Instance.new("UIStroke")
    headerStroke.Color = Color3.fromRGB(160, 120, 240)
    headerStroke.Thickness = 1
    headerStroke.Transparency = 0.4
    headerStroke.Parent = header
    
    local headerText = Instance.new("TextLabel")
    headerText.Size = UDim2.new(1, -20, 1, 0)
    headerText.Position = UDim2.new(0, 10, 0, 0)
    headerText.BackgroundTransparency = 1
    headerText.Text = title
    headerText.TextColor3 = Color3.fromRGB(210, 190, 255)
    headerText.Font = Enum.Font.GothamBold
    headerText.TextSize = 13
    headerText.TextXAlignment = Enum.TextXAlignment.Left
    headerText.Parent = header
    
    local countBadge = Instance.new("TextLabel")
    countBadge.Size = UDim2.new(0, 32, 0, 18)
    countBadge.Position = UDim2.new(1, -40, 0.5, -9)
    countBadge.BackgroundColor3 = Color3.fromRGB(100, 70, 180)
    countBadge.BorderSizePixel = 0
    countBadge.Text = ""
    countBadge.TextColor3 = Color3.fromRGB(255, 255, 255)
    countBadge.Font = Enum.Font.GothamBold
    countBadge.TextSize = 9
    countBadge.Parent = header
    
    local badgeCorner = Instance.new("UICorner")
    badgeCorner.CornerRadius = UDim.new(0, 0)
    badgeCorner.Parent = countBadge
    
    return header, countBadge
end

-- ===== SCRIPT BUTTON =====
local function createScriptButton(parent, title, desc, callback, order)
    local btn = Instance.new("TextButton")
    btn.Size = UDim2.new(0.93, 0, 0, 38)
    btn.BackgroundColor3 = Color3.fromRGB(30, 26, 52)
    btn.BorderSizePixel = 0
    btn.Text = ""
    btn.Parent = parent
    btn.LayoutOrder = order
    
    local btnCorner = Instance.new("UICorner")
    btnCorner.CornerRadius = UDim.new(0, 0)
    btnCorner.Parent = btn
    
    local btnStroke = Instance.new("UIStroke")
    btnStroke.Color = Color3.fromRGB(120, 90, 200)
    btnStroke.Thickness = 1
    btnStroke.Transparency = 0.6
    btnStroke.Parent = btn
    
    local accentBar = Instance.new("Frame")
    accentBar.Size = UDim2.new(0, 3, 1, 0)
    accentBar.BackgroundColor3 = Color3.fromRGB(160, 120, 240)
    accentBar.BorderSizePixel = 0
    accentBar.Parent = btn
    
    local btnTitle = Instance.new("TextLabel")
    btnTitle.Size = UDim2.new(1, -30, 0, 16)
    btnTitle.Position = UDim2.new(0, 12, 0, 3)
    btnTitle.BackgroundTransparency = 1
    btnTitle.Text = title
    btnTitle.TextColor3 = Color3.fromRGB(255, 255, 255)
    btnTitle.Font = Enum.Font.GothamBold
    btnTitle.TextSize = 12
    btnTitle.TextXAlignment = Enum.TextXAlignment.Left
    btnTitle.Parent = btn
    
    local btnDesc = Instance.new("TextLabel")
    btnDesc.Size = UDim2.new(1, -30, 0, 12)
    btnDesc.Position = UDim2.new(0, 12, 0, 21)
    btnDesc.BackgroundTransparency = 1
    btnDesc.Text = desc
    btnDesc.TextColor3 = Color3.fromRGB(165, 160, 195)
    btnDesc.Font = Enum.Font.Gotham
    btnDesc.TextSize = 10
    btnDesc.TextXAlignment = Enum.TextXAlignment.Left
    btnDesc.Parent = btn
    
    btn.MouseEnter:Connect(function()
        TweenService:Create(btn, TweenInfo.new(0.1), {
            BackgroundColor3 = Color3.fromRGB(50, 42, 95)
        }):Play()
        TweenService:Create(btnStroke, TweenInfo.new(0.1), {
            Transparency = 0
        }):Play()
        TweenService:Create(accentBar, TweenInfo.new(0.1), {
            BackgroundColor3 = Color3.fromRGB(220, 180, 255)
        }):Play()
    end)
    btn.MouseLeave:Connect(function()
        TweenService:Create(btn, TweenInfo.new(0.1), {
            BackgroundColor3 = Color3.fromRGB(30, 26, 52)
        }):Play()
        TweenService:Create(btnStroke, TweenInfo.new(0.1), {
            Transparency = 0.6
        }):Play()
        TweenService:Create(accentBar, TweenInfo.new(0.1), {
            BackgroundColor3 = Color3.fromRGB(160, 120, 240)
        }):Play()
    end)
    
    btn.MouseButton1Click:Connect(callback)
    return btn
end

-- ===== SCRIPT LOADER =====
local function loadScript(url, config)
    return function()
        local tween = TweenService:Create(MainFrame, TweenInfo.new(0.3), {BackgroundTransparency = 1})
        for _, child in ipairs(MainFrame:GetDescendants()) do
            if child:IsA("TextLabel") or child:IsA("TextButton") then
                TweenService:Create(child, TweenInfo.new(0.3), {
                    TextTransparency = 1,
                    BackgroundTransparency = child:IsA("TextButton") and 1 or child.BackgroundTransparency
                }):Play()
            elseif child:IsA("UIStroke") then
                TweenService:Create(child, TweenInfo.new(0.3), {Transparency = 1}):Play()
            end
        end
        tween:Play()
        tween.Completed:Connect(function()
            ScreenGui:Destroy()
            pcall(function()
                if config then
                    for k, v in pairs(config) do
                        getgenv()[k] = v
                    end
                end
                loadstring(game:HttpGet(url))()
            end)
        end)
    end
end

-- ===== UPDATE CANVAS =====
local function updateCanvas()
    ScrollFrame.CanvasSize = UDim2.new(0, 0, 0, ScrollLayout.AbsoluteContentSize.Y + 10)
end
ScrollLayout:GetPropertyChangedSignal("AbsoluteContentSize"):Connect(updateCanvas)

-- ===== BUILD SCRIPTS =====
local orderCounter = 1

-- ===== TSB CATEGORY =====
local tsbHeader, tsbBadge = createCategoryHeader(ScrollFrame, "⚔️ THE STRONGEST BATTLEGROUNDS", orderCounter)
tsbBadge.Text = "4"
orderCounter = orderCounter + 1

local tsbScripts = {
    {"Rank Fram TSB", "Auto rank 1v1/2v2/3v3", "https://gitlab.com/zkay404-group/ProjectYielding/-/raw/main/ZKRankFarm", {AutoExecute = true, RankMode = "1v1s", RankParty = false, QueueMethod = "Direct"}},
    {"V1 - NTK Hub", "Fram kill (GitHub)", "https://raw.githubusercontent.com/kietkidlo-hub/script-fram-kill-tsb/refs/heads/main/README.md"},
    {"V2 - ProjectYielding", "Fram kill (GitLab)", "https://gitlab.com/zkay404-group/ProjectYielding/-/raw/main/ZKPublicFarm"},
    {"SUPA TECH TSB", "Advanced TSB script", "https://api.getpolsec.com/scripts/hosted/2753546c83053761e44664d36ffe5035d6e20fc8aee1d19f0eb7b933974ae537.lua"},
}

for i, data in ipairs(tsbScripts) do
    createScriptButton(ScrollFrame, data[1], data[2], loadScript(data[3], data[4]), orderCounter)
    orderCounter = orderCounter + 1
end

-- ===== BLOX FRUITS CATEGORY =====
local bfHeader, bfBadge = createCategoryHeader(ScrollFrame, "🍎 BLOX FRUITS", orderCounter)
bfBadge.Text = "4"
orderCounter = orderCounter + 1

local bfScripts = {
    {"Fake Gifter", "Fake gifter for Blox Fruits", "https://api.luarmor.net/files/v4/loaders/edf8e1697953b50b341cfcbc21eef492.lua"},
    {"Kaitun Script", "Evo race, haki, swords", "https://raw.githubusercontent.com/realkidhub/realkid/refs/heads/main/kaitun.lua", {
        Quest = {["Evo Race V1"] = true, ["Evo Race V2"] = true, ["RGB Haki"] = true, ["Pull Lerver"] = true},
        Sword = {"Dual-Headed Blade", "Smoke Admiral", "Wardens Sword", "Cutlass", "Katana", "Dual Katana", "Triple Katana", "Iron Mace", "Saber", "Pole (1st Form)", "Gravity Blade", "Longsword", "Rengoku", "Midnight Blade", "Soul Cane", "Bisento", "Yama", "Tushita", "Cursed Dual Katana"},
        Gun = {"Skull Guitar", "Kabucha", "Venom Bow", "Musket", "Flintlock", "Refined Slingshot", "Magma Blaster", "Dual Flintlock", "Cannon", "Bizarre Revolver", "Bazooka"},
        ["Bypass TP"] = true, ["Auto Active Race V4"] = true, ["FPS Limit"] = 15, ["Boost FPS"] = true,
    }},
    {"Blox Fruits Script", "by realkidhub", "https://raw.githubusercontent.com/realkidhub/Games/refs/heads/main/BloxFruits.lua"},
    {"PVP Blox Fruit", "PVP mode for Blox Fruits", "https://raw.githubusercontent.com/hermanos-dev/hermanos-hub/refs/heads/main/Loader.lua", {script_mode = "PVP"}},
}

for i, data in ipairs(bfScripts) do
    createScriptButton(ScrollFrame, data[1], data[2], loadScript(data[3], data[4]), orderCounter)
    orderCounter = orderCounter + 1
end

-- ===== TROLL TOOLS CATEGORY =====
local trollHeader, trollBadge = createCategoryHeader(ScrollFrame, "🛠️ TROLL TOOLS", orderCounter)
trollBadge.Text = "4"
orderCounter = orderCounter + 1

local trollScripts = {
    {"Touch Fling", "Fling players on touch", "https://raw.githubusercontent.com/kietkidlo-hub/script-touch-fling/refs/heads/main/README.md"},
    {"Ring Script", "Ring tool", "https://raw.githubusercontent.com/kietkidlo-hub/script-ring-NTK-/refs/heads/main/README.md"},
    {"FLY Script", "Fly anywhere", "https://raw.githubusercontent.com/kietkidlo-hub/script-fly-NTK-HUB/refs/heads/main/README.md"},
    {"AIM (PC)", "Aim assist for PC", "https://raw.githubusercontent.com/kietkidlo-hub/script-AIM-PC/refs/heads/main/README.md"},
}

for i, data in ipairs(trollScripts) do
    createScriptButton(ScrollFrame, data[1], data[2], loadScript(data[3], data[4]), orderCounter)
    orderCounter = orderCounter + 1
end

-- ===== GAG2 CATEGORY =====
local gag2Header, gag2Badge = createCategoryHeader(ScrollFrame, "📱 GAG2", orderCounter)
gag2Badge.Text = "3"
orderCounter = orderCounter + 1

local gag2Scripts = {
    {"Fake Gifter GAG2", "Fake gifter for GAG2", "https://api.luarmor.net/files/v4/loaders/4f220b52905d70e4e7600fcc073fac2a.lua"},
    {"Gag2 Script", "GAG2 by realkidhub", "https://raw.githubusercontent.com/realkidhub/Games/refs/heads/main/GaG2.lua"},
    {"Gag2 Spammer", "Spam GAG2 chat", "https://api.luarmor.net/files/v4/loaders/fae8f394bac9be26d78ab2f0864239bc.lua"},
}

for i, data in ipairs(gag2Scripts) do
    createScriptButton(ScrollFrame, data[1], data[2], loadScript(data[3], data[4]), orderCounter)
    orderCounter = orderCounter + 1
end

-- ===== ANIMAL HOSPITAL CATEGORY =====
local ahHeader, ahBadge = createCategoryHeader(ScrollFrame, "🏥 ANIMAL HOSPITAL", orderCounter)
ahBadge.Text = "2"
orderCounter = orderCounter + 1

local ahScripts = {
    {"Animal Hospital Fake", "Fake gifter (old)", "https://api.luarmor.net/files/v4/loaders/a56c4dea1088d8f4bf2746ff90060053.lua"},
    {"FN Animal Hospital", "by caomod2077", "https://raw.githubusercontent.com/caomod2077/Script/refs/heads/main/FN_AnimalHospital.lua"},
}

for i, data in ipairs(ahScripts) do
    createScriptButton(ScrollFrame, data[1], data[2], loadScript(data[3], data[4]), orderCounter)
    orderCounter = orderCounter + 1
end

-- ===== OTHER GAMES CATEGORY =====
local otherHeader, otherBadge = createCategoryHeader(ScrollFrame, "🎮 OTHER GAMES", orderCounter)
otherBadge.Text = "2"
orderCounter = orderCounter + 1

local otherScripts = {
    {"Dead Zone", "Script for Dead Zone", "https://raw.githubusercontent.com/kietkidlo-hub/script-dead-zone-NTK-HUB/refs/heads/main/README.md"},
    {"Steal An Egg", "Steal egg script", "https://raw.githubusercontent.com/caomod2077/Script/refs/heads/main/Fn-stealanegg.lua"},
}

for i, data in ipairs(otherScripts) do
    createScriptButton(ScrollFrame, data[1], data[2], loadScript(data[3], data[4]), orderCounter)
    orderCounter = orderCounter + 1
end

-- ===== FOOTER =====
local Footer = Instance.new("Frame")
Footer.Size = UDim2.new(1, 0, 0, 20)
Footer.Position = UDim2.new(0, 0, 1, -20)
Footer.BackgroundColor3 = Color3.fromRGB(25, 22, 45)
Footer.BorderSizePixel = 0
Footer.Parent = MainFrame

local footerCorner = Instance.new("UICorner")
footerCorner.CornerRadius = UDim.new(0, 0)
footerCorner.Parent = Footer

local footerText = Instance.new("TextLabel")
footerText.Size = UDim2.new(1, 0, 1, 0)
footerText.BackgroundTransparency = 1
footerText.Text = "✦ NTK HUB — 19 scripts loaded ✦"
footerText.TextColor3 = Color3.fromRGB(120, 110, 160)
footerText.Font = Enum.Font.Gotham
footerText.TextSize = 10
footerText.Parent = Footer

-- ===== UPDATE CANVAS =====
task.wait(0.1)
updateCanvas()

-- ===== DRAGGING =====
local dragging = false
local dragInput, dragStart, startPos

MainFrame.InputBegan:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
        dragging = true
        dragStart = input.Position
        startPos = MainFrame.Position
        input.Changed:Connect(function()
            if input.UserInputState == Enum.UserInputState.End then
                dragging = false
            end
        end)
    end
end)

MainFrame.InputChanged:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseMovement or input.UserInputType == Enum.UserInputType.Touch then
        dragInput = input
    end
end)

UserInputService.InputChanged:Connect(function(input)
    if input == dragInput and dragging then
        local delta = input.Position - dragStart
        MainFrame.Position = UDim2.new(startPos.X.Scale, startPos.X.Offset + delta.X, startPos.Y.Scale, startPos.Y.Offset + delta.Y)
    end
end)

-- ===== OPEN ANIMATION =====
MainFrame.Size = UDim2.new(0, 780, 0, 0)
MainFrame.Position = UDim2.new(0.5, -390, 0.5, 0)
TweenService:Create(MainFrame, TweenInfo.new(0.5, Enum.EasingStyle.Back, Enum.EasingDirection.Out), {
    Size = UDim2.new(0, 780, 0, 420),
    Position = UDim2.new(0.5, -390, 0.5, -210)
}):Play()

print("[NTK HUB] Horizontal Rectangle Layout Loaded — 19 scripts")
