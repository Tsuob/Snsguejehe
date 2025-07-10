local Players = game:GetService("Players")
local RunService = game:GetService("RunService")
local player = Players.LocalPlayer
local character = player.Character or player.CharacterAdded:Wait()
local hrp = character:WaitForChild("HumanoidRootPart")

local flying = false
local speed = 5
local direction = Vector3.zero

local screenGui = Instance.new("ScreenGui", player:WaitForChild("PlayerGui"))
screenGui.ResetOnSpawn = false

local button = Instance.new("TextButton", screenGui)
button.Size = UDim2.new(0, 120, 0, 40)
button.Position = UDim2.new(0.05, 0, 0.85, 0)
button.BackgroundColor3 = Color3.fromRGB(30, 150, 255)
button.Text = "Ativar Voo"
button.TextColor3 = Color3.new(1,1,1)
button.TextScaled = true
button.Font = Enum.Font.SourceSansBold
button.BorderSizePixel = 0
button.BackgroundTransparency = 0.2
button.Active = true
button.Draggable = true

local bv = Instance.new("BodyVelocity")
bv.MaxForce = Vector3.new(1e9, 1e9, 1e9)
bv.Velocity = Vector3.new(0,0,0)

local bg = Instance.new("BodyGyro")
bg.MaxTorque = Vector3.new(1e9, 1e9, 1e9)
bg.P = 9e4
bg.CFrame = hrp.CFrame

local function toggleFly()
    flying = not flying
    if flying then
        bv.Parent = hrp
        bg.Parent = hrp
        button.Text = "Desativar Voo"
    else
        bv.Parent = nil
        bg.Parent = nil
        button.Text = "Ativar Voo"
    end
end

button.MouseButton1Click:Connect(toggleFly)

RunService.Heartbeat:Connect(function()
    if flying then
        local cam = workspace.CurrentCamera
        bg.CFrame = cam.CFrame
        bv.Velocity = cam.CFrame.LookVector * speed
    end
end)
