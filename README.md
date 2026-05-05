-- Script Freeze Sederhana (Anti Knockback)
local hrp = game.Players.LocalPlayer.Character:WaitForChild("HumanoidRootPart")

if hrp.Anchored == false then
    hrp.Anchored = true
    print("FREEZE AKTIF: Karakter tidak akan mental")
else
    hrp.Anchored = false
    print("FREEZE MATI: Karakter bisa gerak lagi")
end
