-- King Legacy Hub by Lucas
if game.PlaceId ~= 4520749081 then
    return warn("Este Hub é apenas para King Legacy.")
end

-- Interface
local ScreenGui = Instance.new("ScreenGui", game.Players.LocalPlayer:WaitForChild("PlayerGui"))
ScreenGui.Name = "KingLegacyHub"

local Frame = Instance.new("Frame", ScreenGui)
Frame.Size = UDim2.new(0, 250, 0, 150)
Frame.Position = UDim2.new(0.5, -125, 0.5, -75)
Frame.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
Frame.BorderSizePixel = 0
Frame.Active = true
Frame.Draggable = true

local UICorner = Instance.new("UICorner", Frame)
UICorner.CornerRadius = UDim.new(0, 10)

-- Botão de Teleport
local TeleportButton = Instance.new("TextButton", Frame)
TeleportButton.Size = UDim2.new(0.9, 0, 0.3, 0)
TeleportButton.Position = UDim2.new(0.05, 0, 0.1, 0)
TeleportButton.Text = "Teleport p/ Starter Island"
TeleportButton.BackgroundColor3 = Color3.fromRGB(50, 100, 200)
TeleportButton.TextColor3 = Color3.new(1, 1, 1)
Instance.new("UICorner", TeleportButton)

TeleportButton.MouseButton1Click:Connect(function()
    local plr = game.Players.LocalPlayer
    if plr.Character and plr.Character:FindFirstChild("HumanoidRootPart") then
        plr.Character.HumanoidRootPart.CFrame = CFrame.new(1149, 17, 1685) -- posição da Starter Island
    end
end)

-- Botão de Auto Farm básico
local AutoFarmButton = Instance.new("TextButton", Frame)
AutoFarmButton.Size = UDim2.new(0.9, 0, 0.3, 0)
AutoFarmButton.Position = UDim2.new(0.05, 0, 0.55, 0)
AutoFarmButton.Text = "Auto Farm [ON/OFF]"
AutoFarmButton.BackgroundColor3 = Color3.fromRGB(200, 100, 50)
AutoFarmButton.TextColor3 = Color3.new(1, 1, 1)
Instance.new("UICorner", AutoFarmButton)

local farming = false

AutoFarmButton.MouseButton1Click:Connect(function()
    farming = not farming
    AutoFarmButton.Text = farming and "Auto Farm [ON]" or "Auto Farm [OFF]"

    while farming do
        task.wait(0.5)
        local enemy = workspace.Enemies:FindFirstChildOfClass("Model")
        if enemy and enemy:FindFirstChild("HumanoidRootPart") then
            local player = game.Players.LocalPlayer
            local char = player.Character
            if char and char:FindFirstChild("HumanoidRootPart") then
                char.HumanoidRootPart.CFrame = enemy.HumanoidRootPart.CFrame * CFrame.new(0, 0, 2)
                game:GetService("VirtualInputManager"):SendKeyEvent(true, "Z", false, game)
                task.wait(0.1)
                game:GetService("VirtualInputManager"):SendKeyEvent(false, "Z", false, game)
            end
        end
    end
end)
