local decalsyeeted = true
local g = game
local w = g.Workspace
local l = g.Lighting
local t = w.Terrain

-- 🌊 Água leve
t.WaterWaveSize = 0
t.WaterWaveSpeed = 0
t.WaterReflectance = 0
t.WaterTransparency = 1

-- 💡 Iluminação otimizada mas clara
l.GlobalShadows = false
l.FogEnd = 9e9
l.Brightness = 2 -- 🔥 AQUI estava o problema
l.Ambient = Color3.fromRGB(200,200,200)
l.OutdoorAmbient = Color3.fromRGB(200,200,200)
l.EnvironmentDiffuseScale = 0
l.EnvironmentSpecularScale = 0

-- 🎮 Qualidade mínima
settings().Rendering.QualityLevel = Enum.QualityLevel.Level01

for i,v in pairs(g:GetDescendants()) do
   if v:IsA("Part") or v:IsA("Union") or v:IsA("MeshPart") or v:IsA("CornerWedgePart") or v:IsA("TrussPart") then
       v.Material = Enum.Material.Plastic
       v.Reflectance = 0
       
   elseif v:IsA("Decal") and decalsyeeted then
       v.Transparency = 1
       
   elseif v:IsA("ParticleEmitter") or v:IsA("Trail") then
       v.Lifetime = NumberRange.new(0)
       
   elseif v:IsA("Explosion") then
       v.BlastPressure = 1
       v.BlastRadius = 1
   end
end

for i,e in pairs(l:GetChildren()) do
   if e:IsA("BlurEffect") 
   or e:IsA("SunRaysEffect") 
   or e:IsA("ColorCorrectionEffect") 
   or e:IsA("BloomEffect") 
   or e:IsA("DepthOfFieldEffect") then
       e.Enabled = false
   end
end
