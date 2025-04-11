-- CACHAÇA HUB - Blue Lock Script
local Players = game:GetService("Players")
local LocalPlayer = Players.LocalPlayer
local Workspace = game:GetService("Workspace")
local RunService = game:GetService("RunService")
local TweenService = game:GetService("TweenService")

-- UI simples
local ScreenGui = Instance.new("ScreenGui", LocalPlayer:WaitForChild("PlayerGui"))
local Title = Instance.new("TextLabel", ScreenGui)
Title.Text = "CACHAÇA HUB"
Title.Size = UDim2.new(0.2, 0, 0.05, 0)
Title.Position = UDim2.new(0.4, 0, 0, 0)
Title.BackgroundColor3 = Color3.new(0, 0, 0)
Title.TextColor3 = Color3.new(1, 1, 1)
Title.Font = Enum.Font.GothamBold
Title.TextScaled = true

-- ESP jogadores
function createESP(player)
    if player ~= LocalPlayer and player.Character then
        local Billboard = Instance.new("BillboardGui", player.Character)
        Billboard.Name = "ESP"
        Billboard.Size = UDim2.new(0, 100, 0, 30)
        Billboard.AlwaysOnTop = true
        Billboard.StudsOffset = Vector3.new(0, 3, 0)

        local NameLabel = Instance.new("TextLabel", Billboard)
        NameLabel.Size = UDim2.new(1, 0, 1, 0)
        NameLabel.Text = player.Name
        NameLabel.TextColor3 = Color3.new(1, 0, 0)
        NameLabel.BackgroundTransparency = 1
        NameLabel.Font = Enum.Font.ArialBold
        NameLabel.TextScaled = true
    end
end

for _, p in pairs(Players:GetPlayers()) do
    createESP(p)
end

Players.PlayerAdded:Connect(createESP)

-- Teleportar para o gol
function teleportToGoal()
    for _, goal in pairs(Workspace:GetDescendants()) do
        if goal:IsA("Part") and goal.Name:lower():find("goal") then
            LocalPlayer.Character:MoveTo(goal.Position + Vector3.new(0, 3, 0))
            break
        end
    end
end

-- Crawler automático (simula correr com a bola
