-- MENU HACK BLOX FRUITS COM VISUAL MODERNO E ANIMAÇÕES -- CRIADO POR DAVID E FRANCISCO

local Players = game:GetService("Players") local LocalPlayer = Players.LocalPlayer local TweenService = game:GetService("TweenService") local GuiService = game:GetService("GuiService")

-- Remover GUIs antigas do mesmo nome if LocalPlayer:FindFirstChild("PlayerGui") and LocalPlayer.PlayerGui:FindFirstChild("D_F_Menu") then LocalPlayer.PlayerGui.D_F_Menu:Destroy() end

-- Criar interface local ScreenGui = Instance.new("ScreenGui") ScreenGui.Name = "D_F_Menu" ScreenGui.Parent = LocalPlayer:WaitForChild("PlayerGui") ScreenGui.ResetOnSpawn = false

-- Criar fundo principal local MainFrame = Instance.new("Frame") MainFrame.Name = "MainFrame" MainFrame.Size = UDim2.new(0, 500, 0, 400) MainFrame.Position = UDim2.new(0.5, -250, 0.5, -200) MainFrame.BackgroundColor3 = Color3.fromRGB(20, 20, 20) MainFrame.BackgroundTransparency = 0.3 MainFrame.BorderSizePixel = 0 MainFrame.AnchorPoint = Vector2.new(0.5, 0.5) MainFrame.Parent = ScreenGui MainFrame.Active = true MainFrame.Draggable = true

-- UICorner arredondado local Corner = Instance.new("UICorner", MainFrame) Corner.CornerRadius = UDim.new(0, 16)

-- UIStroke para contorno local Stroke = Instance.new("UIStroke", MainFrame) Stroke.Color = Color3.fromRGB(255, 255, 255) Stroke.Thickness = 1 Stroke.Transparency = 0.5

-- Título do menu local Title = Instance.new("TextLabel") Title.Text = "D_F BY DAVID E FRANCISCO" Title.Size = UDim2.new(1, 0, 0, 40) Title.BackgroundTransparency = 1 Title.Font = Enum.Font.GothamBold Title.TextSize = 22 Title.TextColor3 = Color3.fromRGB(255, 255, 255) Title.Parent = MainFrame

-- Abas local TabFolder = Instance.new("Folder", MainFrame) TabFolder.Name = "Tabs"

-- Lista de abas e suas cores local TabsInfo = { {Name = "Farm", Color = Color3.fromRGB(0, 200, 0)}, {Name = "Combate", Color = Color3.fromRGB(200, 50, 50)}, {Name = "Visual", Color = Color3.fromRGB(50, 100, 200)}, {Name = "Teleport", Color = Color3.fromRGB(255, 200, 0)}, {Name = "Itens", Color = Color3.fromRGB(200, 0, 200)} }

-- Barra de navegação das abas local TabBar = Instance.new("Frame") TabBar.Size = UDim2.new(1, 0, 0, 40) TabBar.Position = UDim2.new(0, 0, 0, 40) TabBar.BackgroundTransparency = 1 TabBar.Parent = MainFrame

local UIListLayout = Instance.new("UIListLayout", TabBar) UIListLayout.FillDirection = Enum.FillDirection.Horizontal UIListLayout.SortOrder = Enum.SortOrder.LayoutOrder

local CurrentTab = nil

for _, tabInfo in ipairs(TabsInfo) do local Button = Instance.new("TextButton") Button.Size = UDim2.new(0, 100, 1, 0) Button.Text = tabInfo.Name Button.Font = Enum.Font.Gotham Button.TextColor3 = Color3.fromRGB(255, 255, 255) Button.BackgroundColor3 = tabInfo.Color Button.AutoButtonColor = false Button.Parent = TabBar

local TabFrame = Instance.new("Frame")
TabFrame.Name = tabInfo.Name
TabFrame.Visible = false
TabFrame.Size = UDim2.new(1, -20, 1, -90)
TabFrame.Position = UDim2.new(0, 10, 0, 80)
TabFrame.BackgroundTransparency = 1
TabFrame.Parent = TabFolder

local Grid = Instance.new("UIGridLayout", TabFrame)
Grid.CellPadding = UDim2.new(0, 10, 0, 10)
Grid.CellSize = UDim2.new(0.45, 0, 0, 40)

Button.MouseButton1Click:Connect(function()
    if CurrentTab then CurrentTab.Visible = false end
    TabFrame.Visible = true
    CurrentTab = TabFrame
end)

end

-- Exemplo de botão com toggle visual local function CreateToggle(tab, name, callback) local Holder = Instance.new("Frame") Holder.Size = UDim2.new(1, 0, 0, 40) Holder.BackgroundTransparency = 1 Holder.Name = name Holder.Parent = tab

local Button = Instance.new("TextButton")
Button.Size = UDim2.new(1, 0, 1, 0)
Button.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
Button.Text = name
Button.Font = Enum.Font.GothamSemibold
Button.TextColor3 = Color3.fromRGB(255, 255, 255)
Button.TextSize = 14
Button.AutoButtonColor = false
Button.Parent = Holder

local Toggle = Instance.new("Frame")
Toggle.Size = UDim2.new(0, 40, 0, 20)
Toggle.Position = UDim2.new(1, -50, 0.5, -10)
Toggle.BackgroundColor3 = Color3.fromRGB(80, 80, 80)
Toggle.AnchorPoint = Vector2.new(0, 0.5)
Toggle.Parent = Button
Toggle.Name = "ToggleBG"

local Ball = Instance.new("Frame")
Ball.Size = UDim2.new(0, 18, 0, 18)
Ball.Position = UDim2.new(0, 1, 0, 1)
Ball.BackgroundColor3 = Color3.fromRGB(200, 0, 0)
Ball.Parent = Toggle
Ball.Name = "Ball"

local ToggleCorner = Instance.new("UICorner", Toggle)
ToggleCorner.CornerRadius = UDim.new(1, 0)

local BallCorner = Instance.new("UICorner", Ball)
BallCorner.CornerRadius = UDim.new(1, 0)

local On = false

Button.MouseButton1Click:Connect(function()
    On = not On
    if On then
        Ball.BackgroundColor3 = Color3.fromRGB(0, 200, 0)
        TweenService:Create(Ball, TweenInfo.new(0.2), {Position = UDim2.new(1, -19, 0, 1)}):Play()
    else
        Ball.BackgroundColor3 = Color3.fromRGB(200, 0, 0)
        TweenService:Create(Ball, TweenInfo.new(0.2), {Position = UDim2.new(0, 1, 0, 1)}):Play()
    end
    if callback then callback(On) end
end)

end

-- EXEMPLO DE USO CreateToggle(TabFolder.Farm, "Auto Farm", function(on) print("Auto Farm:", on) end)

CreateToggle(TabFolder.Combate, "Kill Aura", function(on) print("Kill Aura:", on) end)

CreateToggle(TabFolder.Visual, "ESP", function(on) print("ESP:", on) end)

CreateToggle(TabFolder.Itens, "Dual Flintlock", function(on) print("Dual Flintlock:", on) end)

CreateToggle(TabFolder.Itens, "Sanguine Art", function(on) print("Sanguine Art:", on) end)

CreateToggle(TabFolder.Teleport, "Teleport para Jogador", function(on) print("Teleport ativado:", on) end)

-- Ativar primeira aba ao iniciar TabFolder.Farm.Visible = true CurrentTab = TabFolder.Farm

