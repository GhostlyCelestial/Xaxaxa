local Players = game:GetService("Players")
local LocalPlayer = Players.LocalPlayer
local ReplicatedStorage = game:GetService("ReplicatedStorage")
local StarterGui = game:GetService("StarterGui")

local function InstantRespawn()
    -- Conectar o evento de morte do Humanoid e garantir respawn instantâneo
    local humanoid = LocalPlayer.Character and LocalPlayer.Character:FindFirstChildWhichIsA("Humanoid")
    if humanoid then
        humanoid.Died:Connect(function()
            -- Disparar respawn imediatamente após a morte
            ReplicatedStorage:WaitForChild("Guide"):FireServer()
        end)
    end
end

-- Garantir que a função de respawn seja chamada toda vez que o personagem for adicionado ou reiniciado
LocalPlayer.CharacterAdded:Connect(function()
    -- Verificar se o personagem tem um humanoide imediatamente e aplicar respawn
    repeat
        local humanoid = LocalPlayer.Character:FindFirstChildWhichIsA("Humanoid")
        if humanoid then
            InstantRespawn()  -- Configurar respawn instantâneo assim que o humanoide estiver disponível
            -- Exibir a notificação para o jogador
            StarterGui:SetCore("SendNotification", {
                Title = "Ghostly 👑",
                Text = "O respawn instantâneo foi ativado!",
                Duration = 3
            })
            break
        end
        wait()  -- Só aguarda até o humanoide aparecer
    until false
end)

-- Se o personagem já existir no momento que o script rodar, configurar o respawn
if LocalPlayer.Character then
    InstantRespawn()
    -- Exibir a notificação para o jogador
    StarterGui:SetCore("SendNotification", {
        Title = "Ghostly 👑",
        Text = "O respawn instantâneo foi ativado!",
        Duration = 3
    })
end
# Xaxaxa
