# chatroom.lua hazırlık.

> Oncelikle Visual Studio Code' indiriyoruz.

> Kurulum yaptiktan sonra ana sayfada Sol taraftan eklentilere (extension) tikliyoruz.

![image](https://github.com/ruesandora/AO/assets/101149671/126f07c3-c549-4c31-8c06-b3279c8e8ee3)

> Ardindan arama kismina SSH yazarak Microsoft'un eklentisini indiriyoruz. (Mac de olur)

![image](https://github.com/ruesandora/AO/assets/101149671/b786c7ca-4003-43dd-8457-806eb3c8e237)

> Eklentimiz yuklendikten sonra en altta sol tarafta >< isaretine tikliyoruz.

![image](https://github.com/ruesandora/AO/assets/101149671/6b1e6848-2da9-44ca-b36c-4ad019a73454)

> Connect to Host'a tıklıyoruz.

![image](https://github.com/ruesandora/AO/assets/101149671/d85744f2-4c1b-4b85-a60c-3cd0dac61f67)

> + Add New SSH Host'a

![image](https://github.com/ruesandora/AO/assets/101149671/2ad00eee-a91e-4ada-81d8-746df7473a29)

> IP'mizi girip Enterliyoruz.

> Ardindan en ustteki seçeneğe tıklıyoruz.

> Sag alttaki cikan bildirimden Open config'e tikliyoruz.

![image](https://github.com/ruesandora/AO/assets/101149671/5330cedb-dbbd-4fb4-a441-0fe06b02ce67)

> Host ve Hostname zaten yazili olarak gelecek. CTRL S YAPALIM - Altina gorseldeki gibi - User root yaziyoruz.

![image](https://github.com/ruesandora/AO/assets/101149671/a35ef4a0-1ee5-4bab-90b4-14b8bf9ffc6e)

> Ardindan tekrardan sol alttaki >< ya tiklayip Connect to Host diyoruz.

> Ipmizi secip sifremizi giriyoruz.

#

> Sol taraftan ilk icona tikliyoruz ve Open Folder secenegine tikliyoruz.

![image](https://github.com/ruesandora/AO/assets/101149671/e102c139-b278-4db0-a6fd-5bdf1a77b71e)

> OK diyoruz

![image](https://github.com/ruesandora/AO/assets/101149671/bd6981ab-bcc9-43e5-bc9d-a630ba14f4f3)


> Extension'lara tekrar tiklayip Lua yazip aratip yukluyoruz ve ardindan enable ediyoruz.

![image](https://github.com/ruesandora/AO/assets/101149671/54d1caba-73e8-48c6-9cf0-f05a4f4cfaa7)

> CTRL+ SHIFT +P yapiyoruz.

> Lua: Open Addon Manager... indiriyoruz

![image](https://github.com/ruesandora/AO/assets/101149671/63cbae39-9575-449f-a040-c86e25b05e31)

> Cikan ekrandan AO'yu enable ediyoruz

> Sol taraftan `chatroom.lua` ve `token.lua` adında 2 yeni dosya açıyoruz.

* chatroom.lua dosyasına girelim:
* Rues yazan 4 kısım var kendi chat room adınızı girin oraya
* CTRL S ile dosyayı keydedin.

```console
Rues = Rues or {}

Handlers.add(
  "register",
  Handlers.utils.hasMatchingTag("Action", "Register"),
  function (msg)
    table.insert(Rues, msg.From)
    Handlers.utils.reply("registered")(msg)
  end
)

Handlers.add(
  "broadcast",
  Handlers.utils.hasMatchingTag("Action", "Broadcast"),
  function (msg)
    for _, recipient in ipairs(Rues) do
      ao.send({Target = recipient, Data = msg.Data})
    end
    Handlers.utils.reply("Broadcasted.")(msg)
  end
)
```

* token.lua dosyasına girelim
* 4 Yerde Rues yazıyor orayı değiştirin - Ortada If ile başlayan 2 kod bloğu.
* CTRL S ile kaydedin.

```console
local bint = require('.bint')(256)
local ao = require('ao')
--[[
  This module implements the ao Standard Token Specification.

  Terms:
    Sender: the wallet or Process that sent the Message

  It will first initialize the internal state, and then attach handlers,
    according to the ao Standard Token Spec API:

    - Info(): return the token parameters, like Name, Ticker, Logo, and Denomination

    - Balance(Target?: string): return the token balance of the Target. If Target is not provided, the Sender
        is assumed to be the Target

    - Balances(): return the token balance of all participants

    - Transfer(Target: string, Quantity: number): if the Sender has a sufficient balance, send the specified Quantity
        to the Target. It will also issue a Credit-Notice to the Target and a Debit-Notice to the Sender

    - Mint(Quantity: number): if the Sender matches the Process Owner, then mint the desired Quantity of tokens, adding
        them the Processes' balance
]]
--
local json = require('json')

--[[
     Initialize State

     ao.id is equal to the Process.Id
   ]]
--
if not Balances then Balances = { [ao.id] = tostring(bint(10000 * 1e12)) } end

if Name ~= 'Rues Coin' then Name = 'Rues Coin' end

if Ticker ~= 'Rues' then Ticker = 'RUES' end

if Denomination ~= 12 then Denomination = 12 end

if not Logo then Logo = 'SBCCXwwecBlDqRLUjb8dYABExTJXLieawf7m2aBJ-KY' end

--[[
     Add handlers for each incoming Action defined by the ao Standard Token Specification
   ]]
--

--[[
     Info
   ]]
--
Handlers.add('info', Handlers.utils.hasMatchingTag('Action', 'Info'), function(msg)
  ao.send({
    Target = msg.From,
    Name = Name,
    Ticker = Ticker,
    Logo = Logo,
    Denomination = tostring(Denomination)
  })
end)

--[[
     Balance
   ]]
--
Handlers.add('balance', Handlers.utils.hasMatchingTag('Action', 'Balance'), function(msg)
  local bal = '0'

  -- If not Target is provided, then return the Senders balance
  if (msg.Tags.Target and Balances[msg.Tags.Target]) then
    bal = Balances[msg.Tags.Target]
  elseif Balances[msg.From] then
    bal = Balances[msg.From]
  end

  ao.send({
    Target = msg.From,
    Balance = bal,
    Ticker = Ticker,
    Account = msg.Tags.Target or msg.From,
    Data = bal
  })
end)

--[[
     Balances
   ]]
--
Handlers.add('balances', Handlers.utils.hasMatchingTag('Action', 'Balances'),
  function(msg) ao.send({ Target = msg.From, Data = json.encode(Balances) }) end)

--[[
     Transfer
   ]]
--
Handlers.add('transfer', Handlers.utils.hasMatchingTag('Action', 'Transfer'), function(msg)
  assert(type(msg.Recipient) == 'string', 'Recipient is required!')
  assert(type(msg.Quantity) == 'string', 'Quantity is required!')
  assert(bint.__lt(0, bint(msg.Quantity)), 'Quantity must be greater than 0')

  if not Balances[msg.From] then Balances[msg.From] = "0" end
  if not Balances[msg.Recipient] then Balances[msg.Recipient] = "0" end

  local qty = bint(msg.Quantity)
  local balance = bint(Balances[msg.From])
  if bint.__le(qty, balance) then
    Balances[msg.From] = tostring(bint.__sub(balance, qty))
    Balances[msg.Recipient] = tostring(bint.__add(Balances[msg.Recipient], qty))

    --[[
         Only send the notifications to the Sender and Recipient
         if the Cast tag is not set on the Transfer message
       ]]
    --
    if not msg.Cast then
      -- Send Debit-Notice to the Sender
      ao.send({
        Target = msg.From,
        Action = 'Debit-Notice',
        Recipient = msg.Recipient,
        Quantity = tostring(qty),
        Data = Colors.gray .. "You transferred " .. Colors.blue .. msg.Quantity .. Colors.gray .. " to " .. Colors.green .. msg.Recipient .. Colors.reset
      })
      -- Send Credit-Notice to the Recipient
      ao.send({
        Target = msg.Recipient,
        Action = 'Credit-Notice',
        Sender = msg.From,
        Quantity = tostring(qty),
        Data = Colors.gray .. "You received " .. Colors.blue .. msg.Quantity .. Colors.gray .. " from " .. Colors.green .. msg.Recipient .. Colors.reset
      })
    end
  else
    ao.send({
      Target = msg.From,
      Action = 'Transfer-Error',
      ['Message-Id'] = msg.Id,
      Error = 'Insufficient Balance!'
    })
  end
end)

--[[
    Mint
   ]]
--
Handlers.add('mint', Handlers.utils.hasMatchingTag('Action', 'Mint'), function (msg)
  assert(type(msg.Quantity) == 'string', 'Quantity is required!')
  assert(bint.__lt(0, msg.Quantity), 'Quantity must be greater than zero!')

  if not Balances[ao.id] then Balances[ao.id] = "0" end

  if msg.From == ao.id then
    -- Add tokens to the token pool, according to Quantity
    Balances[msg.From] = tostring(bint.__add(Balances[Owner], msg.Quantity))
    ao.send({
      Target = msg.From,
      Data = Colors.gray .. "Successfully minted " .. Colors.blue .. msg.Quantity .. Colors.reset
    })
  else
    ao.send({
      Target = msg.From,
      Action = 'Mint-Error',
      ['Message-Id'] = msg.Id,
      Error = 'Only the Process Owner can mint new ' .. Ticker .. ' tokens!'
    })
  end
end)
```

> Matrix'e dön Neo.





