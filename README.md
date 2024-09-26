# Animalsimscripts

# -- Variables
local player = game.Players.LocalPlayer
local character = player.Character or player.CharacterAdded:Wait()
local mouse = player:GetMouse()
local autoAttackEnabled = true -- Auto-attack toggle
local attackCooldown = 1 -- Cooldown time for attacks in seconds

-- Function to auto-attack
local function autoAttack()
    while autoAttackEnabled do
        local target = mouse.Target
        if target and target:IsA("Model") and target.Name ~= player.Name then
            -- Your attack logic here (e.g., reduce health of the target)
            print("Attacking: " .. target.Name)
            -- You can add actual attack mechanics here, such as dealing damage.
            wait(attackCooldown)
        end
        wait(0.1) -- Small wait to prevent script from running too fast
    end
end

-- Teleport function
local function teleportToMouse()
    local targetPosition = mouse.Hit.Position
    character:SetPrimaryPartCFrame(CFrame.new(targetPosition))
end

-- Input handling
mouse.Button1Down:Connect(function()
    if game:GetService("UserInputService"):IsKeyDown(Enum.KeyCode.LeftControl) then
        teleportToMouse()
    end
end)

-- Start auto-attacking
autoAttack()

-- Optional: Stop auto-attack when the character dies
character.Humanoid.Died:Connect(function()
    autoAttackEnabled = false
end)
