local lp = game.Players.LocalPlayer
local hrp = lp.Character and lp.Character:FindFirstChild("HumanoidRootPart")
local rs = game:GetService("ReplicatedStorage")
local fruits = {"Fruit", "Banana", "Apple", "Gomu", "Mera"} -- nomes possíveis

local function collect(fruit)
    if rs:FindFirstChild("CollectFruit") then
        rs.CollectFruit:FireServer(fruit)
    else
        fruit:Destroy()
    end
end

while wait(1.5) do
    hrp = lp.Character and lp.Character:FindFirstChild("HumanoidRootPart")
    if not hrp then continue end
    for _, v in ipairs(workspace:GetDescendants()) do
        if v:IsA("BasePart") and table.find(fruits, v.Name) then
            if (v.Position - hrp.Position).Magnitude < 100 then
                collect(v)
            end
        end
    end
end
