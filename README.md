local Library = loadstring(game:HttpGet("https://githubusercontent.com"))()
local Window = Library.CreateLib("Sailor Piece - Anti Knockback", "DarkTheme")
local Tab = Window:NewTab("Main")
local Section = Tab:NewSection("Freeze Character")

Section:NewToggle("Freeze / Anti Knockback", "Mengunci posisi agar tidak terpental", function(state)
    local root = game.Players.LocalPlayer.Character:WaitForChild("HumanoidRootPart")
    if state then
        root.Anchored = true
    else
        root.Anchored = false
    end
end)

Section:NewButton("Manual Unfreeze", "Klik jika karakter nyangkut", function()
    game.Players.LocalPlayer.Character:WaitForChild("HumanoidRootPart").Anchored = false
end)
