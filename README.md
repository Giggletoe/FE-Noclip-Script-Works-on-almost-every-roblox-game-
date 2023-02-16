-- made in a few mins
-- Version: 3.2

-- Instances:

local ScreenGui = Instance.new("ScreenGui")
local Frame = Instance.new("Frame")
local UICorner = Instance.new("UICorner")
local Frame_2 = Instance.new("Frame")
local UICorner_2 = Instance.new("UICorner")
local TextLabel = Instance.new("TextLabel")
local TextLabel_2 = Instance.new("TextLabel")
local TextLabel_3 = Instance.new("TextLabel")

--Properties:

ScreenGui.Parent = game.Players.LocalPlayer:WaitForChild("PlayerGui")
ScreenGui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling

Frame.Parent = ScreenGui
Frame.BackgroundColor3 = Color3.fromRGB(176, 197, 255)
Frame.Position = UDim2.new(0.0431990623, 0, 0.415700257, 0)
Frame.Size = UDim2.new(0, 382, 0, 487)

UICorner.Parent = Frame

Frame_2.Parent = ScreenGui
Frame_2.BackgroundColor3 = Color3.fromRGB(133, 175, 255)
Frame_2.Position = UDim2.new(0.0402802117, 0, 0.408563793, 0)
Frame_2.Size = UDim2.new(0, 395, 0, 44)

UICorner_2.Parent = Frame_2

TextLabel.Parent = ScreenGui
TextLabel.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
TextLabel.BackgroundTransparency = 1.000
TextLabel.Position = UDim2.new(0.0969060138, 0, 0.405887604, 0)
TextLabel.Size = UDim2.new(0, 200, 0, 50)
TextLabel.Font = Enum.Font.Code
TextLabel.Text = "FE Noclip "
TextLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
TextLabel.TextScaled = true
TextLabel.TextSize = 14.000
TextLabel.TextWrapped = true

TextLabel_2.Parent = ScreenGui
TextLabel_2.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
TextLabel_2.BackgroundTransparency = 1.000
TextLabel_2.Position = UDim2.new(0.0636310503, 0, 0.506690502, 0)
TextLabel_2.Size = UDim2.new(0, 314, 0, 219)
TextLabel_2.Font = Enum.Font.Code
TextLabel_2.Text = "FE Noclip has been injected, Press F to enable it, (DO NOT BLAME ME IF YOU GET BANNED)"
TextLabel_2.TextColor3 = Color3.fromRGB(255, 255, 255)
TextLabel_2.TextScaled = true
TextLabel_2.TextSize = 14.000
TextLabel_2.TextWrapped = true

TextLabel_3.Parent = ScreenGui
TextLabel_3.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
TextLabel_3.BackgroundTransparency = 1.000
TextLabel_3.Position = UDim2.new(0.073555164, 0, 0.729705632, 0)
TextLabel_3.Size = UDim2.new(0, 281, 0, 56)
TextLabel_3.Font = Enum.Font.Code
TextLabel_3.Text = "I did not make this noclip script, shoutout to DaintyDust05191, Ui designed by Me."
TextLabel_3.TextColor3 = Color3.fromRGB(255, 255, 255)
TextLabel_3.TextScaled = true
TextLabel_3.TextSize = 14.000
TextLabel_3.TextWrapped = true

-- Scripts:

local function OHMZI_fake_script() -- ScreenGui.Noclip 
	local script = Instance.new('LocalScript', ScreenGui)

	local c = workspace.CurrentCamera
	local player = game.Players.LocalPlayer
	local userInput = game:GetService("UserInputService")
	
	local selected = false
	local speed = 60
	local lastUpdate = 0
	
	function getNextMovement(deltaTime)
		local nextMove = Vector3.new()
		-- Left/Right
		if userInput:IsKeyDown("A") or userInput:IsKeyDown("Left") then
			nextMove = Vector3.new(-1,0,0)
		elseif userInput:IsKeyDown("D") or userInput:IsKeyDown("Right") then
			nextMove = Vector3.new(1,0,0)
		end
		-- Forward/Back
		if userInput:IsKeyDown("W") or userInput:IsKeyDown("Up") then
			nextMove = nextMove + Vector3.new(0,0,-1)
		elseif userInput:IsKeyDown("S") or userInput:IsKeyDown("Down") then
			nextMove = nextMove + Vector3.new(0,0,1)
		end
		-- Up/Down
		if userInput:IsKeyDown("Space") then
			nextMove = nextMove + Vector3.new(0,1,0)
		elseif userInput:IsKeyDown("LeftControl") then
			nextMove = nextMove + Vector3.new(0,-1,0)
		end
		return CFrame.new( nextMove * (speed * deltaTime) )
	end
	
	function onSelected()
		local char = player.Character
		if char then
			local humanoid = char:WaitForChild("Humanoid")
			local root = char:WaitForChild("HumanoidRootPart")
			currentPos = root.Position
			selected = true
			root.Anchored = true
			lastUpdate = tick()
			humanoid.PlatformStand = true
			while selected do
				wait()
				local delta = tick()-lastUpdate
				local look = (c.Focus.p-c.CoordinateFrame.p).unit
				local move = getNextMovement(delta)
				local pos = root.Position
				root.CFrame = CFrame.new(pos,pos+look) * move
				lastUpdate = tick()
			end
			root.Anchored = false
			root.Velocity = Vector3.new()
			humanoid.PlatformStand = false
		end
	end
	
	function onDeselected()
		selected = false
	end
	
	function onkeypressed() 
		if selected == false then
			onSelected()
		elseif selected == true then
			onDeselected()
	
		end
	end 
	
	local mouse = player:GetMouse()
	mouse.KeyDown:Connect(function(key)
			if key == "f" then
			onkeypressed()
		end
	end)
end
coroutine.wrap(OHMZI_fake_script)()

