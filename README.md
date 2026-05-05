_G.Freeze = true

local player = game.Players.LocalPlayer
local root = player.Character:WaitForChild("HumanoidRootPart")
local startPos = root.CFrame

task.spawn(function()
    while _G.Freeze do
        root.CFrame = startPos
        root.Velocity = Vector3.new(0, 0, 0)
        root.RotVelocity = Vector3.new(0, 0, 0)
        task.wait()
    end
end)
