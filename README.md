-- Script de Hub Básico para Roblox

-- Criando a interface gráfica localmente
local ScreenGui = Instance.new("ScreenGui")
local MainFrame = Instance.new("Frame")
local Title = Instance.new("TextLabel")
local Button1 = Instance.new("TextButton")
local Button2 = Instance.new("TextButton")
local SpeedButton = Instance.new("TextButton")
local JumpButton = Instance.new("TextButton")
local GravityButton = Instance.new("TextButton")
local ViewButton = Instance.new("TextButton")
local PlayerNameBox = Instance.new("TextBox")
local ToggleButton = Instance.new("TextButton")

-- URL da imagem para o botão Toggle
local ToggleImage = "https://cdn.discordapp.com/attachments/1238671414702117035/1317550913719767051/Gemini_Generated_Image_u6t6o2u6t6o2u6t6.jpg"

-- Configurando o GUI
ScreenGui.Name = "HubGui"
ScreenGui.Parent = game.Players.LocalPlayer:WaitForChild("PlayerGui")

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

Button1.Name = "Button1"
Button1.Parent = MainFrame
Button1.Text = "Ativar Função 1"
Button1.Size = UDim2.new(0, 200, 0, 50)
Button1.Position = UDim2.new(0.5, -100, 0, 60)
Button1.BackgroundColor3 = Color3.fromRGB(50, 150, 50)

Button2.Name = "Button2"
Button2.Parent = MainFrame
Button2.Text = "Ativar Função 2"
Button2.Size = UDim2.new(0, 200, 0, 50)
Button2.Position = UDim2.new(0.5, -100, 0, 130)
Button2.BackgroundColor3 = Color3.fromRGB(50, 50, 150)

SpeedButton.Name = "SpeedButton"
SpeedButton.Parent = MainFrame
SpeedButton.Text = "Mudar Velocidade"
SpeedButton.Size = UDim2.new(0, 200, 0, 50)
SpeedButton.Position = UDim2.new(0.5, -100, 0, 200)
SpeedButton.BackgroundColor3 = Color3.fromRGB(150, 50, 50)

JumpButton.Name = "JumpButton"
JumpButton.Parent = MainFrame
JumpButton.Text = "Mudar Pulo"
JumpButton.Size = UDim2.new(0, 200, 0, 50)
JumpButton.Position = UDim2.new(0.5, -100, 0, 270)
JumpButton.BackgroundColor3 = Color3.fromRGB(150, 100, 50)

GravityButton.Name = "GravityButton"
GravityButton.Parent = MainFrame
GravityButton.Text = "Mudar Gravidade"
GravityButton.Size = UDim2.new(0, 200, 0, 50)
GravityButton.Position = UDim2.new(0.5, -100, 0, 340)
GravityButton.BackgroundColor3 = Color3.fromRGB(50, 150, 150)

ViewButton.Name = "ViewButton"
ViewButton.Parent = MainFrame
ViewButton.Text = "Ver Jogador"
ViewButton.Size = UDim2.new(0, 200, 0, 50)
ViewButton.Position = UDim2.new(0.5, -100, 0, 410)
ViewButton.BackgroundColor3 = Color3.fromRGB(100, 50, 150)

PlayerNameBox.Name = "PlayerNameBox"
PlayerNameBox.Parent = MainFrame
PlayerNameBox.Text = "Digite o Nickname"
PlayerNameBox.Size = UDim2.new(0, 200, 0, 50)
PlayerNameBox.Position = UDim2.new(0.5, -100, 0, 480)
PlayerNameBox.BackgroundColor3 = Color3.fromRGB(200, 200, 200)

ToggleButton.Name = "ToggleButton"
ToggleButton.Parent = ScreenGui
ToggleButton.Text = ""
ToggleButton.Size = UDim2.new(0, 150, 0, 50)
ToggleButton.Position = UDim2.new(0, 10, 0, 10)
ToggleButton.BackgroundColor3 = Color3.fromRGB(100, 100, 100)
ToggleButton.TextColor3 = Color3.fromRGB(255, 255, 255)
ToggleButton.Font = Enum.Font.SourceSans
ToggleButton.TextSize = 18
ToggleButton.AutoButtonColor = false

-- Adicionando imagem ao botão Toggle
local ToggleImageLabel = Instance.new("ImageLabel")
ToggleImageLabel.Name = "ToggleImage"
ToggleImageLabel.Parent = ToggleButton
ToggleImageLabel.Size = UDim2.new(1, 0, 1, 0)
ToggleImageLabel.Position = UDim2.new(0, 0, 0, 0)
ToggleImageLabel.Image = ToggleImage
ToggleImageLabel.BackgroundTransparency = 1

-- Adicionando funcionalidades aos botões
Button1.MouseButton1Click:Connect(function()
    print("Função 1 ativada!")
    -- Adicione aqui a lógica da Função 1
end)

Button2.MouseButton1Click:Connect(function()
    print("Função 2 ativada!")
    -- Adicione aqui a lógica da Função 2
end)

SpeedButton.MouseButton1Click:Connect(function()
    local player = game.Players.LocalPlayer
    if player and player.Character then
        player.Character.Humanoid.WalkSpeed = 100 -- Mude para o valor desejado
        print("Velocidade alterada para 100!")
    end
end)

JumpButton.MouseButton1Click:Connect(function()
    local player = game.Players.LocalPlayer
    if player and player.Character then
        player.Character.Humanoid.JumpPower = 150 -- Mude para o valor desejado
        print("Pulo alterado para 150!")
    end
end)

GravityButton.MouseButton1Click:Connect(function()
    local workspace = game.Workspace
    workspace.Gravity = 50 -- Mude para o valor desejado
    print("Gravidade alterada para 50!")
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
    MainFrame.Visible = not MainFrame.Visible
end)
