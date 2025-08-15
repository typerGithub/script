local player = game.Players.LocalPlayer
local mouse = player:GetMouse()


local function giveEnderPearl(character)
    local humanoid = character:WaitForChild("Humanoid")

  
    local tool = Instance.new("Tool")
    tool.Name = "EnderPearl"
    tool.RequiresHandle = true
    tool.Parent = player:WaitForChild("Backpack")

   
    local handle = Instance.new("Part")
    handle.Name = "Handle"
    handle.Shape = Enum.PartType.Ball
    handle.Size = Vector3.new(1.5,1.5,1.5)
    handle.Material = Enum.Material.Glass
    handle.Color = Color3.fromRGB(0, 150, 120)
    handle.Transparency = 0.3
    handle.Reflectance = 0.1
    handle.Anchored = false
    handle.CanCollide = false
    handle.Parent = tool

    
    local innerSphere = Instance.new("Part")
    innerSphere.Shape = Enum.PartType.Ball
    innerSphere.Size = Vector3.new(1.2,1.2,1.2)
    innerSphere.Material = Enum.Material.SmoothPlastic
    innerSphere.Color = Color3.fromRGB(0,0,0)
    innerSphere.Anchored = false
    innerSphere.CanCollide = false
    innerSphere.Parent = handle

    local weld = Instance.new("WeldConstraint")
    weld.Part0 = handle
    weld.Part1 = innerSphere
    weld.Parent = handle

   
    for i = 1, 3 do
        local light = Instance.new("PointLight")
        light.Color = Color3.fromRGB(180,255,200)
        light.Brightness = 2
        light.Range = 4
        light.Parent = handle
    end

   
    local particle = Instance.new("ParticleEmitter")
    particle.Texture = "rbxassetid://2529074143"
    particle.Color = ColorSequence.new(Color3.fromRGB(255,255,255))
    particle.LightEmission = 1
    particle.Size = NumberSequence.new(0.2)
    particle.Rate = 8
    particle.Lifetime = NumberRange.new(0.5)
    particle.Speed = NumberRange.new(0)
    particle.Parent = handle

 
    local throwAnim = Instance.new("Animation")
    throwAnim.AnimationId = "rbxassetid://6655555775"
    local animTrack = humanoid:LoadAnimation(throwAnim)

    local debounce = false

    tool.Activated:Connect(function()
        if debounce then return end
        debounce = true

        animTrack:Play()
        task.wait(0)

        local pearl = handle:Clone()
        pearl.Anchored = true
        pearl.CFrame = handle.CFrame * CFrame.new(0, 0, -2)
        pearl.Parent = workspace

        local target = mouse.Hit.Position
        local direction = (target - pearl.Position).Unit
        local distance = (target - pearl.Position).Magnitude
        local speed = 40
        local travelled = 0

        local RS = game:GetService("RunService")
        local conn
        conn = RS.Heartbeat:Connect(function(dt)
            local move = direction * speed * dt
            pearl.CFrame = pearl.CFrame + move
            travelled = travelled + move.Magnitude

            if travelled >= distance then
                character:WaitForChild("HumanoidRootPart").CFrame = CFrame.new(target + Vector3.new(0,3,0))
                pearl:Destroy()
                conn:Disconnect()
            end
        end)

        debounce = false
    end)
end


giveEnderPearl(player.Character or player.CharacterAdded:Wait())


player.CharacterAdded:Connect(function(char)
    giveEnderPearl(char)
end)
