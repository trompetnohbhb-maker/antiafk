-- GUI Anti-AFK dengan Timer Berjalan
local ScreenGui = Instance.new("ScreenGui")
local MainButton = Instance.new("TextButton")
local TimeLabel = Instance.new("TextLabel")
local UICornerBtn = Instance.new("UICorner")
local UICornerLbl = Instance.new("UICorner")

-- Setup GUI Container
ScreenGui.Name = "AntiAFK_WithTimer"
ScreenGui.Parent = game:GetService("CoreGui")

-- Tombol ON/OFF
MainButton.Name = "ToggleButton"
MainButton.Parent = ScreenGui
MainButton.BackgroundColor3 = Color3.fromRGB(255, 0, 0) -- Merah (Off)
MainButton.Position = UDim2.new(0.05, 0, 0.4, 0)
MainButton.Size = UDim2.new(0, 120, 0, 40)
MainButton.Font = Enum.Font.SourceSansBold
MainButton.Text = "Anti-AFK: OFF"
MainButton.TextColor3 = Color3.fromRGB(255, 255, 255)
MainButton.TextSize = 16
MainButton.Draggable = true -- Tombol bisa digeser

UICornerBtn.Parent = MainButton

-- Label Waktu (Nempel di bawah tombol)
TimeLabel.Name = "TimeLabel"
TimeLabel.Parent = MainButton
TimeLabel.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
TimeLabel.BackgroundTransparency = 0.3
TimeLabel.Position = UDim2.new(0, 0, 1, 5) -- Jarak 5 pixel di bawah tombol
TimeLabel.Size = UDim2.new(1, 0, 0, 25)
TimeLabel.Font = Enum.Font.SourceSansItalic
TimeLabel.Text = "Time: 00:00:00"
TimeLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
TimeLabel.TextSize = 14

UICornerLbl.Parent = TimeLabel

local _G = {AntiAFK = false}
local startTime = 0
local VirtualUser = game:GetService("VirtualUser")

-- Fungsi Format Waktu (Detik ke Jam:Menit:Detik)
local function formatTime(s)
    return string.format("%02d:%02d:%02d", math.floor(s/3600), math.floor((s/60)%60), s%60)
end

-- Loop Timer
spawn(function()
    while true do
        if _G.AntiAFK then
            local duration = os.time() - startTime
            TimeLabel.Text = "Active: " .. formatTime(duration)
        else
            TimeLabel.Text = "Status: Idle"
        end
        task.wait(1)
    end
end)

-- Fungsi Anti-AFK
game:GetService("Players").LocalPlayer.Idled:Connect(function()
    if _G.AntiAFK then
        VirtualUser:CaptureController()
        VirtualUser:ClickButton2(Vector2.new())
    end
end)

-- Logika Tombol
MainButton.MouseButton1Click:Connect(function()
    _G.AntiAFK = not _G.AntiAFK
    if _G.AntiAFK then
        startTime = os.time() -- Reset waktu mulai
        MainButton.Text = "Anti-AFK: ON"
        MainButton.BackgroundColor3 = Color3.fromRGB(0, 255, 0) -- Hijau
    else
        MainButton.Text = "Anti-AFK: OFF"
        MainButton.BackgroundColor3 = Color3.fromRGB(255, 0, 0) -- Merah
    end
end)
