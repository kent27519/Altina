local Players = game:GetService("Players")
local UserInputService = game:GetService("UserInputService")

local player = Players.LocalPlayer
local MAX_SPEED = 500
local GOD_MODE = true
local currentSpeed = 16

-- GUI
local gui = Instance.new("ScreenGui")
gui.Name = "Altina"
gui.ResetOnSpawn = false
gui.Parent = player:WaitForChild("PlayerGui")

local frame = Instance.new("Frame")
frame.Size = UDim2.fromOffset(280, 180)
frame.Position = UDim2.new(0.5, -140, 0.5, -90)
frame.BackgroundColor3 = Color3.fromRGB(25, 25, 30)
frame.BorderSizePixel = 0
frame.Parent = gui

local corner = Instance.new("UICorner")
corner.CornerRadius = UDim.new(0, 14)
corner.Parent = frame

-- Title
local title = Instance.new("TextLabel")
title.Size = UDim2.new(1, 0, 0, 40)
title.BackgroundTransparency = 1
title.Text = "ALTINA"
title.TextColor3 = Color3.new(1, 1, 1)
title.TextSize = 22
title.Font = Enum.Font.GothamBold
title.Parent = frame

-- Speed text
local speedText = Instance.new("TextLabel")
speedText.Size = UDim2.new(1, -30, 0, 30)
speedText.Position = UDim2.fromOffset(15, 42)
speedText.BackgroundTransparency = 1
speedText.Text = "Speed: 16 / 500"
speedText.TextColor3 = Color3.new(1, 1, 1)
speedText.TextSize = 17
speedText.Font = Enum.Font.Gotham
speedText.Parent = frame

-- Slider
local slider = Instance.new("TextButton")
slider.Size = UDim2.new(1, -40, 0, 12)
slider.Position = UDim2.fromOffset(20, 82)
slider.Text = ""
slider.BackgroundColor3 = Color3.fromRGB(70, 70, 80)
slider.BorderSizePixel = 0
slider.Parent = frame

local sliderCorner = Instance.new("UICorner")
sliderCorner.CornerRadius = UDim.new(1, 0)
sliderCorner.Parent = slider

local knob = Instance.new("Frame")
knob.Size = UDim2.fromOffset(20, 20)
knob.AnchorPoint = Vector2.new(0.5, 0.5)
knob.Position = UDim2.new(16 / MAX_SPEED, 0, 0.5, 0)
knob.BackgroundColor3 = Color3.new(1, 1, 1)
knob.BorderSizePixel = 0
knob.Parent = slider

local knobCorner = Instance.new("UICorner")
knobCorner.CornerRadius = UDim.new(1, 0)
knobCorner.Parent = knob

-- God Mode
local godButton = Instance.new("TextButton")
godButton.Size = UDim2.new(1, -40, 0, 40)
godButton.Position = UDim2.fromOffset(20, 120)
godButton.Text = "GOD MODE: ON"
godButton.TextColor3 = Color3.new(1, 1, 1)
godButton.TextSize = 16
godButton.Font = Enum.Font.GothamBold
godButton.BackgroundColor3 = Color3.fromRGB(55, 55, 65)
godButton.BorderSizePixel = 0
godButton.Parent = frame

local godCorner = Instance.new("UICorner")
godCorner.CornerRadius = UDim.new(0, 9)
godCorner.Parent = godButton

-- Set speed
local function setSpeed(speed)
	currentSpeed = math.clamp(math.floor(speed), 0, MAX_SPEED)

	local character = player.Character
	local humanoid = character and character:FindFirstChildOfClass("Humanoid")

	if humanoid then
		humanoid.WalkSpeed = currentSpeed
	end

	speedText.Text = "Speed: " .. currentSpeed .. " / " .. MAX_SPEED
	knob.Position = UDim2.new(currentSpeed / MAX_SPEED, 0, 0.5, 0)
end

-- Slider input
local function updateSlider(input)
	local x = input.Position.X
	local start = slider.AbsolutePosition.X
	local width = slider.AbsoluteSize.X

	local percent = math.clamp((x - start) / width, 0, 1)
	setSpeed(percent * MAX_SPEED)
end

slider.InputBegan:Connect(function(input)
	if input.UserInputType == Enum.UserInputType.MouseButton1
		or input.UserInputType == Enum.UserInputType.Touch then
		updateSlider(input)
	end
end)

slider.InputChanged:Connect(function(input)
	if input.UserInputType == Enum.UserInputType.MouseMovement
		or input.UserInputType == Enum.UserInputType.Touch then
		updateSlider(input)
	end
end)

-- God mode toggle
godButton.MouseButton1Click:Connect(function()
	GOD_MODE = not GOD_MODE

	if GOD_MODE then
		godButton.Text = "GOD MODE: ON"
	else
		godButton.Text = "GOD MODE: OFF"
	end
end)

-- Character setup
local function setupCharacter(character)
	local humanoid = character:WaitForChild("Humanoid")

	humanoid.WalkSpeed = currentSpeed

	if GOD_MODE then
		humanoid.MaxHealth = math.huge
		humanoid.Health = math.huge
	end
end

if player.Character then
	setupCharacter(player.Character)
end

player.CharacterAdded:Connect(setupCharacter)
