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
local ESPButton = Instance.new("TextButton")
local ChatButton = Instance.new("TextButton")
local ChatDisplay = Instance.new("ScrollingFrame")
local ChatText = Instance.new("TextLabel")

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
MainFrame.Size = UDim2.new(0, 300, 0, 550)
MainFrame.Position = UDim2.new(0.5, -150, 0.5, -275)
MainFrame.Visible = true

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

ESPButton.Name = "ESPButton"
ESPButton.Parent = MainFrame
ESPButton.Text = "Ativar ESP"
ESPButton.Size = UDim2.new(0, 200, 0, 50)
ESPButton.Position = UDim2.new(0.5, -100, 0, 410)
ESPButton.BackgroundColor3 = Color3.fromRGB(255, 0, 0)

ChatButton.Name = "ChatButton"
ChatButton.Parent = MainFrame
ChatButton.Text = "Ver Conversas Privadas"
ChatButton.Size = UDim2.new(0, 200, 0, 50)
ChatButton.Position = UDim2.new(0.5, -100, 0, 480)
ChatButton.BackgroundColor3 = Color3.fromRGB(0, 150, 150)

ChatDisplay.Name = "ChatDisplay"
ChatDisplay.Parent = MainFrame
ChatDisplay.Size = UDim2.new(0, 280, 0, 150)
ChatDisplay.Position = UDim2.new(0.5, -140, 0, 540)
ChatDisplay.BackgroundColor3 = Color3.fromRGB(20, 20, 20)
ChatDisplay.Visible = false
ChatDisplay.ScrollBarThickness = 10

ChatText.Name = "ChatText"
ChatText.Parent = ChatDisplay
ChatText.Text = ""
ChatText.TextColor3 = Color3.fromRGB(255, 255, 255)
ChatText.BackgroundTransparency = 1
ChatText.Size = UDim2.new(1, 0, 1, 0)
ChatText.TextWrapped = true
ChatText.TextYAlignment = Enum.TextYAlignment.Top
ChatText.Font = Enum.Font.SourceSans
ChatText.TextSize = 14

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
local isESPActive = false

-- Função para alternar visibilidade do painel
ToggleButton.MouseButton1Click:Connect(function()
    MainFrame.Visible = not MainFrame.Visible
end)

-- Função para criar ESP
local function toggleESP()
    if isESPActive then
        for _, player in ipairs(game.Players:GetPlayers()) do
            if player ~= game.Players.LocalPlayer and player.Character then
                for _, part in ipairs(player.Character:GetDescendants()) do
                    if part:IsA("BoxHandleAdornment") and part.Name == "ESP" then
                        part:Destroy()
                    end
                end
            end
        end
        print("ESP desativado")
    else
        for _, player in ipairs(game.Players:GetPlayers()) do
            if player ~= game.Players.LocalPlayer and player.Character then
                for _, part in ipairs(player.Character:GetChildren()) do
                    if part:IsA("BasePart") then
                        local espBox = Instance.new("BoxHandleAdornment")
                        espBox.Name = "ESP"
                        espBox.Size = part.Size
                        espBox.Color3 = Color3.fromRGB(255, 0, 0)
                        espBox.AlwaysOnTop = true
                        espBox.ZIndex = 10
                        espBox.Adornee = part
                        espBox.Parent = part
                    end
                end
            end
        end
        print("ESP ativado")
    end
    isESPActive = not isESPActive
end

-- Função para visualizar conversas privadas
local function monitorChat()
    game.Players.PlayerChatted:Connect(function(chatType, recipient, message)
        if chatType == Enum.PlayerChatType.Whisper and recipient then
            local chatLine = string.format("[%s -> %s]: %s\n", game.Players.LocalPlayer.Name, recipient.Name, message)
            ChatText.Text = ChatText.Text .. chatLine
        end
    end)
    print("Monitoramento de chat ativado!")
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

ESPButton.MouseButton1Click:Connect(toggleESP)

ChatButton.MouseButton1Click:Connect(function()
    ChatDisplay.Visible = not ChatDisplay.Visible
    if ChatDisplay.Visible then
        monitorChat()
    end
end)
