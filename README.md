local Library = loadstring(game:HttpGet("https://pastebin.com/raw/LTn9smKx"))() -- Biblioteca para UI
local Window = Library.CreateLib("Banana Cat Hub - Blox Fruit [Premium]", "DarkTheme")

-- Criando as abas
local StatusTab = Window:NewTab("Status And Server")

-------------------
-- STATUS E SERVIDOR
-------------------
local StatusSection = StatusTab:NewSection("Server & Status")

-- Tempo no Servidor
local function GetServerTime()
    local seconds = math.floor(workspace.DistributedGameTime)
    local minutes = math.floor(seconds / 60)
    local hours = math.floor(minutes / 60)
    return string.format("| Hour: %d | Minute: %d | Second: %d |", hours, minutes % 60, seconds % 60)
end

StatusSection:NewLabel("Time")
StatusSection:NewLabel(GetServerTime())

game:GetService("RunService").RenderStepped:Connect(function()
    StatusSection:UpdateLabel(2, GetServerTime())
end)

-- Elite Mob Status
local function CheckEliteMob()
    local eliteMob = game:GetService("ReplicatedStorage")["Remotes"]["EliteHunter"]:InvokeServer("Elite")
    return eliteMob and "✅" or "❌"
end

StatusSection:NewLabel("Elite Mob: " .. CheckEliteMob())

-- Summon Katakuri Status
local function GetKatakuriKills()
    return game:GetService("ReplicatedStorage")["Remotes"]["GetKills"]:InvokeServer("Katakuri") or 0
end

StatusSection:NewLabel("Summon Katakuri: " .. GetKatakuriKills() .. "/500 Mobs")

game:GetService("RunService").RenderStepped:Connect(function()
    StatusSection:UpdateLabel(4, "Summon Katakuri: " .. GetKatakuriKills() .. "/500 Mobs")
end)

-- Mirage, Prehistoric, Frozen Dimension Status
local function CheckDimension(name)
    local status = game:GetService("ReplicatedStorage")["Remotes"]["CheckDimension"]:InvokeServer(name)
    return status and "✅" or "❌"
end

StatusSection:NewLabel("Mirage: " .. CheckDimension("Mirage"))
StatusSection:NewLabel("Prehistoric Island: " .. CheckDimension("Prehistoric"))
StatusSection:NewLabel("Frozen Dimension: " .. CheckDimension("Frozen"))

-- Lua Status (Lua Phase)
local function GetMoonPhase()
    local moonPhase = game:GetService("ReplicatedStorage")["Remotes"]["MoonPhase"]:InvokeServer()
    return moonPhase or "Unknown"
end

StatusSection:NewLabel("Moon: " .. GetMoonPhase())

game:GetService("RunService").RenderStepped:Connect(function()
    StatusSection:UpdateLabel(8, "Moon: " .. GetMoonPhase())
end)

-- Ancient One Status
local function GetAncientOneStatus()
    return game:GetService("ReplicatedStorage")["Remotes"]["AncientOneStatus"]:InvokeServer() or "Unknown"
end

StatusSection:NewLabel("Ancient One Status: " .. GetAncientOneStatus())

-- JobID Input
StatusSection:NewTextBox("Input JobID", "Enter JobID", function(jobid)
    setclipboard(jobid)
    print("JobID Entered:", jobid)
end)

-- Botões de Servidor
StatusSection:NewButton("Clear JobID", "Clears the JobID", function()
    print("JobID Cleared")
end)

StatusSection:NewToggle("Spam Join", "Toggle Spam Join", function(state)
    print("Spam Join: " .. tostring(state))
end)

StatusSection:NewButton("Join Server", "Joins the server", function()
    print("Joining Server...")
end)

StatusSection:NewButton("Copy JobID", "Copies the JobID", function()
    setclipboard(game.JobId)
    print("JobID Copied")
end)

StatusSection:NewButton("Hop Server", "Hops to another server", function()
    game:GetService("TeleportService"):Teleport(game.PlaceId)
end)

StatusSection:NewButton("Hop Server Less People", "Finds a server with fewer players", function()
    -- Código para encontrar um servidor com menos jogadores
end)
