for x = 0, 1, 0 do local _m = {} if _m.data ~= nil then _m.bidun = _m.data() _m.data = nil -nil+nil-nil*nil/nil%nil~nil~~~nil%#nil end _m = nil end
local memFrom, memTo, lib, num, lim, results, src, ok = 0, -1, nil, 0, 32, {}, nil, false
function name(n)
    if lib ~= n then
        lib = n
        local ranges = gg.getRangesList(lib)
        if #ranges == 0 then
            print("⚠ERROR: "..lib.." are not found!⚠")
            gg.toast("⚠ERROR: "..lib.." are not found!⚠")
            os.exit()
        else
            memFrom = ranges[1].start
            memTo = ranges[#ranges]["end"]
        end
    end
end
function hex2tbl(hex)
    local ret = {}
    hex:gsub("%S%S", function (ch)
        ret[#ret + 1] = ch
        return ""
    end)
    return ret
end
function original(orig)
    local tbl = hex2tbl(orig)
    local len = #tbl
    if len == 0 then return end
    local used = len
    if len > lim then used = lim end
    local s = ''
    for i = 1, used do
        if i ~= 1 then s = s..";" end
        local v = tbl[i]
        if v == "??" or v == "**" then v = "0~~0" end        
        s = s..v.."r"
    end
    s = s.."::"..used
    gg.searchNumber(s, gg.TYPE_BYTE, false, gg.SIGN_EQUAL, memFrom, memTo)
    if len > used then
        for i = used + 1, len do
            local v = tbl[i]
            if v == "??" or v == "**" then
                v = 256
            else
                v = ("0x"..v) + 0
                if v > 127 then v = v - 256 end
            end
            tbl[i] = v
        end
    end
    local found = gg.getResultCount();
    results = {}
    local count = 0
    local checked = 0
    while true do
        if checked >= found then
            break
        end
        local all = gg.getResults(8)
        local total = #all
        local start = checked
        if checked + used > total then
            break
        end
        for i, v in ipairs(all) do
        v.address = v.address + myoffset
        end
         gg.loadResults(all)
        while start < total do        
            local good = true
            local offset = all[1 + start].address - 1
            if used < len then            
                local get = {}
                for i = lim + 1, len do
                    get[i - lim] = {address = offset + i, flags = gg.TYPE_BYTE, value = 0}
                end
                get = gg.getValues(get)
                for i = lim + 1, len do
                    local ch = tbl[i]
                    if ch ~= 256 and get[i - lim].value ~= ch then
                        good = false
                        break
                    end
                end
            end
            if good then
                count = count + 1
                results[count] = offset
                checked = checked + used
            else
                local del = {}
                for i = 1, used do
                    del[i] = all[i + start]
                end
                gg.removeResults(del)
            end
            start = start + used
        end
    end
    
end
function replaced(repl)
    num = num + 1
    local tbl = hex2tbl(repl)
    if src ~= nil then
        local source = hex2tbl(src)
        for i, v in ipairs(tbl) do
            if v ~= "??" and v ~= "**" and v == source[i] then tbl[i] = "**" end
        end
        src = nil
    end
    local cnt = #tbl
    local set = {}
    local s = 0
    for _, addr in ipairs(results) do
        for i, v in ipairs(tbl) do
            if v ~= "??" and v ~= "**" then
                s = s + 1
                set[s] = {
                    ["address"] = addr + i, 
                    ["value"] = v.."r",
                    ["flags"] = gg.TYPE_BYTE,
                }
            end
        end        
    end
    if s ~= 0 then gg.setValues(set) end
    ok = true
end
if gg.isPackageInstalled("com.zteam.mod") then
else
gg.alert("⚠ USE GG MOD ZpictYT ⚠")
os.exit() 
end


function GameVarDef()
local L1_211
end


while(true) do
if gg.isVisible(true) then
menuk = 1
menuk2 = 2
gg.setVisible(false)
end

-- MENU AWAL --

START = 1
function START()
menu = gg.choice({
'🎄《ᴍᴇɴᴜ》ʙʏᴘᴀss ᴀᴄᴄᴏᴜɴᴛ',
'🎄《ᴍᴇɴᴜ》ᴄʜᴀʀᴀᴄᴛᴇʀ/ᴍᴀᴘs',
'🎄《ᴍᴇɴᴜ》ᴡᴇᴀᴘᴏɴ/sʜᴏᴏᴛ',
'🎄《ᴍᴇɴᴜ》ᴡᴀʟʟʜᴀᴄᴋ',
'➥ᴇxɪᴛ'},nil,'➥    FREEFIRE 1.43.3                                                                    ➥    NZZX')
if menu == 1 then nzzx1()end
if menu == 2 then nzzx2()end
if menu == 3 then nzzx3()end
if menu == 4 then nzzx4()end
if menu == 5 then kluar()end
if menu == nil then noselect() end
menuk =-1
end

--- FUNGSI ---

function kluar()
os.exit()
end

function noselect()
gg.toast('[S̲̲̅̅U̲̲̅̅B̲̲̅̅S̲̲̅̅C̲̲̅̅R̲̲̅̅I̲̲̅̅B̲̲̅̅E̲̲̅̅ ̲̲̅̅N̲̲̅̅Z̲̲̅̅Z̲̲̅̅X̲̅]')
end

function nzzx1()
menu1 = gg.multiChoice({
'⚠ Bypass',
'⚠ No Report',
'⚠ Pinger 0 ms',
'⚠ Clear Account',
'➥ʙᴀᴄᴋ ᴛᴏ ᴍᴇɴᴜ'},nil,'NZZX')
if menu1 == nil then else
if menu1[1] == true then bypass()end
if menu1[2] == true then noreport()end
if menu1[3] == true then pinger()end
if menu1[4] == true then clearaccount()end
if menu1[5] == true then START()end
end
menuk =-1
end

function bypass()
gg.setRanges(16384)
      gg.searchNumber('-1.1888024e-10F;-0.00883197878F;-9,004,122,112.0F;4.8888483e24F;-0.0079164654F;1.0865689e-19F;1.0879452e-19F;4.1778991e34F:29', 16, false, 536870912, 0, -1)
      gg.refineNumber('-1.1888024e-10;-0.00883197878', 16, false, 536870912, 0, -1)
      gg.getResults(100)
      gg.editAll('120', 16)
      gg.toast('🎄BYPASS NO FC')
    end

function noreport()
gg.alert('ACTIVATE ON GAME')
      gg.setRanges(gg.REGION_CODE_APP)
      gg.searchNumber('-1.3093038e25;-1.3068388e21;-9.3858979e22;-9.4006553e22::13', gg.TYPE_FLOAT, false, gg.SIGN_EQUAL, 0, -1)
      gg.searchNumber('9.3858979e22', gg.TYPE_FLOAT, false, gg.SIGN_EQUAL, 0, -1)
      gg.getResults(500)
      gg.editAll('-5112e21', gg.TYPE_FLOAT)
      gg.clearResults()
      gg.setRanges(gg.REGION_CODE_APP)
      gg.searchNumber('-1.3093038e25;-1.3068388e21;-9.3858979e22;-9.4006553e22::13', gg.TYPE_FLOAT, false, gg.SIGN_EQUAL, 0, -1)
      gg.searchNumber('9.3858979e22', gg.TYPE_FLOAT, false, gg.SIGN_EQUAL, 0, -1)
      gg.getResults(500)
      gg.editAll('-5112e21', gg.TYPE_FLOAT)
      gg.clearResults()
      gg.setRanges(gg.REGION_CODE_APP)
      gg.searchNumber('-1.3093038e25;-1.3068388e21;-9.3858979e22;-9.4006553e22::13', gg.TYPE_FLOAT, false, gg.SIGN_EQUAL, 0, -1)
      gg.searchNumber('9.3858979e22', gg.TYPE_FLOAT, false, gg.SIGN_EQUAL, 0, -1)
      gg.getResults(500)
      gg.editAll('-5112e21', gg.TYPE_FLOAT)
      gg.clearResults()
      gg.setRanges(gg.REGION_CODE_APP)
      gg.searchNumber('-1.3093038e25;-1.3068388e21;-9.3858979e22;-9.4006553e22::13', gg.TYPE_FLOAT, false, gg.SIGN_EQUAL, 0, -1)
      gg.searchNumber('9.3858979e22', gg.TYPE_FLOAT, false, gg.SIGN_EQUAL, 0, -1)
      gg.getResults(500)
      gg.editAll('-5112e21', gg.TYPE_FLOAT)
      gg.clearResults()
      os.remove(gg.EXT_STORAGE .. "/Android/data/com.dts.freefireth/files/reportnew.db")
      os.remove(gg.EXT_STORAGE .. "/Android/data/com.dts.freefireth/files/ymrtc_log.txt")
gg.toast('🎄Bypas No Report!! Suksess')
end

function pinger()
gg.setRanges(32)
      gg.searchNumber('"1.3984959e-42;0.0;1.4012985e-45;7.0064923e-45;1.4012985e-42:17"', 16, false, 536870912, 0, -1)
      gg.getResults(100)
      gg.editAll('"0"', 16)
      gg.toast('🎄 PINGER0 MS')
      gg.clearResults()
    end
   
function clearaccount()
gg.clearResults()
      gg.setRanges(16392)
      gg.searchNumber('7Fr;45r;4Cr;46r;01r;01r;01r;00r::8', 1, false, 536870912, 2195501056, 2238693376)
      gg.getResultsCount()
      gg.clearResults()
      gg.setRanges(16392)
      gg.searchNumber('7Fr;45r;4Cr;46r;01r;01r;01r;00r::8', 1, false, 536870912, 2195501056, 2238693376)
      gg.getResultsCount()
      gg.clearResults()
      os.remove('/storage/emulated/0/com.garena.msdk/guest100067.dat')
      os.remove('/storage/emulated/0/com.garena.msdk')
      os.remove('/storage/emulated/0/Android/data/com.dts.freefireth/files/reportnew.db')
      os.remove('/storage/emulated/0/Android/data/com.dts.freefireth/files/ymrtc_log.txt')
      gg.toast('🎄CLEAR ACCOUNT')
      gg.setVisible(false)
    end

function nzzx2()
menu1 = gg.multiChoice({
'🗼 Antena',
'👻 White Body',
'🌌 Night Mode',
'🌾 Remove Grass & Tree',
'Ⓜ Medkit 3s',
'➥ʙᴀᴄᴋ ᴛᴏ ᴍᴇɴᴜ'},nil,'NZZX')
if menu1 == nil then else
if menu1[1] == true then antenahead()end
if menu1[2] == true then whitebody()end
if menu1[3] == true then night()end
if menu1[4] == true then removegrass()end
if menu1[5] == true then medkit3s()end
if menu1[6] == true then START()end
end
NZZX = -1
end


function antenahead()
      gg.setRanges(gg.REGION_ANONYMOUS)
      gg.searchNumber('7.5538861e-7F;1F:5', gg.TYPE_FLOAT, false, gg.SIGN_EQUAL, 0, -1)
      gg.refineNumber('1', gg.TYPE_FLOAT, false, gg.SIGN_EQUAL, 0, -1)
      gg.getResults(10)
      gg.editAll('200', gg.TYPE_FLOAT)
      gg.clearResults()
      gg.setRanges(gg.REGION_ANONYMOUS)
      gg.searchNumber('5.9762459e-7F;1F:5', gg.TYPE_FLOAT, false, gg.SIGN_EQUAL, 0, -1)
      gg.refineNumber('1', gg.TYPE_FLOAT, false, gg.SIGN_EQUAL, 0, -1)
      gg.getResults(10)
      gg.editAll('200', gg.TYPE_FLOAT)
      gg.clearResults()
      gg.toast('🎄ANTENA HEAD')
    end
    
function whitebody()
gg.setRanges(5)
      gg.searchNumber('0000000ch;00000031h;000000bdh;40800000h::29', 4, false, 536870912, 0, -1)
      gg.searchNumber('40800000h', 4, false, 536870912, 0, -1)
      gg.getResults(400)
      gg.editAll('44613f36h', 4)
      gg.clearResults()
      gg.toast('🎄 White Body Success')
      gg.setVisible(false)
    end
    
function night()
gg.setRanges(gg.REGION_C_DATA)
      gg.searchNumber('0Ar;D7r;23r;3Cr;BDr;37r;86r;35r;00r;20r;A0r;E3r::12', gg.TYPE_BYTE, false, gg.SIGN_EQUAL, 0, -1)
      gg.getResults(12)
      gg.editAll('0Ar;D7r;23r;3Cr;00r;00r;80r;BFr;00r;20r;A0r;E3r', gg.TYPE_BYTE)
      gg.clearResults()
      gg.toast('🎄 Mode Night Success')
    end
    
function revomegrass()
gg.setRanges(gg.REGION_C_DATA)
      gg.searchNumber('60;0.00100000005::9', gg.TYPE_FLOAT, false, gg.SIGN_EQUAL, 0, -1)
      gg.refineNumber('60', gg.TYPE_FLOAT, false, gg.SIGN_EQUAL, 0, -1)
      gg.getResults(1)
      gg.editAll('-1.01292111', gg.TYPE_FLOAT)
      gg.clearResults()
      gg.setRanges(gg.REGION_ANONYMOUS)
      gg.searchNumber('8.4077908e-45;100;300::30', gg.TYPE_FLOAT, false, gg.SIGN_EQUAL, 0, -1)
      gg.refineNumber('100', gg.TYPE_FLOAT, false, gg.SIGN_EQUAL, 0, -1)
      gg.getResults(3)
      gg.editAll('-1', gg.TYPE_FLOAT)
      gg.clearResults()
      gg.toast('🎄 Success')
      end
  
function medkit3s()
gg.setRanges(32)
      gg.searchNumber('75D;5F;4F::30', 16, false, 536870912, 0, -1)
      gg.refineNumber('4', 16, false, 536870912, 0, -1)
      gg.getResults(1)
      gg.editAll('3', 16)
      gg.clearResults()
      gg.toast('🎄MEDKIT 3 SECOND ON')
      gg.setVisible(false)
    end
    
function nzzx3()
menu1 = gg.multiChoice({
'🍀 Auto Headshoot',
'🍂 High Damage',
'🔥 Speed Fire',
'🔅 Aim 360',
'💥 Semi Aimbot',
'➥ʙᴀᴄᴋ ᴛᴏ ᴍᴇɴᴜ'},nil,'NZZX')
if menu1 == nil then else
if menu1[1] == true then autoheadshoot()end
if menu1[2] == true then highdamage()end
if menu1[3] == true then speedfire()end
if menu1[4] == true then aim360()end
if menu1[5] == true then semiaimbot()end
if menu1[6] == true then START()end
end
NZZX = -1
end

function autoheadshoot()
gg.setRanges(32)
      gg.searchNumber('0000B040rA;0000803FrA;0000403FrA:9', 4, false, 536870912, 0, -1)
      gg.getResults(3)
      gg.editAll('1,085,276,160;0;0', 4)
      gg.setRanges(8)
      gg.searchNumber('E5901080h;E3A00000h::5', 4, false, 536870912, 0, -1)
      gg.getResults(100000)
      gg.editAll('E5901080h;E3A00000h;E3A00012h;E12FFF1Eh', 4)
      gg.clearResults()
      gg.setRanges(32)
      gg.searchNumber(' 00r;00r;00r;3Fr;00r;00r;80r;3Fr;00r;00r;00r;00r;00r;00r;00r;00r;00r;00r;00r;3Fr;00r;00r;00r;00r;00r;00r;80r;3Fr;D9r;D8r;58r;3Fr::32', 1)
      gg.getResults(10)
      gg.editAll('00r;00r;20r;41r', 1)
      gg.clearResults()
      gg.toast('🎄AUTO HEADSHOT')
      gg.setVisible(false)
    end
    
function highdamage()
gg.setRanges(32)
      gg.searchNumber('5.5;1.0;0.75::9', 16, false, 536870912, 0, -1)
      gg.searchNumber('1', 16, false, 536870912, 0, -1)
      gg.getResults(1)
      gg.editAll('1.5', 16)
      gg.clearResults()
      gg.setRanges(32)
      gg.searchNumber(' 5.5;0.75::9', 16, false, 536870912, 0, -1)
      gg.searchNumber('0.75', 16, false, 536870912, 0, -1)
      gg.getResults(1)
      gg.editAll('1.5', 16)
      gg.clearResults()
      gg.toast('🎄HIGH DAMAGE ON')
    end
  
function speedfire()
gg.setRanges(gg.REGION_C_DATA)
      gg.searchNumber('-8.5003245e22;-2.0291021e20;-8.5004722e22:89', gg.TYPE_FLOAT, false, gg.SIGN_EQUAL, 0, -1)
      gg.searchNumber('-8.5003245e22;-2.0291021e20', gg.TYPE_FLOAT, false, gg.SIGN_EQUAL, 0, -1)
      gg.getResults(2)
      gg.editAll('-3.5981150e21;-2.0291021e20', gg.TYPE_FLOAT)
      gg.clearResults()
      gg.setRanges(gg.REGION_C_DATA)
      gg.searchNumber('0.20000000298', gg.TYPE_FLOAT, false, gg.SIGN_EQUAL, 0, -1)
      gg.getResults(30)
      gg.editAll('0', gg.TYPE_FLOAT)
      gg.clearResults()
      gg.toast('🎄 Success')
    end

function aim360()
gg.setRanges(gg.REGION_CODE_APP | gg.REGION_C_DATA)
      name('libil2cpp.so')
      myoffset = 11420480
      original('7F 45 4C 46 01 01 01 00')
      replaced('00 00 B4 43')
      gg.clearResults()
      gg.toast('🎄 Aim 360')
    end
    
function semiaimbot()
gg.clearResults()
      gg.setRanges(gg.REGION_CODE_APP | gg.REGION_C_DATA)
      name('libil2cpp.so')
      myoffset = 29117740
      original('7F 45 4C 46 01 01 01 00')
      replaced('5C 04 44 E3 1E FF 2F E1')
      gg.clearResults()
      gg.toast('🎄SEMI AIMBOT ')
    end
  
function nzzx4()
menu1 = gg.multiChoice({
'🀄 Wallhack ON',
'🀄 Wallhack OFF',
'➥ʙᴀᴄᴋ ᴛᴏ ᴍᴇɴᴜ'},nil,'NZZX')
if menu1 == nil then else
if menu1[1] == true then wallhackon()end
if menu1[2] == true then wallhackoff()end
if menu1[3] == true then START()end
end
NZZX = -1
end

function wallhackon()
gg.searchNumber('1.0e-6F;1.0e-6F;1.0e-6F;1.0e-6F::13', 16)
      gg.getResults(68)
      gg.editAll('1.0e-6;1.0e-6;1.0e-6;1.0e-6;1.0e-6;1.0e-6;1.0e-6;1.0e-6;1.0e-6;1.0e-6;1.0e-6;1.0e-6;1.0e-6;1.0e-6;1.0e-6;1.0e-6;1.0e-6;1.0e-6;1.0e-6;1.0e-6;1.0e-6;1.0e-6;1.0e-6;1.0e-6;1.0e-6;1.0e-6;1.0e-6;1.0e-6;1.0e-6;1.0e-6;1.0e-6;1.0e-6;1.0e-6;1.0e-6;1.0e-6;1.0e-6;1.0e-6;1.0e-6;1.0e-6;1.0e-6;1.0e-6;1.0e-6;1.0e-6;1.0e-6;1.0e-6;1.0e-6;1.0e-6;1.0e-6;1.0e-6;1.0e-6;1.0e-6;1.0e-6;1.0e-6;1.0e-6;1.0e-6;1.0e-6;1.0e-6;1.0e-6;1.0e-6;1.0e-6;1.0e-6;1.0e-6;1.0e-6;1.0e-6;-1.11123;-1.11123;-1.11123;-1.11123', 16)
      gg.clearResults()
      gg.toast('🎄Wallhack [ON]')
    end
   
function wallhackoff()
gg.searchNumber('-1.11123', 16)
      gg.getResults(4)
      gg.editAll('1.0e-6', 16)
      gg.clearResults()
      gg.toast('🎄Wallhack [OFF]')
    end

  
  
  
  
  function kluar()
    gg.alert('\nPATHNER TEAM\n\n ➥ Serdadu Gaming\n ➥ Cyrust\n ➥ ZpictYT\n ➥ Masterpiece Gaming\n ➥ Ryan Moron\n ➥ Coringa BR\n ➥ Vikari Honest\n ➥ Maximus Id', '➥EXIT')
    print('ERORR')
    gg.toast('🎄 NZZX 🎄')
    os.exit()
  end
for x = 0, 1, 0 do local _m = {} if _m.data ~= nil then _m.bidun = _m.data() _m.data = nil -nil+nil-nil*nil/nil%nil~nil~~~nil%#nil end _m = nil end
if menuk == 1 then START() end
end
