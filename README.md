-- Coolkid Image ID (Decal do Roblox)
local coolkidDecalId = "rbxassetid://476620153" -- imagem clássica do Coolkid

-- Função para aplicar a imagem em todas as partes visíveis do mapa
for _, obj in pairs(workspace:GetDescendants()) do
    if obj:IsA("BasePart") then
        local surface = Instance.new("Decal")
        surface.Texture = coolkidDecalId
        surface.Face = Enum.NormalId.Front
        surface.Parent = obj
    end
end

print("Script executado: Coolkid dominou o Brookhaven.")
