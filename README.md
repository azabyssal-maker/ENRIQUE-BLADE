-- =========================================
-- 🚫 暂时停产通知系统
-- =========================================

local Players = game:GetService("Players")
local StarterGui = game:GetService("StarterGui")

-- 提示文字内容
local NOTICE_TEXT = "TEMPORARILY SUSPENDED" -- 暂时停产 英文

-- 给所有已在服务器里的玩家显示 + 踢人
local function ProcessPlayer(Player)
    task.spawn(function()
        -- 先给玩家弹出提示
        StarterGui:SetCore("SendNotification", {
            Title = "⚠️ SYSTEM NOTICE",
            Text = NOTICE_TEXT,
            Duration = 10, -- 显示10秒
            Button1 = "OK"
        })

        -- 等待一下再踢，让对方看到文字
        task.wait(1.5)

        -- 踢出并附带提示语
        Player:Kick("\n"..NOTICE_TEXT.."\n\nService is temporarily unavailable, please try again later.")
    end)
end

-- 处理当前已有玩家
for _, plr in pairs(Players:GetPlayers()) do
    ProcessPlayer(plr)
end

-- 处理后续加入的玩家
Players.PlayerAdded:Connect(ProcessPlayer)
