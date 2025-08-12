-- This script has been converted to FE by iPxter

if game:GetService("RunService"):IsClient() then error("Script must be server-side in order to work; use h/ and not hl/") end local Player,Mouse,mouse,UserInputService,ContextActionService = owner do print("FE Compatibility code by Mokiros | Translated to FE by iPxter") script.Parent = Player.Character

--RemoteEvent for communicating
local Event = Instance.new("RemoteEvent")
Event.Name = "UserInput_Event"

--Fake event to make stuff like Mouse.KeyDown work
local function fakeEvent()
	local t = {_fakeEvent=true,Connect=function(self,f)self.Function=f end}
	t.connect = t.Connect
	return t
end

--Creating fake input objects with fake variables
local m = {Target=nil,Hit=CFrame.new(),KeyUp=fakeEvent(),KeyDown=fakeEvent(),Button1Up=fakeEvent(),Button1Down=fakeEvent()}
local UIS = {InputBegan=fakeEvent(),InputEnded=fakeEvent()}
local CAS = {Actions={},BindAction=function(self,name,fun,touch,...)
	CAS.Actions[name] = fun and {Name=name,Function=fun,Keys={...}} or nil
end}
--Merged 2 functions into one by checking amount of arguments
CAS.UnbindAction = CAS.BindAction

--This function will trigger the events that have been :Connect()'ed
local function te(self,ev,...)
	local t = m[ev]
	if t and t._fakeEvent and t.Function then
		t.Function(...)
	end
end
m.TrigEvent = te
UIS.TrigEvent = te

Event.OnServerEvent:Connect(function(plr,io)
    if plr~=Player then return end
	if io.isMouse then
		m.Target = io.Target
		m.Hit = io.Hit
	else
		local b = io.UserInputState == Enum.UserInputState.Begin
		if io.UserInputType == Enum.UserInputType.MouseButton1 then
			return m:TrigEvent(b and "Button1Down" or "Button1Up")
		end
		for _,t in pairs(CAS.Actions) do
			for _,k in pairs(t.Keys) do
				if k==io.KeyCode then
					t.Function(t.Name,io.UserInputState,io)
				end
			end
		end
		m:TrigEvent(b and "KeyDown" or "KeyUp",io.KeyCode.Name:lower())
		UIS:TrigEvent(b and "InputBegan" or "InputEnded",io,false)
    end
end)
Event.Parent = NLS([==[
local Player = game:GetService("Players").LocalPlayer
local Event = script:WaitForChild("UserInput_Event")

local UIS = game:GetService("UserInputService")
local input = function(io,a)
	if a then return end
	--Since InputObject is a client-side instance, we create and pass table instead
	Event:FireServer({KeyCode=io.KeyCode,UserInputType=io.UserInputType,UserInputState=io.UserInputState})
end
UIS.InputBegan:Connect(input)
UIS.InputEnded:Connect(input)

local Mouse = Player:GetMouse()
local h,t
--Give the server mouse data 30 times every second, but only if the values changed
--If player is not moving their mouse, client won't fire events
while wait(1/30) do
	if h~=Mouse.Hit or t~=Mouse.Target then
		h,t=Mouse.Hit,Mouse.Target
		Event:FireServer({isMouse=true,Target=t,Hit=h})
	end
end]==],Player.Character)
Mouse,mouse,UserInputService,ContextActionService = m,m,UIS,CAS
end

local Player = owner
local FakeMouse = script["1l1l1l1l1l1l1l111l1"]:Clone();
FakeMouse.Parent = Player.Character;
script["1l1l1l1l1l1l1l111l1"]:Destroy()
local Mouse,mouse,UserInputService,ContextActionService
do
	local GUID = {}
	do
	    GUID.IDs = {};
	    function GUID:new(len)
	        local id;
	        if(not len)then
	            id = (tostring(function() end))
	            id = id:gsub("function: ","")
	        else
	            local function genID(len)
	                local newID = ""
	                for i = 1,len do
	                    newID = newID..string.char(math.random(48,90))
	                end
	                return newID
	            end
	            repeat id = genID(len) until not GUID.IDs[id]
				local oid = id;
				id = {Trash=function() GUID.IDs[oid]=nil; end;Get=function() return oid; end}
	            GUID.IDs[oid]=true;
	        end
	        return id
	    end
	end
	local AHB = Instance.new("BindableEvent")
	
	local FPS = 30
	
	local TimeFrame = 0
	
	local LastFrame = tick()
	local Frame = 1/FPS
	
	game:service'RunService'.Heartbeat:connect(function(s,p)
		TimeFrame = TimeFrame + s
		if(TimeFrame >= Frame)then
			for i = 1,math.floor(TimeFrame/Frame) do
				AHB:Fire()
			end
			LastFrame=tick()
			TimeFrame=TimeFrame-Frame*math.floor(TimeFrame/Frame)
		end
	end)
	function swait(dur)
		if(dur == 0 or typeof(dur) ~= 'number')then
			AHB.Event:wait()
		else
			for i = 1, dur*FPS do
				AHB.Event:wait()
			end
		end
	end
	
	local loudnesses={}
	script.Parent = Player.Character
	local CoAS = {Actions={}}
	local Event = Instance.new("RemoteEvent")
	Event.Name = "UserInputEvent"
	Event.Parent = Player.Character
	local Func = Instance.new("RemoteFunction")
	Func.Name = "GetClientProperty"
	Func.Parent = Player.Character
	local fakeEvent = function()
		local t = {_fakeEvent=true,Waited={}}
		t.Connect = function(self,f)
			local ft={Disconnected=false;disconnect=function(s) s.Disconnected=true end}
			ft.Disconnect=ft.disconnect
				
			ft.Func=function(...)
				for id,_ in next, t.Waited do 
					t.Waited[id] = true 
				end 
				return f(...)
			end; 
			self.Function=ft;
			return ft;
		end
		t.connect = t.Connect
		t.Wait = function() 
			local guid = GUID:new(25)
			local waitingId = guid:Get()
			t.Waited[waitingId]=false
			repeat swait() until t.Waited[waitingId]==true  
			t.Waited[waitingId]=nil;
			guid:Trash()
		end
		t.wait = t.Wait
		return t
	end
    local m = {Target=nil,Hit=CFrame.new(),KeyUp=fakeEvent(),KeyDown=fakeEvent(),Button1Up=fakeEvent(),Button1Down=fakeEvent()}
	local UsIS = {InputBegan=fakeEvent(),InputEnded=fakeEvent()}
	
	function CoAS:BindAction(name,fun,touch,...)
		CoAS.Actions[name] = {Name=name,Function=fun,Keys={...}}
	end
	function CoAS:UnbindAction(name)
		CoAS.Actions[name] = nil
	end
	local function te(self,ev,...)
		local t = self[ev]
		if t and t._fakeEvent and t.Function and t.Function.Func and not t.Function.Disconnected then
			t.Function.Func(...)
		elseif t and t._fakeEvent and t.Function and t.Function.Func and t.Function.Disconnected then
			self[ev].Function=nil
		end
	end
	m.TrigEvent = te
	UsIS.TrigEvent = te
	Event.OnServerEvent:Connect(function(plr,io)
	    if plr~=Player then return end
		if io.Mouse then
			m.Target = io.Target
			m.Hit = io.Hit
		elseif io.KeyEvent then
			print('Key'..io.KeyEvent,io.Key)
			m:TrigEvent('Key'..io.KeyEvent,io.Key)
		elseif io.UserInputType == Enum.UserInputType.MouseButton1 then
	        if io.UserInputState == Enum.UserInputState.Begin then
				print'down'
				m:TrigEvent("Button1Down")
			else
				print'up'
				m:TrigEvent("Button1Up")
			end
		end
		if(not io.KeyEvent and not io.Mouse)then
			for n,t in pairs(CoAS.Actions) do
				for _,k in pairs(t.Keys) do
					if k==io.KeyCode then
						t.Function(t.Name,io.UserInputState,io)
					end
				end
			end
	        if io.UserInputState == Enum.UserInputState.Begin then
				UsIS:TrigEvent("InputBegan",io,false)
			else
				UsIS:TrigEvent("InputEnded",io,false)
	        end
	    end
	end)
		
	Func.OnServerInvoke = function(plr,inst,play)
		if plr~=Player then return end
		if(inst and typeof(inst) == 'Instance' and inst:IsA'Sound')then
			loudnesses[inst]=play	
		end
	end
	
	function GetClientProperty(inst,prop)
		if(prop == 'PlaybackLoudness' and loudnesses[inst])then 
			return loudnesses[inst] 
		elseif(prop == 'PlaybackLoudness')then
			return Func:InvokeClient(Player,'RegSound',inst)
		end
		return Func:InvokeClient(Player,inst,prop)
	end
	Mouse, mouse, UserInputService, ContextActionService = m, m, UsIS, CoAS
end
	
	
	
script.Name = "epic edgy aaaa"
--//====================================================\\--
--||			   CREATED BY SHACKLUSTER
--\\====================================================//--
script:ClearAllChildren()
wait(0.2)
PlayerGui = Player.PlayerGui
--Player = game:GetService("Players").BaatatinhacozidaV3
Cam = workspace.CurrentCamera
Backpack = Player.Backpack
Character = Player.Character
Humanoid = Character.Humanoid
RootPart = Character["HumanoidRootPart"]
Torso = Character["Torso"]
Head = Character["Head"]
RightArm = Character["Right Arm"]
LeftArm = Character["Left Arm"]
RightLeg = Character["Right Leg"]
LeftLeg = Character["Left Leg"]
RootJoint = RootPart["RootJoint"]
Neck = Torso["Neck"]
RightShoulder = Torso["Right Shoulder"]
LeftShoulder = Torso["Left Shoulder"]
RightHip = Torso["Right Hip"]
LeftHip = Torso["Left Hip"] 
local sick = Instance.new("Sound",Character)
sick.Parent = Torso
sick.Name = "comander_cool"
sick:resume()
sick.Volume = 1.5
sick.Pitch = 1
sick.Looped = true
sick.SoundId = "rbxassetid://3522311451"
local SIZE = 1
local CLOCKLOOP = 0
local CLOCKTARGET = nil
local CLOCKSPEED = 1
local MODE = "HER"
local epicsound = "coffee"
local TIME = 0
local MATERIALS = {"Plastic","Brick","Cobblestone","ForceField","Grass","Granite","Marble","Metal","WoodPlanks","Wood","Sand","Slate"}
local MESSAGES = {"Think your funny, ", "You know why i killed you, ", "You should stop doing that, ","you've fallen off your horse, ","Your not very fun, "}
local NAMES = {"HER","HeR","hEr","her","HER","HeR","hEr","her","NO SMILE","NO SMILE","NO SMILE","HER","HeR","hEr","her","HER","HeR","hEr","her","HER","HeR","hEr","her","HER","HeR","hEr","her","HER","HeR","hEr","her","HER","HeR","hEr","her","HER","HeR","hEr","her","HER","HeR","hEr","her","HER","HeR","hEr","her","HER","HeR","hEr","her","HER","HeR","hEr","her","HER","HeR","hEr","her","HER","HeR","hEr","her","HER","HeR","hEr","her","HER","HeR","hEr","her","HER","HeR","hEr","her","HER","HeR","hEr","her","HER","HeR","hEr","her","HER","HeR","hEr","her","HER","HeR","hEr","her","hEeR","HELP","kARMa","PaInFuL","HaHaH","IdIoT","WaSte","DIE","pLeAse","Fo0l","LosT","FiNaL","DeAAdLYyY","PoIsOn","CANT","StRuGgLe","LeFt","H E R","HeRo??","BeGonE","LoVeEe?","HU-URtT"}
local NAMES2 = {"HER","HER","HER","HER","HER","HER","HER","HER","HER","HER","HER","CHARA","GASTER","FRISK","UNDYNE","BETE NOIRE","ASRIEL DREEMURR"}
local NAMES3 = {"HER","HER","HER","HER","HER","HER","HER","HER","HER","HER","HER","FUNNY AS HELL","A HELLISH MISTAKE","HEEEEEEEEEEEEEEEEEEELL","YOU'RE FUNNY AS HELL","HELL FIRE","COSMIC HELL"}
local NAMES4 = {"HeR","HEr","hER","hEr","her","HER","HeR","HEr","hER","hEr","her","COSMIC DISGUST","DOING THIS IS USELESS","YOU'RE A DISGUST","I WILL MAKE YOU FEEL PAIN","THIS IS TRUE POWER","DISGUSTING"}
local CHATS = {"YOU'RE A COSMIC DISGUST","I WILL MAKE YOU FEEL PAIN","THIS IS TRUE POWER","DISGUSTING"}
local TESTING = {"HeR","HEr","hER","hEr","her","HER","HeR","HEr","hER","hEr","her","BYE BYE","BÌµÌÌÌÌÍÌÍÍÍÌ Ì»Ì¦Ì±ÌÌ¹ÍÌÌ¼YÌ¶ÍÌÌÍÌ½ÌÌÍÍÌ£Ì¡EÌ·ÍÍÌÌÌÍÌºÍÌÍÌ» Ì¸ÍÍÌ¹ÌÌ¹Ì³BÌ¸ÍÌÍÍÌÌ£Ì«ÌÌ°Ì©YÌ´ÍÌÍÌÌÌÌ¾ÌªÌ Ì£Ì®Ì«Ì¹ÍÌ¹Ì±Ì¯EÌ·ÍÍÍÌÍÌÌÌÍÍÍÌ¨ÍÍÌÍÌ","ãBããYããEã ãBããYããEã","BÌ½ÍYÌ½ÍEÌ½Í Ì½ÍBÌ½ÍYÌ½ÍEÌ½Í","DOING THIS IS USELESS","YOUR A MEANINGLESS PEICE OF TRASH","I WILL MAKE YOU FEEL PAIN","HELP ME","HE DID THIS TO ME"}
local TESTING2 = {"HeR","HEr","hER","hEr","her","HER","HeR","HEr","hER","hEr","her","THIS IS TRUE POWER","LET ME SHOW YOU SOMETHING","D-DID YOU JUST WOUND ME?","FUNNY HOW YOU TRY","YOUR LIFE IS A JOKE"}
local funni = {"WRAPPED IN BLACK","WrApPeD iN bLaCc","BIG BLACK,BIGGGGGGGG","tecks2.Text = 	(funni[MRANDOM(1,#funni)])","EAT MY ATOMIC BIG BRAIn","ÊÆâË¥q NI pÆÔÔâÉ¹M","KCALB NI DEPPARW"}
local NAMESCOOL = {"-","--","---","----","-----","------","-------","--------","---------","----------","-----------","-------------","--------------","---------------","----------------","-----------------","------------------","-------------------","--------------------"}
local AUDIOS = {"rbxassetid://1213699447","rbxassetid://1271928003","rbxassetid://234159472","rbxassetid://4493317788","rbxassetid://1439600000","rbxassetid://186712548","rbxassetid://912913413","rbxassetid://3027170745","rbxassetid://4593045407","rbxassetid://2664096416","rbxassetid://2664096416","rbxassetid://1526982644"}
local PEACE = {"Peaceful","PEaceful","PEAceful","PEACeful","PEACEful","PEACEFul","PEACEFUl","PEACEFUL","peacefuL","peacefUL","peaceFUL","peacEFUL","peaCEFUL","peACEFUL","pEACEFUL","PEACEFUL"}
local AUDIOS2 = {"rbxassetid://4479889057","rbxassetid://4359170694","rbxassetid://4489242348"}
local ANGER = {"Angered","ANGERED","AnGeReD","aNgErEd"}
local HELI = {"ATTACK HELICOPTER","ATTACK HELICOPTER","ATTACK HELICOPTER","ATTACK HELICOPTER","ATTACK HELICOPTER","ATTACK HELICOPTER","ATTACK HELICOPTER","ATTACK HELICOPTER","FEAR ME","SUFFER","I AM GOD HERE","YOU'RE FUNNY"}
local AUDIOS3 = {"rbxassetid://4777239843","rbxassetid://2598224585"}
local HATEFULTEXT = {"HeR","HEr","hER","hEr","her","HER","HeR","HEr","hER","hEr","her","THIS IS THE LAST STRAW","HATE","HATEFUL","MAD","PAINFUL","IT HURTS","WHY?"}
local EffectType = {"Wave","Block","Sphere","Swirl","Skull","Crystal"}
local ErrorText = {"HeR","HEr","hER","hEr","her","HER","HeR","HEr","hER","hEr","H3R","*ER","HE#","H#R","HE#R","@&*","@^$","%^","$%^H#R^%$","ERROR","FATAL ERROR","ORIGINAL_VEX","ERORORORORORORORRR","AHAHAHAHAH","DESTRUC#TIVE ERROR"}
IT = Instance.new
CF = CFrame.new
VT = Vector3.new
CS = ColorSequence.new
RAD = math.rad
C3 = Color3.new
UD2 = UDim2.new
BRICKC = BrickColor.new
ANGLES = CFrame.Angles
EULER = CFrame.fromEulerAnglesXYZ
COS = math.cos
ACOS = math.acos
SIN = math.sin
ASIN = math.asin
ABS = math.abs
BRICKCRNDM = BrickColor.Random
MRANDOM = math.random
FLOOR = math.floor
it = Instance.new
NUMK = NumberSequenceKeypoint.new
NUMS = NumberSequence.new
NUMR = NumberRange.new
local HITFLOOR2 = nil
Rad = math.rad
SIZE = 1
for _,c in pairs(Character:GetChildren()) do
if c:IsA("Accessory") then
c:Destroy()
end
end
--//=================================\\
--|| 	      USEFUL VALUES
--\\=================================//
Animation_Speed = 3
local FORCERESET = false
Frame_Speed = 1 / 60 -- (1 / 30) OR (1 / 60)
local Speed = 16
local ROOTC0 = CF(0, 0, 0) * ANGLES(RAD(-90), RAD(0), RAD(180))
local NECKC0 = CF(0, 1, 0) * ANGLES(RAD(-90), RAD(0), RAD(180))
local RIGHTSHOULDERC0 = CF(-0.5, 0, 0) * ANGLES(RAD(0), RAD(90), RAD(0))
local LEFTSHOULDERC0 = CF(0.5, 0, 0) * ANGLES(RAD(0), RAD(-90), RAD(0))
local DAMAGEMULTIPLIER = 1
local ANIM = "Idle"
local ATTACK = false
local EQUIPPED = false
local HOLD = false
local COMBO = 1
local Rooted = false
local SINE = 0
local KEYHOLD = false
local CHANGE = 2 / Animation_Speed
local WALKINGANIM = false
local VALUE1 = false
local VALUE2 = false
local ROBLOXIDLEANIMATION = IT("Animation")
ROBLOXIDLEANIMATION.Name = "Roblox Idle Animation"
ROBLOXIDLEANIMATION.AnimationId = "http://www.roblox.com/asset/?id=180435571"
--ROBLOXIDLEANIMATION.Parent = Humanoid
local WEAPONGUI = IT("ScreenGui", PlayerGui)
WEAPONGUI.Name = "BanishV3Gui"
local Weapon = IT("Model")
Weapon.Name = "Adds"
local Weapon2 = IT("Model")
Weapon2.Name = "Adds"
local Knife = IT("Model")
Knife.Name = "Adds"
local Knife2 = IT("Model")
Knife2.Name = "Adds"
local Watch = IT("Model")
Watch.Name = "Adds"
local Effects = IT("Folder", Character)
Effects.Name = "Effects"
local Heads = IT("Folder", Character)
Heads.Name = "Heads"
local ANIMATOR = Humanoid.Animator
local ANIMATE = Character:FindFirstChild("Animate")
local UNANCHOR = true
local TOBANISH = {}
script.Parent = PlayerGui
local banned = {}
--//=================================\\
--\\=================================//
ff = Instance.new("ForceField",Character)
ff.Visible = false
local naeeym = IT("BillboardGui",Character)
naeeym.AlwaysOnTop = true
naeeym.Size = UDim2.new(5,35,2,15)
naeeym.StudsOffset = Vector3.new(0,4,0)
naeeym.MaxDistance = 75
naeeym.Adornee = Character.Head
naeeym.Name = "Name"
local naeeym2 = IT("BillboardGui",Character)
naeeym2.AlwaysOnTop = true
naeeym2.Size = UDim2.new(7,35,3,15)
naeeym2.StudsOffset = Vector3.new(0,5,0)
naeeym2.MaxDistance = 75
naeeym2.Adornee = Character.Head
naeeym2.Name = "Name2"
local tecks2 = IT("TextLabel",naeeym2)
tecks2.BackgroundTransparency = 1
tecks2.TextScaled = true
tecks2.BorderSizePixel = 0.5
tecks2.Text = ""
tecks2.Font = "Arcade"
tecks2.TextSize = 30
tecks2.TextStrokeTransparency = 0
tecks2.TextColor3 = Color3.fromRGB(MRANDOM(1,255),MRANDOM(1,255),MRANDOM(1,255))
tecks2.TextStrokeColor3 = Color3.fromRGB(MRANDOM(1,255),MRANDOM(1,255),MRANDOM(1,255))
tecks2.Size = UDim2.new(1,0,0.5,0)
tecks2.Parent = naeeym
local tecks3 = IT("TextLabel",naeeym2)
tecks3.BackgroundTransparency = 1
tecks3.TextScaled = true
tecks3.BorderSizePixel = 0.5
tecks3.Text = ""
tecks3.Font = "Arcade"
tecks3.TextSize = 30
tecks3.TextStrokeTransparency = 0
tecks3.TextColor3 = Color3.fromRGB(MRANDOM(1,255),MRANDOM(1,255),MRANDOM(1,255))
tecks3.TextStrokeColor3 = Color3.fromRGB(MRANDOM(1,255),MRANDOM(1,255),MRANDOM(1,255))
tecks3.Size = UDim2.new(1,0,0.5,0)
tecks3.Parent = naeeym
local SKILLTEXTCOLOR = C3(0,0,0)
local SKILLFONT = "Arcade"
local SKILLTEXTSIZE = 6
--//=================================\\
--|| BLACKLIST TO ALL THE SKIDS HERE
--\\=================================//
local BannedIds = {1326245282}
for _,Banned in pairs(BannedIds) do
if Player.UserId == Banned then
Player:Kick("Stop using this you fat skid")
end
end
--//=================================\\
--|| SAZERENOS' ARTIFICIAL HEARTBEAT
--\\=================================//
ArtificialHB = Instance.new("BindableEvent", script)
ArtificialHB.Name = "ArtificialHB"
script:WaitForChild("ArtificialHB")
frame = Frame_Speed
tf = 0
allowframeloss = false
tossremainder = false
lastframe = tick()
script.ArtificialHB:Fire()
game:GetService("RunService").Heartbeat:connect(function(s, p)
	tf = tf + s
	if tf >= frame then
		if allowframeloss then
			script.ArtificialHB:Fire()
			lastframe = tick()
		else
			for i = 1, math.floor(tf / frame) do
				script.ArtificialHB:Fire()
			end
		lastframe = tick()
		end
		if tossremainder then
			tf = 0
		else
			tf = tf - frame * math.floor(tf / frame)
		end
	end
end)
--//=================================\\
--\\=================================//
	Player.Chatted:connect(function(m)
		if(m:sub(1,7) == 'reason/')then
			Reason = m:sub(8) or "You're weak. You'll always be weak, you'll never change."
		end
	end)
--//=================================\\
--|| 	      SOME FUNCTIONS
--\\=================================//
function Raycast(POSITION, DIRECTION, RANGE, IGNOREDECENDANTS)
	return workspace:FindPartOnRay(Ray.new(POSITION, DIRECTION.unit * RANGE), IGNOREDECENDANTS)
end
function PositiveAngle(NUMBER)
	if NUMBER >= 0 then
		NUMBER = 0
	end
	return NUMBER
end
function FadeAway(part)
	local fade = IT("ParticleEmitter",part)
	fade.Texture = "rbxassetid://244221535"
	fade.EmissionDirection = "Top"
	fade.Speed = NUMR(5.21)
	fade.Size = NUMS(0.77,0.48)
	fade.Enabled = true
	fade.Drag = 4.75
	fade.LockedToPart = true
	fade.Lifetime = NUMR(0.54)
	fade.Rate = 66
	fade.LightEmission = 0.85
	fade.Rotation = NUMR(-360,360)
	fade.VelocitySpread = 0.6	
	fade.ZOffset = 2.75
	fade.Acceleration = VT(-11,4,6)
	coroutine.wrap(function()
		while part do
			Swait()
			fade.Color = CS(Color3.fromRGB(0,0,0))
			part.Transparency = part.Transparency + 0.009
			if part.Transparency >= 0.99 then
				part:Destroy()
			end
		end
	end)()
end
function CreateWave(SIZE,WAIT,CFRAME,DOESROT,ROT,COLOR,GROW)
	local wave = CreatePart(3, Effects, "Neon", 0, 0.5, Color3.fromRGB(0,0,0), "Effect", VT(0,0,0))
	local mesh = IT("SpecialMesh",wave)
	mesh.MeshType = "FileMesh"
	mesh.MeshId = "http://www.roblox.com/asset/?id=20329976"
	mesh.Scale = SIZE
	mesh.Offset = VT(0,0,-SIZE.X/8)
	wave.CFrame = CFRAME
	coroutine.resume(coroutine.create(function(PART)
		for i = 1, WAIT do
			Swait()
			mesh.Scale = mesh.Scale + GROW
			mesh.Offset = VT(0,0,-(mesh.Scale.X/8))
			if DOESROT == true then
				wave.CFrame = wave.CFrame * CFrame.fromEulerAnglesXYZ(0,ROT,0)
			end
			wave.Transparency = wave.Transparency + (0.5/WAIT)
			if wave.Transparency > 0.99 then
				wave:remove()
			end
		end
	end))
end
function NegativeAngle(NUMBER)
	if NUMBER <= 0 then
		NUMBER = 0
	end
	return NUMBER
end
function Swait(NUMBER)
	if NUMBER == 0 or NUMBER == nil then
		ArtificialHB.Event:wait()
	else
		for i = 1, NUMBER do
			ArtificialHB.Event:wait()
		end
	end
end
function CreateDebreeRing(FLOOR,POSITION,SIZE,BLOCKSIZE,SWAIT)
	if FLOOR ~= nil then
		coroutine.resume(coroutine.create(function()
			local PART = CreatePart(3, Effects, "Plastic", 0, 1, "Pearl", "DebreeCenter", VT(0,0,0))
			PART.CFrame = CF(POSITION)
			for i = 1, 45 do
				local RingPiece = CreatePart(3, Effects, "Plastic", 0, 0, "Pearl", "DebreePart", BLOCKSIZE)
				RingPiece.Material = FLOOR.Material
				RingPiece.Color = FLOOR.Color
				RingPiece.CFrame = PART.CFrame * ANGLES(RAD(0), RAD(i*8), RAD(0)) * CF(SIZE*4, 0, 0) * ANGLES(RAD(MRANDOM(-360,360)),RAD(MRANDOM(-360,360)),RAD(MRANDOM(-360,360)))
				Debris:AddItem(RingPiece,SWAIT/100)
			end
			PART:remove()
		end))
	end
end
function CreateMesh(MESH, PARENT, MESHTYPE, MESHID, TEXTUREID, SCALE, OFFSET)
	local NEWMESH = IT(MESH)
	if MESH == "SpecialMesh" then
		NEWMESH.MeshType = MESHTYPE
		if MESHID ~= "nil" and MESHID ~= "" then
			NEWMESH.MeshId = "http://www.roblox.com/asset/?id="..MESHID
		end
		if TEXTUREID ~= "nil" and TEXTUREID ~= "" then
			NEWMESH.TextureId = "http://www.roblox.com/asset/?id="..TEXTUREID
		end
	end
	NEWMESH.Offset = OFFSET or VT(0, 0, 0)
	NEWMESH.Scale = SCALE
	NEWMESH.Parent = PARENT
	return NEWMESH
end
function CreatePart(FORMFACTOR, PARENT, MATERIAL, REFLECTANCE, TRANSPARENCY, BRICKCOLOR, NAME, SIZE, ANCHOR)
	local NEWPART = IT("Part")
	NEWPART.formFactor = FORMFACTOR
	NEWPART.Reflectance = REFLECTANCE
	NEWPART.Transparency = TRANSPARENCY
	NEWPART.CanCollide = false
	NEWPART.Locked = true
	NEWPART.Anchored = true
	if ANCHOR == false then
		NEWPART.Anchored = false
	end
	NEWPART.BrickColor = BRICKC(tostring(BRICKCOLOR))
	NEWPART.Name = NAME
	NEWPART.Size = SIZE
	NEWPART.Position = Torso.Position
	NEWPART.Material = MATERIAL
	NEWPART:BreakJoints()
	NEWPART.Parent = PARENT
	return NEWPART
end
	local function weldBetween(a, b)
	    local weldd = Instance.new("ManualWeld")
	    weldd.Part0 = a
	    weldd.Part1 = b
	    weldd.C0 = CFrame.new()
	    weldd.C1 = b.CFrame:inverse() * a.CFrame
	    weldd.Parent = a
	    return weldd
	end
function QuaternionFromCFrame(cf)
	local mx, my, mz, m00, m01, m02, m10, m11, m12, m20, m21, m22 = cf:components()
	local trace = m00 + m11 + m22
	if trace > 0 then 
		local s = math.sqrt(1 + trace)
		local recip = 0.5 / s
		return (m21 - m12) * recip, (m02 - m20) * recip, (m10 - m01) * recip, s * 0.5
	else
		local i = 0
		if m11 > m00 then
			i = 1
		end
		if m22 > (i == 0 and m00 or m11) then
			i = 2
		end
		if i == 0 then
			local s = math.sqrt(m00 - m11 - m22 + 1)
			local recip = 0.5 / s
			return 0.5 * s, (m10 + m01) * recip, (m20 + m02) * recip, (m21 - m12) * recip
		elseif i == 1 then
			local s = math.sqrt(m11 - m22 - m00 + 1)
			local recip = 0.5 / s
			return (m01 + m10) * recip, 0.5 * s, (m21 + m12) * recip, (m02 - m20) * recip
		elseif i == 2 then
			local s = math.sqrt(m22 - m00 - m11 + 1)
			local recip = 0.5 / s return (m02 + m20) * recip, (m12 + m21) * recip, 0.5 * s, (m10 - m01) * recip
		end
	end
end
 
function CreateRing(SIZE,DOESROT,ROT,WAIT,CFRAME,COLOR,GROW)
    local wave = CreatePart(3, Effects, "Neon", 0, 0.5, BRICKC(COLOR), "Effect", VT(0,0,0))
    local mesh = IT("SpecialMesh",wave)
    mesh.MeshType = "FileMesh"
    mesh.MeshId = "http://www.roblox.com/asset/?id=3270017"
    mesh.Scale = SIZE
    mesh.Offset = VT(0,0,0)
    wave.CFrame = CFRAME
    coroutine.resume(coroutine.create(function(PART)
        for i = 1, WAIT do
            Swait()
            mesh.Scale = mesh.Scale + GROW
            if DOESROT == true then
                wave.CFrame = wave.CFrame * CFrame.fromEulerAnglesXYZ(0,ROT,0)
            end
            wave.Transparency = wave.Transparency + (0.5/WAIT)
            if wave.Transparency > 0.99 then
                wave:remove()
            end
        end
    end))
end
 
function MagicSphere(SIZE,WAIT,CFRAME,COLOR,GROW)
    local wave = CreatePart(3, Effects, "Neon", 0, 0, BRICKC(COLOR), "Effect", VT(1,1,1), true)
    local mesh = IT("SpecialMesh",wave)
    mesh.MeshType = "Sphere"
    mesh.Scale = SIZE
    mesh.Offset = VT(0,0,0)
    wave.CFrame = CFRAME
    coroutine.resume(coroutine.create(function(PART)
        for i = 1, WAIT do
            Swait()
            mesh.Scale = mesh.Scale + GROW
            wave.Transparency = wave.Transparency + (1/WAIT)
            if wave.Transparency > 0.99 then
                wave:remove()
            end
        end
    end))
end
 
function Slice(SIZE,WAIT,CFRAME,COLOR,GROW)
    local wave = CreatePart(3, Effects, "Neon", 0, 0.5, BRICKC(COLOR), "Effect", VT(1,1,1), true)
    local mesh = CreateMesh("SpecialMesh", wave, "FileMesh", "448386996", "", VT(0,SIZE/10,SIZE/10), VT(0,0,0))
    wave.CFrame = CFRAME
    coroutine.resume(coroutine.create(function(PART)
        for i = 1, WAIT do
            Swait()
            mesh.Scale = mesh.Scale * GROW
            wave.Transparency = wave.Transparency + (0.5/WAIT)
            if wave.Transparency > 0.99 then
                wave:remove()
            end
        end
    end))
end
function QuaternionToCFrame(px, py, pz, x, y, z, w)
	local xs, ys, zs = x + x, y + y, z + z
	local wx, wy, wz = w * xs, w * ys, w * zs
	local xx = x * xs
	local xy = x * ys
	local xz = x * zs
	local yy = y * ys
	local yz = y * zs
	local zz = z * zs
	return CFrame.new(px, py, pz, 1 - (yy + zz), xy - wz, xz + wy, xy + wz, 1 - (xx + zz), yz - wx, xz - wy, yz + wx, 1 - (xx + yy))
end
 
function QuaternionSlerp(a, b, t)
	local cosTheta = a[1] * b[1] + a[2] * b[2] + a[3] * b[3] + a[4] * b[4]
	local startInterp, finishInterp;
	if cosTheta >= 0.0001 then
		if (1 - cosTheta) > 0.0001 then
			local theta = ACOS(cosTheta)
			local invSinTheta = 1 / SIN(theta)
			startInterp = SIN((1 - t) * theta) * invSinTheta
			finishInterp = SIN(t * theta) * invSinTheta
		else
			startInterp = 1 - t
			finishInterp = t
		end
	else
		if (1 + cosTheta) > 0.0001 then
			local theta = ACOS(-cosTheta)
			local invSinTheta = 1 / SIN(theta)
			startInterp = SIN((t - 1) * theta) * invSinTheta
			finishInterp = SIN(t * theta) * invSinTheta
		else
			startInterp = t - 1
			finishInterp = t
		end
	end
	return a[1] * startInterp + b[1] * finishInterp, a[2] * startInterp + b[2] * finishInterp, a[3] * startInterp + b[3] * finishInterp, a[4] * startInterp + b[4] * finishInterp
end
function Clerp(a, b, t)
	local qa = {QuaternionFromCFrame(a)}
	local qb = {QuaternionFromCFrame(b)}
	local ax, ay, az = a.x, a.y, a.z
	local bx, by, bz = b.x, b.y, b.z
	local _t = 1 - t
	return QuaternionToCFrame(_t * ax + t * bx, _t * ay + t * by, _t * az + t * bz, QuaternionSlerp(qa, qb, t))
end
function CreateFrame(PARENT, TRANSPARENCY, BORDERSIZEPIXEL, POSITION, SIZE, COLOR, BORDERCOLOR, NAME)
	local frame = IT("Frame")
	frame.BackgroundTransparency = TRANSPARENCY
	frame.BorderSizePixel = BORDERSIZEPIXEL
	frame.Position = POSITION
	frame.Size = SIZE
	frame.BackgroundColor3 = COLOR
	frame.BorderColor3 = BORDERCOLOR
	frame.Name = NAME
	frame.Parent = PARENT
	return frame
end
function CreateLabel(PARENT, TEXT, TEXTCOLOR, TEXTFONTSIZE, TEXTFONT, TRANSPARENCY, BORDERSIZEPIXEL, STROKETRANSPARENCY, NAME)
	local label = IT("TextLabel")
	label.BackgroundTransparency = 1
	label.Size = UD2(1, 0, 1, 0)
	label.Position = UD2(0, 0, 0, 0)
	label.TextColor3 = TEXTCOLOR
	label.TextStrokeTransparency = STROKETRANSPARENCY
	label.TextTransparency = TRANSPARENCY
	label.FontSize = TEXTFONTSIZE
	label.Font = TEXTFONT
	label.BorderSizePixel = BORDERSIZEPIXEL
	label.TextScaled = false
	label.Text = TEXT
	label.Name = NAME
	label.Parent = PARENT
	return label
end
function NoOutlines(PART)
	PART.TopSurface, PART.BottomSurface, PART.LeftSurface, PART.RightSurface, PART.FrontSurface, PART.BackSurface = 10, 10, 10, 10, 10, 10
end
function CreateWeldOrSnapOrMotor(TYPE, PARENT, PART0, PART1, C0, C1)
	local NEWWELD = IT(TYPE)
	NEWWELD.Part0 = PART0
	NEWWELD.Part1 = PART1
	NEWWELD.C0 = C0
	NEWWELD.C1 = C1
	NEWWELD.Parent = PARENT
	return NEWWELD
end
local S = IT("Sound")
function CreateSound(ID, PARENT, VOLUME, PITCH, DOESLOOP)
	local NEWSOUND = nil
	coroutine.resume(coroutine.create(function()
		NEWSOUND = S:Clone()
		NEWSOUND.Parent = PARENT
		NEWSOUND.Volume = VOLUME
		NEWSOUND.Pitch = PITCH
		NEWSOUND.SoundId = "http://www.roblox.com/asset/?id="..ID
		NEWSOUND:play()
		if DOESLOOP == true then
			NEWSOUND.Looped = true
		else
			repeat wait(1) until NEWSOUND.Playing == false or NEWSOUND.Parent ~= PARENT
			NEWSOUND:remove()
		end
	end))
	return NEWSOUND
end
function CFrameFromTopBack(at, top, back)
	local right = top:Cross(back)
	return CF(at.x, at.y, at.z, right.x, top.x, back.x, right.y, top.y, back.y, right.z, top.z, back.z)
end
--WACKYEFFECT({EffectType = "", Size = VT(1,1,1), Size2 = VT(0,0,0), Transparency = 0, Transparency2 = 1, CFrame = CF(), MoveToPos = nil, RotationX = 0, RotationY = 0, RotationZ = 0, Material = "Neon", Color = C3(1,1,1), SoundID = nil, SoundPitch = nil, SoundVolume = nil})
function WACKYEFFECT(Table)
	local TYPE = (Table.EffectType or "Sphere")
	local SIZE = (Table.Size or VT(1,1,1))
	local ENDSIZE = (Table.Size2 or VT(0,0,0))
	local TRANSPARENCY = (Table.Transparency or 0)
	local ENDTRANSPARENCY = (Table.Transparency2 or 1)
	local CFRAME = (Table.CFrame or Torso.CFrame)
	local MOVEDIRECTION = (Table.MoveToPos or nil)
	local ROTATION1 = (Table.RotationX or 0)
	local ROTATION2 = (Table.RotationY or 0)
	local ROTATION3 = (Table.RotationZ or 0)
	local MATERIAL = (Table.Material or "Neon")
	local COLOR = (Table.Color or C3(1,1,1))
	local TIME = (Table.Time or 45)
	local SOUNDID = (Table.SoundID or nil)
	local SOUNDPITCH = (Table.SoundPitch or nil)
	local SOUNDVOLUME = (Table.SoundVolume or nil)
	coroutine.resume(coroutine.create(function()
		local PLAYSSOUND = false
		local SOUND = nil
		local EFFECT = CreatePart(3, Effects, MATERIAL, 0, TRANSPARENCY, BRICKC("Pearl"), "Effect", VT(1,1,1), true)
		if SOUNDID ~= nil and SOUNDPITCH ~= nil and SOUNDVOLUME ~= nil then
			PLAYSSOUND = true
			SOUND = CreateSound(SOUNDID, EFFECT, SOUNDVOLUME, SOUNDPITCH, false)
		end
		EFFECT.Color = COLOR
		local MSH = nil
		if TYPE == "Sphere" then
			MSH = CreateMesh("SpecialMesh", EFFECT, "Sphere", "", "", SIZE, VT(0,0,0))
		elseif TYPE == "Block" then
			MSH = IT("BlockMesh",EFFECT) 
			MSH.Scale = VT(SIZE.X,SIZE.X,SIZE.X)
		elseif TYPE == "Wave" then
			MSH = CreateMesh("SpecialMesh", EFFECT, "FileMesh", "20329976", "", SIZE, VT(0,0,-SIZE.X/8))
		elseif TYPE == "Ring" then
			MSH = CreateMesh("SpecialMesh", EFFECT, "FileMesh", "559831844", "", VT(SIZE.X,SIZE.X,0.1), VT(0,0,0))
		elseif TYPE == "Slash" then
			MSH = CreateMesh("SpecialMesh", EFFECT, "FileMesh", "662586858", "", VT(SIZE.X/10,0,SIZE.X/10), VT(0,0,0))
		elseif TYPE == "Round Slash" then
			MSH = CreateMesh("SpecialMesh", EFFECT, "FileMesh", "662585058", "", VT(SIZE.X/10,0,SIZE.X/10), VT(0,0,0))
		elseif TYPE == "Swirl" then
			MSH = CreateMesh("SpecialMesh", EFFECT, "FileMesh", "1051557", "", SIZE, VT(0,0,0))
		elseif TYPE == "Skull" then
			MSH = CreateMesh("SpecialMesh", EFFECT, "FileMesh", "4770583", "", SIZE, VT(0,0,0))
		elseif TYPE == "Crystal" then
			MSH = CreateMesh("SpecialMesh", EFFECT, "FileMesh", "9756362", "", SIZE, VT(0,0,0))
		elseif TYPE == "Hat" then
			MSH = CreateMesh("SpecialMesh", EFFECT, "FileMesh", "173774068", "", SIZE, VT(0,0,0))
		elseif TYPE == "Arm" then
			MSH = CreateMesh("SpecialMesh", EFFECT, "FileMesh", "2828256740", "", SIZE, VT(0,0,0))
		elseif TYPE == "torso" then
			MSH = CreateMesh("SpecialMesh", EFFECT, "FileMesh", "48112070", "", SIZE, VT(0,0,0))
		elseif TYPE == "Head" then
			MSH = CreateMesh("SpecialMesh", EFFECT, "FileMesh", "539723444", "", SIZE, VT(0,0,0))
		elseif TYPE == "Mask" then
			MSH = CreateMesh("SpecialMesh", EFFECT, "FileMesh", "4548197626", "", SIZE, VT(0,0,0))
		end
		if MSH ~= nil then
			local MOVESPEED = nil
			if MOVEDIRECTION ~= nil then
				MOVESPEED = (CFRAME.p - MOVEDIRECTION).Magnitude/TIME
			end
			local GROWTH = SIZE - ENDSIZE
			local TRANS = TRANSPARENCY - ENDTRANSPARENCY
			if TYPE == "Block" then
				EFFECT.CFrame = CFRAME
			else
				EFFECT.CFrame = CFRAME
			end
			for LOOP = 1, TIME+1 do
				Swait()
				MSH.Scale = MSH.Scale - GROWTH/TIME
				if TYPE == "Wave" then
					MSH.Offset = VT(0,0,-MSH.Scale.X/8)
				end
				EFFECT.Transparency = EFFECT.Transparency - TRANS/TIME
				if TYPE == "Block" then
					EFFECT.CFrame = EFFECT.CFrame*ANGLES(RAD(ROTATION1),RAD(ROTATION2),RAD(ROTATION3))
				else
					EFFECT.CFrame = EFFECT.CFrame*ANGLES(RAD(ROTATION1),RAD(ROTATION2),RAD(ROTATION3))
				end
				if MOVEDIRECTION ~= nil then
					local ORI = EFFECT.Orientation
					EFFECT.CFrame = CF(EFFECT.Position,MOVEDIRECTION)*CF(0,0,-MOVESPEED)
					EFFECT.Orientation = ORI
				end
			end
			if PLAYSSOUND == false then
				EFFECT:remove()
			else
				SOUND.Stopped:Connect(function()
					EFFECT:remove()
				end)
			end
		else
			if PLAYSSOUND == false then
				EFFECT:remove()
			else
				repeat Swait() until SOUND.Playing == false
				EFFECT:remove()
			end
		end
	end))
end
Modco = C3(1,1,1)
local cR=255
local cG=0
local cB=0
local flg5=1 local omgidk=1
local add=15
game:GetService("RunService").Heartbeat:Connect(function()
	if omgidk>10000 then omgidk=0 end
	omgidk=omgidk+1
	if cR>=255 then flg5=1 end
	if cG>=255 then flg5=2 end
	if cB>=255 then flg5=3 end
	if flg5==1 then cR=cR-add cG=cG+add end
	if flg5==2 then cG=cG-add cB=cB+add end
	if flg5==3 then cB=cB-add cR=cR+add end
	color=Color3.fromRGB(cR,cG,cB)
for _, c in pairs(Weapon:GetDescendants()) do
	if c.ClassName == "Part" and c.Name ~= "Eye" and c.Parent ~= Effects and c.Parent.Parent ~= Effects then
		c.Material = "DiamondPlate"
		local val = MRANDOM(1,250)
		c.Color = Color3.fromRGB(val,val,val)
	elseif c.ClassName == "Part" and c.Name == "Eye" then
		local val = MRANDOM(1,250)
		c.Color = Color3.fromRGB(val,val,val)
		c.Material = "DiamondPlate"
	end
end
for _, c in pairs(Weapon2:GetDescendants()) do
	if c.ClassName == "Part" and c.Name ~= "Eye" and c.Parent ~= Effects and c.Parent.Parent ~= Effects then
		c.Material = "DiamondPlate"
		local val = MRANDOM(1,250)
		c.Color = Color3.fromRGB(MRANDOM(1,250),MRANDOM(1,250),MRANDOM(1,250))
	elseif c.ClassName == "Part" and c.Name == "Eye" then
		local val = MRANDOM(1,250)
		c.Color = Color3.fromRGB(MRANDOM(1,250),MRANDOM(1,250),MRANDOM(1,250))
		c.Material = "DiamondPlate"
	end
end
end)
function MakeForm(PART,TYPE)
	if TYPE == "Cyl" then
		local MSH = IT("CylinderMesh",PART)
	elseif TYPE == "Ball" then
		local MSH = IT("SpecialMesh",PART)
		MSH.MeshType = "Sphere"
	elseif TYPE == "Wedge" then
		local MSH = IT("SpecialMesh",PART)
		MSH.MeshType = "Wedge"
	end
end
function SpawnTrail(FROM,TO,BIG)
local TRAIL = CreatePart(3, Effects, "Neon", 0, 0, "White", "Trail", VT(10,10,10))
	MakeForm(TRAIL,"Cyl")
local flg5=1 local omgidk=1
local add=15
game:GetService("RunService").Heartbeat:Connect(function()
local val = MRANDOM(1,255)
	TRAIL.Color = Color3.fromRGB(val,val,val)
end)
	local DIST = (FROM - TO).Magnitude
	if BIG == true then
		TRAIL.Size = VT(0.5,DIST,0.5)
	else
		TRAIL.Size = VT(0.25,DIST,0.25)
	end
	TRAIL.CFrame = CF(FROM, TO) * CF(0, 0, -DIST/2) * ANGLES(RAD(90),RAD(0),RAD(0))
	coroutine.resume(coroutine.create(function()
		for i = 1, 55 do
			Swait()
			TRAIL.Transparency = TRAIL.Transparency + 0.02
		end
		TRAIL:remove()
	end))
end
Debris = game:GetService("Debris")
function CastProperRay(StartPos, EndPos, Distance, Ignore)
	local DIRECTION = CF(StartPos,EndPos).lookVector
	return Raycast(StartPos, DIRECTION, Distance, Ignore)
end
function turnto(position)
	RootPart.CFrame=CFrame.new(RootPart.CFrame.p,VT(position.X,RootPart.Position.Y,position.Z)) * CFrame.new(0, 0, 0)
end
--//=================================\\
--||	     WEAPON CREATION
--\\=================================//
if Player.Name ~= "Commandcodes1234" then
for i,x in pairs(Character:GetDescendants()) do if x:IsA("Shirt") or x:IsA("Pants") then x:Destroy() end end
top=it("Shirt",Character)
top.Name = "Shirt"
bottom=it("Pants",Character)
bottom.Name = "Pants"
Character.Shirt.ShirtTemplate = "http://www.roblox.com/asset/?id=2193780982"
Character.Pants.PantsTemplate = "http://www.roblox.com/asset/?id=129459076"
end
local CharacterMesh=Instance.new("CharacterMesh",Character)
CharacterMesh.BaseTextureId=0
CharacterMesh.BodyPart=Enum.BodyPart.Torso
CharacterMesh.MeshId=48112070
local FaceGradient = IT("Folder", Character)
FaceGradient.Name = "FaceGradient"
for i = 1, 35 do
	local FACE = CreatePart(3, FaceGradient, "Fabric", 0, 0+(i-1)/35.2, "Dark stone grey", "FaceGradient", VT(1.01,0.5,1.01),false)
	FACE.Color = C3(0,0,0)
	Head:FindFirstChildOfClass("SpecialMesh"):Clone().Parent = FACE
	CreateWeldOrSnapOrMotor("Weld", Head, Head, FACE, CF(0,0.35-(i-1)/75,0), CF(0, 0, 0))
end
local Particle = IT("ParticleEmitter",nil)
Particle.Enabled = false
Particle.Transparency = NumberSequence.new({NumberSequenceKeypoint.new(0,0.3),NumberSequenceKeypoint.new(0.3,0),NumberSequenceKeypoint.new(1,1)})
Particle.LightEmission = 0.5
Particle.Rate = 150
Particle.ZOffset = 0.2
Particle.Rotation = NumberRange.new(-180, 180)
Particle.RotSpeed = NumberRange.new(-180, 180)
Particle.Texture = "http://www.roblox.com/asset/?id=304437537"
Particle.Color = ColorSequence.new(C3(1,0,0),C3(0.4,0,0))
--ParticleEmitter({Speed = 5, Drag = 0, Size1 = 1, Size2 = 5, Lifetime1 = 1, Lifetime2 = 1.5, Parent = Torso, Emit = 100, Offset = 360, Enabled = false})
function ParticleEmitter(Table)
	local PRTCL = Particle:Clone()
	local Speed = Table.Speed or 5
	local Drag = Table.Drag or 0
	local Size1 = Table.Size1 or 1
	local Size2 = Table.Size2 or 5
	local Lifetime1 = Table.Lifetime1 or 1
	local Lifetime2 = Table.Lifetime2 or 1.5
	local Parent = Table.Parent or Torso
	local Emit = Table.Emit or 100
	local Offset = Table.Offset or 360
	local Acel = Table.Acel or VT(0,0,0)
	local Enabled = Table.Enabled or false
	PRTCL.Parent = Parent
	PRTCL.Size = NumberSequence.new(Size1,Size2)
	PRTCL.Lifetime = NumberRange.new(Lifetime1,Lifetime2)
	PRTCL.Speed = NumberRange.new(Speed)
	PRTCL.VelocitySpread = Offset
	PRTCL.Drag = Drag
	PRTCL.Acceleration = Acel
	if Enabled == false then
		PRTCL:Emit(Emit)
		Debris:AddItem(PRTCL,Lifetime2)
	else
		PRTCL.Enabled = true
	end
	return PRTCL
end
local HitBox = CreatePart(3, Character, "Neon", 0, 1, "Black", "Hitbox", VT(5,5,5),false)
local weld = CreateWeldOrSnapOrMotor("Weld", HitBox, Torso, HitBox, CF(0,0,0) * ANGLES(RAD(0), RAD(0), RAD(0)), CF(0, 0, 0))
local PRT = CreatePart(3, Heads, "Fabric", 0, 0, "Really black", "Hood", VT(1,1,1),false)
local HoodWeld = CreateWeldOrSnapOrMotor("Weld", Head, Head, PRT, CF(0,1,-0.099), CF(0, 0, 0))
CreateMesh("SpecialMesh", PRT, "FileMesh", 173774068, "", VT(1,1,1)*0.9, VT(0,0,0))
local Gun2 = CreatePart(3, Weapon2, "Fabric", 0, 0, "Mid gray", "Gun", VT(0,0,0),false)
local GEARWELD6 = CreateWeldOrSnapOrMotor("Weld", Torso, Torso, Gun2, CF(1, -1.5, 0.2), CF(0, 0, 0))
CreateMesh("SpecialMesh", Gun2, "FileMesh", 457297958, "", VT(4,4,4), VT(0,0,0))
GEARWELD6.C0 = GEARWELD6.C0 * ANGLES(RAD(-120), RAD(0), RAD(0))
local Gun = CreatePart(3, Weapon, "Fabric", 0, 0, "Mid gray", "Gun", VT(0,0,0),false)
local GEARWELD3 = CreateWeldOrSnapOrMotor("Weld", RightArm, RightArm, Gun, CF(0, -1.7, -0.3), CF(0, 0, 0))
CreateMesh("SpecialMesh", Gun, "FileMesh", 457297958, "", VT(4,4,4), VT(0,0,0))
GEARWELD3.C0 = GEARWELD3.C0 * ANGLES(RAD(-90), RAD(0), RAD(0))
local Hole = CreatePart(3, Weapon, "Metal", 0, 0, "Mid gray", "Eye", VT(0.125,0,0.125),false)
MakeForm(Hole,"Cyl")
CreateWeldOrSnapOrMotor("Weld", Gun, RightArm, Hole, CF(0, -2.83, -0.8), CF(0, 0, 0))
local Knife = CreatePart(3, Knife, "Fabric", 0, 0, "Mid gray", "Knife", VT(0,0,0),false)
local GEARWELD5 = CreateWeldOrSnapOrMotor("Weld", LeftArm, LeftArm, Knife, CF(0.2, -1, -2), CF(0, 0, 0))
CreateMesh("SpecialMesh", Knife, "FileMesh", 1137985639, "", VT(1,1,1), VT(0,0,0))
GEARWELD5.C0 = GEARWELD5.C0 * ANGLES(RAD(90), RAD(-90), RAD(-900))
local Knife2 = CreatePart(3, Knife2, "Fabric", 0, 0, "Mid gray", "Knife2", VT(0,0,0),false)
local GEARWELD4 = CreateWeldOrSnapOrMotor("Weld", Torso, Torso, Knife2, CF(0, 0, 0.7), CF(0, 0, 0))
CreateMesh("SpecialMesh", Knife2, "FileMesh", 1137985639, "", VT(1,1,1), VT(0,0,0))
GEARWELD4.C0 = GEARWELD4.C0 * ANGLES(RAD(900), RAD(0), RAD(-50))
coroutine.resume(coroutine.create(function()
	while wait() do
if MODE == "FIRE" then
	 		RightArm.Material = "Plastic"
		LeftArm.Material = "Plastic"
		Head.Material = "Plastic"
		Torso.Material = "Plastic"
		LeftLeg.Material = "Plastic"
		RightLeg.Material = "Plastic"
	tecks3.Text =  ""
tecks2.TextColor3 = Color3.fromRGB(255,255,255)
tecks2.TextStrokeColor3 = Color3.fromRGB(MRANDOM(1,255),MRANDOM(1,255),MRANDOM(1,255))
tecks2.Text = 	(NAMES2[MRANDOM(1,#NAMES2)])
 		RightArm.Color = Color3.fromRGB(255,255,255)
		LeftArm.Color = Color3.fromRGB(255,255,255)
		Head.Color = Color3.fromRGB(255,255,255)
		Torso.Color = Color3.fromRGB(255,255,255)
		LeftLeg.Color = Color3.fromRGB(255,255,255)
		RightLeg.Color = Color3.fromRGB(255,255,255)
PRT.Color = Color3.fromRGB(255,255,255)
Knife.Color = Color3.fromRGB(MRANDOM(1,255),MRANDOM(1,255),MRANDOM(1,255))
Knife2.Color = Color3.fromRGB(MRANDOM(1,255),MRANDOM(1,255),MRANDOM(1,255))
elseif MODE == "HELL" then
	 		RightArm.Material = "Plastic"
		LeftArm.Material = "Plastic"
		Head.Material = "Plastic"
		Torso.Material = "Plastic"
		LeftLeg.Material = "Plastic"
		RightLeg.Material = "Plastic"
	tecks3.Text =  ""
Knife.Color = Color3.fromRGB(MRANDOM(1,255),MRANDOM(1,255),MRANDOM(1,255))
Knife2.Color = Color3.fromRGB(MRANDOM(1,255),MRANDOM(1,255),MRANDOM(1,255))
tecks2.Text = 	(NAMES3[MRANDOM(1,#NAMES3)])
PRT.Color = Color3.fromRGB(MRANDOM(1,255),50,50)
tecks2.TextColor3 = Color3.fromRGB(MRANDOM(1,255),50,50)
tecks2.TextStrokeColor3 = Color3.fromRGB(MRANDOM(1,255),50,50)
 		RightArm.Color = Color3.fromRGB(MRANDOM(1,255),50,50)
		LeftArm.Color = Color3.fromRGB(MRANDOM(1,255),50,50)
		Head.Color = Color3.fromRGB(MRANDOM(1,255),50,50)
		Torso.Color = Color3.fromRGB(MRANDOM(1,255),50,50)
		LeftLeg.Color = Color3.fromRGB(MRANDOM(1,255),50,50)
		RightLeg.Color = Color3.fromRGB(MRANDOM(1,255),50,50)
elseif MODE == "PAIN" then
	 		RightArm.Material = "Plastic"
		LeftArm.Material = "Plastic"
		Head.Material = "Plastic"
		Torso.Material = "Plastic"
		LeftLeg.Material = "Plastic"
		RightLeg.Material = "Plastic"
	tecks3.Text =  ""
Knife.Color = Color3.fromRGB(MRANDOM(1,255),MRANDOM(1,255),MRANDOM(1,255))
Knife2.Color = Color3.fromRGB(MRANDOM(1,255),MRANDOM(1,255),MRANDOM(1,255))
tecks2.TextColor3 = Color3.fromRGB(MRANDOM(1,255),MRANDOM(1,255),MRANDOM(1,255))
tecks2.TextStrokeColor3 = Color3.fromRGB(MRANDOM(1,255),MRANDOM(1,255),MRANDOM(1,255))
tecks2.Text = 	(NAMES[MRANDOM(1,#NAMES)])
PRT.Color = Color3.fromRGB(MRANDOM(1,255),MRANDOM(1,255),MRANDOM(1,255))
 		RightArm.Color = BrickColor.Random().Color
		LeftArm.Color = BrickColor.Random().Color
		Head.Color = BrickColor.Random().Color
		Torso.Color = BrickColor.Random().Color
		LeftLeg.Color = BrickColor.Random().Color
		RightLeg.Color = BrickColor.Random().Color
elseif MODE == "bruh" then
	 		RightArm.Material = "Plastic"
		LeftArm.Material = "Plastic"
		Head.Material = "Plastic"
		Torso.Material = "Plastic"
		LeftLeg.Material = "Plastic"
		RightLeg.Material = "Plastic"
local pl = GetClientProperty(sick,'PlaybackLoudness')
WACKYEFFECT({Time = 5, EffectType = "Sphere", Size = VT(1+pl/350,1+pl/350,1+pl/350), Size2 = VT(1+pl/350,1+pl/350,1+pl/350), Transparency = 0, Transparency2 = 0.5, CFrame = LeftArm.CFrame*CF(0,-1,0), MoveToPos = nil, RotationX = MRANDOM(500,500), RotationY = MRANDOM(500,500), RotationZ = MRANDOM(500,500), Material = (MATERIALS[MRANDOM(1,#MATERIALS)]), Color = Color3.fromRGB(0,0,0+178*pl/100), SoundID = nil, SoundPitch = nil, SoundVolume = nil})
Knife.Color = Color3.fromRGB(0,0,0+178*pl/100)
Knife2.Color = Color3.fromRGB(0,0,0+178*pl/100)
tecks3.Text =  ""
tecks2.TextColor3 = Color3.fromRGB(0,0,0+178*pl/100)
tecks2.TextStrokeColor3 = Color3.fromRGB(0,0,0+178*pl/100)
tecks2.Text = 	(NAMES4[MRANDOM(1,#NAMES4)])
PRT.Color = Color3.fromRGB(0,0,0+178*pl/100)
 		RightArm.Color = Color3.fromRGB(0,0,0+178*pl/100)
		LeftArm.Color = Color3.fromRGB(0,0,0+178*pl/100)
		Head.Color = Color3.fromRGB(0,0,0+178*pl/100)
		Torso.Color = Color3.fromRGB(0,0,0+178*pl/100)
		LeftLeg.Color = Color3.fromRGB(0,0,0+178*pl/100)
		RightLeg.Color = Color3.fromRGB(0,0,0+178*pl/100)
elseif MODE == "Angered" then
	 		RightArm.Material = "Plastic"
		LeftArm.Material = "Plastic"
		Head.Material = "Plastic"
		Torso.Material = "Plastic"
		LeftLeg.Material = "Plastic"
		RightLeg.Material = "Plastic"
local pl = GetClientProperty(sick,'PlaybackLoudness')
WACKYEFFECT({Time = 5, EffectType = "Block", Size = VT(0.5,0.5,0.5), Size2 = VT(1,1,1), Transparency = 0, Transparency2 = 0.5, CFrame = Hole.CFrame*CF(0,0,0), MoveToPos = nil, RotationX = MRANDOM(0,360), RotationY = MRANDOM(0,360), RotationZ = MRANDOM(0,360), Material = (MATERIALS[MRANDOM(1,#MATERIALS)]), Color = Color3.fromRGB(150,50+178*pl/100,0), SoundID = nil, SoundPitch = nil, SoundVolume = nil})
Knife.Color = Color3.fromRGB(0,50+178*pl/100,0)
Knife2.Color = Color3.fromRGB(0,50+178*pl/100,0)
tecks3.Text =  ""
tecks2.TextColor3 = Color3.fromRGB(150,50+178*pl/100,0)
tecks2.TextStrokeColor3 = Color3.fromRGB(150+178*pl/100,150,0)
tecks2.Text = 	(ANGER[MRANDOM(1,#ANGER)])
PRT.Color = Color3.fromRGB(150,50+178*pl/100,0)
 		RightArm.Color = Color3.fromRGB(150,50+178*pl/100,0)
		LeftArm.Color = Color3.fromRGB(150,50+178*pl/100,0)
		Head.Color = Color3.fromRGB(150,50+178*pl/100,0)
		Torso.Color = Color3.fromRGB(150,50+178*pl/100,0)
		LeftLeg.Color = Color3.fromRGB(150,50+178*pl/100,0)
		RightLeg.Color = Color3.fromRGB(150,50+178*pl/100,0)
elseif MODE == "Fighter" then
	 		RightArm.Material = "Plastic"
		LeftArm.Material = "Plastic"
		Head.Material = "Plastic"
		Torso.Material = "Plastic"
		LeftLeg.Material = "Plastic"
		RightLeg.Material = "Plastic"
local pl = GetClientProperty(sick,'PlaybackLoudness')
WACKYEFFECT({Time = 50, EffectType = "Block", Size = VT(0.5,0.5,0.5), Size2 = VT(1,1,1), Transparency = 0, Transparency2 = 0.5, CFrame = LeftArm.CFrame*CF(0,-1,0), MoveToPos = nil, RotationX = MRANDOM(0,360), RotationY = MRANDOM(0,360), RotationZ = MRANDOM(0,360), Material = (MATERIALS[MRANDOM(1,#MATERIALS)]), Color = Color3.fromRGB(0,100+178*pl/100,0), SoundID = nil, SoundPitch = nil, SoundVolume = nil})
WACKYEFFECT({Time = 50, EffectType = "Block", Size = VT(0.5,0.5,0.5), Size2 = VT(1,1,1), Transparency = 0, Transparency2 = 0.5, CFrame = RightArm.CFrame*CF(0,-1,0), MoveToPos = nil, RotationX = MRANDOM(0,360), RotationY = MRANDOM(0,360), RotationZ = MRANDOM(0,360), Material = (MATERIALS[MRANDOM(1,#MATERIALS)]), Color = Color3.fromRGB(0,100+178*pl/100,0), SoundID = nil, SoundPitch = nil, SoundVolume = nil})
Knife.Color = Color3.fromRGB(0,50+178*pl/100,0)
Knife2.Color = Color3.fromRGB(0,50+178*pl/100,0)
tecks3.Text =  (HELI[MRANDOM(1,#HELI)])
tecks2.TextColor3 = Color3.fromRGB(0,100+178*pl/300,0)
tecks2.TextStrokeColor3 = Color3.fromRGB(0,100+178*pl/300,0)
tecks3.TextColor3 = Color3.fromRGB(0,100+178*pl/300,0)
tecks3.TextStrokeColor3 = Color3.fromRGB(0,100+178*pl/300,0)
tecks2.Text = 	(HELI[MRANDOM(1,#HELI)])
PRT.Color = Color3.fromRGB(0,100+178*pl/100,0)
 		RightArm.Color = Color3.fromRGB(0,100+178*pl/100,0)
		LeftArm.Color = Color3.fromRGB(0,100+178*pl/100,0)
		Head.Color = Color3.fromRGB(0,100+178*pl/100,0)
		Torso.Color = Color3.fromRGB(0,100+178*pl/100,0)
		LeftLeg.Color = Color3.fromRGB(0,100+178*pl/100,0)
		RightLeg.Color = Color3.fromRGB(150,50+178*pl/100,0)
elseif MODE == "Peaceful" then
local pl = GetClientProperty(sick,'PlaybackLoudness')
Knife.Color = Color3.fromRGB(0,50+178*pl/100,150)
Knife2.Color = Color3.fromRGB(0,50+178*pl/100,1510)
tecks3.Text =  ""
 		RightArm.Material = "Plastic"
		LeftArm.Material = "Plastic"
		Head.Material = "Plastic"
		Torso.Material = "Plastic"
		LeftLeg.Material = "Plastic"
		RightLeg.Material = "Plastic"
tecks2.TextColor3 = Color3.fromRGB(0,50+178*pl/100,150)
tecks2.TextStrokeColor3 = Color3.fromRGB(0,50+178*pl/100,150)
tecks2.Text = 	(PEACE[MRANDOM(1,#PEACE)])
PRT.Color = Color3.fromRGB(0,50+178*pl/100,150)
 		RightArm.Color = Color3.fromRGB(0,50+178*pl/100,150)
		LeftArm.Color = Color3.fromRGB(0,50+178*pl/100,150)
		Head.Color = Color3.fromRGB(0,50+178*pl/100,150)
		Torso.Color = Color3.fromRGB(0,50+178*pl/100,150)
		LeftLeg.Color = Color3.fromRGB(0,50+178*pl/100,150)
		RightLeg.Color = Color3.fromRGB(0,50+178*pl/100,150)
elseif MODE == "ByeBye" then
tecks3.Text =  ""
 		RightArm.Material = "Plastic"
		LeftArm.Material = "Plastic"
		Head.Material = "Plastic"
		Torso.Material = "Plastic"
		LeftLeg.Material = "Plastic"
		RightLeg.Material = "Plastic"
local pl = GetClientProperty(sick,'PlaybackLoudness')
tecks2.TextColor3 = Color3.fromRGB(MRANDOM(1,255),MRANDOM(1,255),MRANDOM(1,255))
tecks2.TextStrokeColor3 = Color3.fromRGB(MRANDOM(1,255),MRANDOM(1,255),MRANDOM(1,255))
tecks2.Text = 	(TESTING[MRANDOM(1,#TESTING)])
PRT.Color = Color3.fromRGB(MRANDOM(1,255),MRANDOM(1,255),MRANDOM(1,255))
 		RightArm.Color = BrickColor.Random().Color
		LeftArm.Color = BrickColor.Random().Color
		Head.Color = BrickColor.Random().Color
		Torso.Color = BrickColor.Random().Color
		LeftLeg.Color = BrickColor.Random().Color
		RightLeg.Color = BrickColor.Random().Color
elseif MODE == "HATEFUL" then
tecks3.Text =  ""
 		RightArm.Material = "Plastic"
		LeftArm.Material = "Plastic"
		Head.Material = "Plastic"
		Torso.Material = "Plastic"
		LeftLeg.Material = "Plastic"
		RightLeg.Material = "Plastic"
local pl = GetClientProperty(sick,'PlaybackLoudness')
tecks2.TextColor3 = Color3.fromRGB(MRANDOM(1,255),MRANDOM(1,255),MRANDOM(1,255))
tecks2.TextStrokeColor3 = Color3.fromRGB(MRANDOM(1,255),MRANDOM(1,255),MRANDOM(1,255))
tecks2.Text = 	(HATEFULTEXT[MRANDOM(1,#HATEFULTEXT)])
 		RightArm.Color = Color3.fromRGB(0,0,MRANDOM(100,255))
		LeftArm.Color = Color3.fromRGB(0,0,MRANDOM(100,255))
		Head.Color = Color3.fromRGB(0,0,MRANDOM(100,255))
		Torso.Color = Color3.fromRGB(0,0,MRANDOM(100,255))
		LeftLeg.Color = Color3.fromRGB(0,0,MRANDOM(100,255))
		RightLeg.Color = Color3.fromRGB(0,0,MRANDOM(100,255))
tecks2.TextColor3 = Color3.fromRGB(0,0,MRANDOM(100,255))
tecks2.TextStrokeColor3 = Color3.fromRGB(0,0,MRANDOM(100,255))
PRT.Color = Color3.fromRGB(0,0,MRANDOM(100,255))
tecks2.TextStrokeColor3 = Color3.fromRGB(0,0,MRANDOM(100,255))
PRT.Color = Color3.fromRGB(0,0,MRANDOM(100,255))
			if MRANDOM(1,30) == 10  then
					Neck.C0 = Clerp(Neck.C0, NECKC0 * CF(0, 0, 0) * ANGLES(RAD(0+MRANDOM(-900,900)), RAD(0+MRANDOM(-900,900)), RAD(0+MRANDOM(-900,900))), 3 / Animation_Speed)
		CreateSound(363808674,Head,100,MRANDOM(8,11)/10,false)
WACKYEFFECT({Time = 50, EffectType = "Ring", Size = VT(1,1,0), Size2 = VT(0.5,0.5,0), Transparency = 0.7, Transparency2 = 1, CFrame = RootPart.CFrame*CF(0,0,0), MoveToPos = nil, RotationX = MRANDOM(-30,30), RotationY = MRANDOM(-30,30), RotationZ = MRANDOM(-30,30), Material = (MATERIALS[MRANDOM(1,#MATERIALS)]), Color = Color3.fromRGB(0,0,MRANDOM(100,255)), SoundID = nil, SoundPitch = nil, SoundVolume = nil})
			end
WACKYEFFECT({Time = 50, EffectType = "Skull", Size = VT(2,2,2)*MRANDOM(1,2), Size2 = VT(2,2,2)*MRANDOM(-2,2), Transparency = 0, Transparency2 = 1, CFrame = RootPart.CFrame*CF(0+MRANDOM(-10,10),5,0+MRANDOM(-10,10)), MoveToPos = RootPart.CFrame*CF(0+MRANDOM(-10,10),-5,0+MRANDOM(-10,10)).p, RotationX = MRANDOM(500,500), RotationY = MRANDOM(500,500), RotationZ = MRANDOM(500,500), Material = (MATERIALS[MRANDOM(1,#MATERIALS)]), Color = Color3.fromRGB(0,0,MRANDOM(100,255)), SoundID = nil, SoundPitch = nil, SoundVolume = nil})
elseif MODE == "Sitting" then
tecks3.Text =  ""
local pl = GetClientProperty(sick,'PlaybackLoudness')
tecks2.TextColor3 = Color3.fromRGB(0+225*COS(SINE / 15),0+225*COS(SINE / 15),0+225*COS(SINE / 15))
tecks2.TextStrokeColor3 = Color3.fromRGB(0-225*COS(SINE / 15),0-225*COS(SINE / 15),0-225*COS(SINE / 15))
tecks3.TextColor3 = Color3.fromRGB(0-225*COS(SINE / 15),0-225*COS(SINE / 15),0-225*COS(SINE / 15))
tecks3.TextStrokeColor3 = Color3.fromRGB(0+225*COS(SINE / 15),0+225*COS(SINE / 15),0+225*COS(SINE / 15))
tecks2.Text = 	"relaxing..."
tecks3.Text = 	"relaxing..."
 		RightArm.Material = "Plastic"
		LeftArm.Material = "Plastic"
		Head.Material = "Plastic"
		Torso.Material = "Plastic"
		LeftLeg.Material = "Plastic"
		RightLeg.Material = "Plastic"
PRT.Color = Color3.fromRGB(0+225*COS(SINE / 15),0+225*COS(SINE / 15),0+225*COS(SINE / 15))
 		RightArm.Color = Color3.fromRGB(0+225*COS(SINE / 15),0+225*COS(SINE / 15),0+225*COS(SINE / 15))
		LeftArm.Color = Color3.fromRGB(0+225*COS(SINE / 15),0+225*COS(SINE / 15),0+225*COS(SINE / 15))
		Head.Color = Color3.fromRGB(0+225*COS(SINE / 15),0+225*COS(SINE / 15),0+225*COS(SINE / 15))
		Torso.Color = Color3.fromRGB(0+225*COS(SINE / 15),0+225*COS(SINE / 15),0+225*COS(SINE / 15))
		LeftLeg.Color = Color3.fromRGB(0+225*COS(SINE / 15),0+225*COS(SINE / 15),0+225*COS(SINE / 15))
		RightLeg.Color = Color3.fromRGB(0+225*COS(SINE / 15),0+225*COS(SINE / 15),0+225*COS(SINE / 15))
elseif MODE == "ATTACKER" then
tecks3.Text =  ""
local pl = GetClientProperty(sick,'PlaybackLoudness')
	local val = MRANDOM(1,255)
tecks2.TextColor3 = Color3.fromRGB(val,val,val)
tecks2.TextStrokeColor3 = Color3.fromRGB(val,val,val)
tecks2.Text = 	(TESTING2[MRANDOM(1,#TESTING2)])
PRT.Color = Color3.fromRGB(0+178*pl/100,0+178*pl/100,0+178*pl/100)
 		RightArm.Color = Color3.fromRGB(0+178*pl/100,0+178*pl/100,0+178*pl/100)
		LeftArm.Color = Color3.fromRGB(0+178*pl/100,0+178*pl/100,0+178*pl/100)
		Head.Color = Color3.fromRGB(0+178*pl/100,0+178*pl/100,0+178*pl/100)
		Torso.Color = Color3.fromRGB(0+178*pl/100,0+178*pl/100,0+178*pl/100)
		LeftLeg.Color = Color3.fromRGB(0+178*pl/100,0+178*pl/100,0+178*pl/100)
		RightLeg.Color = Color3.fromRGB(0+178*pl/100,0+178*pl/100,0+178*pl/100)
		 		RightArm.Material = "Plastic"
		LeftArm.Material = "Plastic"
		Head.Material = "Plastic"
		Torso.Material = "Plastic"
		LeftLeg.Material = "Plastic"
		RightLeg.Material = "Plastic"
elseif MODE == "ABRUGER" then
tecks3.Text =  ""
local pl = GetClientProperty(sick,'PlaybackLoudness')
	local val = MRANDOM(1,255)
tecks2.TextColor3 = Color3.fromRGB(val,val,val)
tecks2.TextStrokeColor3 = Color3.fromRGB(val,val,val)
tecks2.Text = 	(funni[MRANDOM(1,#funni)])
PRT.Color = Color3.fromRGB(0+178*pl/100,0+178*pl/100,0+178*pl/100)
 		RightArm.Color = Color3.fromRGB(0+178*pl/100,0+178*pl/100,0+178*pl/100)
		LeftArm.Color = Color3.fromRGB(0+178*pl/100,0+178*pl/100,0+178*pl/100)
		Head.Color = Color3.fromRGB(0+178*pl/100,0+178*pl/100,0+178*pl/100)
		Torso.Color = Color3.fromRGB(0+178*pl/100,0+178*pl/100,0+178*pl/100)
		LeftLeg.Color = Color3.fromRGB(0+178*pl/100,0+178*pl/100,0+178*pl/100)
		RightLeg.Color = Color3.fromRGB(0+178*pl/100,0+178*pl/100,0+178*pl/100)
							sick.Pitch = MRANDOM(11,15)/11
							 		RightArm.Material = "Plastic"
		LeftArm.Material = "Plastic"
		Head.Material = "Plastic"
		Torso.Material = "Plastic"
		LeftLeg.Material = "Plastic"
		RightLeg.Material = "Plastic"
elseif MODE == "Test2" then
tecks3.Text =  ""
local pl = GetClientProperty(sick,'PlaybackLoudness')
	local val = MRANDOM(1,255)
	local val2 = MRANDOM(1,255)
	local epic = MRANDOM(-10,10)
	local epic2 = MRANDOM(-10,10)
WACKYEFFECT({Time = 50, EffectType = "Block", Size = VT(1,1,1), Size2 = VT(0.5,0.5,0.5), Transparency = 0, Transparency2 = 1, CFrame = RootPart.CFrame*CF(epic,-5,epic2), MoveToPos = RootPart.CFrame*CF(epic,5,epic2).p, RotationX = MRANDOM(-250,250), RotationY = MRANDOM(-250,250), RotationZ = MRANDOM(-250,250), Material = (MATERIALS[MRANDOM(1,#MATERIALS)]), Color = Color3.fromRGB(val2,val2,val2), SoundID = nil, SoundPitch = nil, SoundVolume = nil})
tecks2.TextColor3 = Color3.fromRGB(val,val,val)
tecks2.TextStrokeColor3 = Color3.fromRGB(val2,val2,val2)
tecks2.Text = 	(NAMES[MRANDOM(1,#NAMES)])
PRT.Color = Color3.fromRGB(0+pl/1,0+pl/1,0+pl/1)
 		RightArm.Color = Color3.fromRGB(0+pl/1,0+pl/1,0+pl/1)
		LeftArm.Color = Color3.fromRGB(0+pl/1,0+pl/1,0+pl/1)
		Head.Color = Color3.fromRGB(0+pl/1,0+pl/1,0+pl/1)
		Torso.Color = Color3.fromRGB(0+pl/1,0+pl/1,0+pl/1)
		LeftLeg.Color = Color3.fromRGB(0+pl/1,0+pl/1,0+pl/1)
		RightLeg.Color = Color3.fromRGB(0+pl/1,0+pl/1,0+pl/1)
		 		RightArm.Material = "Plastic"
		LeftArm.Material = "Plastic"
		Head.Material = "Plastic"
		Torso.Material = "Plastic"
		LeftLeg.Material = "Plastic"
		RightLeg.Material = "Plastic"
		 		RightArm.Material = "Plastic"
		LeftArm.Material = "Plastic"
		Head.Material = "Plastic"
		Torso.Material = "Plastic"
		LeftLeg.Material = "Plastic"
		RightLeg.Material = "Plastic"
elseif MODE == "HORROR" then
tecks3.Text =  ""
local pl = GetClientProperty(sick,'PlaybackLoudness')
WACKYEFFECT({Time = 50, EffectType = "Sphere", Size = VT(1.5,1.5,1.5)*MRANDOM(1,2), Size2 = VT(1.5,1.5,1.5)*MRANDOM(-2,2), Transparency = 0, Transparency2 = 1, CFrame = RootPart.CFrame*CF(0+MRANDOM(-10,10),-5,0+MRANDOM(-10,10)), MoveToPos = RootPart.CFrame*CF(0+MRANDOM(-10,10),5,0+MRANDOM(-10,10)).p, RotationX = MRANDOM(500,500), RotationY = MRANDOM(500,500), RotationZ = MRANDOM(500,500), Material = (MATERIALS[MRANDOM(1,#MATERIALS)]), Color = Color3.fromRGB(MRANDOM(1,255),50,50), SoundID = nil, SoundPitch = nil, SoundVolume = nil})
tecks2.TextColor3 = Color3.fromRGB(MRANDOM(1,255),50,50)
tecks2.TextStrokeColor3 = Color3.fromRGB(MRANDOM(1,255),50,50)
tecks2.Text = 	(NAMES[MRANDOM(1,#NAMES)])
PRT.Color = Color3.fromRGB(MRANDOM(1,255),50,50)
 		RightArm.Color = Color3.fromRGB(MRANDOM(1,255),50,50)
		LeftArm.Color = Color3.fromRGB(MRANDOM(1,255),50,50)
		Head.Color = Color3.fromRGB(MRANDOM(1,255),50,50)
		Torso.Color = Color3.fromRGB(MRANDOM(1,255),50,50)
		LeftLeg.Color = Color3.fromRGB(MRANDOM(1,255),50,50)
		RightLeg.Color = Color3.fromRGB(MRANDOM(1,255),50,50)
							--sick.Pitch = MRANDOM(11,12)/11
							 		RightArm.Material = "Plastic"
		LeftArm.Material = "Plastic"
		Head.Material = "Plastic"
		Torso.Material = "Plastic"
		LeftLeg.Material = "Plastic"
		RightLeg.Material = "Plastic"
elseif MODE == "Error" then
tecks3.Text =  ""
local pl = GetClientProperty(sick,'PlaybackLoudness')
tecks2.TextColor3 = Color3.fromRGB(50,MRANDOM(1,255),50)
tecks2.TextStrokeColor3 = Color3.fromRGB(50,MRANDOM(1,255),50)
tecks2.Text = 	(ErrorText[MRANDOM(1,#ErrorText)])
PRT.Color = Color3.fromRGB(50,MRANDOM(1,255),50)
 		RightArm.Color = Color3.fromRGB(0,MRANDOM(1,255),0)
		LeftArm.Color = Color3.fromRGB(0,MRANDOM(1,255),0)
		Head.Color = Color3.fromRGB(0,MRANDOM(1,255),0)
		Torso.Color = Color3.fromRGB(0,MRANDOM(1,255),0)
		LeftLeg.Color = Color3.fromRGB(0,MRANDOM(1,255),0)
		RightLeg.Color = Color3.fromRGB(0,MRANDOM(1,255),0)
							--sick.Pitch = MRANDOM(11,12)/11
							 		RightArm.Material = "Plastic"
		LeftArm.Material = "Plastic"
		Head.Material = "Plastic"
		Torso.Material = "Plastic"
		LeftLeg.Material = "Plastic"
		RightLeg.Material = "Plastic"
   WACKYEFFECT({Time = 3, EffectType = "Sphere", Size = VT(0.5+pl/50,0.55,0.5+pl/50), Size2 = VT(0.5+pl/50,0.55,0.5+pl/50), Transparency = 0, Transparency2 = 0, CFrame = RootPart.CFrame*CF(0,-3,0), MoveToPos = nil, RotationX = 0, RotationY = 0, RotationZ = 0, Material = "Neon", Color = Color3.fromRGB(0,0+pl/3,0), SoundID = nil, SoundPitch = nil, SoundVolume = nil})
elseif MODE == "Test3" then
tecks3.Text =  ""
local pl = GetClientProperty(sick,'PlaybackLoudness')
tecks2.TextColor3 = Color3.fromRGB(0+pl/1.5,0,0+pl/1.5)
tecks2.TextStrokeColor3 = Color3.fromRGB(0+pl/1.5,0,0+pl/1.5)
tecks3.TextColor3 = Color3.fromRGB(0+pl/1.5,0,0+pl/1.5)
tecks3.TextStrokeColor3 = Color3.fromRGB(0+pl/1.5,0,0+pl/1.5)
tecks2.Text = 	(NAMESCOOL[MRANDOM(1+pl/30,1+pl/30)])
tecks3.Text = 	(NAMESCOOL[MRANDOM(1+pl/30,1+pl/30)])
PRT.Color = Color3.fromRGB(0+pl/1.5,0,0+pl/1.5)
 		RightArm.Color = Color3.fromRGB(0+pl/1.5,0,0+pl/1.5)
		LeftArm.Color = Color3.fromRGB(0+pl/1.5,0,0+pl/1.5)
		Head.Color = Color3.fromRGB(0+pl/1.5,0,0+pl/1.5)
		Torso.Color = Color3.fromRGB(0+pl/1.5,0,0+pl/1.5)
		LeftLeg.Color = Color3.fromRGB(0+pl/1.5,0,0+pl/1.5)
		RightLeg.Color = Color3.fromRGB(0+pl/1.5,0,0+pl/1.5)
							--sick.Pitch = MRANDOM(11,12)/11
							 		RightArm.Material = "Plastic"
		LeftArm.Material = "Plastic"
		Head.Material = "Plastic"
		Torso.Material = "Plastic"
		LeftLeg.Material = "Plastic"
		RightLeg.Material = "Plastic"
   WACKYEFFECT({Time = 3, EffectType = "Sphere", Size = VT(0.5+pl/50,0.55,0.5+pl/50), Size2 = VT(0.5+pl/50,0.55,0.5+pl/50), Transparency = 0, Transparency2 = 0, CFrame = RootPart.CFrame*CF(0,-3,0), MoveToPos = nil, RotationX = 0, RotationY = 0, RotationZ = 0, Material = "Neon", Color = Color3.fromRGB(0+pl/1.5,0,0+pl/1.5), SoundID = nil, SoundPitch = nil, SoundVolume = nil})
elseif MODE == "HECKING" then
local pl = GetClientProperty(sick,'PlaybackLoudness')
	tecks3.Text =  (NAMESCOOL[MRANDOM(1+pl/50,1+pl/50)])
Knife.Color = Color3.fromRGB(0+178*pl/100,0,0+178*pl/100)
Knife2.Color = Color3.fromRGB(0+178*pl/100,0,0+178*pl/100)
tecks2.TextColor3 = Color3.fromRGB(0+178*pl/100,0+178*pl/100,0+178*pl/100)
tecks2.TextStrokeColor3 = Color3.fromRGB(0+178*pl/100,0+178*pl/100,0+178*pl/100)
tecks3.TextColor3 = Color3.fromRGB(0+178*pl/100,0,0+178*pl/100)
tecks3.TextStrokeColor3 = Color3.fromRGB(0+178*pl/100,0,0+178*pl/100)
tecks2.Text = 	(NAMESCOOL[MRANDOM(1+pl/50,1+pl/50)])
PRT.Color = Color3.fromRGB(0+178*pl/100,0+178*pl/100,0+178*pl/100)
 		RightArm.Color = Color3.fromRGB(0+178*pl/100,0,0+178*pl/100)
		LeftArm.Color = Color3.fromRGB(0+178*pl/100,0,0+178*pl/100)
		Head.Color = Color3.fromRGB(0+178*pl/100,0,0+178*pl/100)
		Torso.Color = Color3.fromRGB(0+178*pl/100,0,0+178*pl/100)
		LeftLeg.Color = Color3.fromRGB(0+178*pl/100,0,0+178*pl/100)
		RightLeg.Color = Color3.fromRGB(0+178*pl/100,0,0+178*pl/100)
		 		RightArm.Material = "Plastic"
		LeftArm.Material = "Plastic"
		Head.Material = "Plastic"
		Torso.Material = "Plastic"
		LeftLeg.Material = "Plastic"
		RightLeg.Material = "Plastic"
elseif MODE == "TwoTime" then
	tecks3.Text =  ""
Knife.Color = Color3.fromRGB(60,60,160)
Knife2.Color =Color3.fromRGB(60,60,160)
 		RightArm.Material = "Plastic"
		LeftArm.Material = "Plastic"
		Head.Material = "Plastic"
		Torso.Material = "Plastic"
		LeftLeg.Material = "Plastic"
		RightLeg.Material = "Plastic"
else
	tecks3.Text =  ""
Knife.Color = Color3.fromRGB(MRANDOM(1,255),MRANDOM(1,255),MRANDOM(1,255))
Knife2.Color = Color3.fromRGB(MRANDOM(1,255),MRANDOM(1,255),MRANDOM(1,255))
tecks2.TextColor3 = Color3.fromRGB(MRANDOM(1,255),MRANDOM(1,255),MRANDOM(1,255))
tecks2.TextStrokeColor3 = Color3.fromRGB(MRANDOM(1,255),MRANDOM(1,255),MRANDOM(1,255))
tecks2.Text = 	(NAMES[MRANDOM(1,#NAMES)])
PRT.Color = Color3.fromRGB(MRANDOM(1,255),MRANDOM(1,255),MRANDOM(1,255))
 		RightArm.Color = BrickColor.Random().Color
		LeftArm.Color = BrickColor.Random().Color
		Head.Color = BrickColor.Random().Color
		Torso.Color = BrickColor.Random().Color
		LeftLeg.Color = BrickColor.Random().Color
		RightLeg.Color = BrickColor.Random().Color
		 		RightArm.Material = "Plastic"
		LeftArm.Material = "Plastic"
		Head.Material = "Plastic"
		Torso.Material = "Plastic"
		LeftLeg.Material = "Plastic"
		RightLeg.Material = "Plastic"
		end
	end
end))
local Part = CreatePart(3, Watch, "Metal", 0, 0, "Mid gray", "Watch", VT(1.05,0.06,1.05)*SIZE,false)
CreateWeldOrSnapOrMotor("Weld", RightArm, RightArm, Part, CF(0,-0.5*SIZE,0) * ANGLES(RAD(0), RAD(0), RAD(0)), CF(0, 0, 0))
local Part = CreatePart(3, Watch, "Metal", 0, 0, "Mid gray", "Watch", VT(0.5,0.1,0.5)*SIZE,false)
CreateWeldOrSnapOrMotor("Weld", RightArm, RightArm, Part, CF(0,-0.5*SIZE,0) * ANGLES(RAD(90), RAD(0), RAD(0)), CF(0, -0.5*SIZE, 0))
MakeForm(Part,"Cyl")
local Part = CreatePart(3, Watch, "Neon", 0, 0, "Mid gray", "Watch", VT(0.45,0.11,0.45)*SIZE,false)
CreateWeldOrSnapOrMotor("Weld", RightArm, RightArm, Part, CF(0,-0.5*SIZE,0) * ANGLES(RAD(90), RAD(0), RAD(0)), CF(0, -0.5*SIZE, 0))
MakeForm(Part,"Cyl")
Part.Color = Color3.fromRGB(MRANDOM(1,255),MRANDOM(1,255),MRANDOM(1,255))
coroutine.resume(coroutine.create(function()
	while wait() do
Part.Color = Color3.fromRGB(MRANDOM(1,255),MRANDOM(1,255),MRANDOM(1,255))
	end
end))
local RING = CreatePart(3, Watch, "Metal", 0, 0, "Mid gray", "Watch", VT(0.055,0.15,0.055)*SIZE,false)
CreateWeldOrSnapOrMotor("Weld", RightArm, RightArm, RING, CF(0,-0.5*SIZE,0) * ANGLES(RAD(90), RAD(0), RAD(0)), CF(0, -0.5*SIZE, 0))
MakeForm(RING,"Cyl")
RING.Color = C3(0,0,0)
for i = 1, 12 do
	local Part = CreatePart(3, Watch, "Metal", 0, 0, "Mid gray", "Watch", VT(0,0.15,0)*SIZE,false)
Part.Color = Color3.fromRGB(MRANDOM(1,255),MRANDOM(1,255),MRANDOM(1,255))
	local MSH = IT("BlockMesh",Part)
	MSH.Scale = VT(0.6,1,1)
	CreateWeldOrSnapOrMotor("Weld", RightArm, RightArm, Part, CF(0,-0.5*SIZE,0) * ANGLES(RAD(90), RAD((360/12)*i), RAD(0)), CF(0, -0.49*SIZE, 0) * CF(0, 0, -0.2*SIZE))
end
local Part = CreatePart(3, Watch, "Metal", 0, 0, "Mid gray", "Watch", VT(0,0.15,0.15)*SIZE,false)
Part.Color = Color3.fromRGB(MRANDOM(1,255),MRANDOM(1,255),MRANDOM(1,255))
local MSH = IT("BlockMesh",Part)
MSH.Scale = VT(0.4,1,1)
local WATCH1 = CreateWeldOrSnapOrMotor("Weld", RightArm, RightArm, Part, CF(0,-0.5*SIZE,0) * ANGLES(RAD(90), RAD(0), RAD(0)), CF(0, -0.49*SIZE, 0) * CF(0, 0, -0.075*SIZE))
local Part = CreatePart(3, Watch, "Metal", 0, 0, "Mid gray", "Watch", VT(0,0.15,0.15/1.5)*SIZE,false)
Part.Color = Color3.fromRGB(MRANDOM(1,255),MRANDOM(1,255),MRANDOM(1,255))
local MSH = IT("BlockMesh",Part)
MSH.Scale = VT(0.4,1,1)
local WATCH2 = CreateWeldOrSnapOrMotor("Weld", RightArm, RightArm, Part, CF(0,-0.5*SIZE,0) * ANGLES(RAD(90), RAD(0), RAD(0)), CF(0, -0.49*SIZE, 0) * CF(0, 0, -(0.075/1.5)*SIZE))
coroutine.resume(coroutine.create(function()
	while true do
		Swait()
		CLOCKLOOP = CLOCKLOOP - 1*CLOCKSPEED
		WATCH1.C0 = Clerp(WATCH1.C0, CF(0,-0.5*SIZE,0) * ANGLES(RAD(90), RAD(CLOCKLOOP*5), RAD(0)), 1 / Animation_Speed)
		WATCH2.C0 = Clerp(WATCH2.C0, CF(0,-0.5*SIZE,0) * ANGLES(RAD(90), RAD(CLOCKLOOP*5/2), RAD(0)), 1 / Animation_Speed)
		if CLOCKLOOP <= -70 then
			if MODE == "HER" then
				CLOCKLOOP = 0
				WACKYEFFECT({Time = 15, EffectType = "Sphere", Size = VT(20,20,20)*SIZE, Size2 = VT(10,10,10), Transparency = 0, Transparency2 = 0, CFrame = Torso.CFrame, MoveToPos = nil, RotationX = 0, RotationY = 0, RotationZ = 0, Material = "ForceField", Color = Color3.fromRGB(MRANDOM(1,255),MRANDOM(1,255),MRANDOM(1,255)), SoundID = nil, SoundPitch = nil, SoundVolume = nil})
				CreateSound(4508352522, Torso, 5, MRANDOM(8,11)/10, false)	
				local HITFLOOR,HITPOS = Raycast(RootPart.Position, (CF(RootPart.Position, RootPart.Position + VT(0, -1, 0))).lookVector, 25*SIZE, Character)
--				ApplyAoE3(HITPOS,10,0,50,50,false)
			elseif MODE == "HELL" then
				CLOCKLOOP = 30
				WACKYEFFECT({Time = 15, EffectType = "Sphere", Size = VT(20,20,20)*SIZE, Size2 = VT(10,10,10), Transparency = 0, Transparency2 = 0, CFrame = Torso.CFrame, MoveToPos = nil, RotationX = 0, RotationY = 0, RotationZ = 0, Material = "ForceField", Color = Color3.fromRGB(MRANDOM(1,255),50,50), SoundID = nil, SoundPitch = nil, SoundVolume = nil})
				CreateSound(4508352522, Torso, 5, MRANDOM(8,11)/10, false)	
				local HITFLOOR,HITPOS = Raycast(RootPart.Position, (CF(RootPart.Position, RootPart.Position + VT(0, -1, 0))).lookVector, 25*SIZE, Character)
--				ApplyAoE3(HITPOS,10,0,50,50,false)
			elseif MODE == "PAIN" then
				CLOCKLOOP = -60
				WACKYEFFECT({Time = 15, EffectType = "Sphere", Size = VT(20,20,20)*SIZE, Size2 = VT(10,10,10), Transparency = 0, Transparency2 = 0, CFrame = Torso.CFrame, MoveToPos = nil, RotationX = 0, RotationY = 0, RotationZ = 0, Material = "ForceField", Color = Color3.fromRGB(MRANDOM(1,255),MRANDOM(1,255),MRANDOM(1,255)), SoundID = nil, SoundPitch = nil, SoundVolume = nil})
				CreateSound(4508352522, Torso, 5, MRANDOM(8,11)/10, false)	
				local HITFLOOR,HITPOS = Raycast(RootPart.Position, (CF(RootPart.Position, RootPart.Position + VT(0, -1, 0))).lookVector, 25*SIZE, Character)
--				ApplyAoE3(HITPOS,10,0,50,50,false)
				if CLOCKTARGET ~= nil then
					CLOCKTARGET.Health = CLOCKTARGET.Health - 20
					if CLOCKTARGET.Torso ~= nil then
						CLOCKTARGET.Torso.CFrame = CLOCKTARGET.Torso.CFrame * ANGLES(RAD(MRANDOM(0,360)), RAD(MRANDOM(0,360)), RAD(MRANDOM(0,360)))
					end
					if CLOCKTARGET.Health == 0 then
						CLOCKTARGET = nil
					end
				end
			end
		end
	end
end))
Knife2.Parent = Character
Knife.Parent = nil
Watch.Parent = Character
Weapon.Parent = nil
local SKILL1FRAME = CreateFrame(WEAPONGUI, 1, 2, UD2(0.1, 0, 0.90, 0), UD2(0.26, 0, 0.07, 0), C3(0,0,0), C3(0, 0, 0), "Skill 1 Frame")
local SKILL2FRAME = CreateFrame(WEAPONGUI, 1, 2, UD2(0.63, 0, 0.90, 0), UD2(0.26, 0, 0.07, 0), C3(0,0,0), C3(0, 0, 0), "Skill 2 Frame")
local SKILL3FRAME = CreateFrame(WEAPONGUI, 1, 2, UD2(0.215, 0, 0.90, 0), UD2(0.26, 0, 0.07, 0), C3(0,0,0), C3(0, 0, 0), "Skill 3 Frame")
local SKILL4FRAME = CreateFrame(WEAPONGUI, 1, 2, UD2(0.525, 0, 0.90, 0), UD2(0.26, 0, 0.07, 0), C3(0,0,0), C3(0, 0, 0), "Skill 4 Frame")
local SKILL5FRAME = CreateFrame(WEAPONGUI, 1, 2, UD2(0.365, 0, 0.90, 0), UD2(0.26, 0, 0.07, 0), C3(0,0,0), C3(0, 0, 0), "Skill 5 Frame")
function printbye(Name)
end
workspace.ChildAdded:connect(function(instance)
    for BANISH = 1, #TOBANISH do
		if TOBANISH[BANISH] ~= nil then
			if instance.Name == TOBANISH[BANISH] then
				coroutine.resume(coroutine.create(function()
					printbye(instance.Name)
					instance:ClearAllChildren()
					Debris:AddItem(instance,0.0005)
				end))
			end
		end
	end
end)
--//=================================\\
--||			DAMAGING
--\\=================================//
function chatfunc(text)
	local chat = coroutine.wrap(function()
	if Character:FindFirstChild("TalkingBillBoard")~= nil then
		Character:FindFirstChild("TalkingBillBoard"):destroy()
	end
	local Bill = Instance.new("BillboardGui",Character)
	Bill.Size = UDim2.new(0,40,0,20)
	Bill.StudsOffset = Vector3.new(0,6,0)
	Bill.Adornee = Character.Head
	Bill.Name = "TalkingBillBoard"
	local Hehe = Instance.new("TextLabel",Bill)
	Hehe.BackgroundTransparency = 1
	Hehe.BorderSizePixel = 0
	Hehe.Text = ""
	Hehe.Font = "Arcade"
	Hehe.TextSize = 20
	Hehe.TextStrokeTransparency = 0
	Hehe.Size = UDim2.new(1,0,0.5,0)
	coroutine.resume(coroutine.create(function()
		while Hehe ~= nil do
			wait()
			Hehe.Position = UDim2.new(math.random(-.3,.3),math.random(-3,3),.1,math.random(-3,3))	
			--Hehe.Rotation = math.random(-5,5)
			Hehe.TextColor3 = Color3.fromRGB(0,0,0)
			Hehe.TextStrokeColor3 = Color3.fromRGB(255,255,255)
		end
	end))
	for i = 1,string.len(text),1 do
		wait()
		Hehe.Text = string.sub(text,1,i)
	end
	wait(3)--Re[math.random(1, 93)]
	for i = 0, 5, .025 do
		wait()
		Bill.ExtentsOffset = Vector3.new(math.random(-i, i), math.random(-i, i), math.random(-i, i))
		Hehe.TextStrokeTransparency = i
		Hehe.TextTransparency = i
	end
	Bill:Destroy()
	end)
chat()
end
chatfunc("THINK YOUR FUNNY")
function onChatted(msg)
	chatfunc(msg)
end
Player.Chatted:connect(onChatted)
function StatLabel(CFRAME, TEXT, COLOR)
	local STATPART = CreatePart(3, Effects, "SmoothPlastic", 0, 1, "Really black", "Effect", VT())
	STATPART.CFrame = CF(CFRAME.p,CFRAME.p+VT(MRANDOM(-5,5),MRANDOM(0,5),MRANDOM(-5,5)))
	local BODYGYRO = IT("BodyGyro", STATPART)
	game:GetService("Debris"):AddItem(STATPART ,5)
	local BILLBOARDGUI = Instance.new("BillboardGui", STATPART)
	BILLBOARDGUI.Adornee = STATPART
	BILLBOARDGUI.Size = UD2(2.5, 0, 2.5 ,0)
	BILLBOARDGUI.StudsOffset = VT(-2, 2, 0)
	BILLBOARDGUI.AlwaysOnTop = false
	local TEXTLABEL = Instance.new("TextLabel", BILLBOARDGUI)
	TEXTLABEL.BackgroundTransparency = 1
	TEXTLABEL.Size = UD2(2.5, 0, 2.5, 0)
	TEXTLABEL.Text = TEXT
	TEXTLABEL.Font = SKILLFONT
	TEXTLABEL.FontSize="Size42"
	TEXTLABEL.TextColor3 = COLOR
	TEXTLABEL.TextStrokeTransparency = 0
	TEXTLABEL.TextScaled = true
	TEXTLABEL.TextWrapped = true
	coroutine.resume(coroutine.create(function(THEPART, THEBODYPOSITION, THETEXTLABEL)
		for i = 1, 10 do
			Swait()
			STATPART.CFrame = STATPART.CFrame * CF(0,0,-0.2)
			TEXTLABEL.TextTransparency = TEXTLABEL.TextTransparency + (1/10)
			TEXTLABEL.TextStrokeTransparency = TEXTLABEL.TextTransparency
		end
		THEPART.Parent = nil
	end),STATPART, TEXTLABEL)
end
function ApplyDamage2(Humanoid,Damage,TorsoPart)
	local defence = Instance.new("BoolValue",Humanoid.Parent)
	defence.Name = ("HitBy"..Player.Name)
	game:GetService("Debris"):AddItem(defence, 0.001)
	Damage = Damage * DAMAGEMULTIPLIER
	if Humanoid.Health ~= 0 then
		local CritChance = MRANDOM(1,100)
		if Damage > Humanoid.Health then
			Damage = math.ceil(Humanoid.Health)
			if Damage == 0 then
				Damage = 0.1
			end
		end
		Humanoid.Health = Humanoid.Health - Damage
	end
end
function ApplyAoE3(POSITION,RANGE,MINDMG,MAXDMG,FLING,INSTAKILL)
	local CHILDREN = workspace:GetDescendants()
	for index, CHILD in pairs(CHILDREN) do
		if CHILD.ClassName == "Model" and CHILD ~= Character and CHILD.Parent ~= Effects then
			local HUM = CHILD:FindFirstChildOfClass("Humanoid")
			if HUM then
				local TORSO = CHILD:FindFirstChild("Torso") or CHILD:FindFirstChild("UpperTorso")
				if TORSO then
					if (TORSO.Position - POSITION).Magnitude <= RANGE then
						if INSTAKILL == true then
							CHILD:BreakJoints()
						else
							local DMG = MRANDOM(MINDMG,MAXDMG)
							ApplyDamage2(HUM,DMG,TORSO)
						end
						if FLING > 0 then
							for _, c in pairs(CHILD:GetChildren()) do
								if c:IsA("BasePart") then
									local bv = Instance.new("BodyVelocity") 
									bv.maxForce = Vector3.new(1e9, 1e9, 1e9)
									bv.velocity = CF(POSITION,TORSO.Position).lookVector*FLING
									bv.Parent = c
									Debris:AddItem(bv,0.05)
								end
							end
						end
					end
				end
			end
		end
	end
end
function ApplyDamage(Humanoid,Damage,TorsoPart)
	local defence = Instance.new("BoolValue",Humanoid.Parent)
	defence.Name = ("HitBy"..Player.Name)
	game:GetService("Debris"):AddItem(defence, 0.001)
	Damage = Damage * DAMAGEMULTIPLIER
	if Humanoid.Health ~= 0 then
		local CritChance = MRANDOM(1,100)
		if Damage > Humanoid.Health then
			Damage = math.ceil(Humanoid.Health)
			if Damage == 0 then
				Damage = 0.1
			end
		end
		Humanoid.Health = Humanoid.Health - Damage
		StatLabel(TorsoPart.CFrame * CF(0, 0 + (TorsoPart.Size.z - 1), 0), Damage, C3(0, 0, 0))
	end
end
function KickThatBruh(CHARACTER)
	g = game.Players:GetPlayers()
	local kickfolder = IT("Folder",Effects)
	local naeeym2 = Instance.new("BillboardGui",kickfolder)
	naeeym2.AlwaysOnTop = false
	naeeym2.Size = UDim2.new(5,35,2,35)
	naeeym2.StudsOffset = Vector3.new(0,1,0)
	naeeym2.Name = "Mark"
	local tecks2 = Instance.new("TextLabel",naeeym2)
	tecks2.BackgroundTransparency = 1
	tecks2.TextScaled = true
	tecks2.BorderSizePixel = 0
	tecks2.Text = "YOUR ALL GONE"
	tecks2.Font = "Arcade"
	tecks2.TextSize = 30
	tecks2.TextStrokeTransparency = 1
	tecks2.TextColor3 = Color3.new(1,1,1)
	tecks2.TextStrokeColor3 = Color3.new(1,0,0)
	tecks2.Size = UDim2.new(1,0,0.5,0)
	tecks2.Parent = naeeym2
	 CreateSound("527749592", CHARACTER, 600, 1, false)
	for i,v in ipairs(CHARACTER:GetChildren()) do
		if v.ClassName == "Part" or v.ClassName == "MeshPart" then
			if v.Name ~= "HumanoidRootPart" then
				local BOD = v:Clone()
				BOD.CanCollide = false
				BOD.Anchored = true
				BOD.CFrame = v.CFrame
				BOD.Parent = kickfolder
				BOD.Material = "Granite"
				BOD.Color = C3(.3,0,0)
				if BOD:FindFirstChildOfClass("Decal") then
					BOD:FindFirstChildOfClass("Decal"):remove()
				end
				if BOD.Name == "Head" then
					naeeym2.Adornee = BOD
				end
				if BOD.ClassName == "MeshPart" then
					BOD.TextureID = ""
				end
			end
		end
	end
	for i,v in pairs(g) do
	v:remove()
	end 
	if CHARACTER ~= "Character" then
	CHARACTER:remove()
	end
	coroutine.resume(coroutine.create(function()
		for i = 1, 50 do
			Swait()
			for i,v in ipairs(kickfolder:GetChildren()) do
				if v.ClassName == "Part" or v.ClassName == "MeshPart" then
					v.Transparency = 1
				end
				naeeym2.Enabled = false
			end
			Swait()
			for i,v in ipairs(kickfolder:GetChildren()) do
				if v.ClassName == "Part" or v.ClassName == "MeshPart" then
					v.Transparency = 0
				end
				naeeym2.Enabled = true
			end
		end
		kickfolder:remove()
	end))
end
function Banish(Foe) 
	if Foe then
		coroutine.resume(coroutine.create(function()
			local plr = game:service'Players':GetPlayerFromCharacter(Foe)
			if plr then
				coroutine.resume(coroutine.create(function()
				wait(0.5)
				plr:Kick(Reason)		
				end))		
			end
			if(Foe:FindFirstChildOfClass'Humanoid')then	
				printbye(Foe.Name)
				Foe.Archivable = true
				local CLONE = Foe:Clone()
				Foe:Destroy()
				CLONE.Parent = Effects
				CLONE:BreakJoints()
				local MATERIALS = {"Glass","Neon"}
				for _, c in pairs(CLONE:GetDescendants()) do
					if c:IsA("BasePart") then
						if c.Name == "Torso" or c.Name == "UpperTorso" or c == CLONE.PrimaryPart then
	 						CreateSound(2152227673, c, 10, 1, false)
						end
						c.Anchored = true
						c.Transparency = c.Transparency + 0.2
						c.Material = MATERIALS[MRANDOM(1,2)]
						c.Color = color
						if c.ClassName == "MeshPart" then
							c.TextureID = ""
						end
						if c:FindFirstChildOfClass("SpecialMesh") then
							c:FindFirstChildOfClass("SpecialMesh").TextureId = ""
						end
						if c:FindFirstChildOfClass("Decal") then
							c:FindFirstChildOfClass("Decal"):remove()
						end
						c.Name = "Banished"
						c.CanCollide = false
					else
						c:remove()
					end
				end
				local A = false
				for i = 1, 35 do
					if A == false then
						A = true
					elseif A == true then
						A = false
					end
					for _, c in pairs(CLONE:GetDescendants()) do
						if c:IsA("BasePart") then
							c.Anchored = true
							c.Material = MATERIALS[MRANDOM(1,2)]
							c.Transparency = c.Transparency + 0.8/35
							if A == false then
								c.CFrame = c.CFrame*CF(MRANDOM(-45,45)/45,MRANDOM(-45,45)/45,MRANDOM(-45,45)/45)
							elseif A == true then
								c.CFrame = c.CFrame*CF(MRANDOM(-45,45)/45,MRANDOM(-45,45)/45,MRANDOM(-45,45)/45)						
							end
						end
					end
					Swait()
				end
				CLONE:remove()
			end
		end))
	end
end
function ApplyAoE(POSITION,RANGE,ISBANISH)
	local CHILDREN = workspace:GetDescendants()
	for index, CHILD in pairs(CHILDREN) do
		if CHILD.ClassName == "Model" and CHILD ~= Character then
			local HUM = CHILD:FindFirstChildOfClass("Humanoid")
			if HUM then
				local TORSO = CHILD:FindFirstChild("Torso") or CHILD:FindFirstChild("UpperTorso")
				if TORSO then
					if (TORSO.Position - POSITION).Magnitude <= RANGE then
						if ISBANISH == true then
							Banish(CHILD)
						else
							if ISBANISH == "Gravity" then
								HUM.PlatformStand = true
								if TORSO:FindFirstChild("V3BanishForce"..Player.Name) then
									local grav = Instance.new("BodyPosition",TORSO)
									grav.D = 15
									grav.P = 20000
									grav.maxForce = Vector3.new(math.huge,math.huge,math.huge)
									grav.position = TORSO.Position
									grav.Name = "V3BanishForce"..Player.Name
								else
									TORSO:FindFirstChild("V3BanishForce"..Player.Name).position = TORSO.Position+VT(0,0.3,0)
									TORSO.RotVelocity = VT(MRANDOM(-25,25),MRANDOM(-25,25),MRANDOM(-25,25))
								end
							else
								HUM.PlatformStand = false
							end
						end
					elseif ISBANISH == "Gravity" then
						if TORSO:FindFirstChild("V3BanishForce"..Player.Name) then
							TORSO:FindFirstChild("V3BanishForce"..Player.Name):remove()
							HUM.PlatformStand = false
						end
					end
				end
			end
		end
	end
end
--//=================================\\
--||	ATTACK FUNCTIONS AND STUFF
--\\=================================//
function killnearest(position,range,maxstrength,direction)
	for i,v in ipairs(workspace:GetChildren()) do
	local body = v:GetChildren()
		for part = 1, #body do
			if((body[part].ClassName == "Part" or body[part].ClassName == "MeshPart") and v ~= Character) then
				if(body[part].Position - position).Magnitude < range then
					local POS = position
					coroutine.resume(coroutine.create(function()
						--body[part].Anchored = true
						body[part].Parent = Effects
						body[part].CanCollide = true
						local SIZE = body[part].Size
						body[part].Material = "Neon"
						CreateSound("2013169887", body[part], 2, MRANDOM(7, 12) / 10)
						for i = 1, 75 do
							Swait()
							body[part].Color = Color3.fromRGB(cR,cG,cB)
						end
						coroutine.resume(coroutine.create(function()
							while true do
								Swait()
								body[part].Color = Color3.fromRGB(cR,cG,cB)
								body[part]:BreakJoints()
							end
						end))
						body[part].Anchored = false
						body[part]:BreakJoints()
						body[part].Velocity = direction.lookVector*maxstrength
						wait(3.7)
						--body[part]:Destroy()
						FadeAway(body[part])
					end))
				end
			end
		end
		if v.ClassName == "Part" and v.Name ~= Player.Name.."'s Protecting Shield of Rainbowness" then
			if v.Anchored == false and (v.Position - position).Magnitude < range then
				local POS = position
				coroutine.resume(coroutine.create(function()
					--v.Anchored = true
					v.Parent = Effects
					local SIZE = v.Size
					v.Material = "Neon"
					CreateSound("2013169887", v, 2, MRANDOM(7, 12) / 10)
					for i = 1, 75 do
						Swait()
						v.Color = Color3.fromRGB(cR,cG,cB)
					end
					coroutine.resume(coroutine.create(function()
						while true do
							Swait()
							v.Color = Color3.fromRGB(cR,cG,cB)
						end
					end))
					v.Anchored = false
					v.Velocity = direction.lookVector*maxstrength
					wait(3.7)
					--v:Destroy()
					FadeAway(v)
				end))
			end
		end
	end
	for i,v in ipairs(workspace:FindFirstChildOfClass("Terrain"):GetChildren()) do
	local body = v:GetChildren()
		for part = 1, #body do
			if((body[part].ClassName == "Part" or body[part].ClassName == "MeshPart") and v ~= Character) then
				if(body[part].Position - position).Magnitude < range then
					local POS = position
					coroutine.resume(coroutine.create(function()
						--body[part].Anchored = true
						body[part].Parent = Effects
						body[part].CanCollide = true
						local SIZE = body[part].Size
						body[part].Material = "Neon"
						CreateSound("2013169887", body[part], 2, MRANDOM(7, 12) / 10)
						for i = 1, 75 do
							Swait()
							body[part].Color = Color3.fromRGB(cR,cG,cB)
						end
						coroutine.resume(coroutine.create(function()
							while true do
								Swait()
								body[part].Color = Color3.fromRGB(cR,cG,cB)
								body[part]:BreakJoints()
							end
						end))
						body[part].Anchored = false
						body[part]:BreakJoints()
						body[part].Velocity = direction.lookVector*maxstrength
						wait(3.7)
						--body[part]:Destroy()
						FadeAway(body[part])
					end))
				end
			end
		end
		if v.ClassName == "Part" and v.Name ~= Player.Name.."'s Protecting Shield of Rainbowness" then
			if v.Anchored == false and (v.Position - position).Magnitude < range then
				local POS = position
				coroutine.resume(coroutine.create(function()
					--v.Anchored = true
					v.Parent = Effects
					local SIZE = v.Size
					v.Material = "Neon"
					CreateSound("2013169887", v, 2, MRANDOM(7, 12) / 10)
					for i = 1, 75 do
						Swait()
						v.Color = Color3.fromRGB(cR,cG,cB)
					end
					coroutine.resume(coroutine.create(function()
						while true do
							Swait()
							v.Color = Color3.fromRGB(cR,cG,cB)
						end
					end))
					v.Anchored = false
					v.Velocity = direction.lookVector*maxstrength
					wait(3.7)
					--v:Destroy()
					FadeAway(v)
				end))
			end
		end
	end
end
function Punish()
	ATTACK = true
	Rooted = false
    VALUE2 = true
	local GYRO = IT("BodyGyro", RootPart)
	GYRO.D = 20
	GYRO.P = 4000
	GYRO.MaxTorque = VT(0, 40000, 0)
	local POS = RootPart.Position + VT(0, 25, 0)
	CreateSound("1371567007", Effects, 35, MRANDOM(9, 10) / 10)
		RootJoint.C0 = Clerp(RootJoint.C0,ROOTC0 * CF(0, 0, 0 + 0.05 * COS(SINE / 12)) * ANGLES(RAD(0), RAD(0), RAD(0)), 0.15 / Animation_Speed)
		Neck.C0 = Clerp(Neck.C0, NECKC0 * CF(0, 0, 0 + ((1) - 1)) * ANGLES(RAD(0 - 2.5 * SIN(SINE / 12)), RAD(0), RAD(0)), 0.15 / Animation_Speed)
		RightShoulder.C0 = Clerp(RightShoulder.C0, CF(1.5, 0.5, -0.5) * ANGLES(RAD(90), RAD(0), RAD(12)) * RIGHTSHOULDERC0, 2 / Animation_Speed)
		--LeftShoulder.C0 = Clerp(LeftShoulder.C0, CF(-1.5, 0.5, -0.5) * ANGLES(RAD(90), RAD(0), RAD(-12)) * LEFTSHOULDERC0, 2 / Animation_Speed)
		RightHip.C0 = Clerp(RightHip.C0, CF(1, -1 - 0.05 * COS(SINE / 12), -0.01) * ANGLES(RAD(0), RAD(90), RAD(0)) * ANGLES(RAD(-8), RAD(0), RAD(0)), 0.15 / Animation_Speed)
		LeftHip.C0 = Clerp(LeftHip.C0, CF(-1, -1 - 0.05 * COS(SINE / 12), -0.01) * ANGLES(RAD(0), RAD(-90), RAD(0)) * ANGLES(RAD(-8), RAD(0), RAD(0)), 0.15 / Animation_Speed)
	coroutine.resume(coroutine.create(function()
		local E = 0
		repeat
			E = E + 5
			GYRO.CFrame = CF(RootPart.Position, Mouse.Hit.p)
			Swait()
		RootJoint.C0 = Clerp(RootJoint.C0,ROOTC0 * CF(0, 0, 0 + 0.05 * COS(SINE / 12)) * ANGLES(RAD(0), RAD(0), RAD(0)), 0.15 / Animation_Speed)
		Neck.C0 = Clerp(Neck.C0, NECKC0 * CF(0, 0, 0 + ((1) - 1)) * ANGLES(RAD(0 - 2.5 * SIN(SINE / 12)), RAD(0), RAD(0)), 0.15 / Animation_Speed)
		RightShoulder.C0 = Clerp(RightShoulder.C0, CF(1.5, 0.5, -0.5) * ANGLES(RAD(90), RAD(0), RAD(12)) * RIGHTSHOULDERC0, 2 / Animation_Speed)
		--LeftShoulder.C0 = Clerp(LeftShoulder.C0, CF(-1.5, 0.5, -0.5) * ANGLES(RAD(90), RAD(0), RAD(-12)) * LEFTSHOULDERC0, 2 / Animation_Speed)
		RightHip.C0 = Clerp(RightHip.C0, CF(1, -1 - 0.05 * COS(SINE / 12), -0.01) * ANGLES(RAD(0), RAD(90), RAD(0)) * ANGLES(RAD(-8), RAD(0), RAD(0)), 0.15 / Animation_Speed)
		LeftHip.C0 = Clerp(LeftHip.C0, CF(-1, -1 - 0.05 * COS(SINE / 12), -0.01) * ANGLES(RAD(0), RAD(-90), RAD(0)) * ANGLES(RAD(-8), RAD(0), RAD(0)), 0.15 / Animation_Speed)
		until ATTACK == false
		GYRO:remove()
	end))
	for i = 1, 50 do
		Swait()
	end
	for i = 1, 25 do
		Swait()
		WACKYEFFECT({
			Time = 15,
			EffectType = "Skull",
			Size = VT(4, 4, 4),
			Size2 = VT(0, 0, 0),
			Transparency = 1,
			Transparency2 = 0,
			CFrame = CF(RightArm.Position) * ANGLES(RAD(MRANDOM(0, 360)), RAD(MRANDOM(0, 360)), RAD(MRANDOM(0, 360))) * CF(0, 0, 35),
			MoveToPos = RightArm.Position,
			RotationX = 0,
			RotationY = 0,
			RotationZ = 0,
			Material = "Neon",
			Color = C3(1, 0, 0),
			SoundID = nil,
			SoundPitch = nil,
			SoundVolume = nil
		})
	end
	local LOOP = 0
	local BEAMO = CreatePart(3, Effects, "Neon", 0, 0, BRICKC("Lime green"), "Beamo", VT(0,0,0))
	MakeForm(BEAMO, "Ball")
	local BEAM = CreatePart(3, Effects, "Neon", 0, 0, BRICKC("Really red"), "Beam", VT(0, 0, 0), true)
	MakeForm(BEAM, "Cyl")
	repeat
		local DISTANCE = (RightArm.Position - Mouse.Hit.p).Magnitude
		if DISTANCE < 2000 then
			BEAMO.Size = VT(3 + 1 * COS(SINE / 4),  3 + 1 * COS(SINE / 4), 3 + 1 * COS(SINE / 4))
	        BEAMO.CFrame = CF(RightArm.Position)
			BEAM.Size = VT(2 + 1 * COS(SINE / 4), DISTANCE, 2 + 1 * COS(SINE / 4))
			BEAM.CFrame = CF(RightArm.Position, Mouse.Hit.p) * CF(0, 0, -DISTANCE / 2) * ANGLES(RAD(90), RAD(0), RAD(0))
			killnearest(Mouse.Hit.p,14,156,RootPart.CFrame)
			WACKYEFFECT({
				Time = 35,
				EffectType = "Sphere",
				Size = VT(6 + 2 * COS(SINE / 4), 6 + 2 * COS(SINE / 4), 6 + 2 * COS(SINE / 4)) * 2,
				Size2 = VT(5, 75, 5),
				Transparency = 0,
				Transparency2 = 1,
				CFrame = CF(Mouse.Hit.p) * ANGLES(RAD(MRANDOM(0, 360)), RAD(MRANDOM(0, 360)), RAD(MRANDOM(0, 360))),
				MoveToPos = nil,
				RotationX = 0,
				RotationY = 0,
				RotationZ = 0,
				Material = "Neon",
				Color = C3(1, 0, 0),
				SoundID = nil,
				SoundPitch = MRANDOM(9, 12) / 10,
				SoundVolume = 10
			})
		WACKYEFFECT({TIME = 25, EffectType = "Sphere", Size = VT(1.5,1.5,1.5), Size2 = VT(0,0,0), Transparency = 0.5, Transparency2 = 1, CFrame = RightArm.CFrame, MoveToPos = RightArm.CFrame*ANGLES(RAD(MRANDOM(0,360)),RAD(MRANDOM(0,360)),RAD(MRANDOM(0,360)))*CF(0,0,-6).p, RotationX = 0, RotationY = 0, RotationZ = 0, Material = "Neon", Color = SKILLTEXTCOLOR, SoundID = nil, SoundPitch = nil, SoundVolume = nil})
			Swait()
			LOOP = LOOP + 1
		end
	until KEYHOLD == false and LOOP >= 35 or DISTANCE >= 2000
	coroutine.resume(coroutine.create(function()
		for i = 1, 15 do
			Swait()
			BEAM.Size = BEAM.Size - VT(0.1, 0, 0.1)
			BEAMO.Size = BEAMO.Size - VT(0.1, 0.1, 0.1)
			BEAM.Transparency = BEAM.Transparency + 0.06666666666666667
			BEAMO.Transparency = BEAMO.Transparency + 0.06666666666666667
end
		BEAM:remove()
		BEAMO:remove()
	end))
	ATTACK = false
	Rooted = false
    VALUE2 = false
end
local BEANED = {}
local BEANED = {}
function BEAN(skid)	
if skid then	
g = game.Players:GetPlayers()
	local kickfolder = IT("Folder",Effects)
	local naeeym2 = Instance.new("BillboardGui",kickfolder)
	naeeym2.AlwaysOnTop = false
	naeeym2.Size = UDim2.new(5,35,2,35)
	naeeym2.StudsOffset = Vector3.new(0,1,0)
	naeeym2.Name = "Mark"
	local tecks2 = Instance.new("TextLabel",naeeym2)
	tecks2.BackgroundTransparency = 1
	tecks2.TextScaled = true
	tecks2.BorderSizePixel = 0
	tecks2.Text = ""
	tecks2.Font = "Arcade"
	tecks2.TextSize = 30
	tecks2.TextStrokeTransparency = 0
	tecks2.TextColor3 = Color3.fromRGB(cR,cG,cB)
	tecks2.TextStrokeColor3 = Color3.fromRGB(cR,cG,cB)
	tecks2.Size = UDim2.new(1,0,0.5,0)
	tecks2.Parent = naeeym2
--CreateSound("395664538", skid, 5, 1, false)
local Players = game:GetService("Players")
local die = Players:FindFirstChild(skid.Name)
--die:Kick()
	if Players:FindFirstChild(skid.Name) then
	die:Kick("You were never allowed here in the first place.")
	end
		if Players:FindFirstChild(skid.Name) then
	die:Kick("You were never allowed here in the first place.")
		end
			if Players:FindFirstChild(skid.Name) then
	die:Kick("You were never allowed here in the first place.")
			end
				if Players:FindFirstChild(skid.Name) then
	die:Kick("You were never allowed here in the first place.")
				end
					if Players:FindFirstChild(skid.Name) then
	die:Kick("You were never allowed here in the first place.")
					end
						if Players:FindFirstChild(skid.Name) then
	die:Kick("You were never allowed here in the first place.")
						end
						table.insert(BEANED,skid.name)
	--]]
			--CreateSound("527749592", game.Workspace, 700, 1, false)
	--CHARACTER:Remove()
	--[[
	for i,v in pairs(g) do
	--v:remove()
	end ]]--
	--[[
	if CHARACTER.Name ~= "Default Dummy" or CHARACTER.Name ~= "NPC" then
for i,v in pairs(g) do
	if string.find(string.upper(v.Name),CHARACTER) == 1 then
v:remove()
end
end
	end]]--
	--[[
		for _, p in pairs(game.Players:GetChildren()) do
		if p:FindFirstChild("CHARACTER") then
		end
	end]]--
	coroutine.resume(coroutine.create(function()
		for i = 1, 50 do
			Swait()
			for i,v in ipairs(kickfolder:GetChildren()) do
				if v.ClassName == "Part" or v.ClassName == "MeshPart" then
					v.Transparency = 1
				end
				naeeym2.Enabled = false
			end
			Swait()
			for i,v in ipairs(kickfolder:GetChildren()) do
				if v.ClassName == "Part" or v.ClassName == "MeshPart" then
					v.Transparency = 0
				end
				naeeym2.Enabled = true
			end
		end
		kickfolder:remove()
	end))
	--wait(6)
	--skid:Remove()
end
end 
function Warp()
    local HITFLOOR,HITPOS = Raycast(Mouse.Hit.p+VT(0,1,0), (CF(RootPart.Position, RootPart.Position + VT(0, -1, 0))).lookVector, 100, Character)
    if HITFLOOR then
        HITPOS = HITPOS + VT(0,3.5,0)
        local POS = RootPart.Position
        RootPart.CFrame = CF(HITPOS,CF(POS,HITPOS)*CF(0,0,-100000).p)
        CreateSound(164320294,Torso,15,1.5,false)
	end
end
function Mach20()
    local HITFLOOR,HITPOS = Raycast(Mouse.Hit.p+VT(0,1,0), (CF(RootPart.Position, RootPart.Position + VT(0, -1, 0))).lookVector, 100, Character)
    if HITFLOOR then
        HITPOS = HITPOS + VT(0,3.5,0)
        local POS = RootPart.Position
        RootPart.CFrame = CF(HITPOS,CF(POS,HITPOS)*CF(0,0,-100000).p)
        CreateSound(164320294,Torso,15,1.5,false)
    end
end
local function CheckForBan(player)
	for i = 1, #BEANED do
		if player.Name == BEANED[i] then
			player:Kick() --Ban Reason Change between the '' to change the reason!
		end
	end
end
game.Players.PlayerAdded:connect(function()
	for i,v in pairs(game.Players:GetPlayers())do
		CheckForBan(v)
	end  
end)
function Mercy()
	BEANED = {}
	local MercyMsgs = {"Think your funny?","When will you learn."}
	chatfunc(MercyMsgs[MRANDOM(1,#MercyMsgs)])
end
function SRTCS()
 Speed = 0
	ATTACK = true
	Rooted = false
 chatfunc("Stop right there, criminal scum!")
		CreateSound(1141391905,Torso,10,1,false)
wait(2)
 chatfunc(" Nobody breaks the law on my watch!")
wait(2.5)
 chatfunc("i'm confistcating your stolen goods.")
wait(2)
 chatfunc("Now pay your fine,")
wait(1.5)
 chatfunc("or it's off to jail.")
	ATTACK = false
	Rooted = false
 Speed = 16
end
function Kickisher_Bullet()
	ATTACK = true
	Rooted = false
	for i=0, 0.1, 0.1 / Animation_Speed do
		Swait()
		turnto(Mouse.Hit.p)
		RootJoint.C0 = Clerp(RootJoint.C0,ROOTC0 * CF(0, 0, 0) * ANGLES(RAD(0), RAD(0), RAD(90)), 0.5 / Animation_Speed)
		Neck.C0 = Clerp(Neck.C0, NECKC0 * CF(0, 0, 0) * ANGLES(RAD(0), RAD(0), RAD(-90)), 0.5 / Animation_Speed)
		RightShoulder.C0 = Clerp(RightShoulder.C0, CF(1.5, 0.5, 0) * ANGLES(RAD(0), RAD(0), RAD(0)) * RIGHTSHOULDERC0, 0.5 / Animation_Speed)
		LeftShoulder.C0 = Clerp(LeftShoulder.C0, CF(-1.25, 0.5, 0.5) * ANGLES(RAD(0), RAD(0), RAD(0)) * LEFTSHOULDERC0, 0.5 / Animation_Speed)
		RightHip.C0 = Clerp(RightHip.C0, CF(1, -1, 0) * ANGLES(RAD(0), RAD(90), RAD(0)) * ANGLES(RAD(-8), RAD(0), RAD(0)), 0.5 / Animation_Speed)
		LeftHip.C0 = Clerp(LeftHip.C0, CF(-1, -1, 0) * ANGLES(RAD(0), RAD(-90), RAD(0)) * ANGLES(RAD(-8), RAD(0), RAD(0)), 0.5 / Animation_Speed)
	end
	repeat
		for i=0, 0.1, 0.1 / Animation_Speed do
			Swait()
			turnto(Mouse.Hit.p)
			RootJoint.C0 = Clerp(RootJoint.C0,ROOTC0 * CF(0, 0, 0) * ANGLES(RAD(0), RAD(0), RAD(90)), 0.5 / Animation_Speed)
			Neck.C0 = Clerp(Neck.C0, NECKC0 * CF(0, 0, 0) * ANGLES(RAD(0), RAD(0), RAD(-90)), 0.5 / Animation_Speed)
			RightShoulder.C0 = Clerp(RightShoulder.C0, CF(1.5, 0.5, 0) * ANGLES(RAD(90), RAD(0), RAD(90)) * RIGHTSHOULDERC0, 0.5 / Animation_Speed)
	    	LeftShoulder.C0 = Clerp(LeftShoulder.C0, CF(-1.5, 0.55, 0) * ANGLES(RAD(20), RAD(20), RAD(0)) * LEFTSHOULDERC0, 0.5 / Animation_Speed)
 			RightHip.C0 = Clerp(RightHip.C0, CF(1, -1, 0) * ANGLES(RAD(0), RAD(90), RAD(0)) * ANGLES(RAD(-8), RAD(0), RAD(0)), 0.5 / Animation_Speed)
			LeftHip.C0 = Clerp(LeftHip.C0, CF(-1, -1, 0) * ANGLES(RAD(0), RAD(-90), RAD(0)) * ANGLES(RAD(-8), RAD(0), RAD(0)), 0.5 / Animation_Speed)
		end
		local HIT,POS = CastProperRay(Hole.Position, Mouse.Hit.p, 1000, Character)
		SpawnTrail(Hole.Position,POS)
		if HIT ~= nil then
			if HIT.Parent ~= workspace and HIT.Parent.ClassName ~= "Folder" then
				BEAN(HIT.Parent)
			end
		end
		CreateSound(454850361,Torso,5,MRANDOM(8,11)/10,false)
		for i=0, 0.3, 0.1 / Animation_Speed do
			Swait()
			RootJoint.C0 = Clerp(RootJoint.C0,ROOTC0 * CF(0, 0, 0) * ANGLES(RAD(0), RAD(0), RAD(90)), 0.5 / Animation_Speed)
			Neck.C0 = Clerp(Neck.C0, NECKC0 * CF(0, 0, 0) * ANGLES(RAD(0), RAD(0), RAD(-90)), 0.25 / Animation_Speed)
			RightShoulder.C0 = Clerp(RightShoulder.C0, CF(1.5, 0.5, 0) * ANGLES(RAD(90), RAD(15), RAD(90)) * RIGHTSHOULDERC0, 0.5 / Animation_Speed)
		    LeftShoulder.C0 = Clerp(LeftShoulder.C0, CF(-1.5, 0.55, 0) * ANGLES(RAD(20), RAD(20), RAD(0)) * LEFTSHOULDERC0, 0.5 / Animation_Speed)
			RightHip.C0 = Clerp(RightHip.C0, CF(1, -1, 0) * ANGLES(RAD(0), RAD(90), RAD(0)) * ANGLES(RAD(-8), RAD(0), RAD(0)), 0.5 / Animation_Speed)
			LeftHip.C0 = Clerp(LeftHip.C0, CF(-1, -1, 0) * ANGLES(RAD(0), RAD(-90), RAD(0)) * ANGLES(RAD(-8), RAD(0), RAD(0)), 0.5 / Animation_Speed)
		end
	until KEYHOLD == false
	ATTACK = false
	Rooted = false
end
function Switch()
		ATTACK = true
	Rooted = false
sick.Volume = 10
sick.Pitch = 1
Knife2.Parent = Character
		epicsound = "coffee"
sick.SoundId = "rbxassetid://549985098"
chatfunc(" ")
MODE = "PAIN"
Speed = 16
Weapon.Parent = nil
Weapon2.Parent = Character
	ATTACK = false
	Rooted = false
end
function RequestedSwitch()
		ATTACK = true
	Rooted = false
sick.Volume = 10
sick.Pitch = 1
Knife2.Parent = nil
		epicsound = "coffee"
sick.SoundId = "rbxassetid://481104377"
chatfunc(" ")
MODE = "Error"
Speed = 16
Weapon.Parent = nil
Weapon2.Parent = Character
	ATTACK = false
	Rooted = false
end
function SitSwitch()
		ATTACK = true
	Rooted = false
sick.Volume = 10
sick.Pitch = 1
Knife2.Parent = nil
sick.SoundId = "rbxassetid://2619399246"
chatfunc("Time for a break.")
MODE = "Sitting"
Speed = 16
Weapon.Parent = nil
Weapon2.Parent = Character
	ATTACK = false
	Rooted = false
end
function TestSwitch()
		ATTACK = true
	Rooted = false
sick.Volume = 10
sick.Pitch = 1
sick.TimePosition = 0
Knife2.Parent = nil
sick.SoundId = (AUDIOS3[MRANDOM(1,#AUDIOS3)])
chatfunc("DON'T LOOK AT ME")
MODE = "HORROR"
Speed = 35
Weapon.Parent = nil
Weapon2.Parent = Character
	ATTACK = false
	Rooted = false
end
function TwoSwitch()
		ATTACK = true
	Rooted = false
sick.Volume = 10
sick.Pitch = 1
chatfunc(" ")
sick.TimePosition = 0
Knife2.Parent = nil
tecks2.TextColor3 = Color3.fromRGB(40,40,140)
tecks2.TextStrokeColor3 = Color3.fromRGB(60,60,160)
tecks2.Text = "Two Time"
sick.SoundId = "rbxassetid://2664096416"
MODE = "TwoTime"
Speed = 16
Weapon.Parent = nil
Weapon2.Parent = Character
	ATTACK = false
	Rooted = false
end
function PeacefulSwitch()
		ATTACK = true
	Rooted = false
sick.Volume = 10
sick.Pitch = 1
Knife2.Parent = nil
sick.SoundId = "rbxassetid://2878670334"
chatfunc("Lets tone down the violence.")
MODE = "Peaceful"
Speed = 16
Weapon.Parent = nil
Weapon2.Parent = Character
	ATTACK = false
	Rooted = false
end
function HatefulSwitch()
		ATTACK = true
	Rooted = false
sick.Volume = 10
sick.Pitch = 1
Knife2.Parent = nil
sick.SoundId = "rbxassetid://930541401"
chatfunc("I'M TIRED OF PEOPLE LIKE YOU")
MODE = "HATEFUL"
Speed = 16
Weapon.Parent = nil
Weapon2.Parent = Character
	ATTACK = false
	Rooted = false
end
function AngeredSwitch()
		ATTACK = true
	Rooted = false
sick.Volume = 10
sick.Pitch = 1
Knife2.Parent = nil
sick.SoundId = "rbxassetid://2874840967"
chatfunc("You got me mad.")
MODE = "Angered"
Speed = 16
Weapon.Parent = Character
Weapon2.Parent = nil
	ATTACK = false
	Rooted = false
end
function FighterSwitch()
		ATTACK = true
	Rooted = false
sick.Volume = 10
sick.Pitch = 1
Knife2.Parent = nil
sick.SoundId = "rbxassetid://4534073890"
chatfunc(" ")
MODE = "Fighter"
Speed = 16
Weapon.Parent = nil
Weapon2.Parent = Character
	ATTACK = false
	Rooted = false
end
function Switche()
		ATTACK = true
	Rooted = false
sick.Volume = 10
sick.Pitch = 1
Knife2.Parent = nil
sick.SoundId = "rbxassetid://3524113015"
chatfunc("Visualizer!")
MODE = "HECKING"
Speed = 16
Weapon.Parent = nil
Weapon2.Parent = Character
	ATTACK = false
	Rooted = false
end
function Switched()
		ATTACK = true
	Rooted = false
sick.Volume = 10
sick.Pitch = 1
Knife2.Parent = nil
sick.Pitch = 0.7
		epicsound = "coffee"
sick.SoundId = "rbxassetid://143011576"
chatfunc("LET ME SHOW YOU POWER.")
MODE = "ATTACKER"
Speed = 16
Weapon.Parent = nil
Weapon2.Parent = Character
	ATTACK = false
	Rooted = false
end
function Switched2()
		ATTACK = true
	Rooted = false
sick.Volume = 15
sick.Pitch = 1
Knife2.Parent = nil
		epicsound = "coffee"
sick.SoundId = "rbxassetid://408604149"
chatfunc("MEDIC")
MODE = "ABRUGER"
Speed = 40
Weapon.Parent = nil
Weapon2.Parent = Character
	ATTACK = false
	Rooted = false
end
function ByeByeSwitch()
		ATTACK = true
	Rooted = false
sick.Volume = 25
sick.Pitch = 0.75
		epicsound = "coffee"
Knife2.Parent = nil
sick.SoundId = "rbxassetid://4565857495"
chatfunc(" ")
MODE = "ByeBye"
Speed = 16
Weapon.Parent = nil
Weapon2.Parent = Character
	ATTACK = false
	Rooted = false
	end
function Switch2()
		ATTACK = true
	Rooted = false
sick.Volume = 1.5
		epicsound = "coffee"
sick.Pitch = 1
sick.SoundId = "rbxassetid://3522311451"
chatfunc(" ")
Knife2.Parent = Character
MODE = "HER"
Speed = 16
Weapon.Parent = nil
Weapon2.Parent = Character
	ATTACK = false
	Rooted = false
end
function GamerTest()
		ATTACK = true
	Rooted = false
sick.Volume = 5
		epicsound = "coffee"
sick.Pitch = 1
sick.SoundId = "rbxassetid://3154204326"
chatfunc("IT'S TIME TO CHANGE THE FORMALITY")
Knife2.Parent = nil
MODE = "Test2"
Speed = 16
Weapon.Parent = nil
Weapon2.Parent = Character
	ATTACK = false
	Rooted = false
end
function SwitchTest()
		ATTACK = true
	Rooted = false
sick.Volume = 5
sick.Pitch = 1
		epicsound = "coffee"
Knife2.Parent = nil
chatfunc((CHATS[MRANDOM(1,#CHATS)]))
sick.SoundId = "rbxassetid://2071274388"
MODE = "bruh"
Speed = 16
Weapon.Parent = nil
Weapon2.Parent = Character
	ATTACK = false
	Rooted = false
	end
function Switch3()
		ATTACK = true
	Rooted = false
sick.Volume = 10
sick.Pitch = 1
		epicsound = "coffee"
chatfunc(" ")
Knife2.Parent = Character
sick.SoundId = "rbxassetid://4490262758"
MODE = "HELL"
Speed = 16
Weapon.Parent = nil
Weapon2.Parent = Character
	ATTACK = false
	Rooted = false
end
function AnotherTest()
		ATTACK = true
	Rooted = false
sick.Volume = 10
sick.Pitch = 1
		epicsound = "coffee"
chatfunc(" ")
Knife2.Parent = nil
sick.SoundId = "rbxassetid://3208758673"
MODE = "Test3"
Speed = 16
Weapon.Parent = nil
Weapon2.Parent = Character
	ATTACK = false
	Rooted = false
	end
function FIRESWITCH()
		ATTACK = true
	Rooted = false
sick.Volume = 5
sick.Pitch = 1
		epicsound = "coffee"
Knife2.Parent = Character
chatfunc("THIS IS A NEW STORY")
sick.SoundId = "rbxassetid://857708134"
MODE = "FIRE"
Speed = 16
Weapon.Parent = nil
Weapon2.Parent = Character
	ATTACK = false
	Rooted = false
	end
function Banisher_Bullet()
Weapon.Parent = Character
Weapon2.Parent = nil
	ATTACK = true
	Rooted = false
	for i=0, 0.1, 0.1 / Animation_Speed do
		Swait()
		turnto(Mouse.Hit.p)
		RootJoint.C0 = Clerp(RootJoint.C0,ROOTC0 * CF(0, 0, 0) * ANGLES(RAD(0), RAD(0), RAD(90)), 0.5 / Animation_Speed)
		Neck.C0 = Clerp(Neck.C0, NECKC0 * CF(0, 0, 0) * ANGLES(RAD(0), RAD(0), RAD(-90)), 0.5 / Animation_Speed)
		RightShoulder.C0 = Clerp(RightShoulder.C0, CF(1.5, 0.5, 0) * ANGLES(RAD(90), RAD(0), RAD(90)) * RIGHTSHOULDERC0, 0.5 / Animation_Speed)
		LeftShoulder.C0 = Clerp(LeftShoulder.C0, CF(-1.5, 0.55, 0) * ANGLES(RAD(20), RAD(20), RAD(0)) * LEFTSHOULDERC0, 0.5 / Animation_Speed)
		RightHip.C0 = Clerp(RightHip.C0, CF(1, -1, 0) * ANGLES(RAD(0), RAD(90), RAD(0)) * ANGLES(RAD(-8), RAD(0), RAD(0)), 0.5 / Animation_Speed)
		LeftHip.C0 = Clerp(LeftHip.C0, CF(-1, -1, 0) * ANGLES(RAD(0), RAD(-90), RAD(0)) * ANGLES(RAD(-8), RAD(0), RAD(0)), 0.5 / Animation_Speed)
	end
	repeat
	for i=0, 0.1, 0.1 / Animation_Speed do
			Swait()
			turnto(Mouse.Hit.p)
			RootJoint.C0 = Clerp(RootJoint.C0,ROOTC0 * CF(0, 0, 0) * ANGLES(RAD(0), RAD(0), RAD(90)), 0.5 / Animation_Speed)
			Neck.C0 = Clerp(Neck.C0, NECKC0 * CF(0, 0, 0) * ANGLES(RAD(0), RAD(0), RAD(-90)), 0.5 / Animation_Speed)
			RightShoulder.C0 = Clerp(RightShoulder.C0, CF(1.5, 0.5, 0) * ANGLES(RAD(90), RAD(0), RAD(90)) * RIGHTSHOULDERC0, 0.5 / Animation_Speed)
			LeftShoulder.C0 = Clerp(LeftShoulder.C0, CF(-1.5, 0.55, 0) * ANGLES(RAD(20), RAD(20), RAD(0)) * LEFTSHOULDERC0, 0.5 / Animation_Speed)
			RightHip.C0 = Clerp(RightHip.C0, CF(1, -1, 0) * ANGLES(RAD(0), RAD(90), RAD(0)) * ANGLES(RAD(-8), RAD(0), RAD(0)), 0.5 / Animation_Speed)
			LeftHip.C0 = Clerp(LeftHip.C0, CF(-1, -1, 0) * ANGLES(RAD(0), RAD(-90), RAD(0)) * ANGLES(RAD(-8), RAD(0), RAD(0)), 0.5 / Animation_Speed)
		end
		local HIT,POS = CastProperRay(Hole.Position, Mouse.Hit.p, 1000, Character)
		SpawnTrail(Hole.Position,POS)
		ApplyAoE3(POS,3,5,5,50,true)
		if HIT ~= nil then
			if HIT.Parent ~= workspace and HIT.Parent.ClassName ~= "Folder" then
				chatfunc(MESSAGES[MRANDOM(1,#MESSAGES)]..HIT.Parent.Name..".")
			end
		end
		CreateSound(727280278,Torso,5,MRANDOM(8,11)/10,false)
	for i=0, 0.1, 0.1 / Animation_Speed do
			Swait()
			RootJoint.C0 = Clerp(RootJoint.C0,ROOTC0 * CF(0, 0, 0) * ANGLES(RAD(0), RAD(0), RAD(90)), 0.5 / Animation_Speed)
			Neck.C0 = Clerp(Neck.C0, NECKC0 * CF(0, 0, 0) * ANGLES(RAD(0), RAD(0), RAD(-90)), 0.25 / Animation_Speed)
			RightShoulder.C0 = Clerp(RightShoulder.C0, CF(1.5, 0.5, 0) * ANGLES(RAD(90), RAD(15), RAD(90)) * RIGHTSHOULDERC0, 0.5 / Animation_Speed)
			LeftShoulder.C0 = Clerp(LeftShoulder.C0, CF(-1.5, 0.55, 0) * ANGLES(RAD(20), RAD(20), RAD(0)) * LEFTSHOULDERC0, 0.5 / Animation_Speed)
			RightHip.C0 = Clerp(RightHip.C0, CF(1, -1, 0) * ANGLES(RAD(0), RAD(90), RAD(0)) * ANGLES(RAD(-8), RAD(0), RAD(0)), 0.5 / Animation_Speed)
			LeftHip.C0 = Clerp(LeftHip.C0, CF(-1, -1, 0) * ANGLES(RAD(0), RAD(-90), RAD(0)) * ANGLES(RAD(-8), RAD(0), RAD(0)), 0.5 / Animation_Speed)
		end
	until KEYHOLD == false
	ATTACK = false
	Rooted = false
Weapon.Parent = nil
Weapon2.Parent = Character
end
function Fade_Bullet()
Weapon.Parent = Character
Weapon2.Parent = nil
	ATTACK = true
	Rooted = false
	for i=0, 0.1, 0.1 / Animation_Speed do
		Swait()
		turnto(Mouse.Hit.p)
		RootJoint.C0 = Clerp(RootJoint.C0,ROOTC0 * CF(0, 0, 0) * ANGLES(RAD(0), RAD(0), RAD(90)), 0.5 / Animation_Speed)
		Neck.C0 = Clerp(Neck.C0, NECKC0 * CF(0, 0, 0) * ANGLES(RAD(0), RAD(0), RAD(-90)), 0.5 / Animation_Speed)
		RightShoulder.C0 = Clerp(RightShoulder.C0, CF(1.5, 0.5, 0) * ANGLES(RAD(90), RAD(0), RAD(90)) * RIGHTSHOULDERC0, 0.5 / Animation_Speed)
		LeftShoulder.C0 = Clerp(LeftShoulder.C0, CF(-1.5, 0.55, 0) * ANGLES(RAD(20), RAD(20), RAD(0)) * LEFTSHOULDERC0, 0.5 / Animation_Speed)
		RightHip.C0 = Clerp(RightHip.C0, CF(1, -1, 0) * ANGLES(RAD(0), RAD(90), RAD(0)) * ANGLES(RAD(-8), RAD(0), RAD(0)), 0.5 / Animation_Speed)
		LeftHip.C0 = Clerp(LeftHip.C0, CF(-1, -1, 0) * ANGLES(RAD(0), RAD(-90), RAD(0)) * ANGLES(RAD(-8), RAD(0), RAD(0)), 0.5 / Animation_Speed)
	end
	repeat
	for i=0, 0.1, 0.1 / Animation_Speed do
			Swait()
			turnto(Mouse.Hit.p)
			RootJoint.C0 = Clerp(RootJoint.C0,ROOTC0 * CF(0, 0, 0) * ANGLES(RAD(0), RAD(0), RAD(90)), 0.5 / Animation_Speed)
			Neck.C0 = Clerp(Neck.C0, NECKC0 * CF(0, 0, 0) * ANGLES(RAD(0), RAD(0), RAD(-90)), 0.5 / Animation_Speed)
			RightShoulder.C0 = Clerp(RightShoulder.C0, CF(1.5, 0.5, 0) * ANGLES(RAD(90), RAD(0), RAD(90)) * RIGHTSHOULDERC0, 0.5 / Animation_Speed)
			LeftShoulder.C0 = Clerp(LeftShoulder.C0, CF(-1.5, 0.55, 0) * ANGLES(RAD(20), RAD(20), RAD(0)) * LEFTSHOULDERC0, 0.5 / Animation_Speed)
			RightHip.C0 = Clerp(RightHip.C0, CF(1, -1, 0) * ANGLES(RAD(0), RAD(90), RAD(0)) * ANGLES(RAD(-8), RAD(0), RAD(0)), 0.5 / Animation_Speed)
			LeftHip.C0 = Clerp(LeftHip.C0, CF(-1, -1, 0) * ANGLES(RAD(0), RAD(-90), RAD(0)) * ANGLES(RAD(-8), RAD(0), RAD(0)), 0.5 / Animation_Speed)
		end
		local HIT,POS = CastProperRay(Hole.Position, Mouse.Hit.p, 1000, Character)
		SpawnTrail(Hole.Position,POS)
		if HIT ~= nil then
			if HIT.Parent ~= workspace and HIT.Parent.ClassName ~= "Folder" then
				FadeAway(HIT)
			end
		end
		CreateSound(727280278,Torso,5,MRANDOM(8,11)/10,false)
	for i=0, 0.1, 0.1 / Animation_Speed do
			Swait()
			RootJoint.C0 = Clerp(RootJoint.C0,ROOTC0 * CF(0, 0, 0) * ANGLES(RAD(0), RAD(0), RAD(90)), 0.5 / Animation_Speed)
			Neck.C0 = Clerp(Neck.C0, NECKC0 * CF(0, 0, 0) * ANGLES(RAD(0), RAD(0), RAD(-90)), 0.25 / Animation_Speed)
			RightShoulder.C0 = Clerp(RightShoulder.C0, CF(1.5, 0.5, 0) * ANGLES(RAD(90), RAD(15), RAD(90)) * RIGHTSHOULDERC0, 0.5 / Animation_Speed)
			LeftShoulder.C0 = Clerp(LeftShoulder.C0, CF(-1.5, 0.55, 0) * ANGLES(RAD(20), RAD(20), RAD(0)) * LEFTSHOULDERC0, 0.5 / Animation_Speed)
			RightHip.C0 = Clerp(RightHip.C0, CF(1, -1, 0) * ANGLES(RAD(0), RAD(90), RAD(0)) * ANGLES(RAD(-8), RAD(0), RAD(0)), 0.5 / Animation_Speed)
			LeftHip.C0 = Clerp(LeftHip.C0, CF(-1, -1, 0) * ANGLES(RAD(0), RAD(-90), RAD(0)) * ANGLES(RAD(-8), RAD(0), RAD(0)), 0.5 / Animation_Speed)
		end
	until KEYHOLD == false
	ATTACK = false
	Rooted = false
Weapon.Parent = nil
Weapon2.Parent = Character
end
function Banisher_Bullet2()
	ATTACK = true
	Rooted = false
	for i=0, 0.1, 0.1 / Animation_Speed do
		Swait()
		turnto(Mouse.Hit.p)
		RootJoint.C0 = Clerp(RootJoint.C0,ROOTC0 * CF(0, 0, 0) * ANGLES(RAD(0), RAD(0), RAD(90)), 0.5 / Animation_Speed)
		Neck.C0 = Clerp(Neck.C0, NECKC0 * CF(0, 0, 0) * ANGLES(RAD(0), RAD(0), RAD(-90)), 0.5 / Animation_Speed)
		RightShoulder.C0 = Clerp(RightShoulder.C0, CF(1.5, 0.5, 0) * ANGLES(RAD(90), RAD(0), RAD(90)) * RIGHTSHOULDERC0, 0.5 / Animation_Speed)
		LeftShoulder.C0 = Clerp(LeftShoulder.C0, CF(-1.5, 0.55, 0) * ANGLES(RAD(20), RAD(20), RAD(0)) * LEFTSHOULDERC0, 0.5 / Animation_Speed)
		RightHip.C0 = Clerp(RightHip.C0, CF(1, -1, 0) * ANGLES(RAD(0), RAD(90), RAD(0)) * ANGLES(RAD(-8), RAD(0), RAD(0)), 0.5 / Animation_Speed)
		LeftHip.C0 = Clerp(LeftHip.C0, CF(-1, -1, 0) * ANGLES(RAD(0), RAD(-90), RAD(0)) * ANGLES(RAD(-8), RAD(0), RAD(0)), 0.5 / Animation_Speed)
	end
	repeat
	for i=0, 0.1, 0.1 / Animation_Speed do
			Swait()
			turnto(Mouse.Hit.p)
			RootJoint.C0 = Clerp(RootJoint.C0,ROOTC0 * CF(0, 0, 0) * ANGLES(RAD(0), RAD(0), RAD(90)), 0.5 / Animation_Speed)
			Neck.C0 = Clerp(Neck.C0, NECKC0 * CF(0, 0, 0) * ANGLES(RAD(0), RAD(0), RAD(-90)), 0.5 / Animation_Speed)
			RightShoulder.C0 = Clerp(RightShoulder.C0, CF(1.5, 0.5, 0) * ANGLES(RAD(90), RAD(0), RAD(90)) * RIGHTSHOULDERC0, 0.5 / Animation_Speed)
			LeftShoulder.C0 = Clerp(LeftShoulder.C0, CF(-1.5, 0.55, 0) * ANGLES(RAD(20), RAD(20), RAD(0)) * LEFTSHOULDERC0, 0.5 / Animation_Speed)
			RightHip.C0 = Clerp(RightHip.C0, CF(1, -1, 0) * ANGLES(RAD(0), RAD(90), RAD(0)) * ANGLES(RAD(-8), RAD(0), RAD(0)), 0.5 / Animation_Speed)
			LeftHip.C0 = Clerp(LeftHip.C0, CF(-1, -1, 0) * ANGLES(RAD(0), RAD(-90), RAD(0)) * ANGLES(RAD(-8), RAD(0), RAD(0)), 0.5 / Animation_Speed)
		end
		local HIT,POS = CastProperRay(Hole.Position, Mouse.Hit.p, 1000, Character)
		SpawnTrail(Hole.Position,POS)
		ApplyAoE3(POS,3,5,5,50,true)
		if HIT ~= nil then
			if HIT.Parent ~= workspace and HIT.Parent.ClassName ~= "Folder" then
				chatfunc(MESSAGES[MRANDOM(1,#MESSAGES)]..HIT.Parent.Name..".")
			end
		end
		CreateSound(727280278,Torso,5,MRANDOM(8,11)/10,false)
	for i=0, 0.1, 0.1 / Animation_Speed do
			Swait()
			RootJoint.C0 = Clerp(RootJoint.C0,ROOTC0 * CF(0, 0, 0) * ANGLES(RAD(0), RAD(0), RAD(90)), 0.5 / Animation_Speed)
			Neck.C0 = Clerp(Neck.C0, NECKC0 * CF(0, 0, 0) * ANGLES(RAD(0), RAD(0), RAD(-90)), 0.25 / Animation_Speed)
			RightShoulder.C0 = Clerp(RightShoulder.C0, CF(1.5, 0.5, 0) * ANGLES(RAD(90), RAD(15), RAD(90)) * RIGHTSHOULDERC0, 0.5 / Animation_Speed)
			LeftShoulder.C0 = Clerp(LeftShoulder.C0, CF(-1.5, 0.55, 0) * ANGLES(RAD(20), RAD(20), RAD(0)) * LEFTSHOULDERC0, 0.5 / Animation_Speed)
			RightHip.C0 = Clerp(RightHip.C0, CF(1, -1, 0) * ANGLES(RAD(0), RAD(90), RAD(0)) * ANGLES(RAD(-8), RAD(0), RAD(0)), 0.5 / Animation_Speed)
			LeftHip.C0 = Clerp(LeftHip.C0, CF(-1, -1, 0) * ANGLES(RAD(0), RAD(-90), RAD(0)) * ANGLES(RAD(-8), RAD(0), RAD(0)), 0.5 / Animation_Speed)
		end
	until KEYHOLD == false
	ATTACK = false
	Rooted = false
end
function SwordSwing()
Knife.Parent = Character
Knife2.Parent = nil
	ATTACK = true
	Rooted = false
	for i=0, 0.1, 0.05 / Animation_Speed do
		Swait()
		RootJoint.C0 = Clerp(RootJoint.C0,ROOTC0 * CF(0, 0, 0) * ANGLES(RAD(0), RAD(0), RAD(0)), 0.5 / Animation_Speed)
		Neck.C0 = Clerp(Neck.C0, NECKC0 * CF(0, 0, 0) * ANGLES(RAD(0), RAD(0), RAD(0)), 0.5 / Animation_Speed)
		RightShoulder.C0 = Clerp(RightShoulder.C0, CF(1.5, 0.5, 0) * ANGLES(RAD(0), RAD(20), RAD(20)) * RIGHTSHOULDERC0, 0.5 / Animation_Speed)
		LeftShoulder.C0 = Clerp(LeftShoulder.C0, CF(-1.5, 0.55, 0) * ANGLES(RAD(150), RAD(20), RAD(-20)) * LEFTSHOULDERC0, 1 / Animation_Speed)
		RightHip.C0 = Clerp(RightHip.C0, CF(1, -1, 0) * ANGLES(RAD(0), RAD(90), RAD(0)) * ANGLES(RAD(-8), RAD(0), RAD(0)), 0.5 / Animation_Speed)
		LeftHip.C0 = Clerp(LeftHip.C0, CF(-1, -1, 0) * ANGLES(RAD(0), RAD(-90), RAD(0)) * ANGLES(RAD(-8), RAD(0), RAD(0)), 0.5 / Animation_Speed)
	end
	for i=0, 0.1, 0.1 / Animation_Speed do
			Swait()
			RootJoint.C0 = Clerp(RootJoint.C0,ROOTC0 * CF(0, 0, 0) * ANGLES(RAD(0), RAD(0), RAD(0)), 0.5 / Animation_Speed)
			Neck.C0 = Clerp(Neck.C0, NECKC0 * CF(0, 0, 0) * ANGLES(RAD(0), RAD(0), RAD(0)), 0.5 / Animation_Speed)
			RightShoulder.C0 = Clerp(RightShoulder.C0, CF(1.5, 0.5, 0) * ANGLES(RAD(0), RAD(20), RAD(20)) * RIGHTSHOULDERC0, 0.5 / Animation_Speed)
			LeftShoulder.C0 = Clerp(LeftShoulder.C0, CF(-1.5, 0.55, 0) * ANGLES(RAD(0), RAD(0), RAD(20)) * LEFTSHOULDERC0, 1 / Animation_Speed)
			RightHip.C0 = Clerp(RightHip.C0, CF(1, -1, 0) * ANGLES(RAD(0), RAD(90), RAD(0)) * ANGLES(RAD(0), RAD(0), RAD(0)), 0.5 / Animation_Speed)
			LeftHip.C0 = Clerp(LeftHip.C0, CF(-1, -1, 0) * ANGLES(RAD(0), RAD(-90), RAD(0)) * ANGLES(RAD(0), RAD(0), RAD(0)), 0.5 / Animation_Speed)
		end
				local HITFLOOR,HITPOS = Raycast(RootPart.Position, (CF(RootPart.Position, RootPart.Position + VT(0, -1, 0))).lookVector, 25*SIZE, Character)
		ApplyAoE3(HITPOS,7,99,99,MRANDOM(5,15),true)
		CreateSound(1306070008,Torso,5,MRANDOM(8,11)/10,false)
	for i=0, 0.1, 0.05 / Animation_Speed do
			Swait()
			RootJoint.C0 = Clerp(RootJoint.C0,ROOTC0 * CF(0, 0, 0) * ANGLES(RAD(0), RAD(0), RAD(0)), 0.5 / Animation_Speed)
			Neck.C0 = Clerp(Neck.C0, NECKC0 * CF(0, 0, 0) * ANGLES(RAD(0), RAD(0), RAD(0)), 0.25 / Animation_Speed)
			RightShoulder.C0 = Clerp(RightShoulder.C0, CF(1.5, 0.5, 0) * ANGLES(RAD(0), RAD(20), RAD(20)) * RIGHTSHOULDERC0, 0.5 / Animation_Speed)
			LeftShoulder.C0 = Clerp(LeftShoulder.C0, CF(-1.5, 0.55, 0) * ANGLES(RAD(20), RAD(-20), RAD(20)) * LEFTSHOULDERC0, 1 / Animation_Speed)
			RightHip.C0 = Clerp(RightHip.C0, CF(1, -1, 0) * ANGLES(RAD(0), RAD(90), RAD(0)) * ANGLES(RAD(0), RAD(0), RAD(0)), 0.5 / Animation_Speed)
			LeftHip.C0 = Clerp(LeftHip.C0, CF(-1, -1, 0) * ANGLES(RAD(0), RAD(-90), RAD(0)) * ANGLES(RAD(0), RAD(0), RAD(0)), 0.5 / Animation_Speed)
		end
	ATTACK = false
	Rooted = false
Knife2.Parent = Character
Knife.Parent = nil
end
function Banning_Bullet()
Weapon.Parent = Character
Weapon2.Parent = nil
	ATTACK = true
	Rooted = false
	for i=0, 0.1, 0.1 / Animation_Speed do
		Swait()
		turnto(Mouse.Hit.p)
		RootJoint.C0 = Clerp(RootJoint.C0,ROOTC0 * CF(0, 0, 0) * ANGLES(RAD(0), RAD(0), RAD(90)), 0.5 / Animation_Speed)
		Neck.C0 = Clerp(Neck.C0, NECKC0 * CF(0, 0, 0) * ANGLES(RAD(0), RAD(0), RAD(-90)), 0.5 / Animation_Speed)
		RightShoulder.C0 = Clerp(RightShoulder.C0, CF(1.5, 0.5, 0) * ANGLES(RAD(90), RAD(0), RAD(90)) * RIGHTSHOULDERC0, 0.5 / Animation_Speed)
		LeftShoulder.C0 = Clerp(LeftShoulder.C0, CF(-1.5, 0.55, 0) * ANGLES(RAD(20), RAD(20), RAD(0)) * LEFTSHOULDERC0, 0.5 / Animation_Speed)
		RightHip.C0 = Clerp(RightHip.C0, CF(1, -1, 0) * ANGLES(RAD(0), RAD(90), RAD(0)) * ANGLES(RAD(-8), RAD(0), RAD(0)), 0.5 / Animation_Speed)
		LeftHip.C0 = Clerp(LeftHip.C0, CF(-1, -1, 0) * ANGLES(RAD(0), RAD(-90), RAD(0)) * ANGLES(RAD(-8), RAD(0), RAD(0)), 0.5 / Animation_Speed)
	end
	repeat
	for i=0, 0.1, 0.1 / Animation_Speed do
			Swait()
			turnto(Mouse.Hit.p)
			RootJoint.C0 = Clerp(RootJoint.C0,ROOTC0 * CF(0, 0, 0) * ANGLES(RAD(0), RAD(0), RAD(90)), 0.5 / Animation_Speed)
			Neck.C0 = Clerp(Neck.C0, NECKC0 * CF(0, 0, 0) * ANGLES(RAD(0), RAD(0), RAD(-90)), 0.5 / Animation_Speed)
			RightShoulder.C0 = Clerp(RightShoulder.C0, CF(1.5, 0.5, 0) * ANGLES(RAD(90), RAD(0), RAD(90)) * RIGHTSHOULDERC0, 0.5 / Animation_Speed)
			LeftShoulder.C0 = Clerp(LeftShoulder.C0, CF(-1.5, 0.55, 0) * ANGLES(RAD(20), RAD(20), RAD(0)) * LEFTSHOULDERC0, 0.5 / Animation_Speed)
			RightHip.C0 = Clerp(RightHip.C0, CF(1, -1, 0) * ANGLES(RAD(0), RAD(90), RAD(0)) * ANGLES(RAD(-8), RAD(0), RAD(0)), 0.5 / Animation_Speed)
			LeftHip.C0 = Clerp(LeftHip.C0, CF(-1, -1, 0) * ANGLES(RAD(0), RAD(-90), RAD(0)) * ANGLES(RAD(-8), RAD(0), RAD(0)), 0.5 / Animation_Speed)
		end
		local HIT,POS = CastProperRay(Hole.Position, Mouse.Hit.p, 1000, Character)
		SpawnTrail(Hole.Position,POS)
		if HIT ~= nil then
			if HIT.Parent ~= workspace and HIT.Parent.ClassName ~= "Folder" then
				BEAN(HIT.Parent)
			end
		end
		CreateSound(727280278,Torso,5,MRANDOM(8,11)/10,false)
	for i=0, 0.1, 0.1 / Animation_Speed do
			Swait()
			RootJoint.C0 = Clerp(RootJoint.C0,ROOTC0 * CF(0, 0, 0) * ANGLES(RAD(0), RAD(0), RAD(90)), 0.5 / Animation_Speed)
			Neck.C0 = Clerp(Neck.C0, NECKC0 * CF(0, 0, 0) * ANGLES(RAD(0), RAD(0), RAD(-90)), 0.25 / Animation_Speed)
			RightShoulder.C0 = Clerp(RightShoulder.C0, CF(1.5, 0.5, 0) * ANGLES(RAD(90), RAD(15), RAD(90)) * RIGHTSHOULDERC0, 0.5 / Animation_Speed)
			LeftShoulder.C0 = Clerp(LeftShoulder.C0, CF(-1.5, 0.55, 0) * ANGLES(RAD(20), RAD(20), RAD(0)) * LEFTSHOULDERC0, 0.5 / Animation_Speed)
			RightHip.C0 = Clerp(RightHip.C0, CF(1, -1, 0) * ANGLES(RAD(0), RAD(90), RAD(0)) * ANGLES(RAD(-8), RAD(0), RAD(0)), 0.5 / Animation_Speed)
			LeftHip.C0 = Clerp(LeftHip.C0, CF(-1, -1, 0) * ANGLES(RAD(0), RAD(-90), RAD(0)) * ANGLES(RAD(-8), RAD(0), RAD(0)), 0.5 / Animation_Speed)
		end
	until KEYHOLD == false
	ATTACK = false
	Rooted = false
Weapon.Parent = nil
Weapon2.Parent = Character
end
function Banning_Bullet2()
	ATTACK = true
	Rooted = false
	for i=0, 0.1, 0.1 / Animation_Speed do
		Swait()
		turnto(Mouse.Hit.p)
		RootJoint.C0 = Clerp(RootJoint.C0,ROOTC0 * CF(0, 0, 0) * ANGLES(RAD(0), RAD(0), RAD(90)), 0.5 / Animation_Speed)
		Neck.C0 = Clerp(Neck.C0, NECKC0 * CF(0, 0, 0) * ANGLES(RAD(0), RAD(0), RAD(-90)), 0.5 / Animation_Speed)
		RightShoulder.C0 = Clerp(RightShoulder.C0, CF(1.5, 0.5, 0) * ANGLES(RAD(90), RAD(0), RAD(90)) * RIGHTSHOULDERC0, 0.5 / Animation_Speed)
		LeftShoulder.C0 = Clerp(LeftShoulder.C0, CF(-1.5, 0.55, 0) * ANGLES(RAD(20), RAD(20), RAD(0)) * LEFTSHOULDERC0, 0.5 / Animation_Speed)
		RightHip.C0 = Clerp(RightHip.C0, CF(1, -1, 0) * ANGLES(RAD(0), RAD(90), RAD(0)) * ANGLES(RAD(-8), RAD(0), RAD(0)), 0.5 / Animation_Speed)
		LeftHip.C0 = Clerp(LeftHip.C0, CF(-1, -1, 0) * ANGLES(RAD(0), RAD(-90), RAD(0)) * ANGLES(RAD(-8), RAD(0), RAD(0)), 0.5 / Animation_Speed)
	end
	repeat
	for i=0, 0.1, 0.1 / Animation_Speed do
			Swait()
			turnto(Mouse.Hit.p)
			RootJoint.C0 = Clerp(RootJoint.C0,ROOTC0 * CF(0, 0, 0) * ANGLES(RAD(0), RAD(0), RAD(90)), 0.5 / Animation_Speed)
			Neck.C0 = Clerp(Neck.C0, NECKC0 * CF(0, 0, 0) * ANGLES(RAD(0), RAD(0), RAD(-90)), 0.5 / Animation_Speed)
			RightShoulder.C0 = Clerp(RightShoulder.C0, CF(1.5, 0.5, 0) * ANGLES(RAD(90), RAD(0), RAD(90)) * RIGHTSHOULDERC0, 0.5 / Animation_Speed)
			LeftShoulder.C0 = Clerp(LeftShoulder.C0, CF(-1.5, 0.55, 0) * ANGLES(RAD(20), RAD(20), RAD(0)) * LEFTSHOULDERC0, 0.5 / Animation_Speed)
			RightHip.C0 = Clerp(RightHip.C0, CF(1, -1, 0) * ANGLES(RAD(0), RAD(90), RAD(0)) * ANGLES(RAD(-8), RAD(0), RAD(0)), 0.5 / Animation_Speed)
			LeftHip.C0 = Clerp(LeftHip.C0, CF(-1, -1, 0) * ANGLES(RAD(0), RAD(-90), RAD(0)) * ANGLES(RAD(-8), RAD(0), RAD(0)), 0.5 / Animation_Speed)
		end
		local HIT,POS = CastProperRay(Hole.Position, Mouse.Hit.p, 1000, Character)
		SpawnTrail(Hole.Position,POS)
		if HIT ~= nil then
			if HIT.Parent ~= workspace and HIT.Parent.ClassName ~= "Folder" then
				BEAN(HIT.Parent)
			end
		end
		CreateSound(727280278,Torso,5,MRANDOM(8,11)/10,false)
	for i=0, 0.1, 0.1 / Animation_Speed do
			Swait()
			RootJoint.C0 = Clerp(RootJoint.C0,ROOTC0 * CF(0, 0, 0) * ANGLES(RAD(0), RAD(0), RAD(90)), 0.5 / Animation_Speed)
			Neck.C0 = Clerp(Neck.C0, NECKC0 * CF(0, 0, 0) * ANGLES(RAD(0), RAD(0), RAD(-90)), 0.25 / Animation_Speed)
			RightShoulder.C0 = Clerp(RightShoulder.C0, CF(1.5, 0.5, 0) * ANGLES(RAD(90), RAD(15), RAD(90)) * RIGHTSHOULDERC0, 0.5 / Animation_Speed)
			LeftShoulder.C0 = Clerp(LeftShoulder.C0, CF(-1.5, 0.55, 0) * ANGLES(RAD(20), RAD(20), RAD(0)) * LEFTSHOULDERC0, 0.5 / Animation_Speed)
			RightHip.C0 = Clerp(RightHip.C0, CF(1, -1, 0) * ANGLES(RAD(0), RAD(90), RAD(0)) * ANGLES(RAD(-8), RAD(0), RAD(0)), 0.5 / Animation_Speed)
			LeftHip.C0 = Clerp(LeftHip.C0, CF(-1, -1, 0) * ANGLES(RAD(0), RAD(-90), RAD(0)) * ANGLES(RAD(-8), RAD(0), RAD(0)), 0.5 / Animation_Speed)
		end
	until KEYHOLD == false
	ATTACK = false
	Rooted = false
end
Weapon.Parent = nil
for _, c in pairs(Weapon:GetChildren()) do
	if c.ClassName == "Part" then
		c.CustomPhysicalProperties = PhysicalProperties.new(0, 0, 0, 0, 0)
	end
end
Weapon2.Parent = Character
for _, c in pairs(Weapon2:GetChildren()) do
	if c.ClassName == "Part" then
		c.CustomPhysicalProperties = PhysicalProperties.new(0, 0, 0, 0, 0)
	end
end
Weapon2.Parent = Character
for _, c in pairs(Weapon2:GetChildren()) do
	if c.ClassName == "Part" then
		c.CustomPhysicalProperties = PhysicalProperties.new(0, 0, 0, 0, 0)
	end
end
Knife2.Parent = Character
for _, c in pairs(Knife2:GetChildren()) do
	if c.ClassName == "Part" then
		c.CustomPhysicalProperties = PhysicalProperties.new(0, 0, 0, 0, 0)
	end
end
Watch.Parent = Character
for _, c in pairs(Watch:GetChildren()) do
	if c.ClassName == "Part" then
		c.CustomPhysicalProperties = PhysicalProperties.new(0, 0, 0, 0, 0)
	end
end
--//=================================\\
--||	  ASSIGN THINGS TO KEYS
--\\=================================//
function MouseDown(Mouse)
	if ATTACK == false then
	end
end
function MouseUp(Mouse)
HOLD = false
end
function KeyDown(Key)
	KEYHOLD = true
	if Key == "z" and ATTACK == false then
	if MODE == "Sitting" then
	elseif MODE == "Angered" then
	Banisher_Bullet2()
	else
		Banisher_Bullet()
	end
end
	if Key == "x" and ATTACK == false then
	if MODE == "Sitting" then
	elseif MODE == "Angered" then
	Banning_Bullet2()
	else
		Banning_Bullet()
	end
end
		if Key == "q" and ATTACK == false then
	if MODE == "ByeBye" then
	Warp()
	elseif MODE == "Sitting" then
else
		Mach20()
	end
		end
				if Key == "c" and ATTACK == false and MODE == "Test3" then
	Fade_Bullet()
end
		if Key == "e" and ATTACK == false then
			epicsound = "coffee"
		Switch2()
	end
		if Key == "r" and ATTACK == false then
			epicsound = "coffee"
		Switch()
		end
		if Key == "h" and ATTACK == false then
			epicsound = "coffee"
		ByeByeSwitch()
		end
		if Key == "m" and ATTACK == false and MODE == "HER" then
		TwoSwitch()
		end
		if Key == "k" and ATTACK == false and MODE == "HER" then
		GamerTest()
		end
		if Key == "l" and ATTACK == false and MODE == "HER" then
		RequestedSwitch()
		end
		if Key == "m" and ATTACK == false and MODE == "Error" then
		AnotherTest()
		end
		if Key == "m" and ATTACK == false  then
if MODE == "HELL" then
		TestSwitch()
		elseif MODE == "HORROR" then
sick.SoundId = (AUDIOS3[MRANDOM(1,#AUDIOS3)])
else
	end
		end
		if Key == "k" and ATTACK == false  then
if MODE == "HORROR" then
		HatefulSwitch()
	end
end
		if Key == "m" and ATTACK == false then
if MODE == "TwoTime" then
		Neck.C0 = Clerp(Neck.C0, NECKC0 * CF(0, 0, 0) * ANGLES(RAD(0+MRANDOM(-90000,90000)), RAD(0+MRANDOM(-90000,90000)), RAD(0+MRANDOM(-90000,90000))), 3 / Animation_Speed)
		CreateSound(363808674,Head,20,MRANDOM(8,11)/10,false)
tecks2.TextColor3 = Color3.fromRGB(MRANDOM(1,255),0,0)
tecks2.TextStrokeColor3 = Color3.fromRGB(MRANDOM(1,255),0,0)
tecks2.Text = 	"H E L P  M E"
 		RightArm.Color = Color3.fromRGB(MRANDOM(1,255),0,0)
		LeftArm.Color = Color3.fromRGB(MRANDOM(1,255),0,0)
		Head.Color = Color3.fromRGB(MRANDOM(1,255),0,0)
		Torso.Color = Color3.fromRGB(MRANDOM(1,255),0,0)
		LeftLeg.Color = Color3.fromRGB(MRANDOM(1,255),0,0)
		RightLeg.Color = Color3.fromRGB(MRANDOM(1,255),0,0)
PRT.Color = Color3.fromRGB(MRANDOM(1,255),0,0)
wait (0.08) 
tecks2.TextColor3 = Color3.fromRGB(40,40,140)
tecks2.TextStrokeColor3 = Color3.fromRGB(60,60,160)
tecks2.Text = "Two Time"
 		RightArm.Color = Color3.fromRGB(60,60,160)
		LeftArm.Color = Color3.fromRGB(60,60,160)
		Head.Color = Color3.fromRGB(60,60,160)
		Torso.Color = Color3.fromRGB(60,60,160)
		LeftLeg.Color = Color3.fromRGB(60,60,160)
		RightLeg.Color = Color3.fromRGB(60,60,160)
PRT.Color = Color3.fromRGB(60,60,160)
		end
end
		if Key == "b" and ATTACK == false then
		if MODE == "HECKING" then
		sick.SoundId = (AUDIOS[MRANDOM(1,#AUDIOS)])
		else
epicsound = "coffee"
		Switche()
	end
		end
		if Key == "j" and ATTACK == false then
		if MODE == "Fighter" then
				sick.SoundId = (AUDIOS2[MRANDOM(1,#AUDIOS2)])
		else
		FighterSwitch()
	end
end
		if Key == "t" and ATTACK == false then
			epicsound = "coffee"
		Switch3()
		end
		if Key == "p" and ATTACK == false then
			epicsound = "coffee"
		Switched()
		end
		if Key == "m" and ATTACK == false and MODE == "ATTACKER"  then
			epicsound = "coffee"
		Switched2()
		end
		if Key == "m" and ATTACK == false and MODE == "Sitting"  then
		PeacefulSwitch()
		end
		if Key == "l" and ATTACK == false and MODE == "Peaceful"  then
		AngeredSwitch()
		end
		if Key == "f" and ATTACK == false then
			epicsound = "coffee"
		FIRESWITCH()
	end
		if Key == "g" and ATTACK == false then
			epicsound = "coffee"
		SwitchTest()
	end
		if Key == "n" and ATTACK == false then
		SitSwitch()
	end
end
function KeyUp(Key)
	KEYHOLD = false
end
	Mouse.Button1Down:connect(function(NEWKEY)
		MouseDown(NEWKEY)
	end)
	Mouse.Button1Up:connect(function(NEWKEY)
		MouseUp(NEWKEY)
	end)
	Mouse.KeyDown:connect(function(NEWKEY)
		KeyDown(NEWKEY)
	end)
	Mouse.KeyUp:connect(function(NEWKEY)
		KeyUp(NEWKEY)
	end)
--//=================================\\
--\\=================================//
function unanchor()
	if UNANCHOR == true then
		g = Character:GetChildren()
		for i = 1, #g do
			if g[i].ClassName == "Part" then
				g[i].Anchored = false
			end
		end
	end
end
--//=================================\\
--||	WRAP THE WHOLE SCRIPT UP
--\\=================================//
Humanoid.Changed:connect(function(Jump)
	if Jump == "Jump" and (Disable_Jump == true) then
		Humanoid.Jump = false
	end
end)
local CONNECT = nil
while true do
	Swait()
	ANIMATE.Parent = nil
	if Character:FindFirstChildOfClass("Humanoid") == nil then
		Humanoid = IT("Humanoid",Character)
	end
	for _,v in next, Humanoid:GetPlayingAnimationTracks() do
	    v:Stop();
	end
	SINE = SINE + CHANGE
	local TORSOVELOCITY = (RootPart.Velocity * VT(1, 0, 1)).magnitude
	local TORSOVERTICALVELOCITY = RootPart.Velocity.y
	local HITFLOOR = Raycast(RootPart.Position, (CF(RootPart.Position, RootPart.Position + VT(0, -1, 0))).lookVector, 4, Character)
	local WALKSPEEDVALUE = 6 / (Humanoid.WalkSpeed / 16)
	if ANIM == "Walk" and TORSOVELOCITY > 1 then
	if MODE == "Fighter" then
	elseif MODE == "Test2" then
else
		RootJoint.C1 = Clerp(RootJoint.C1, ROOTC0 * CF(0, 0, -0.15 * COS(SINE / (WALKSPEEDVALUE / 2))) * ANGLES(RAD(0), RAD(0) - RootPart.RotVelocity.Y / 75, RAD(0)), 2 * (Humanoid.WalkSpeed / 16) / Animation_Speed)
		Neck.C1 = Clerp(Neck.C1, CF(0, -0.5, 0) * ANGLES(RAD(-90), RAD(0), RAD(180)) * ANGLES(RAD(2.5 * SIN(SINE / (WALKSPEEDVALUE / 2))), RAD(0), RAD(0) - Head.RotVelocity.Y / 30), 0.2 * (Humanoid.WalkSpeed / 16) / Animation_Speed)
		RightHip.C1 = Clerp(RightHip.C1, CF(0.5, 0.875 - 0.125 * SIN(SINE / WALKSPEEDVALUE) - 0.15 * COS(SINE / WALKSPEEDVALUE*2), -0.125 * COS(SINE / WALKSPEEDVALUE) +0.2+ 0.2 * COS(SINE / WALKSPEEDVALUE)) * ANGLES(RAD(0), RAD(90), RAD(0)) * ANGLES(RAD(0) - RightLeg.RotVelocity.Y / 75, RAD(0), RAD(76 * COS(SINE / WALKSPEEDVALUE))), 0.2 * (Humanoid.WalkSpeed / 16) / Animation_Speed)
		LeftHip.C1 = Clerp(LeftHip.C1, CF(-0.5, 0.875 + 0.125 * SIN(SINE / WALKSPEEDVALUE) - 0.15 * COS(SINE / WALKSPEEDVALUE*2), 0.125 * COS(SINE / WALKSPEEDVALUE) +0.2+ -0.2 * COS(SINE / WALKSPEEDVALUE)) * ANGLES(RAD(0), RAD(-90), RAD(0)) * ANGLES(RAD(0) + LeftLeg.RotVelocity.Y / 75, RAD(0), RAD(76 * COS(SINE / WALKSPEEDVALUE))), 0.2 * (Humanoid.WalkSpeed / 16) / Animation_Speed)
	end
	elseif (ANIM ~= "Walk") or (TORSOVELOCITY < 1) then
		RootJoint.C1 = Clerp(RootJoint.C1, ROOTC0 * CF(0, 0, 0) * ANGLES(RAD(0), RAD(0), RAD(0)), 0.2 / Animation_Speed)
		Neck.C1 = Clerp(Neck.C1, CF(0, -0.5, 0) * ANGLES(RAD(-90), RAD(0), RAD(180)) * ANGLES(RAD(0), RAD(0), RAD(0)), 0.2 / Animation_Speed)
		RightHip.C1 = Clerp(RightHip.C1, CF(0.5, 1, 0) * ANGLES(RAD(0), RAD(90), RAD(0)) * ANGLES(RAD(0), RAD(0), RAD(0)), 0.2 / Animation_Speed)
		LeftHip.C1 = Clerp(LeftHip.C1, CF(-0.5, 1, 0) * ANGLES(RAD(0), RAD(-90), RAD(0)) * ANGLES(RAD(0), RAD(0), RAD(0)), 0.2 / Animation_Speed)
end
	if TORSOVERTICALVELOCITY > 1 and HITFLOOR == nil then
		ANIM = "Jump"
		if ATTACK == false then
local pl = GetClientProperty(sick,'PlaybackLoudness')
			RootJoint.C0 = Clerp(RootJoint.C0, ROOTC0 * CF(0, 0, 0) * ANGLES(RAD(0), RAD(0), RAD(0)), 0.2 / Animation_Speed)
			Neck.C0 = Clerp(Neck.C0, NECKC0 * CF(0, 0, 0 + ((1) - 1)) * ANGLES(RAD(-20), RAD(0), RAD(0)), 0.2 / Animation_Speed)
			RightShoulder.C0 = Clerp(RightShoulder.C0, CF(1.5, 0.5, 0) * ANGLES(RAD(45), RAD(0), RAD(25))* RIGHTSHOULDERC0, 0.15 / Animation_Speed)
			LeftShoulder.C0 = Clerp(LeftShoulder.C0, CF(-1.5, 0.5, 0) * ANGLES(RAD(-40), RAD(0), RAD(-20)) * LEFTSHOULDERC0, 0.2 / Animation_Speed)
			RightHip.C0 = Clerp(RightHip.C0, CF(1, -1, -0.3) * ANGLES(RAD(0), RAD(90), RAD(0)) * ANGLES(RAD(-5), RAD(0), RAD(-20)), 0.2 / Animation_Speed)
			LeftHip.C0 = Clerp(LeftHip.C0, CF(-1, -1, -0.3) * ANGLES(RAD(0), RAD(-90), RAD(0)) * ANGLES(RAD(-5), RAD(0), RAD(20)), 0.2 / Animation_Speed)
	    end
	elseif TORSOVERTICALVELOCITY < -1 and HITFLOOR == nil then
		ANIM = "Fall"
		if ATTACK == false then
local pl = GetClientProperty(sick,'PlaybackLoudness')
			RootJoint.C0 = Clerp(RootJoint.C0, ROOTC0 * CF(0, 0, 0 ) * ANGLES(RAD(0), RAD(0), RAD(0)), 0.2 / Animation_Speed)
			Neck.C0 = Clerp(Neck.C0, NECKC0 * CF(0, 0 , 0 + ((1) - 1)) * ANGLES(RAD(20), RAD(0), RAD(0)), 0.2 / Animation_Speed)
			RightShoulder.C0 = Clerp(RightShoulder.C0, CF(1.5, 0.5, 0) * ANGLES(RAD(45), RAD(0), RAD(25))* RIGHTSHOULDERC0, 0.15 / Animation_Speed)
			LeftShoulder.C0 = Clerp(LeftShoulder.C0, CF(-1.5, 0.5, 0) * ANGLES(RAD(0), RAD(0), RAD(-60)) * LEFTSHOULDERC0, 0.2 / Animation_Speed)
			RightHip.C0 = Clerp(RightHip.C0, CF(1, -1, 0) * ANGLES(RAD(0), RAD(90), RAD(0)) * ANGLES(RAD(0), RAD(0), RAD(20)), 0.2 / Animation_Speed)
			LeftHip.C0 = Clerp(LeftHip.C0, CF(-1, -1, 0) * ANGLES(RAD(0), RAD(-90), RAD(0)) * ANGLES(RAD(0), RAD(0), RAD(10)), 0.2 / Animation_Speed)
		end
	elseif TORSOVELOCITY < 1 and HITFLOOR ~= nil then
		ANIM = "Idle"
		if ATTACK == false then
		if MODE == "HER" then
local pl = GetClientProperty(sick,'PlaybackLoudness')
			RootJoint.C0 = Clerp(RootJoint.C0,ROOTC0 * CF(0 , 0 , -0.7) * ANGLES(RAD(MRANDOM(-15,15)), RAD(MRANDOM(-15,15)), RAD(MRANDOM(-15,15))), 0.35 / Animation_Speed)
			Neck.C0 = Clerp(Neck.C0, NECKC0 * CF(0, 0, 0) * ANGLES(RAD(30+MRANDOM(-15,15)), RAD(0+MRANDOM(-15,15)), RAD(0+MRANDOM(-15,15))), 0.35 / Animation_Speed)
			RightShoulder.C0 = Clerp(RightShoulder.C0, CF(1.5, 0.5, 0) * ANGLES(RAD(160+MRANDOM(-15,15)), RAD(0+MRANDOM(-15,15)), RAD(-30+MRANDOM(-15,15)))* RIGHTSHOULDERC0, 0.35 / Animation_Speed)
		    LeftShoulder.C0 = Clerp(LeftShoulder.C0, CF(-1.5, 0.5, 0) * ANGLES(RAD(160+MRANDOM(-15,15)), RAD(0+MRANDOM(-15,15)), RAD(30+MRANDOM(-15,15))) * LEFTSHOULDERC0, 0.35 / Animation_Speed)
			RightHip.C0 = Clerp(RightHip.C0, CF(1, -0.5, -0.5) * ANGLES(RAD(0), RAD(0), RAD(0)) * ANGLES(RAD(0), RAD(90), RAD(0)), 0.35 / Animation_Speed)
			LeftHip.C0 = Clerp(LeftHip.C0, CF(-1, -1 , 0) * ANGLES(RAD(-60), RAD(0), RAD(0)) * ANGLES(RAD(0), RAD(-90), RAD(0)), 0.35 / Animation_Speed)
		elseif MODE == "PAIN" then
			snap = math.random(1,6)
			if snap == 1 then
	Neck.C0 = Clerp(Neck.C0, NECKC0 * CF(0, 0, 0) * ANGLES(RAD(0+MRANDOM(-35,35)), RAD(0+MRANDOM(-35,35)), RAD(0+MRANDOM(-35,35))), 2 / Animation_Speed)
			end
			RootJoint.C0 = Clerp(RootJoint.C0,ROOTC0 * CF(0,0,-.2+.05*COS(SINE / 12))*ANGLES(RAD(1-2*COS(SINE / 12)),RAD(0),RAD(0)), 1 / Animation_Speed)
	        Neck.C0 = Clerp(Neck.C0, NECKC0 * CF(0, 0, 0 + ((1) - 1)) * ANGLES(RAD(-2.5+1*COS(SINE / 12)), RAD(MRANDOM(-5,5)), RAD(0)), 1 / Animation_Speed) 
	        RightShoulder.C0 = Clerp(RightShoulder.C0, CF(1.5, 0.5, 0) * ANGLES(RAD(0), RAD(0), RAD(15 + 3 * COS(SINE / 40) - 3 * SIN(SINE / 40) + MRANDOM(-35,35))) * RIGHTSHOULDERC0, 1 / Animation_Speed)
	        LeftShoulder.C0 = Clerp(LeftShoulder.C0, CF(-1.5, 0.5, 0) * ANGLES(RAD(0), RAD(0), RAD(-15 + 3 * COS(SINE / 40) + 3 * SIN(SINE / 40) - MRANDOM(-35,35))) * LEFTSHOULDERC0, 1 / Animation_Speed)
		    RightHip.C0 = Clerp(RightHip.C0, CF(1, -1-.05*COS(SINE / 12), -0.01) * ANGLES(RAD(0), RAD(80), RAD(0)) * ANGLES(RAD(-8), RAD(0), RAD(0)), 1 / Animation_Speed)
		    LeftHip.C0 = Clerp(LeftHip.C0, CF(-1, -1-.05*COS(SINE  / 12), -0.01) * ANGLES(RAD(0), RAD(-80), RAD(0)) * ANGLES(RAD(-8), RAD(0), RAD(0)), 1 / Animation_Speed)
		elseif MODE == "HELL" then
				if math.random(1,8) == 1 then
		Neck.C0 = Clerp(Neck.C0, NECKC0 * CF(0, 0, 0 + ((1) - 1)) * ANGLES(RAD(MRANDOM(-87498,12093847)), RAD(MRANDOM(-123456,3746525)), RAD(MRANDOM(-2134567876,98764356))), 0.15 / Animation_Speed)
				end
		if(math.random(1,4)==1)then
		RightShoulder.C0 = Clerp(RightShoulder.C0, CF(1.5, 0.5, 0) * ANGLES(RAD(MRANDOM(-99999999,99999999)), RAD(MRANDOM(-99999999,99999999)), RAD(MRANDOM(-99999999,99999999))) * RIGHTSHOULDERC0, 0.15 / Animation_Speed)
		LeftShoulder.C0 = Clerp(LeftShoulder.C0, CF(-1.5, 0.5, 0) * ANGLES(RAD(MRANDOM(-99999999,99999999)), RAD(MRANDOM(-99999999,99999999)), RAD(MRANDOM(-99999999,99999999))) * LEFTSHOULDERC0, 0.15 / Animation_Speed)
		end
		RootJoint.C0 = Clerp(RootJoint.C0,ROOTC0 * CF(0, 0, 0 + 0.2 * SIN(SINE / 12)) * ANGLES(RAD(0), RAD(0), RAD(0)), 0.15 / Animation_Speed)
		Neck.C0 = Clerp(Neck.C0, NECKC0 * CF(0, 0, 0 + ((1) - 1)) * ANGLES(RAD(15 - 2.5 * SIN(SINE / 12)), RAD(MRANDOM(-25,25)), RAD(0)), 0.15 / Animation_Speed)
		RightShoulder.C0 = Clerp(RightShoulder.C0, CF(1.5, 0.5, 0) * ANGLES(RAD(0), RAD(MRANDOM(-25,25)), RAD(12)) * RIGHTSHOULDERC0, 0.15 / Animation_Speed)
		LeftShoulder.C0 = Clerp(LeftShoulder.C0, CF(-1.5, 0.5, 0) * ANGLES(RAD(0), RAD(MRANDOM(-25,25)), RAD(-12)) * LEFTSHOULDERC0, 0.15 / Animation_Speed)
		RightHip.C0 = Clerp(RightHip.C0, CF(1, -1 - 0.2 * SIN(SINE / 12), -0.01) * ANGLES(RAD(0), RAD(90), RAD(0)) * ANGLES(RAD(-8), RAD(0), RAD(0)), 0.15 / Animation_Speed)
		LeftHip.C0 = Clerp(LeftHip.C0, CF(-1, -1 - 0.2 * SIN(SINE / 12), -0.01) * ANGLES(RAD(0), RAD(-90), RAD(0)) * ANGLES(RAD(-8), RAD(0), RAD(0)), 0.15 / Animation_Speed)
		elseif MODE == "FIRE" then
				if math.random(1,10) == 1 then
            Neck.C0 = Clerp(Neck.C0, NECKC0 * CF(0 , 0 , 0 ) * ANGLES(RAD(0+MRANDOM(-200,200)), RAD(0+MRANDOM(-200,200)), RAD(0+15*COS(SINE / 12)+MRANDOM(-200,200))), 1 / Animation_Speed)
				end
				if math.random(1,15) == 1 then
            Neck.C0 = Clerp(Neck.C0, NECKC0 * CF(0+MRANDOM(-1,1) , 0+MRANDOM(-1,1) , 0+MRANDOM(-1,1) ) * ANGLES(RAD(0+MRANDOM(-15,15)), RAD(0+MRANDOM(-15,15)), RAD(0+15*COS(SINE / 12))), 1 / Animation_Speed)
            RightShoulder.C0 = Clerp(RightShoulder.C0, CF(1.5+MRANDOM(-1,1) , 0.5+MRANDOM(-1,1) , 0+MRANDOM(-1,1) ) * ANGLES(RAD(0), RAD(0), RAD(-20))* ANGLES(RAD(0), RAD(0), RAD(0)) * RIGHTSHOULDERC0, 1 / Animation_Speed)
            LeftShoulder.C0 = Clerp(LeftShoulder.C0, CF(-1.5+MRANDOM(-1,1) , 0.5+MRANDOM(-1,1) , 0+MRANDOM(-1,1) ) * ANGLES(RAD(900), RAD(0), RAD(20))* ANGLES(RAD(0), RAD(0), RAD(0)) * LEFTSHOULDERC0, 1 / Animation_Speed)
				end
				RootJoint.C0 = Clerp(RootJoint.C0,ROOTC0 * CF(0 , 0 , -0.2) * ANGLES(RAD(0+MRANDOM(-15,15)), RAD(0+MRANDOM(-15,15)), RAD(0+MRANDOM(-15,15))), 1 / Animation_Speed)
            Neck.C0 = Clerp(Neck.C0, NECKC0 * CF(0 , 0 , 0 ) * ANGLES(RAD(0+MRANDOM(-15,15)), RAD(0+MRANDOM(-15,15)), RAD(0+15*COS(SINE / 12))), 1 / Animation_Speed)
            RightShoulder.C0 = Clerp(RightShoulder.C0, CF(1.5 , 0.5 , 0 ) * ANGLES(RAD(0+MRANDOM(-15,15)), RAD(0+MRANDOM(-15,15)), RAD(-20+MRANDOM(-15,15)))* ANGLES(RAD(0), RAD(0), RAD(0)) * RIGHTSHOULDERC0, 1 / Animation_Speed)
            LeftShoulder.C0 = Clerp(LeftShoulder.C0, CF(-1.5 , 0.5 , 0 ) * ANGLES(RAD(900+MRANDOM(-15,15)), RAD(0+MRANDOM(-15,15)), RAD(20+MRANDOM(-15,15)))* ANGLES(RAD(0), RAD(0), RAD(0)) * LEFTSHOULDERC0, 1 / Animation_Speed)
            RightHip.C0 = Clerp(RightHip.C0, CF(1 , -0.8  - 0 ,0 ) * ANGLES(RAD(0+MRANDOM(-15,15)), RAD(-5+MRANDOM(-15,15)), RAD(0+MRANDOM(-15,15))) * ANGLES(RAD(0), RAD(90), RAD(0)), 1 / Animation_Speed)
            LeftHip.C0 = Clerp(LeftHip.C0, CF(-1 , -0.8  - 0 , 0 ) * ANGLES(RAD(0+MRANDOM(-15,15)), RAD(5+MRANDOM(-15,15)), RAD(0+MRANDOM(-15,15))) * ANGLES(RAD(0), RAD(-90), RAD(0)), 1 / Animation_Speed)
		elseif MODE == "bruh" then
     			local pl = GetClientProperty(sick,'PlaybackLoudness')
			bounce = pl / 1200
				if math.random(12,14+pl/400) == 15 then
            Neck.C0 = Clerp(Neck.C0, NECKC0 * CF(0 , 0 , 0 ) * ANGLES(RAD(0+15*COS(SINE / 6)+MRANDOM(-100,100)), RAD(0+15*COS(SINE / 4)+MRANDOM(-100,100)), RAD(0+15*COS(SINE / 5)+MRANDOM(-100,100))), 3 / Animation_Speed)
				end
			RootJoint.C0 = Clerp(RootJoint.C0,ROOTC0 * CF(0 , 0 , 0+.1*COS(SINE / 18)) * ANGLES(RAD(0), RAD(0), RAD(0)), 0.35 / Animation_Speed)
            Neck.C0 = Clerp(Neck.C0, NECKC0 * CF(0 , 0 , 0 ) * ANGLES(RAD(0+15*COS(SINE / 6)--[[+MRANDOM(-15,15)]]), RAD(0+15*COS(SINE / 4)--[[+MRANDOM(-15,15)]]), RAD(0+15*COS(SINE / 5)--[[+MRANDOM(-15,15)]])), 1 / Animation_Speed)
            RightShoulder.C0 = Clerp(RightShoulder.C0, CF(1, 0.5+.1*COS(SINE / 18), 0.5) * ANGLES(RAD(-20), RAD(-.6), RAD(-43)) * RIGHTSHOULDERC0, 1 / Animation_Speed)
            LeftShoulder.C0 = Clerp(LeftShoulder.C0, CF(-1.5, 0.5+.1*COS(SINE / 18), 0) * ANGLES(RAD(0), RAD(0), RAD(-43)) * LEFTSHOULDERC0, 1 / Animation_Speed)
		    RightHip.C0 = Clerp(RightHip.C0, CF(1, -1-.1*COS(SINE / 18), -0.01) * ANGLES(RAD(0), RAD(75), RAD(0)) * ANGLES(RAD(0), RAD(0), RAD(0)), 1 / Animation_Speed)
		    LeftHip.C0 = Clerp(LeftHip.C0, CF(-1, -0.-pl/470, -0.6) * ANGLES(RAD(0), RAD(-75), RAD(0)) * ANGLES(RAD(0), RAD(0), RAD(0)), 1 / Animation_Speed)
		elseif MODE == "ByeBye" then
			local pl = GetClientProperty(sick,'PlaybackLoudness')
			bounce = pl / 1200
 			RootJoint.C0 = Clerp(RootJoint.C0,ROOTC0 * CF(0 , 0 , -0.2 + 0.2*COS(SINE / 13) ) * ANGLES(RAD(-20), RAD(0), RAD(0)), 0.35 / Animation_Speed)
			Neck.C0 = Clerp(Neck.C0, NECKC0 * CF(0, 0, 0) * ANGLES(RAD(-20+MRANDOM(-15-pl/200,15+pl/200)), RAD(0+MRANDOM(-15-pl/200,15+pl/200)), RAD(0+MRANDOM(-15-pl/200,15+pl/200))), 0.35 / Animation_Speed)
			RightShoulder.C0 = Clerp(RightShoulder.C0, CF(1.5, 0.5+ 0.2*COS(SINE / 13), 0) * ANGLES(RAD(-20+MRANDOM(-15-pl/200,15+pl/200)), RAD(0+MRANDOM(-15-pl/200,15+pl/200)), RAD(0+MRANDOM(-15-pl/200,15+pl/200)))* RIGHTSHOULDERC0, 0.35 / Animation_Speed)
		    LeftShoulder.C0 = Clerp(LeftShoulder.C0, CF(-1.5, 0.5+ 0.2*COS(SINE / 13), 0) * ANGLES(RAD(-20+MRANDOM(-15-pl/200,15+pl/200)), RAD(0+MRANDOM(-15-pl/200,15+pl/200)), RAD(0+MRANDOM(-15-pl/200,15+pl/200))) * LEFTSHOULDERC0, 0.35 / Animation_Speed)
			RightHip.C0 = Clerp(RightHip.C0, CF(1, -1- 0.2*COS(SINE / 13), 0) * ANGLES(RAD(-20), RAD(0), RAD(0)) * ANGLES(RAD(0), RAD(90), RAD(0)), 0.35 / Animation_Speed)
			LeftHip.C0 = Clerp(LeftHip.C0, CF(-1, -1- 0.2*COS(SINE / 13) , 0) * ANGLES(RAD(-20), RAD(0), RAD(0)) * ANGLES(RAD(0), RAD(-90), RAD(0)), 0.35 / Animation_Speed)
		elseif MODE == "ATTACKER" then
			local pl = GetClientProperty(sick,'PlaybackLoudness')
			bounce = pl / 1200
			RootJoint.C0 = Clerp(RootJoint.C0,ROOTC0 * CF(0 , 0 , 00 + 0.2 * COS(SINE / 12)) * ANGLES(RAD(0), RAD(0), RAD(0)), 1 / Animation_Speed)
			Neck.C0 = Clerp(Neck.C0, NECKC0 * CF(0, 0, 0) * ANGLES(RAD(30), RAD(0), RAD(0 + 25 * COS(SINE / 20+pl/100))), 1 / Animation_Speed)
			RightShoulder.C0 = Clerp(RightShoulder.C0, CF(1.5, 0.5+ 0.35 * SIN(SINE / 12), 0) * ANGLES(RAD(0+MRANDOM(-15-pl/100,15+pl/100)), RAD(0+MRANDOM(-15-pl/100,15+pl/100)), RAD(0+MRANDOM(-15-pl/100,15+pl/100)))* RIGHTSHOULDERC0, 1 / Animation_Speed)
		    LeftShoulder.C0 = Clerp(LeftShoulder.C0, CF(-1.5, 0.5 + 0.35 * SIN(SINE / 12), 0) * ANGLES(RAD(0+MRANDOM(-15-pl/100,15+pl/100)), RAD(0+MRANDOM(-15-pl/100,15+pl/100)), RAD(0+MRANDOM(-15-pl/100,15+pl/100)))* LEFTSHOULDERC0, 1 / Animation_Speed)
			RightHip.C0 = Clerp(RightHip.C0, CF(1, -1- 0.2 * COS(SINE / 12), 0) * ANGLES(RAD(0), RAD(75), RAD(0)) * ANGLES(RAD(-8), RAD(0), RAD(0)), 1 / Animation_Speed)
			LeftHip.C0 = Clerp(LeftHip.C0, CF(-1, -1- 0.2 * COS(SINE / 12) , 0) * ANGLES(RAD(0), RAD(-75), RAD(0)) * ANGLES(RAD(-8), RAD(0), RAD(0)), 1 / Animation_Speed)
			if MRANDOM(1,250) == 1 then
					ATTACK = true
				for i = 1, 75 do
						Swait()
							sick.Pitch = MRANDOM(11,15)/11
			RootJoint.C0 = Clerp(RootJoint.C0,ROOTC0 * CF(0 , 0 , 0) * ANGLES(RAD(MRANDOM(-9000,9000)), RAD(MRANDOM(-9000,9000)), RAD(MRANDOM(-9000,9000))), 0.35 / Animation_Speed)
			Neck.C0 = Clerp(Neck.C0, NECKC0 * CF(0, 0, 0) * ANGLES(RAD(MRANDOM(-9000,9000)), RAD(MRANDOM(-9000,9000)), RAD(MRANDOM(-9000,9000))), 0.35 / Animation_Speed)
			RightShoulder.C0 = Clerp(RightShoulder.C0, CF(1.5, 0.5, 0) * ANGLES(RAD(MRANDOM(-9000,9000)), RAD(MRANDOM(-9000,9000)), RAD(MRANDOM(-9000,9000)))* RIGHTSHOULDERC0, 0.35 / Animation_Speed)
		    LeftShoulder.C0 = Clerp(LeftShoulder.C0, CF(-1.5, 0.5, 0) * ANGLES(RAD(MRANDOM(-9000,9000)), RAD(MRANDOM(-9000,9000)), RAD(MRANDOM(-9000,9000))) * LEFTSHOULDERC0, 0.35 / Animation_Speed)
			RightHip.C0 = Clerp(RightHip.C0, CF(1, -1, 0) * ANGLES(RAD(MRANDOM(-9000,9000)), RAD(MRANDOM(-9000,9000)), RAD(MRANDOM(-9000,9000))) * ANGLES(RAD(0), RAD(90), RAD(0)), 0.35 / Animation_Speed)
			LeftHip.C0 = Clerp(LeftHip.C0, CF(-1, -1 , 0) * ANGLES(RAD(MRANDOM(-9000,9000)), RAD(MRANDOM(-9000,9000)), RAD(MRANDOM(-9000,9000))) * ANGLES(RAD(0), RAD(-90), RAD(0)), 0.35 / Animation_Speed)
				       end
										sick.Pitch = 0.7
									ATTACK = false
			end		
		elseif MODE == "ABRUGER" then
			RootJoint.C0 = Clerp(RootJoint.C0,ROOTC0 * CF(0 , 0 , 0) * ANGLES(RAD(MRANDOM(-9000,9000)), RAD(MRANDOM(-9000,9000)), RAD(MRANDOM(-9000,9000))), 0.35 / Animation_Speed)
			Neck.C0 = Clerp(Neck.C0, NECKC0 * CF(0, 0, 0) * ANGLES(RAD(MRANDOM(-9000,9000)), RAD(MRANDOM(-9000,9000)), RAD(MRANDOM(-9000,9000))), 0.35 / Animation_Speed)
			RightShoulder.C0 = Clerp(RightShoulder.C0, CF(1.5, 0.5, 0) * ANGLES(RAD(MRANDOM(-9000,9000)), RAD(MRANDOM(-9000,9000)), RAD(MRANDOM(-9000,9000)))* RIGHTSHOULDERC0, 0.35 / Animation_Speed)
		    LeftShoulder.C0 = Clerp(LeftShoulder.C0, CF(-1.5, 0.5, 0) * ANGLES(RAD(MRANDOM(-9000,9000)), RAD(MRANDOM(-9000,9000)), RAD(MRANDOM(-9000,9000))) * LEFTSHOULDERC0, 0.35 / Animation_Speed)
			RightHip.C0 = Clerp(RightHip.C0, CF(1, -1, 0) * ANGLES(RAD(MRANDOM(-9000,9000)), RAD(MRANDOM(-9000,9000)), RAD(MRANDOM(-9000,9000))) * ANGLES(RAD(0), RAD(90), RAD(0)), 0.35 / Animation_Speed)
			LeftHip.C0 = Clerp(LeftHip.C0, CF(-1, -1 , 0) * ANGLES(RAD(MRANDOM(-9000,9000)), RAD(MRANDOM(-9000,9000)), RAD(MRANDOM(-9000,9000))) * ANGLES(RAD(0), RAD(-90), RAD(0)), 0.35 / Animation_Speed)
		elseif MODE == "HECKING" then
			local pl = GetClientProperty(sick,'PlaybackLoudness')
			if MRANDOM(1+pl/150,1+pl/150) == 15 then
			Neck.C0 = Clerp(Neck.C0, NECKC0 * CF(0, 0, 0) * ANGLES(RAD(0+MRANDOM(-25,25)), RAD(0+MRANDOM(-25,25)), RAD(-20+MRANDOM(-25,25))), 0.35 / Animation_Speed)
			end
			RootJoint.C0 = Clerp(RootJoint.C0,ROOTC0 * CF(0 , 0 , 0) * ANGLES(RAD(0), RAD(0), RAD(20)), 0.35 / Animation_Speed)
			Neck.C0 = Clerp(Neck.C0, NECKC0 * CF(0, 0, 0) * ANGLES(RAD(0), RAD(0), RAD(-20)), 0.35 / Animation_Speed)
			RightShoulder.C0 = Clerp(RightShoulder.C0, CF(1.5, 0.5, 0) * ANGLES(RAD(90-20*pl/150), RAD(0), RAD(0))* RIGHTSHOULDERC0, 0.35 / Animation_Speed)
		    LeftShoulder.C0 = Clerp(LeftShoulder.C0, CF(-1.5, 0.7, -0.1) * ANGLES(RAD(160), RAD(20), RAD(30)) * LEFTSHOULDERC0, 0.35 / Animation_Speed)
			RightHip.C0 = Clerp(RightHip.C0, CF(1, -1, 0) * ANGLES(RAD(0), RAD(-15), RAD(0)) * ANGLES(RAD(0), RAD(90), RAD(0)), 0.35 / Animation_Speed)
			LeftHip.C0 = Clerp(LeftHip.C0, CF(-1, -1 , 0) * ANGLES(RAD(0), RAD(15), RAD(0)) * ANGLES(RAD(0), RAD(-90), RAD(0)), 0.35 / Animation_Speed)
		elseif MODE == "Sitting" then
			local pl = GetClientProperty(sick,'PlaybackLoudness')
			RootJoint.C0 = Clerp(RootJoint.C0,ROOTC0 * CF(0+0.5*COS(SINE / 15) , 0+0.5*COS(SINE / 14) , 0+0.5*COS(SINE / 16)) * ANGLES(RAD(0), RAD(0), RAD(0)), 0.35 / Animation_Speed)
			Neck.C0 = Clerp(Neck.C0, NECKC0 * CF(0, 0, 0) * ANGLES(RAD(20), RAD(0), RAD(0)), 0.35 / Animation_Speed)
			RightShoulder.C0 = Clerp(RightShoulder.C0, CF(0.6, 0.5, -0.3) * ANGLES(RAD(120), RAD(0), RAD(-70))* RIGHTSHOULDERC0, 0.35 / Animation_Speed)
		    LeftShoulder.C0 = Clerp(LeftShoulder.C0, CF(-0.6, 0.5, -0.3) * ANGLES(RAD(60), RAD(0), RAD(70)) * LEFTSHOULDERC0, 0.35 / Animation_Speed)
			RightHip.C0 = Clerp(RightHip.C0, CF(1, -1, -1) * ANGLES(RAD(90), RAD(-20), RAD(-70)) * ANGLES(RAD(0), RAD(90), RAD(0)), 0.35 / Animation_Speed)
			LeftHip.C0 = Clerp(LeftHip.C0, CF(-1, -1 , 0) * ANGLES(RAD(90), RAD(0), RAD(0)) * ANGLES(RAD(0), RAD(-90), RAD(0)), 0.35 / Animation_Speed)
			elseif MODE == "Peaceful" then
			local pl = GetClientProperty(sick,'PlaybackLoudness')
			RootJoint.C0 = Clerp(RootJoint.C0,ROOTC0 * CF(0 , 0 , 0+0.3*COS(SINE / 17)) * ANGLES(RAD(0), RAD(0), RAD(0)), 0.35 / Animation_Speed)
			Neck.C0 = Clerp(Neck.C0, NECKC0 * CF(0, 0, 0) * ANGLES(RAD(30), RAD(0), RAD(0+25*COS(SINE / 14))), 0.35 / Animation_Speed)
			RightShoulder.C0 = Clerp(RightShoulder.C0, CF(1, 0.5, 0.3) * ANGLES(RAD(-30), RAD(0), RAD(-30))* RIGHTSHOULDERC0, 0.35 / Animation_Speed)
		    LeftShoulder.C0 = Clerp(LeftShoulder.C0, CF(-1, 0.5, 0.3) * ANGLES(RAD(-30), RAD(0), RAD(30)) * LEFTSHOULDERC0, 0.35 / Animation_Speed)
			RightHip.C0 = Clerp(RightHip.C0, CF(1, -1-0.3*COS(SINE / 17), 0) * ANGLES(RAD(0), RAD(-10), RAD(0)) * ANGLES(RAD(0), RAD(90), RAD(0)), 0.35 / Animation_Speed)
			LeftHip.C0 = Clerp(LeftHip.C0, CF(-1, -1-0.3*COS(SINE / 17) , 0) * ANGLES(RAD(0), RAD(10), RAD(0)) * ANGLES(RAD(0), RAD(-90), RAD(0)), 0.35 / Animation_Speed)
			elseif MODE == "Angered" then
			local pl = GetClientProperty(sick,'PlaybackLoudness')
			if MRANDOM(5+pl/60,5+pl/60) == 10 or 15 or 20 or 25 or 30 or 35 or 40 or 50 then
			Neck.C0 = Clerp(Neck.C0, NECKC0 * CF(0, 0, 0) * ANGLES(RAD(0+MRANDOM(-25,25)), RAD(0+MRANDOM(-25,25)), RAD(-30+MRANDOM(-25,25))), 0.35 / Animation_Speed)
			end
			RootJoint.C0 = Clerp(RootJoint.C0,ROOTC0 * CF(0 , 0 , 0) * ANGLES(RAD(0), RAD(0), RAD(30)), 0.35 / Animation_Speed)
			RightShoulder.C0 = Clerp(RightShoulder.C0, CF(1.5, 0.5, 0) * ANGLES(RAD(50), RAD(0+MRANDOM(-45,45)), RAD(20))* RIGHTSHOULDERC0, 0.35 / Animation_Speed)
		    LeftShoulder.C0 = Clerp(LeftShoulder.C0, CF(-1.5, 0.5, 0) * ANGLES(RAD(0+MRANDOM(-10,10)), RAD(20+MRANDOM(-10,10)), RAD(-20+MRANDOM(-10,10))) * LEFTSHOULDERC0, 0.35 / Animation_Speed)
			RightHip.C0 = Clerp(RightHip.C0, CF(1, -1, 0) * ANGLES(RAD(0), RAD(-20), RAD(0)) * ANGLES(RAD(0), RAD(90), RAD(0)), 0.35 / Animation_Speed)
			LeftHip.C0 = Clerp(LeftHip.C0, CF(-1, -1 , 0) * ANGLES(RAD(0), RAD(20), RAD(0)) * ANGLES(RAD(0), RAD(-90), RAD(0)), 0.35 / Animation_Speed)
		elseif MODE == "Fighter" then
				RootJoint.C0 = Clerp(RootJoint.C0,ROOTC0 * CF(0, 0, 1+0.5*COS(SINE / 16)) * ANGLES(RAD(0), RAD(0), RAD(0+900*COS(SINE / 16))), 1 / Animation_Speed)
            Neck.C0 = Clerp(Neck.C0, NECKC0 * CF(0, 0, 0) * ANGLES(RAD(0), RAD(0), RAD(0-900*COS(SINE / 16))), 1 / Animation_Speed)
            RightShoulder.C0 = Clerp(RightShoulder.C0, CF(1.5, 0.5, 0) * ANGLES(RAD(90), RAD(0), RAD(90)) * RIGHTSHOULDERC0, 1 / Animation_Speed)
            LeftShoulder.C0 = Clerp(LeftShoulder.C0, CF(-1.5, 0.5, 0) * ANGLES(RAD(90), RAD(0), RAD(-90)) * LEFTSHOULDERC0, 1 / Animation_Speed)
            RightHip.C0 = Clerp(RightHip.C0, CF(1, -1, -0.01) * ANGLES(RAD(0), RAD(90), RAD(0)) * ANGLES(RAD(0), RAD(0), RAD(0)), 0.15 / Animation_Speed)
            LeftHip.C0 = Clerp(LeftHip.C0, CF(-1, -1, -0.01) * ANGLES(RAD(0), RAD(-90), RAD(0)) * ANGLES(RAD(0), RAD(0), RAD(0)), 0.15 / Animation_Speed)
		elseif MODE == "TwoTime" then
			local pl = GetClientProperty(sick,'PlaybackLoudness')
			RootJoint.C0 = Clerp(RootJoint.C0,ROOTC0 * CF(0 , 0 , 0) * ANGLES(RAD(0), RAD(0), RAD(0)), 0.35 / Animation_Speed)
			Neck.C0 = Clerp(Neck.C0, NECKC0 * CF(0, 0, 0) * ANGLES(RAD(0), RAD(0), RAD(0-20*COS(SINE / 10))), 0.35 / Animation_Speed)
			RightShoulder.C0 = Clerp(RightShoulder.C0, CF(1.5, 0.5, 0) * ANGLES(RAD(0-40*COS(SINE / 10)), RAD(0), RAD(0))* RIGHTSHOULDERC0, 0.35 / Animation_Speed)
		    LeftShoulder.C0 = Clerp(LeftShoulder.C0, CF(-1, 0.5, 0.5) * ANGLES(RAD(-36), RAD(0), RAD(40)) * LEFTSHOULDERC0, 0.35 / Animation_Speed)
			RightHip.C0 = Clerp(RightHip.C0, CF(1, -1, 0) * ANGLES(RAD(0), RAD(0), RAD(0)) * ANGLES(RAD(0), RAD(90), RAD(0)), 0.35 / Animation_Speed)
		    LeftHip.C0 = Clerp(LeftHip.C0, CF(-1, -0.-pl/270, -0.6) * ANGLES(RAD(0), RAD(-75), RAD(0)) * ANGLES(RAD(0), RAD(0), RAD(0)), 1 / Animation_Speed)
			elseif MODE == "HORROR" then
			local pl = GetClientProperty(sick,'PlaybackLoudness')
			if MRANDOM(1,25) == 1 then
					Neck.C0 = Clerp(Neck.C0, NECKC0 * CF(0, 0, 0) * ANGLES(RAD(0+MRANDOM(-900,900)), RAD(0+MRANDOM(-900,900)), RAD(0+MRANDOM(-900,900))), 3 / Animation_Speed)
		CreateSound(363808674,Head,100,MRANDOM(8,11)/10,false)
			RightShoulder.C0 = Clerp(RightShoulder.C0, CF(1.5, 0.5, 0) * ANGLES(RAD(900), RAD(0), RAD(0))* RIGHTSHOULDERC0, 2 / Animation_Speed)
		    LeftShoulder.C0 = Clerp(LeftShoulder.C0, CF(-1.5, 0.5, 0) * ANGLES(RAD(900), RAD(0), RAD(0)) * LEFTSHOULDERC0, 2 / Animation_Speed)
			end
			RootJoint.C0 = Clerp(RootJoint.C0,ROOTC0 * CF(0 , 0 , 0+0.1*COS(SINE / 2)) * ANGLES(RAD(0), RAD(0), RAD(0)), 0.35 / Animation_Speed)
			Neck.C0 = Clerp(Neck.C0, NECKC0 * CF(0, 0, 0) * ANGLES(RAD(30+MRANDOM(-15,15)), RAD(0+MRANDOM(-15,15)), RAD(0+MRANDOM(-15,15))), 0.35 / Animation_Speed)
			RightShoulder.C0 = Clerp(RightShoulder.C0, CF(1.5, 0.5, -0.2) * ANGLES(RAD(120), RAD(-30), RAD(-40))* RIGHTSHOULDERC0, 0.35 / Animation_Speed)
		    LeftShoulder.C0 = Clerp(LeftShoulder.C0, CF(-1.5, 0.5, -0.2) * ANGLES(RAD(120), RAD(30), RAD(40)) * LEFTSHOULDERC0, 0.35 / Animation_Speed)
			RightHip.C0 = Clerp(RightHip.C0, CF(1, -1-0.1*COS(SINE / 2), 0) * ANGLES(RAD(0), RAD(-10), RAD(0)) * ANGLES(RAD(0), RAD(90), RAD(0)), 0.35 / Animation_Speed)
			LeftHip.C0 = Clerp(LeftHip.C0, CF(-1, -1-0.1*COS(SINE / 2) , 0) * ANGLES(RAD(0), RAD(10), RAD(0)) * ANGLES(RAD(0), RAD(-90), RAD(0)), 0.35 / Animation_Speed)		
			elseif MODE == "HATEFUL" then
			local pl = GetClientProperty(sick,'PlaybackLoudness')
			RootJoint.C0 = Clerp(RootJoint.C0,ROOTC0 * CF(0 , 0 , 0+0.3*COS(SINE / 13)) * ANGLES(RAD(0), RAD(0), RAD(0)), 0.35 / Animation_Speed)
			Neck.C0 = Clerp(Neck.C0, NECKC0 * CF(0, 0, 0) * ANGLES(RAD(20+MRANDOM(-15,15)), RAD(0+MRANDOM(-15,15)), RAD(0+25*COS(SINE / 6)+MRANDOM(-15,15))), 0.35 / Animation_Speed)
			RightShoulder.C0 = Clerp(RightShoulder.C0, CF(1, 0.5, 0.5) * ANGLES(RAD(-35.8), RAD(0), RAD(-40))* RIGHTSHOULDERC0, 0.35 / Animation_Speed)
		    LeftShoulder.C0 = Clerp(LeftShoulder.C0, CF(-1, 0.5, 0.5) * ANGLES(RAD(-36), RAD(0), RAD(40)) * LEFTSHOULDERC0, 0.35 / Animation_Speed)
			RightHip.C0 = Clerp(RightHip.C0, CF(1, -1-0.3*COS(SINE / 13), 0) * ANGLES(RAD(0), RAD(-20), RAD(0)) * ANGLES(RAD(0), RAD(90), RAD(0)), 0.35 / Animation_Speed)
			LeftHip.C0 = Clerp(LeftHip.C0, CF(-1, -1-0.3*COS(SINE / 13) , 0) * ANGLES(RAD(0), RAD(20), RAD(0)) * ANGLES(RAD(0), RAD(-90), RAD(0)), 0.35 / Animation_Speed)
			elseif MODE == "Test2" then
			local pl = GetClientProperty(sick,'PlaybackLoudness')
			RootJoint.C0 = Clerp(RootJoint.C0,ROOTC0 * CF(0, 0, 1  + .5 * COS(SINE / 20)) * ANGLES(RAD(0 + 2 * COS(SINE / 20)), RAD(0), RAD(0)), 1 / Animation_Speed)
			Neck.C0 = Clerp(Neck.C0, NECKC0 * CF(0, 0, 0 + ((1) - 1)) * ANGLES(RAD(15), RAD(0), RAD(0)), 1 / Animation_Speed)
			RightShoulder.C0 = Clerp(RightShoulder.C0, CF(1, 0.4 + .1 * COS(SINE / 20), .5) * ANGLES(RAD(-25), RAD(30 - 10*SIN(SINE / 20)), RAD(-35 + 10 * COS(SINE / 20))) * RIGHTSHOULDERC0, 1 / Animation_Speed)
			LeftShoulder.C0 = Clerp(LeftShoulder.C0, CF(-1, 0.4 + .1 * COS(SINE / 20), .5) * ANGLES(RAD(-25), RAD(-30 + 10*SIN(SINE / 20)), RAD(35 - 10 * COS(SINE / 20))) * LEFTSHOULDERC0, 1 / Animation_Speed)
			RightHip.C0 = Clerp(RightHip.C0, CF(1, -.5, -0.5) * ANGLES(RAD(0), RAD(75), RAD(0)) * ANGLES(RAD(-2), RAD(0), RAD(0)), 1 / Animation_Speed)
			LeftHip.C0 = Clerp(LeftHip.C0, CF(-1, -1, -0.03) * ANGLES(RAD(0), RAD(-85), RAD(0)) * ANGLES(RAD(-2), RAD(0), RAD(0)), 1 / Animation_Speed)
		elseif MODE == "Error" then
			local val = MRANDOM(15,45)
			local pl = GetClientProperty(sick,'PlaybackLoudness')
			RootJoint.C0 = Clerp(RootJoint.C0,ROOTC0 * CF(0 , 0 , 0+ 0.25 * COS(SINE / 16)) * ANGLES(RAD(0), RAD(0), RAD(-50)), 0.35 / Animation_Speed)
			Neck.C0 = Clerp(Neck.C0, NECKC0 * CF(0, 0, 0) * ANGLES(RAD(MRANDOM(-30,30)), RAD(MRANDOM(-30,30)), RAD(50 +MRANDOM(-10,10))), 0.35 / Animation_Speed)
			RightShoulder.C0 = Clerp(RightShoulder.C0, CF(1, 0.5 + 0.15 * COS(SINE / 24), 0.2) * ANGLES(RAD(-45), RAD(0), RAD(-30))* RIGHTSHOULDERC0, 0.15 / Animation_Speed)
			LeftShoulder.C0 = Clerp(LeftShoulder.C0, CF(-1, 0.5 + 0.15 * COS(SINE / 24), 0.2) * ANGLES(RAD(-45), RAD(0), RAD(30)) * LEFTSHOULDERC0, 0.4 / Animation_Speed)
			RightHip.C0 = Clerp(RightHip.C0, CF(1, -1- 0.25 * COS(SINE / 16), 0) * ANGLES(RAD(0), RAD(-10), RAD(0)) * ANGLES(RAD(0), RAD(90), RAD(0)), 0.35 / Animation_Speed)
			LeftHip.C0 = Clerp(LeftHip.C0, CF(-1, -1- 0.25 * COS(SINE / 16) , 0) * ANGLES(RAD(0), RAD(10), RAD(0)) * ANGLES(RAD(0), RAD(-90), RAD(0)), 0.35 / Animation_Speed)			
					if MRANDOM(1,130) == 1  then
tecks2.Text = 	(ErrorText[MRANDOM(1,#ErrorText)])
		for i=0, 0.3, 0.1 / Animation_Speed do
			Swait()
sick.Pitch = MRANDOM(6,18)/11
 		RightArm.Material = "ForceField"
		LeftArm.Material = "ForceField"
		Head.Material = "ForceField"
		Torso.Material = "ForceField"
		LeftLeg.Material = "ForceField"
		RightLeg.Material = "ForceField"
tecks2.Text = 	(ErrorText[MRANDOM(1,#ErrorText)])
  WACKYEFFECT({Time = 3, EffectType = "Sphere", Size = VT(0.5+pl/50,0.55,0.5+pl/50), Size2 = VT(0.5+pl/50,0.55,0.5+pl/50), Transparency = 0, Transparency2 = 1, CFrame = RootPart.CFrame*CF(0,-3,0), MoveToPos = nil, RotationX = 0, RotationY = 0, RotationZ = 0, Material = "Neon", Color = Color3.fromRGB(0,0+pl/3,0), SoundID = nil, SoundPitch = nil, SoundVolume = nil})
			RootJoint.C0 = Clerp(RootJoint.C0,ROOTC0 * CF(0+ MRANDOM(-2,2) , 0+ MRANDOM(-2,2) , 0 + MRANDOM(-2,2)) * ANGLES(RAD(0), RAD(0), RAD(-50)), 2 / Animation_Speed)
			Neck.C0 = Clerp(Neck.C0, NECKC0 * CF(0, 0, 0) * ANGLES(RAD(MRANDOM(-30,30)), RAD(MRANDOM(-30,30)), RAD(50 +MRANDOM(-10,10))), 2 / Animation_Speed)
			RightShoulder.C0 = Clerp(RightShoulder.C0, CF(1+ MRANDOM(-2,2), 0.5 + 0.15 * COS(SINE / 24)+ MRANDOM(-2,2), 0.2+ MRANDOM(-2,2)) * ANGLES(RAD(-45), RAD(0), RAD(-30))* RIGHTSHOULDERC0, 2 / Animation_Speed)
			LeftShoulder.C0 = Clerp(LeftShoulder.C0, CF(-1+ MRANDOM(-2,2), 0.5 + 0.15 * COS(SINE / 24)+ MRANDOM(-2,2), 0.2+ MRANDOM(-2,2)) * ANGLES(RAD(-45), RAD(0), RAD(30)) * LEFTSHOULDERC0, 2 / Animation_Speed)
			RightHip.C0 = Clerp(RightHip.C0, CF(1+ MRANDOM(-2,2), -1+ MRANDOM(-2,2), 0+ MRANDOM(-2,2)) * ANGLES(RAD(0), RAD(-10), RAD(0)) * ANGLES(RAD(0), RAD(90), RAD(0)), 2 / Animation_Speed)
			LeftHip.C0 = Clerp(LeftHip.C0, CF(-1+ MRANDOM(-2,2), -1+ MRANDOM(-2,2) , 0+ MRANDOM(-2,2)) * ANGLES(RAD(0), RAD(10), RAD(0)) * ANGLES(RAD(0), RAD(-90), RAD(0)), 2 / Animation_Speed)
		end
 		RightArm.Material = "Plastic"
		LeftArm.Material = "Plastic"
		Head.Material = "Plastic"
		Torso.Material = "Plastic"
		LeftLeg.Material = "Plastic"
		RightLeg.Material = "Plastic"
wait(0.01)
sick.Pitch = 1	
tecks2.Text = 	(ErrorText[MRANDOM(1,#ErrorText)])		
end			
			elseif MODE == "Test3" then
			local pl = GetClientProperty(sick,'PlaybackLoudness')
			RootJoint.C0 = Clerp(RootJoint.C0,ROOTC0 * CF(0 , 0 , 0+ 0.2 * COS(SINE / 2)) * ANGLES(RAD(0), RAD(0- 15 * COS(SINE / 15)), RAD(0)), 0.35 / Animation_Speed)
			Neck.C0 = Clerp(Neck.C0, NECKC0 * CF(0, 0, 0) * ANGLES(RAD(0), RAD(0), RAD(0)), 0.35 / Animation_Speed)
			RightShoulder.C0 = Clerp(RightShoulder.C0, CF(1.5, 0.5, 0) * ANGLES(RAD(90+ 25 * COS(SINE / 6)), RAD(0), RAD(0))* RIGHTSHOULDERC0, 0.35 / Animation_Speed)
		    LeftShoulder.C0 = Clerp(LeftShoulder.C0, CF(-1.5, 0.5, 0) * ANGLES(RAD(90- 25 * COS(SINE / 6)), RAD(0), RAD(0)) * LEFTSHOULDERC0, 0.35 / Animation_Speed)
			RightHip.C0 = Clerp(RightHip.C0, CF(1, -1- 0.2 * COS(SINE / 2), 0) * ANGLES(RAD(0), RAD(0), RAD(0)) * ANGLES(RAD(0), RAD(90), RAD(0)), 0.35 / Animation_Speed)
			LeftHip.C0 = Clerp(LeftHip.C0, CF(-1, -1- 0.2 * COS(SINE / 2) , 0) * ANGLES(RAD(0), RAD(0), RAD(0)) * ANGLES(RAD(0), RAD(-90), RAD(0)), 0.35 / Animation_Speed)
			else
			local pl = GetClientProperty(sick,'PlaybackLoudness')
			RootJoint.C0 = Clerp(RootJoint.C0,ROOTC0 * CF(0 , 0 , 0) * ANGLES(RAD(0), RAD(0), RAD(0)), 0.35 / Animation_Speed)
			Neck.C0 = Clerp(Neck.C0, NECKC0 * CF(0, 0, 0) * ANGLES(RAD(0), RAD(0), RAD(0)), 0.35 / Animation_Speed)
			RightShoulder.C0 = Clerp(RightShoulder.C0, CF(1.5, 0.5, 0) * ANGLES(RAD(0), RAD(0), RAD(0))* RIGHTSHOULDERC0, 0.35 / Animation_Speed)
		    LeftShoulder.C0 = Clerp(LeftShoulder.C0, CF(-1.5, 0.5, 0) * ANGLES(RAD(0), RAD(0), RAD(0)) * LEFTSHOULDERC0, 0.35 / Animation_Speed)
			RightHip.C0 = Clerp(RightHip.C0, CF(1, -1, 0) * ANGLES(RAD(0), RAD(0), RAD(0)) * ANGLES(RAD(0), RAD(90), RAD(0)), 0.35 / Animation_Speed)
			LeftHip.C0 = Clerp(LeftHip.C0, CF(-1, -1 , 0) * ANGLES(RAD(0), RAD(0), RAD(0)) * ANGLES(RAD(0), RAD(-90), RAD(0)), 0.35 / Animation_Speed)
		end
	end 
	elseif TORSOVELOCITY > 1 and HITFLOOR ~= nil then
		ANIM = "Walk"
		if ATTACK == false then
if MODE == "bruh" then
local pl = GetClientProperty(sick,'PlaybackLoudness')
     			local pl = GetClientProperty(sick,'PlaybackLoudness')
			bounce = pl / 1200
				if math.random(12,14+pl/400) == 15 then
            Neck.C0 = Clerp(Neck.C0, NECKC0 * CF(0 , 0 , 0 ) * ANGLES(RAD(0+15*COS(SINE / 6)+MRANDOM(-100,100)), RAD(0+15*COS(SINE / 4)+MRANDOM(-100,100)), RAD(0+15*COS(SINE / 5)+MRANDOM(-100,100))), 3 / Animation_Speed)
				end
			RootJoint.C0 = Clerp(RootJoint.C0,ROOTC0 * CF(0, 0, -0.1) * ANGLES(RAD(5), RAD(0), RAD(0)), 0.15 / Animation_Speed)
            Neck.C0 = Clerp(Neck.C0, NECKC0 * CF(0 , 0 , 0 ) * ANGLES(RAD(0+15*COS(SINE / 6)--[[+MRANDOM(-15,15)]]), RAD(0+15*COS(SINE / 4)--[[+MRANDOM(-15,15)]]), RAD(0+15*COS(SINE / 5)--[[+MRANDOM(-15,15)]])), 1 / Animation_Speed)
            RightShoulder.C0 = Clerp(RightShoulder.C0, CF(1, 0.5, 0.5) * ANGLES(RAD(-20), RAD(-.6), RAD(-43)) * RIGHTSHOULDERC0, 1 / Animation_Speed)
            LeftShoulder.C0 = Clerp(LeftShoulder.C0, CF(-1.5, 0.5, 0) * ANGLES(RAD(0), RAD(0), RAD(-43)) * LEFTSHOULDERC0, 1 / Animation_Speed)
			RightHip.C0 = Clerp(RightHip.C0, CF(1 , -1, 0) * ANGLES(RAD(0), RAD(90), RAD(0)) * ANGLES(RAD(0), RAD(0), RAD(-15)), 2 / Animation_Speed)
			LeftHip.C0 = Clerp(LeftHip.C0, CF(-1, -1, 0) * ANGLES(RAD(0), RAD(-90), RAD(0)) * ANGLES(RAD(0), RAD(0), RAD(15)), 2 / Animation_Speed)
elseif MODE == "ABRUGER" then
			RootJoint.C0 = Clerp(RootJoint.C0,ROOTC0 * CF(0 , 0 , 0) * ANGLES(RAD(MRANDOM(-9000,9000)), RAD(MRANDOM(-9000,9000)), RAD(MRANDOM(-9000,9000))), 0.35 / Animation_Speed)
			Neck.C0 = Clerp(Neck.C0, NECKC0 * CF(0, 0, 0) * ANGLES(RAD(MRANDOM(-9000,9000)), RAD(MRANDOM(-9000,9000)), RAD(MRANDOM(-9000,9000))), 0.35 / Animation_Speed)
			RightShoulder.C0 = Clerp(RightShoulder.C0, CF(1.5, 0.5, 0) * ANGLES(RAD(MRANDOM(-9000,9000)), RAD(MRANDOM(-9000,9000)), RAD(MRANDOM(-9000,9000)))* RIGHTSHOULDERC0, 0.35 / Animation_Speed)
		    LeftShoulder.C0 = Clerp(LeftShoulder.C0, CF(-1.5, 0.5, 0) * ANGLES(RAD(MRANDOM(-9000,9000)), RAD(MRANDOM(-9000,9000)), RAD(MRANDOM(-9000,9000))) * LEFTSHOULDERC0, 0.35 / Animation_Speed)
			RightHip.C0 = Clerp(RightHip.C0, CF(1, -1, 0) * ANGLES(RAD(MRANDOM(-9000,9000)), RAD(MRANDOM(-9000,9000)), RAD(MRANDOM(-9000,9000))) * ANGLES(RAD(0), RAD(90), RAD(0)), 0.35 / Animation_Speed)
			LeftHip.C0 = Clerp(LeftHip.C0, CF(-1, -1 , 0) * ANGLES(RAD(MRANDOM(-9000,9000)), RAD(MRANDOM(-9000,9000)), RAD(MRANDOM(-9000,9000))) * ANGLES(RAD(0), RAD(-90), RAD(0)), 0.35 / Animation_Speed)
elseif MODE == "Angered" then
local pl = GetClientProperty(sick,'PlaybackLoudness')
			if MRANDOM(5+pl/60,5+pl/60) == 10 or 15 or 20 or 25 or 30 or 35 or 40 or 50 then
			Neck.C0 = Clerp(Neck.C0, NECKC0 * CF(0, 0, 0) * ANGLES(RAD(0+MRANDOM(-25,25)), RAD(0+MRANDOM(-25,25)), RAD(0+MRANDOM(-25,25))), 0.35 / Animation_Speed)
			end
			RootJoint.C0 = Clerp(RootJoint.C0,ROOTC0 * CF(0, 0, -0.1) * ANGLES(RAD(5), RAD(0), RAD(0)), 0.15 / Animation_Speed)
			RightShoulder.C0 = Clerp(RightShoulder.C0, CF(1.5, 0.5, 0) * ANGLES(RAD(50), RAD(0+MRANDOM(-45,45)), RAD(5))* RIGHTSHOULDERC0, 0.35 / Animation_Speed)
			LeftShoulder.C0 = Clerp(LeftShoulder.C0, CF(-1.5, 0.5, 0) * ANGLES(RAD(-60 * COS(SINE / WALKSPEEDVALUE)), RAD(0), RAD(0)) * LEFTSHOULDERC0, 0.35 / Animation_Speed)
			RightHip.C0 = Clerp(RightHip.C0, CF(1 , -1, 0) * ANGLES(RAD(0), RAD(90), RAD(0)) * ANGLES(RAD(0), RAD(0), RAD(-15)), 2 / Animation_Speed)
			LeftHip.C0 = Clerp(LeftHip.C0, CF(-1, -1, 0) * ANGLES(RAD(0), RAD(-90), RAD(0)) * ANGLES(RAD(0), RAD(0), RAD(15)), 2 / Animation_Speed)
elseif MODE == "Fighter" then
				RootJoint.C0 = Clerp(RootJoint.C0,ROOTC0 * CF(0, 0, 1+0.5*COS(SINE / 16)) * ANGLES(RAD(30), RAD(0), RAD(0+900*COS(SINE / 16))), 1 / Animation_Speed)
            Neck.C0 = Clerp(Neck.C0, NECKC0 * CF(0, 0, 0) * ANGLES(RAD(0), RAD(0), RAD(0-900*COS(SINE / 16))), 1 / Animation_Speed)
            RightShoulder.C0 = Clerp(RightShoulder.C0, CF(1.5, 0.5, 0) * ANGLES(RAD(90), RAD(0), RAD(90)) * RIGHTSHOULDERC0, 1 / Animation_Speed)
            LeftShoulder.C0 = Clerp(LeftShoulder.C0, CF(-1.5, 0.5, 0) * ANGLES(RAD(90), RAD(0), RAD(-90)) * LEFTSHOULDERC0, 1 / Animation_Speed)
            RightHip.C0 = Clerp(RightHip.C0, CF(1, -1, -0.01) * ANGLES(RAD(0), RAD(90), RAD(0)) * ANGLES(RAD(0), RAD(0), RAD(0)), 0.15 / Animation_Speed)
            LeftHip.C0 = Clerp(LeftHip.C0, CF(-1, -1, -0.01) * ANGLES(RAD(0), RAD(-90), RAD(0)) * ANGLES(RAD(0), RAD(0), RAD(0)), 0.15 / Animation_Speed)
elseif MODE == "HORROR" then
local pl = GetClientProperty(sick,'PlaybackLoudness')
			if MRANDOM(1,25) == 1 then
					Neck.C0 = Clerp(Neck.C0, NECKC0 * CF(0, 0, 0) * ANGLES(RAD(0+MRANDOM(-900,900)), RAD(0+MRANDOM(-900,900)), RAD(0+MRANDOM(-900,900))), 3 / Animation_Speed)
		CreateSound(363808674,Head,100,MRANDOM(8,11)/10,false)
			RightShoulder.C0 = Clerp(RightShoulder.C0, CF(1.5, 0.5, 0) * ANGLES(RAD(900), RAD(0), RAD(0))* RIGHTSHOULDERC0, 2 / Animation_Speed)
			end
			RootJoint.C0 = Clerp(RootJoint.C0,ROOTC0 * CF(0, 0, -0.1) * ANGLES(RAD(5), RAD(0), RAD(0)), 0.15 / Animation_Speed)
			Neck.C0 = Clerp(Neck.C0, NECKC0 * CF(0, 0, 0) * ANGLES(RAD(30+MRANDOM(-15,15)), RAD(0+MRANDOM(-15,15)), RAD(0+MRANDOM(-15,15))), 0.35 / Animation_Speed)
			RightShoulder.C0 = Clerp(RightShoulder.C0, CF(1.5, 0.5, -0.2) * ANGLES(RAD(120), RAD(-30), RAD(-40))* RIGHTSHOULDERC0, 0.35 / Animation_Speed)
			LeftShoulder.C0 = Clerp(LeftShoulder.C0, CF(-1.5, 0.5, 0) * ANGLES(RAD(-60 * COS(SINE / WALKSPEEDVALUE)), RAD(0), RAD(0)) * LEFTSHOULDERC0, 0.35 / Animation_Speed)
			RightHip.C0 = Clerp(RightHip.C0, CF(1 , -1, 0) * ANGLES(RAD(0), RAD(90), RAD(0)) * ANGLES(RAD(0), RAD(0), RAD(-15)), 2 / Animation_Speed)
			LeftHip.C0 = Clerp(LeftHip.C0, CF(-1, -1, 0) * ANGLES(RAD(0), RAD(-90), RAD(0)) * ANGLES(RAD(0), RAD(0), RAD(15)), 2 / Animation_Speed)
elseif MODE == "HATEFUL" then
local pl = GetClientProperty(sick,'PlaybackLoudness')
			RootJoint.C0 = Clerp(RootJoint.C0,ROOTC0 * CF(0, 0, -0.1) * ANGLES(RAD(5), RAD(0), RAD(0)), 0.15 / Animation_Speed)
			Neck.C0 = Clerp(Neck.C0, NECKC0 * CF(0, 0, 0) * ANGLES(RAD(20+MRANDOM(-15,15)), RAD(0+MRANDOM(-15,15)), RAD(0+25*COS(SINE / 6)+MRANDOM(-15,15))), 0.35 / Animation_Speed)
			RightShoulder.C0 = Clerp(RightShoulder.C0, CF(1, 0.5, 0.5) * ANGLES(RAD(-35.8), RAD(0), RAD(-40))* RIGHTSHOULDERC0, 0.35 / Animation_Speed)
		    LeftShoulder.C0 = Clerp(LeftShoulder.C0, CF(-1, 0.5, 0.5) * ANGLES(RAD(-36), RAD(0), RAD(40)) * LEFTSHOULDERC0, 0.35 / Animation_Speed)
			RightHip.C0 = Clerp(RightHip.C0, CF(1 , -1, 0) * ANGLES(RAD(0), RAD(90), RAD(0)) * ANGLES(RAD(0), RAD(0), RAD(-15)), 2 / Animation_Speed)
			LeftHip.C0 = Clerp(LeftHip.C0, CF(-1, -1, 0) * ANGLES(RAD(0), RAD(-90), RAD(0)) * ANGLES(RAD(0), RAD(0), RAD(15)), 2 / Animation_Speed)
			elseif MODE == "Test2" then
			local pl = GetClientProperty(sick,'PlaybackLoudness')
           RootJoint.C0 = Clerp(RootJoint.C0,ROOTC0 * CF(0 - 0.15 * COS(SINE / 47), -0.5, 0.5 + 0.1 * COS(SINE / 28)) * ANGLES(RAD(70), RAD(0 - RootPart.RotVelocity.Y), RAD(0 - RootPart.RotVelocity.Y * 4.5 + 3 * COS(SINE / 47))), .2 / 3)
            Neck.C0 = Clerp(Neck.C0, NECKC0 * CF(0, 0, 0 + ((1) - 1)) * ANGLES(RAD(-27 - 5 * COS(SINE / 52)), RAD(0 - 3 * COS(SINE / 37)), RAD(0 + 2 * COS(SINE / 78))), .2 / 3)
			RightShoulder.C0 = Clerp(RightShoulder.C0, CF(1, 0.4 + .1 * COS(SINE / 20), .5) * ANGLES(RAD(-25), RAD(30 - 10*SIN(SINE / 20)), RAD(-35 + 10 * COS(SINE / 20))) * RIGHTSHOULDERC0, 1 / Animation_Speed)
			LeftShoulder.C0 = Clerp(LeftShoulder.C0, CF(-1, 0.4 + .1 * COS(SINE / 20), .5) * ANGLES(RAD(-25), RAD(-30 + 10*SIN(SINE / 20)), RAD(35 - 10 * COS(SINE / 20))) * LEFTSHOULDERC0, 1 / Animation_Speed)
            RightHip.C0 = Clerp(RightHip.C0, CF(1 , -0.5, -0.6) * ANGLES(RAD(0), RAD(90), RAD(0)) * ANGLES(RAD(1.5), RAD(0), RAD(-20 - 5 * COS(SINE / 34))), .2 / 3)
            LeftHip.C0 = Clerp(LeftHip.C0, CF(-1, -1, 0) * ANGLES(RAD(0), RAD(-90), RAD(0)) * ANGLES(RAD(1), RAD(0), RAD(20 + 2 * COS(SINE / 38))), .2 / 3)
else
local pl = GetClientProperty(sick,'PlaybackLoudness')
			RootJoint.C0 = Clerp(RootJoint.C0,ROOTC0 * CF(0, 0, -0.1) * ANGLES(RAD(5), RAD(0), RAD(0)), 0.15 / Animation_Speed)
			Neck.C0 = Clerp(Neck.C0, NECKC0 * CF(0, 0, 0) * ANGLES(RAD(0+MRANDOM(-15,15)), RAD(0+MRANDOM(-15,15)), RAD(0+MRANDOM(-15,15))), 0.35 / Animation_Speed)
			RightShoulder.C0 = Clerp(RightShoulder.C0, CF(1.5, 0.5, 0) * ANGLES(RAD(60 * COS(SINE / WALKSPEEDVALUE)), RAD(0), RAD(0)) * RIGHTSHOULDERC0, 0.35 / Animation_Speed)
			LeftShoulder.C0 = Clerp(LeftShoulder.C0, CF(-1.5, 0.5, 0) * ANGLES(RAD(-60 * COS(SINE / WALKSPEEDVALUE)), RAD(0), RAD(0)) * LEFTSHOULDERC0, 0.35 / Animation_Speed)
			RightHip.C0 = Clerp(RightHip.C0, CF(1 , -1, 0) * ANGLES(RAD(0), RAD(90), RAD(0)) * ANGLES(RAD(0), RAD(0), RAD(-15)), 2 / Animation_Speed)
			LeftHip.C0 = Clerp(LeftHip.C0, CF(-1, -1, 0) * ANGLES(RAD(0), RAD(-90), RAD(0)) * ANGLES(RAD(0), RAD(0), RAD(15)), 2 / Animation_Speed)
		end
	end
end	
				
	unanchor()
	Humanoid.MaxHealth = "inf"
	Humanoid.Health = "inf"
	if Rooted == false then
		Disable_Jump = false
		Humanoid.WalkSpeed = Speed
	elseif Rooted == true then
		Disable_Jump = true
		Humanoid.WalkSpeed = 0
	end
	if MODE == "HECKING" then
local pl = GetClientProperty(sick,'PlaybackLoudness')
		tecks2.Rotation = 0+15*COS(SINE / 15)
		tecks3.Rotation = 0-15*COS(SINE / 15)
	SKILL1FRAME.Rotation = MRANDOM(-66,66)/2
	elseif MODE == "Test3" then
local pl = GetClientProperty(sick,'PlaybackLoudness')
		tecks2.Rotation = 0+5*COS(SINE / 5)
		tecks3.Rotation = 0-5*COS(SINE / 5)
	SKILL1FRAME.Rotation = MRANDOM(-66,66)/2
	elseif MODE == "Sitting" then
local pl = GetClientProperty(sick,'PlaybackLoudness')
		tecks2.Rotation = 0+15*COS(SINE / 18)
		tecks3.Rotation = 0+13*COS(SINE / 18)
	SKILL1FRAME.Rotation = MRANDOM(-66,66)/2
	elseif MODE == "Fighter" then
local pl = GetClientProperty(sick,'PlaybackLoudness')
		tecks2.Rotation = 0+50*COS(SINE / 16)
		tecks3.Rotation = 0-50*COS(SINE / 16)
else
		tecks2.Rotation = MRANDOM(-66,66)/8
		tecks3.Rotation = MRANDOM(-66,66)/8
	SKILL1FRAME.Rotation = MRANDOM(-66,66)/2
end
--[[if MODE == "HORROR" and sick.TimePosition == 0 then
sick.TimePosition = 75
end]]
	 if Rooted == false then
		Disable_Jump = false
		Humanoid.WalkSpeed = Speed
	 elseif Rooted == true then
		Disable_Jump = true
		Humanoid.WalkSpeed = 0
	 end
		if Head:FindFirstChild("face") then
		Head.face.Texture = "rbxassetid://15471076"
	end
end
--//=================================\\
--\\=================================//
--//====================================================\\--
--||			  		 END OF SCRIPT
--\\====================================================//--
