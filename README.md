-- Exemplo educativo (coloque em um LocalScript ou ServerScript no SEU jogo)

local player = game.Players.LocalPlayer
local character = player.Character or player.CharacterAdded:Wait()
local hrp = character:WaitForChild("HumanoidRootPart")

local basePosition = Vector3.new(0, 10, 0) -- posição da sua base
local itemFolder = workspace:WaitForChild("ItensFarm") -- pasta com os itens

local function pegarItem(item)
    if item and item:IsA("BasePart") then
        hrp.CFrame = item.CFrame + Vector3.new(0, 5, 0)
        wait(0.5)
        -- Aqui você faria a lógica de "pegar" (ex: item.Parent = player.Backpack ou remover)
        item:Destroy() -- exemplo simples
    end
end

local function voltarPraBase()
    hrp.CFrame = CFrame.new(basePosition)
end

local function autoFarm()
    while true do
        for _, item in pairs(itemFolder:GetChildren()) do
            if item.Name == "BrainrotCelestial" then -- nome do item no SEU jogo
                pegarItem(item)
                voltarPraBase()
                wait(1)
            end
        end
        wait(2)
    end
end

-- Para rebirth automático (exemplo)
local function autoRebirth()
    -- Aqui você chamaria RemoteEvent ou função do seu sistema de rebirth
    print("Rebirth automático ativado!")
end

-- Ativar com um botão ou comando
game:GetService("UserInputService").InputBegan:Connect(function(input)
    if input.KeyCode == Enum.KeyCode.F then
        autoFarm()
    end
end)
