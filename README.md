# Scripts
Teleport-to-Base System 

local teleportKey = Enum.KeyCode.B
local teleportCooldown = 5
local maxDistance = 50

local player = game.Players.LocalPlayer
local userInputService = game:GetService("UserInputService")
local teleporting = false

local baseSpawn = workspace:WaitForChild("BaseSpawn")

local function getDistance(pos1, pos2)
	return (pos1 - pos2).Magnitude
end

userInputService.InputBegan:Connect(function(input, isProcessed)
	if isProcessed then return end
	if input.KeyCode == teleportKey then
		if not teleporting and player.Character and player.Character:FindFirstChild("HumanoidRootPart") then
			local charPos = player.Character.HumanoidRootPart.Position
			local basePos = baseSpawn.Position
			local dist = getDistance(charPos, basePos)

			if dist > maxDistance then
				teleporting = true
				player.Character:SetPrimaryPartCFrame(CFrame.new(basePos + Vector3.new(0, 3, 0)))
				print("Teleportado de volta para a base!")
				task.wait(teleportCooldown)
				teleporting = false
			else
				print("Você está muito perto da base para teleportar.")
			end
		end
	end
end)
