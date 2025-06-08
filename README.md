-- // Variável da Key Correta
local correctKey = "FREE_WZNMODZKEY7293728!"

-- // Serviços
local Players = game:GetService("Players")
local player = Players.LocalPlayer
local UIS = game:GetService("UserInputService")

-- // Função Drag
local function dragify(frame)
	local dragging, dragInput, startPos, startInputPos

	frame.InputBegan:Connect(function(input)
		if input.UserInputType == Enum.UserInputType.Touch or input.UserInputType == Enum.UserInputType.MouseButton1 then
			dragging = true
			startPos = frame.Position
			startInputPos = input.Position

			input.Changed:Connect(function()
				if input.UserInputState == Enum.UserInputState.End then
					dragging = false
				end
			end)
		end
	end)

	frame.InputChanged:Connect(function(input)
		if dragging and (input.UserInputType == Enum.UserInputType.Touch or input.UserInputType == Enum.UserInputType.MouseMovement) then
			local delta = input.Position - startInputPos
			frame.Position = UDim2.new(startPos.X.Scale, startPos.X.Offset + delta.X, startPos.Y.Scale, startPos.Y.Offset + delta.Y)
		end
	end)
end

-- // GUI Principal
local gui = Instance.new("ScreenGui", player:WaitForChild("PlayerGui"))
gui.Name = "WZN_KeySystem"
gui.ResetOnSpawn = false

-- // Key Frame
local keyFrame = Instance.new("Frame", gui)
keyFrame.BackgroundColor3 = Color3.fromRGB(25, 25, 25)
keyFrame.Size = UDim2.new(0, 360, 0, 200)
keyFrame.Position = UDim2.new(0.5, -180, 0.5, -100)
keyFrame.AnchorPoint = Vector2.new(0.5, 0.5)
keyFrame.BackgroundTransparency = 0.1
keyFrame.BorderSizePixel = 0
keyFrame.ClipsDescendants = true
keyFrame.Name = "KeyFrame"

-- Drag
dragify(keyFrame)

-- // Título
local title = Instance.new("TextLabel", keyFrame)
title.Size = UDim2.new(1, -20, 0, 30)
title.Position = UDim2.new(0, 10, 0, 5)
title.BackgroundTransparency = 1
title.Text = "WZN MODZ - Key System"
title.Font = Enum.Font.GothamBold
title.TextColor3 = Color3.fromRGB(0, 255, 255)
title.TextSize = 18
title.TextXAlignment = Enum.TextXAlignment.Left

-- // Texto explicativo
local info = Instance.new("TextLabel", keyFrame)
info.Size = UDim2.new(1, -20, 0, 40)
info.Position = UDim2.new(0, 10, 0, 35)
info.BackgroundTransparency = 1
info.TextWrapped = true
info.Text = "CLIQUE EM GET KEY PARA PEGAR SUA KEY"
info.Font = Enum.Font.Gotham
info.TextColor3 = Color3.fromRGB(200, 200, 200)
info.TextSize = 14
info.TextXAlignment = Enum.TextXAlignment.Left

-- // Caixa de texto para Key
local keyBox = Instance.new("TextBox", keyFrame)
keyBox.Size = UDim2.new(1, -20, 0, 30)
keyBox.Position = UDim2.new(0, 10, 0, 80)
keyBox.PlaceholderText = "Enter Key..."
keyBox.Font = Enum.Font.Gotham
keyBox.TextSize = 14
keyBox.Text = ""
keyBox.TextColor3 = Color3.new(1, 1, 1)
keyBox.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
keyBox.BorderSizePixel = 0

-- // Botão GET KEY
local getKeyBtn = Instance.new("TextButton", keyFrame)
getKeyBtn.Size = UDim2.new(0.45, -5, 0, 30)
getKeyBtn.Position = UDim2.new(0, 10, 0, 120)
getKeyBtn.Text = "🔑 Get Key"
getKeyBtn.Font = Enum.Font.GothamBold
getKeyBtn.TextSize = 14
getKeyBtn.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
getKeyBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
getKeyBtn.BorderSizePixel = 0

-- // Botão SUBMIT
local submitBtn = Instance.new("TextButton", keyFrame)
submitBtn.Size = UDim2.new(0.45, -5, 0, 30)
submitBtn.Position = UDim2.new(0.55, 0, 0, 120)
submitBtn.Text = "→ Submit"
submitBtn.Font = Enum.Font.GothamBold
submitBtn.TextSize = 14
submitBtn.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
submitBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
submitBtn.BorderSizePixel = 0

-- // Aviso
local warning = Instance.new("TextLabel", keyFrame)
warning.Size = UDim2.new(1, -20, 0, 20)
warning.Position = UDim2.new(0, 10, 1, -25)
warning.BackgroundTransparency = 1
warning.TextColor3 = Color3.fromRGB(255, 0, 0)
warning.TextSize = 13
warning.Font = Enum.Font.Gotham
warning.Text = ""

-- // Get Key Click
getKeyBtn.MouseButton1Click:Connect(function()
	setclipboard("https://link-target.net/1356478/K6VWYqEeAK2M")
	warning.Text = "✅ Link copiado! Cole no navegador para obter a Key."
end)

-- // Submit Click
submitBtn.MouseButton1Click:Connect(function()
	if keyBox.Text == correctKey then
		keyFrame.Visible = false

-- Gunfight Arena ESP + Aimbot com cores de time (vermelho/inimigo, verde/aliado)

local Players = game:GetService("Players")
local RunService = game:GetService("RunService")
local Camera = workspace.CurrentCamera
local LocalPlayer = Players.LocalPlayer

-- Variáveis
local Aimbot = false
local ESPLine = false
local ESPBox = false

-- Função para achar o inimigo visível mais próximo
local function GetClosestVisibleEnemy()
    local closest, shortestDist = nil, math.huge
    for _, player in pairs(Players:GetPlayers()) do
        if player ~= LocalPlayer and player.Character and player.Character:FindFirstChild("Head") then
            if player.Team ~= LocalPlayer.Team then
                local head = player.Character.Head
                local root = player.Character:FindFirstChild("HumanoidRootPart")
                if root then
                    local screenPos, onScreen = Camera:WorldToViewportPoint(head.Position)
                    if onScreen then
                        -- Checar visibilidade
                        local rayOrigin = Camera.CFrame.Position
                        local rayDirection = (head.Position - rayOrigin).Unit * (head.Position - rayOrigin).Magnitude
                        local raycastParams = RaycastParams.new()
                        raycastParams.FilterDescendantsInstances = {LocalPlayer.Character}
                        raycastParams.FilterType = Enum.RaycastFilterType.Blacklist
                        local raycastResult = workspace:Raycast(rayOrigin, rayDirection, raycastParams)
                        if raycastResult and raycastResult.Instance and raycastResult.Instance:IsDescendantOf(player.Character) then
                            local dist = (Vector2.new(screenPos.X, screenPos.Y) - Vector2.new(Camera.ViewportSize.X / 2, Camera.ViewportSize.Y / 2)).Magnitude
                            if dist < shortestDist then
                                shortestDist = dist
                                closest = player
                            end
                        end
                    end
                end
            end
        end
    end
    return closest
end

-- Aimbot que puxa para a cabeça do inimigo
RunService.RenderStepped:Connect(function()
    if Aimbot then
        local target = GetClosestVisibleEnemy()
        if target and target.Character and target.Character:FindFirstChild("Head") then
            local headPos = target.Character.Head.Position
            Camera.CFrame = CFrame.new(Camera.CFrame.Position, headPos)
        end
    end
end)

-- ESPs armazenadas por jogador
local ESPs = {}

-- Criar ESP para jogador
local function CreateESP(player)
    local line = Drawing.new("Line")
    line.Thickness = 2
    line.Visible = false

    local box = Drawing.new("Square")
    box.Thickness = 2
    box.Filled = false
    box.Visible = false

    ESPs[player] = {line = line, box = box}
end

-- Criar ESPs para todos os jogadores
for _, p in pairs(Players:GetPlayers()) do
    if p ~= LocalPlayer then
        CreateESP(p)
    end
end

-- Criar ESP ao entrar jogador novo
Players.PlayerAdded:Connect(function(p)
    if p ~= LocalPlayer then
        CreateESP(p)
    end
end)

-- Atualizar ESPs
RunService.RenderStepped:Connect(function()
    for player, esp in pairs(ESPs) do
        if player.Character and player.Character:FindFirstChild("HumanoidRootPart") and player.Character:FindFirstChild("Head") then
            local rootPos, onScreen = Camera:WorldToViewportPoint(player.Character.HumanoidRootPart.Position)
            local headPos, headOnScreen = Camera:WorldToViewportPoint(player.Character.Head.Position)

            local isEnemy = player.Team ~= LocalPlayer.Team
            local color = isEnemy and Color3.fromRGB(255, 0, 0) or Color3.fromRGB(0, 255, 0)

            if onScreen and headOnScreen and ESPLine then
                esp.line.Color = color
                esp.line.From = Vector2.new(Camera.ViewportSize.X / 2, Camera.ViewportSize.Y)
                esp.line.To = Vector2.new(headPos.X, headPos.Y)
                esp.line.Visible = true
            else
                esp.line.Visible = false
            end

            if onScreen and ESPBox then
                esp.box.Color = color
                local sizeX, sizeY = 50, 100
                esp.box.Size = Vector2.new(sizeX, sizeY)
                esp.box.Position = Vector2.new(rootPos.X - sizeX / 2, rootPos.Y - sizeY / 2)
                esp.box.Visible = true
            else
                esp.box.Visible = false
            end
        else
            esp.line.Visible = false
            esp.box.Visible = false
        end
    end
end)

-- UI Fluent com botão WZN MODZ
local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Name = "WZN_MODZ_GUI"
ScreenGui.Parent = game.CoreGui
ScreenGui.IgnoreGuiInset = true
ScreenGui.ResetOnSpawn = false

local TopBar = Instance.new("TextButton")
TopBar.Size = UDim2.new(0, 160, 0, 24)
TopBar.Position = UDim2.new(0.4, 0, 0, 10)
TopBar.BackgroundColor3 = Color3.fromRGB(25, 25, 25)
TopBar.Text = "WZN MODZ"
TopBar.TextColor3 = Color3.fromRGB(255, 255, 255)
TopBar.TextSize = 14
TopBar.Parent = ScreenGui
TopBar.Active = true
TopBar.Draggable = true

local MainFrame = Instance.new("Frame")
MainFrame.Size = UDim2.new(0, 220, 0, 260)
MainFrame.Position = UDim2.new(0.4, 0, 0.1, 0)
MainFrame.BackgroundColor3 = Color3.fromRGB(10, 10, 10)
MainFrame.Visible = false
MainFrame.Parent = ScreenGui
MainFrame.Active = true
MainFrame.Draggable = true

local CloseBtn = Instance.new("TextButton")
CloseBtn.Size = UDim2.new(0, 20, 0, 20)
CloseBtn.Position = UDim2.new(1, -24, 0, 4)
CloseBtn.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
CloseBtn.Text = "-"
CloseBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
CloseBtn.Parent = MainFrame

CloseBtn.MouseButton1Click:Connect(function()
    MainFrame.Visible = false
end)

-- Criar botão toggle
local function makeToggle(name, y, callback)
    local btn = Instance.new("TextButton")
    btn.Size = UDim2.new(0, 180, 0, 30)
    btn.Position = UDim2.new(0, 20, 0, y)
    btn.BackgroundColor3 = Color3.fromRGB(25, 25, 25)
    btn.TextColor3 = Color3.fromRGB(255, 255, 255)
    btn.Text = "OFF - "..name
    btn.Parent = MainFrame

    local state = false
    btn.MouseButton1Click:Connect(function()
        state = not state
        btn.Text = (state and "ON  - " or "OFF - ")..name
        callback(state)
    end)
end

-- Funções UI
makeToggle("Aimbot", 40, function(state) Aimbot = state end)
makeToggle("ESP Line", 80, function(state) ESPLine = state end)
makeToggle("ESP Box", 120, function(state) ESPBox = state end)

TopBar.MouseButton1Click:Connect(function()
    MainFrame.Visible = not MainFrame.Visible
end)

		-- ==============================

	else
		warning.Text = "❌ Key incorreta!"
	end
end)
