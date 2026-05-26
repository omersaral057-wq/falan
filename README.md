-- [[ DYNEX v560 MOBILE ]] --

local Player = game:GetService("Players").LocalPlayer
local PPS = game:GetService("ProximityPromptService")

-- UI
local UI_Target = Player:WaitForChild("PlayerGui")
if UI_Target:FindFirstChild("DynexMobile") then
    UI_Target.DynexMobile:Destroy()
end

local sg = Instance.new("ScreenGui", UI_Target)
sg.Name = "DynexMobile"
sg.ResetOnSpawn = false

local Button = Instance.new("TextButton", sg)
Button.Size = UDim2.new(0, 120, 0, 50)
Button.Position = UDim2.new(0, 20, 0.5, -25)
Button.BackgroundColor3 = Color3.fromRGB(15,15,15)
Button.Text = "INSTANT E: kürt osman"
Button.TextColor3 = Color3.fromRGB(255,50,50)
Button.Font = Enum.Font.GothamBold

Instance.new("UICorner", Button)

local stroke = Instance.new("UIStroke", Button)
stroke.Thickness = 2
stroke.Color = Button.TextColor3

-- LOGIC
local IsActive = false

local function toggle()
    IsActive = not IsActive
    Button.Text = IsActive and "INSTANT E: ON" or "INSTANT E: OFF"
    Button.TextColor3 = IsActive and Color3.fromRGB(0,255,150) or Color3.fromRGB(255,50,50)
    stroke.Color = Button.TextColor3
end

Button.MouseButton1Click:Connect(toggle)

-- TETİKLEME
PPS.PromptButtonHoldBegan:Connect(function(prompt)
    if IsActive then
        prompt.HoldDuration = 0
        task.spawn(function()
            prompt:InputHoldBegin()
            prompt:InputHoldEnd()
            if fireproximityprompt then 
                fireproximityprompt(prompt) 
            end
        end)
    end
end)

PPS.PromptShown:Connect(function(prompt)
    if IsActive then
        prompt.HoldDuration = 0
    end
end)

print("Dynex Mobile Loaded!")
