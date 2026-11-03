-- ====================================================
-- 🍄 MUSHROOM HUB (PREMIUM SELLER EDITION)
-- 👑 Created & Developed by Kit
-- 🔑 Key Access: ae24_56as
-- ====================================================

local Players = game:GetService("Players")
local ReplicatedStorage = game:GetService("ReplicatedStorage")
local StarterGui = game:GetService("StarterGui")
local Workspace = game:GetService("Workspace")
local TweenService = game:GetService("TweenService")

local LocalPlayer = Players.LocalPlayer
local PlayerGui = LocalPlayer:WaitForChild("PlayerGui")

-- เคลียร์ UI เก่าก่อนรันเพื่อความลื่นไหล
if PlayerGui:FindFirstChild("KitMushroomUI") then
    PlayerGui.KitMushroomUI:Destroy()
end

local CorrectKey = "ae24_56as"
local CurrentLang = "TH"
local AutoPlantActive = false
local SelectedSeedForAuto = "Brown Mushroom Seed"

-- 1. Main ScreenGui
local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Name = "KitMushroomUI"
ScreenGui.ResetOnSpawn = false
ScreenGui.Parent = PlayerGui

-- ----------------------------------------------------
-- 🔑 KEY GATE WINDOW (หน้าต่างรับคีย์สุดหรู)
-- ----------------------------------------------------
local KeyFrame = Instance.new("Frame")
KeyFrame.Name = "KeyFrame"
KeyFrame.Size = UDim2.new(0, 300, 0, 190)
KeyFrame.Position = UDim2.new(0.5, -150, 0.4, -95)
KeyFrame.BackgroundColor3 = Color3.fromRGB(18, 22, 20)
KeyFrame.BorderSizePixel = 0
KeyFrame.Active = true
KeyFrame.Draggable = true
KeyFrame.Parent = ScreenGui

Instance.new("UICorner", KeyFrame).CornerRadius = UDim.new(0, 12)
local KeyStroke = Instance.new("UIStroke", KeyFrame)
KeyStroke.Color = Color3.fromRGB(46, 204, 113)
KeyStroke.Thickness = 2

local KeyHeader = Instance.new("Frame", KeyFrame)
KeyHeader.Size = UDim2.new(1, 0, 0, 40)
KeyHeader.BackgroundColor3 = Color3.fromRGB(24, 30, 26)
Instance.new("UICorner", KeyHeader).CornerRadius = UDim.new(0, 12)

local KeyTitle = Instance.new("TextLabel", KeyHeader)
KeyTitle.Size = UDim2.new(1, 0, 1, 0)
KeyTitle.BackgroundTransparency = 1
KeyTitle.Text = "🔒 KEY VERIFICATION | BY KIT"
KeyTitle.TextColor3 = Color3.fromRGB(46, 204, 113)
KeyTitle.TextSize = 14
KeyTitle.Font = Enum.Font.FredokaOne

local KeyInputBox = Instance.new("TextBox", KeyFrame)
KeyInputBox.Size = UDim2.new(0.85, 0, 0, 38)
KeyInputBox.Position = UDim2.new(0.075, 0, 0.32, 0)
KeyInputBox.BackgroundColor3 = Color3.fromRGB(28, 34, 31)
KeyInputBox.Text = ""
KeyInputBox.PlaceholderText = "Enter License Key..."
KeyInputBox.TextColor3 = Color3.fromRGB(255, 255, 255)
KeyInputBox.TextSize = 13
KeyInputBox.Font = Enum.Font.SourceSans
KeyInputBox.ClearTextOnFocus = false
Instance.new("UICorner", KeyInputBox).CornerRadius = UDim.new(0, 8)
local InputStroke = Instance.new("UIStroke", KeyInputBox)
InputStroke.Color = Color3.fromRGB(40, 50, 44)
InputStroke.Thickness = 1

local VerifyBtn = Instance.new("TextButton", KeyFrame)
VerifyBtn.Size = UDim2.new(0.85, 0, 0, 38)
VerifyBtn.Position = UDim2.new(0.075, 0, 0.65, 0)
VerifyBtn.BackgroundColor3 = Color3.fromRGB(46, 204, 113)
VerifyBtn.Text = "UNLOCK SYSTEM"
VerifyBtn.TextColor3 = Color3.fromRGB(15, 20, 17)
VerifyBtn.TextSize = 14
VerifyBtn.Font = Enum.Font.FredokaOne
Instance.new("UICorner", VerifyBtn).CornerRadius = UDim.new(0, 8)

-- ----------------------------------------------------
-- 💎 MAIN SYSTEM WINDOW (หน้าต่างหลักพรีเมียม)
-- ----------------------------------------------------
local MainFrame = Instance.new("Frame")
MainFrame.Name = "MainFrame"
MainFrame.Size = UDim2.new(0, 400, 0, 270)
MainFrame.Position = UDim2.new(0.5, -200, 0.4, -135)
MainFrame.BackgroundColor3 = Color3.fromRGB(15, 18, 16)
MainFrame.BorderSizePixel = 0
MainFrame.Active = true
MainFrame.Draggable = true
MainFrame.Visible = false
MainFrame.Parent = ScreenGui

Instance.new("UICorner", MainFrame).CornerRadius = UDim.new(0, 12)
local MainStroke = Instance.new("UIStroke", MainFrame)
MainStroke.Color = Color3.fromRGB(46, 204, 113)
MainStroke.Thickness = 2

-- Header Bar
local HeaderBar = Instance.new("Frame", MainFrame)
HeaderBar.Size = UDim2.new(1, 0, 0, 40)
HeaderBar.BackgroundColor3 = Color3.fromRGB(22, 28, 24)
Instance.new("UICorner", HeaderBar).CornerRadius = UDim.new(0, 12)

local MainTitle = Instance.new("TextLabel", HeaderBar)
MainTitle.Size = UDim2.new(1, -50, 1, 0)
MainTitle.Position = UDim2.new(0, 15, 0, 0)
MainTitle.BackgroundTransparency = 1
MainTitle.Text = "🍄 MUSHROOM HUB  [V2.0]  |  by Kit"
MainTitle.TextColor3 = Color3.fromRGB(46, 204, 113)
MainTitle.TextSize = 14
MainTitle.Font = Enum.Font.FredokaOne
MainTitle.TextXAlignment = Enum.TextXAlignment.Left

local MinimizeBtn = Instance.new("TextButton", HeaderBar)
MinimizeBtn.Size = UDim2.new(0, 30, 0, 30)
MinimizeBtn.Position = UDim2.new(1, -35, 0, 5)
MinimizeBtn.BackgroundTransparency = 1
MinimizeBtn.Text = "—"
MinimizeBtn.TextColor3 = Color3.fromRGB(180, 180, 180)
MinimizeBtn.TextSize = 18
MinimizeBtn.Font = Enum.Font.SourceSansBold

-- 🟢 Floating Toggle Button (ปุ่มย่อ KIT ทรงกลมนีออน)
local ToggleBtn = Instance.new("TextButton")
ToggleBtn.Name = "ToggleButton"
ToggleBtn.Size = UDim2.new(0, 45, 0, 45)
ToggleBtn.Position = UDim2.new(0, 15, 0.25, 0)
ToggleBtn.BackgroundColor3 = Color3.fromRGB(22, 28, 24)
ToggleBtn.Text = "KIT"
ToggleBtn.TextColor3 = Color3.fromRGB(46, 204, 113)
ToggleBtn.TextSize = 15
ToggleBtn.Font = Enum.Font.FredokaOne
ToggleBtn.Active = true
ToggleBtn.Draggable = true
ToggleBtn.Visible = false
ToggleBtn.Parent = ScreenGui

Instance.new("UICorner", ToggleBtn).CornerRadius = UDim.new(1, 0)
local ToggleStroke = Instance.new("UIStroke", ToggleBtn)
ToggleStroke.Color = Color3.fromRGB(46, 204, 113)
ToggleStroke.Thickness = 2.5

ToggleBtn.MouseButton1Click:Connect(function()
    MainFrame.Visible = not MainFrame.Visible
end)

MinimizeBtn.MouseButton1Click:Connect(function()
    MainFrame.Visible = false
end)

-- Sidebar Tab Container
local TabHolder = Instance.new("Frame", MainFrame)
TabHolder.Size = UDim2.new(0, 105, 1, -48)
TabHolder.Position = UDim2.new(0, 6, 0, 42)
TabHolder.BackgroundColor3 = Color3.fromRGB(20, 25, 22)
Instance.new("UICorner", TabHolder).CornerRadius = UDim.new(0, 8)

local TabButtons = {}
local function CreateTabBtn(name, posIndex)
    local Btn = Instance.new("TextButton", TabHolder)
    Btn.Size = UDim2.new(0.9, 0, 0, 24)
    Btn.Position = UDim2.new(0.05, 0, 0, 5 + (posIndex - 1) * 27)
    Btn.BackgroundColor3 = posIndex == 1 and Color3.fromRGB(46, 204, 113) or Color3.fromRGB(28, 34, 30)
    Btn.Text = name
    Btn.TextColor3 = posIndex == 1 and Color3.fromRGB(15, 20, 17) or Color3.fromRGB(200, 200, 200)
    Btn.TextSize = 10
    Btn.Font = Enum.Font.SourceSansBold
    Instance.new("UICorner", Btn).CornerRadius = UDim.new(0, 5)
    return Btn
end

local Tab1Btn = CreateTabBtn("⚙️ ตั้งค่า", 1)
local Tab2Btn = CreateTabBtn("🍄 เสกเห็ด", 2)
local Tab3Btn = CreateTabBtn("🌱 ปลูกเห็ด", 3)
local Tab4Btn = CreateTabBtn("🧺 เก็บเห็ด", 4)
local Tab5Btn = CreateTabBtn("🛒 ขายเห็ด", 5)

-- Content Frame
local ContentFrame = Instance.new("Frame", MainFrame)
ContentFrame.Size = UDim2.new(1, -125, 1, -48)
ContentFrame.Position = UDim2.new(0, 116, 0, 42)
ContentFrame.BackgroundTransparency = 1

-- Menu 1: Settings
local SettingsFrame = Instance.new("Frame", ContentFrame)
SettingsFrame.Size = UDim2.new(1, 0, 1, 0)
SettingsFrame.BackgroundTransparency = 1

local LangTitle = Instance.new("TextLabel", SettingsFrame)
LangTitle.Size = UDim2.new(1, 0, 0, 25)
LangTitle.BackgroundTransparency = 1
LangTitle.Text = "🌐 SELECT LANGUAGE"
LangTitle.TextColor3 = Color3.fromRGB(46, 204, 113)
LangTitle.TextSize = 12
LangTitle.Font = Enum.Font.FredokaOne

local LangTHBtn = Instance.new("TextButton", SettingsFrame)
LangTHBtn.Size = UDim2.new(1, 0, 0, 30)
LangTHBtn.Position = UDim2.new(0, 0, 0, 28)
LangTHBtn.BackgroundColor3 = Color3.fromRGB(46, 204, 113)
LangTHBtn.Text = "🇹🇭 ภาษาไทย"
LangTHBtn.TextColor3 = Color3.fromRGB(15, 20, 17)
LangTHBtn.TextSize = 12
LangTHBtn.Font = Enum.Font.SourceSansBold
Instance.new("UICorner", LangTHBtn).CornerRadius = UDim.new(0, 6)

local LangENBtn = Instance.new("TextButton", SettingsFrame)
LangENBtn.Size = UDim2.new(1, 0, 0, 30)
LangENBtn.Position = UDim2.new(0, 0, 0, 64)
LangENBtn.BackgroundColor3 = Color3.fromRGB(28, 34, 30)
LangENBtn.Text = "🇬🇧 English"
LangENBtn.TextColor3 = Color3.fromRGB(200, 200, 200)
LangENBtn.TextSize = 12
LangENBtn.Font = Enum.Font.SourceSansBold
Instance.new("UICorner", LangENBtn).CornerRadius = UDim.new(0, 6)

local DevCard = Instance.new("Frame", SettingsFrame)
DevCard.Size = UDim2.new(1, 0, 0, 45)
DevCard.Position = UDim2.new(0, 0, 0, 110)
DevCard.BackgroundColor3 = Color3.fromRGB(22, 28, 24)
Instance.new("UICorner", DevCard).CornerRadius = UDim.new(0, 6)

local DevText = Instance.new("TextLabel", DevCard)
DevText.Size = UDim2.new(1, 0, 1, 0)
DevText.BackgroundTransparency = 1
DevText.Text = "👑 Developer: by Kit\nStatus: Premium Verified ✔️"
DevText.TextColor3 = Color3.fromRGB(150, 170, 160)
DevText.TextSize = 11
DevText.Font = Enum.Font.SourceSans

-- Menu 2: Spawn Mushrooms
local ScrollFrame = Instance.new("ScrollingFrame", ContentFrame)
ScrollFrame.Size = UDim2.new(1, 0, 1, 0)
ScrollFrame.BackgroundTransparency = 1
ScrollFrame.ScrollBarThickness = 3
ScrollFrame.Visible = false

local UIList = Instance.new("UIListLayout", ScrollFrame)
UIList.SortOrder = Enum.SortOrder.LayoutOrder
UIList.Padding = UDim.new(0, 4)

-- Menu 3: Auto Plant
local AutoPlantFrame = Instance.new("Frame", ContentFrame)
AutoPlantFrame.Size = UDim2.new(1, 0, 1, 0)
AutoPlantFrame.BackgroundTransparency = 1
AutoPlantFrame.Visible = false

local AutoPlantBtn = Instance.new("TextButton", AutoPlantFrame)
AutoPlantBtn.Size = UDim2.new(1, 0, 0, 38)
AutoPlantBtn.Position = UDim2.new(0, 0, 0, 10)
AutoPlantBtn.BackgroundColor3 = Color3.fromRGB(192, 57, 43)
AutoPlantBtn.Text = "🌱 AUTO PLANT: OFF"
AutoPlantBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
AutoPlantBtn.TextSize = 12
AutoPlantBtn.Font = Enum.Font.FredokaOne
Instance.new("UICorner", AutoPlantBtn).CornerRadius = UDim.new(0, 6)

local AutoDesc = Instance.new("TextLabel", AutoPlantFrame)
AutoDesc.Size = UDim2.new(1, 0, 0, 50)
AutoDesc.Position = UDim2.new(0, 0, 0, 58)
AutoDesc.BackgroundTransparency = 1
AutoDesc.Text = "ระบบจะทำการซื้อเมล็ดและวิ่งกดแปลงปลูกในสวนให้อัตโนมัติในสปีดสูงสุด"
AutoDesc.TextColor3 = Color3.fromRGB(160, 175, 165)
AutoDesc.TextSize = 11
AutoDesc.Font = Enum.Font.SourceSans
AutoDesc.TextWrapped = true

-- Menu 4: Harvest
local CollectFrame = Instance.new("Frame", ContentFrame)
CollectFrame.Size = UDim2.new(1, 0, 1, 0)
CollectFrame.BackgroundTransparency = 1
CollectFrame.Visible = false

local CollectBtn = Instance.new("TextButton", CollectFrame)
CollectBtn.Size = UDim2.new(1, 0, 0, 38)
CollectBtn.Position = UDim2.new(0, 0, 0, 10)
CollectBtn.BackgroundColor3 = Color3.fromRGB(46, 204, 113)
CollectBtn.Text = "🧺 เก็บเห็ดทั้งหมดในสวน"
CollectBtn.TextColor3 = Color3.fromRGB(15, 20, 17)
CollectBtn.TextSize = 13
CollectBtn.Font = Enum.Font.FredokaOne
Instance.new("UICorner", CollectBtn).CornerRadius = UDim.new(0, 6)

-- Menu 5: Sell
local SellFrame = Instance.new("Frame", ContentFrame)
SellFrame.Size = UDim2.new(1, 0, 1, 0)
SellFrame.BackgroundTransparency = 1
SellFrame.Visible = false

local SellAllInvBtn = Instance.new("TextButton", SellFrame)
SellAllInvBtn.Size = UDim2.new(1, 0, 0, 28)
SellAllInvBtn.Position = UDim2.new(0, 0, 0, 5)
SellAllInvBtn.BackgroundColor3 = Color3.fromRGB(46, 204, 113)
SellAllInvBtn.Text = "📦 ขายทั้งหมดในคลัง"
SellAllInvBtn.TextColor3 = Color3.fromRGB(15, 20, 17)
SellAllInvBtn.TextSize = 11
SellAllInvBtn.Font = Enum.Font.SourceSansBold
Instance.new("UICorner", SellAllInvBtn).CornerRadius = UDim.new(0, 5)

local SellHandBtn = Instance.new("TextButton", SellFrame)
SellHandBtn.Size = UDim2.new(1, 0, 0, 28)
SellHandBtn.Position = UDim2.new(0, 0, 0, 38)
SellHandBtn.BackgroundColor3 = Color3.fromRGB(28, 34, 30)
SellHandBtn.Text = "✋ ขายเห็ดในมือ"
SellHandBtn.TextColor3 = Color3.fromRGB(200, 200, 200)
SellHandBtn.TextSize = 11
SellHandBtn.Font = Enum.Font.SourceSansBold
Instance.new("UICorner", SellHandBtn).CornerRadius = UDim.new(0, 5)

local CheckPriceBtn = Instance.new("TextButton", SellFrame)
CheckPriceBtn.Size = UDim2.new(1, 0, 0, 28)
CheckPriceBtn.Position = UDim2.new(0, 0, 0, 71)
CheckPriceBtn.BackgroundColor3 = Color3.fromRGB(28, 34, 30)
CheckPriceBtn.Text = "🔍 ตรวจสอบราคาเห็ด"
CheckPriceBtn.TextColor3 = Color3.fromRGB(200, 200, 200)
CheckPriceBtn.TextSize = 11
CheckPriceBtn.Font = Enum.Font.SourceSansBold
Instance.new("UICorner", CheckPriceBtn).CornerRadius = UDim.new(0, 5)

local BackBtn = Instance.new("TextButton", SellFrame)
BackBtn.Size = UDim2.new(1, 0, 0, 28)
BackBtn.Position = UDim2.new(0, 0, 0, 104)
BackBtn.BackgroundColor3 = Color3.fromRGB(192, 57, 43)
BackBtn.Text = "⬅️ กลับไปที่เดิม (ตั้งค่า)"
BackBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
BackBtn.TextSize = 11
BackBtn.Font = Enum.Font.SourceSansBold
Instance.new("UICorner", BackBtn).CornerRadius = UDim.new(0, 5)

-- Tab Switcher Manager
local function ResetTabs()
    local btns = {Tab1Btn, Tab2Btn, Tab3Btn, Tab4Btn, Tab5Btn}
    local frames = {SettingsFrame, ScrollFrame, AutoPlantFrame, CollectFrame, SellFrame}
    for i = 1, 5 do
        btns[i].BackgroundColor3 = Color3.fromRGB(28, 34, 30)
        btns[i].TextColor3 = Color3.fromRGB(200, 200, 200)
        frames[i].Visible = false
    end
end

local function SetActiveTab(btn, frame)
    ResetTabs()
    btn.BackgroundColor3 = Color3.fromRGB(46, 204, 113)
    btn.TextColor3 = Color3.fromRGB(15, 20, 17)
    frame.Visible = true
end

Tab1Btn.MouseButton1Click:Connect(function() SetActiveTab(Tab1Btn, SettingsFrame) end)
Tab2Btn.MouseButton1Click:Connect(function() SetActiveTab(Tab2Btn, ScrollFrame) end)
Tab3Btn.MouseButton1Click:Connect(function() SetActiveTab(Tab3Btn, AutoPlantFrame) end)
Tab4Btn.MouseButton1Click:Connect(function() SetActiveTab(Tab4Btn, CollectFrame) end)
Tab5Btn.MouseButton1Click:Connect(function() SetActiveTab(Tab5Btn, SellFrame) end)
BackBtn.MouseButton1Click:Connect(function() SetActiveTab(Tab1Btn, SettingsFrame) end)

-- Seeds Data List
local seedsData = {
    {en = "Brown Mushroom Seed", th = "เมล็ดเห็ดน้ำตาล"},
    {en = "Red Mushroom Seed", th = "เมล็ดเห็ดแดง"},
    {en = "Chestnut Cap Seed", th = "เมล็ดเห็ดเกาลัด"},
    {en = "Yellow Button Seed", th = "เมล็ดเห็ดกระดุมเหลือง"},
    {en = "Blue Oyster Seed", th = "เมล็ดเห็ดนางรมฟ้า"},
    {en = "Bright Bell Seed", th = "เมล็ดเห็ดระฆังเรืองแสง"},
    {en = "Bubble Shroom Seed", th = "เมล็ดเห็ดฟองสบู่"},
    {en = "Ghost Cap Seed", th = "เมล็ดเห็ดผี"},
    {en = "Starcap Seed", th = "เมล็ดเห็ดดาว"},
    {en = "Glow Shroom Seed", th = "เมล็ดเห็ดเรืองแสง"},
    {en = "Glacier Crown Seed", th = "เมล็ดเห็ดมงกุฎน้ำแข็ง"},
    {en = "Lava Fungus Seed", th = "เมล็ดเห็ดลาวา"},
    {en = "Amethyst Bloom Seed", th = "เมล็ดเห็ดอเมทิสต์"},
    {en = "Candy Puff Seed", th = "เมล็ดเห็ดลูกอมพัฟ"},
    {en = "Galaxy Cap Seed", th = "เมล็ดเห็ดกาแล็กซี"},
    {en = "Magic Mushroom Seed", th = "เมล็ดเห็ดวิเศษ"}
}

local seedButtons = {}
for i, data in ipairs(seedsData) do
    local SeedBtn = Instance.new("TextButton", ScrollFrame)
    SeedBtn.Size = UDim2.new(0.95, 0, 0, 28)
    SeedBtn.BackgroundColor3 = Color3.fromRGB(24, 30, 26)
    SeedBtn.Text = i .. ". " .. data.th
    SeedBtn.TextColor3 = Color3.fromRGB(220, 220, 220)
    SeedBtn.TextSize = 11
    SeedBtn.Font = Enum.Font.SourceSans
    Instance.new("UICorner", SeedBtn).CornerRadius = UDim.new(0, 5)
    
    table.insert(seedButtons, {btn = SeedBtn, data = data, index = i})
    
    SeedBtn.MouseButton1Click:Connect(function()
        SelectedSeedForAuto = data.en
        pcall(function()
            ReplicatedStorage:WaitForChild("BuySeedRequest"):FireServer(data.en, 0)
        end)
    end)
end
ScrollFrame.CanvasSize = UDim2.new(0, 0, 0, #seedsData * 32)

-- 🔄 Auto Plant Loop
task.spawn(function()
    while true do
        task.wait(0.8)
        if AutoPlantActive then
            pcall(function()
                ReplicatedStorage:WaitForChild("BuySeedRequest"):FireServer(SelectedSeedForAuto, 0)
                for _, prompt in pairs(Workspace:GetDescendants()) do
                    if prompt:IsA("ProximityPrompt") then
                        local txt = string.lower(prompt.ActionText .. " " .. prompt.ObjectText)
                        if txt:find("plant") or txt:find("soil") or txt:find("plot") or txt:find("seed") then
                            fireproximityprompt(prompt)
                        end
                    end
                end
            end)
        end
    end
end)

AutoPlantBtn.MouseButton1Click:Connect(function()
    AutoPlantActive = not AutoPlantActive
    if AutoPlantActive then
        AutoPlantBtn.BackgroundColor3 = Color3.fromRGB(46, 204, 113)
        AutoPlantBtn.TextColor3 = Color3.fromRGB(15, 20, 17)
        AutoPlantBtn.Text = CurrentLang == "TH" and "🌱 AUTO PLANT: เปิดอยู่" or "🌱 AUTO PLANT: ON"
    else
        AutoPlantBtn.BackgroundColor3 = Color3.fromRGB(192, 57, 43)
        AutoPlantBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
        AutoPlantBtn.Text = CurrentLang == "TH" and "🌱 AUTO PLANT: ปิดอยู่" or "🌱 AUTO PLANT: OFF"
    end
end)

-- Harvest Action
CollectBtn.MouseButton1Click:Connect(function()
    pcall(function()
        for _, obj in pairs(Workspace:GetDescendants()) do
            if obj:IsA("ProximityPrompt") then
                fireproximityprompt(obj)
            elseif obj:IsA("ClickDetector") then
                fireclickdetector(obj)
            end
        end
    end)
end)

-- Sell Actions
SellAllInvBtn.MouseButton1Click:Connect(function()
    pcall(function()
        for _, remote in pairs(ReplicatedStorage:GetDescendants()) do
            if remote:IsA("RemoteEvent") and (string.lower(remote.Name):find("sell") or string.lower(remote.Name):find("shop")) then
                remote:FireServer("SellAll")
            end
        end
    end)
end)

SellHandBtn.MouseButton1Click:Connect(function()
    pcall(function()
        for _, remote in pairs(ReplicatedStorage:GetDescendants()) do
            if remote:IsA("RemoteEvent") and (string.lower(remote.Name):find("sell") or string.lower(remote.Name):find("shop")) then
                remote:FireServer("SellHeld")
            end
        end
    end)
end)

-- Multi-Language Manager
LangTHBtn.MouseButton1Click:Connect(function()
    CurrentLang = "TH"
    LangTHBtn.BackgroundColor3 = Color3.fromRGB(46, 204, 113) LangTHBtn.TextColor3 = Color3.fromRGB(15, 20, 17)
    LangENBtn.BackgroundColor3 = Color3.fromRGB(28, 34, 30) LangENBtn.TextColor3 = Color3.fromRGB(200, 200, 200)
    Tab1Btn.Text = "⚙️ ตั้งค่า" Tab2Btn.Text = "🍄 เสกเห็ด" Tab3Btn.Text = "🌱 ปลูกเห็ด" Tab4Btn.Text = "🧺 เก็บเห็ด" Tab5Btn.Text = "🛒 ขายเห็ด"
    CollectBtn.Text = "🧺 เก็บเห็ดทั้งหมดในสวน" SellAllInvBtn.Text = "📦 ขายทั้งหมดในคลัง" SellHandBtn.Text = "✋ ขายเห็ดในมือ"
    CheckPriceBtn.Text = "🔍 ตรวจสอบราคาเห็ด" BackBtn.Text = "⬅️ กลับไปที่เดิม (ตั้งค่า)"
    AutoPlantBtn.Text = AutoPlantActive and "🌱 AUTO PLANT: เปิดอยู่" or "🌱 AUTO PLANT: ปิดอยู่"
    for _, item in ipairs(seedButtons) do item.btn.Text = item.index .. ". " .. item.data.th end
end)

LangENBtn.MouseButton1Click:Connect(function()
    CurrentLang = "EN"
    LangENBtn.BackgroundColor3 = Color3.fromRGB(46, 204, 113) LangENBtn.TextColor3 = Color3.fromRGB(15, 20, 17)
    LangTHBtn.BackgroundColor3 = Color3.fromRGB(28, 34, 30) LangTHBtn.TextColor3 = Color3.fromRGB(200, 200, 200)
    Tab1Btn.Text = "⚙️ Settings" Tab2Btn.Text = "🍄 Seeds" Tab3Btn.Text = "🌱 Auto Plant" Tab4Btn.Text = "🧺 Collect" Tab5Btn.Text = "🛒 Sell"
    CollectBtn.Text = "🧺 Collect All Mushrooms" SellAllInvBtn.Text = "📦 Sell All in Inventory" SellHandBtn.Text = "✋ Sell Held Item"
    CheckPriceBtn.Text = "🔍 Check Prices" BackBtn.Text = "⬅️ Back to Settings"
    AutoPlantBtn.Text = AutoPlantActive and "🌱 AUTO PLANT: ON" or "🌱 AUTO PLANT: OFF"
    for _, item in ipairs(seedButtons) do item.btn.Text = item.index .. ". " .. item.data.en end
    
