-- Script de Hub Básico para Roblox

-- Criando a interface gráfica localmente
local ScreenGui = Instance.new("ScreenGui")
local MainFrame = Instance.new("Frame")
local Title = Instance.new("TextLabel")
local SpeedButton = Instance.new("TextButton")
local JumpButton = Instance.new("TextButton")
local GravityButton = Instance.new("TextButton")
local ViewButton = Instance.new("TextButton")
local PlayerNameBox = Instance.new("TextBox")
local ToggleButton = Instance.new("TextButton")

-- Configurando o GUI
ScreenGui.Name = "HubGui"
local playerGui = game.Players.LocalPlayer:FindFirstChild("PlayerGui")
if not playerGui then
    warn("PlayerGui não encontrado. O script pode não funcionar corretamente.")
    return
end
ScreenGui.Parent = playerGui

MainFrame.Name = "MainFrame"
MainFrame.Parent = ScreenGui
MainFrame.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
MainFrame.Size = UDim2.new(0, 300, 0, 500)
MainFrame.Position = UDim2.new(0.5, -150, 0.5, -250)

Title.Name = "Title"
Title.Parent = MainFrame
Title.Text = "CLH HUB"
Title.TextColor3 = Color3.fromRGB(255, 0, 0)
Title.BackgroundTransparency = 1
Title.Size = UDim2.new(0, 300, 0, 50)
Title.Position = UDim2.new(0, 0, 0, 0)
Title.Font = Enum.Font.SourceSansBold
Title.TextSize = 24
Title.TextScaled = true

SpeedButton.Name = "SpeedButton"
SpeedButton.Parent = MainFrame
SpeedButton.Text = "Mudar Velocidade"
SpeedButton.Size = UDim2.new(0, 200, 0, 50)
SpeedButton.Position = UDim2.new(0.5, -100, 0, 60)
SpeedButton.BackgroundColor3 = Color3.fromRGB(150, 50, 50)

JumpButton.Name = "JumpButton"
JumpButton.Parent = MainFrame
JumpButton.Text = "Mudar Pulo"
JumpButton.Size = UDim2.new(0, 200, 0, 50)
JumpButton.Position = UDim2.new(0.5, -100, 0, 130)
JumpButton.BackgroundColor3 = Color3.fromRGB(150, 100, 50)

GravityButton.Name = "GravityButton"
GravityButton.Parent = MainFrame
GravityButton.Text = "Mudar Gravidade"
GravityButton.Size = UDim2.new(0, 200, 0, 50)
GravityButton.Position = UDim2.new(0.5, -100, 0, 200)
GravityButton.BackgroundColor3 = Color3.fromRGB(50, 150, 150)

ViewButton.Name = "ViewButton"
ViewButton.Parent = MainFrame
ViewButton.Text = "Ver Jogador"
ViewButton.Size = UDim2.new(0, 200, 0, 50)
ViewButton.Position = UDim2.new(0.5, -100, 0, 270)
ViewButton.BackgroundColor3 = Color3.fromRGB(100, 50, 150)

PlayerNameBox.Name = "PlayerNameBox"
PlayerNameBox.Parent = MainFrame
PlayerNameBox.Text = "Digite o Nickname"
PlayerNameBox.Size = UDim2.new(0, 200, 0, 50)
PlayerNameBox.Position = UDim2.new(0.5, -100, 0, 340)
PlayerNameBox.BackgroundColor3 = Color3.fromRGB(200, 200, 200)

ToggleButton.Name = "ToggleButton"
ToggleButton.Parent = ScreenGui
ToggleButton.Text = "CLH HUB"
ToggleButton.Size = UDim2.new(0, 150, 0, 50)
ToggleButton.Position = UDim2.new(0, 10, 0, 10)
ToggleButton.BackgroundColor3 = Color3.fromRGB(100, 100, 100)
ToggleButton.TextColor3 = Color3.fromRGB(255, 255, 255)
ToggleButton.Font = Enum.Font.SourceSans
ToggleButton.TextSize = 18

-- Variáveis para controle das funções
local isSpeedActive = false
local isJumpActive = false
local isGravityActive = false

-- Função para animar transição de visibilidade
local function animateVisibility(frame, isVisible)
    local tweenService = game:GetService("TweenService")
    local tweenInfo = TweenInfo.new(0.5, Enum.EasingStyle.Quad, Enum.EasingDirection.InOut)
    local goal = {Transparency = isVisible and 0 or 1}

    for _, child in ipairs(frame:GetDescendants()) do
        if child:IsA("GuiObject") then
            local tween = tweenService:Create(child, tweenInfo, goal)
            tween:Play()
        end
    end

    wait(0.5)
    frame.Visible = isVisible
end

-- Adicionando funcionalidades aos botões
SpeedButton.MouseButton1Click:Connect(function()
    local player = game.Players.LocalPlayer
    if player and player.Character then
        if isSpeedActive then
            player.Character.Humanoid.WalkSpeed = 16 -- Valor padrão
            print("Velocidade redefinida para padrão!")
        else
            player.Character.Humanoid.WalkSpeed = 100 -- Mude para o valor desejado
            print("Velocidade alterada para 100!")
        end
        isSpeedActive = not isSpeedActive
    end
end)

JumpButton.MouseButton1Click:Connect(function()
    local player = game.Players.LocalPlayer
    if player and player.Character then
        if isJumpActive then
            player.Character.Humanoid.JumpPower = 50 -- Valor padrão
            print("Pulo redefinido para padrão!")
        else
            player.Character.Humanoid.JumpPower = 150 -- Mude para o valor desejado
            print("Pulo alterado para 150!")
        end
        isJumpActive = not isJumpActive
    end
end)

GravityButton.MouseButton1Click:Connect(function()
    local workspace = game.Workspace
    if isGravityActive then
        workspace.Gravity = 196.2 -- Valor padrão
        print("Gravidade redefinida para padrão!")
    else
        workspace.Gravity = 50 -- Mude para o valor desejado
        print("Gravidade alterada para 50!")
    end
    isGravityActive = not isGravityActive
end)

ViewButton.MouseButton1Click:Connect(function()
    local playerName = PlayerNameBox.Text
    local targetPlayer = game.Players:FindFirstChild(playerName)
    if targetPlayer and targetPlayer.Character then
        local camera = workspace.CurrentCamera
        camera.CameraSubject = targetPlayer.Character
        print("Visualizando jogador: " .. playerName)
    else
        print("Jogador não encontrado ou inválido!")
    end
end)

ToggleButton.MouseButton1Click:Connect(function()
    animateVisibility(MainFrame, not MainFrame.Visible)
    if MainFrame.Visible then
        ToggleButton.Text = "Fechar"
    else
        ToggleButton.Text = "CLH HUB"
    end
end)
