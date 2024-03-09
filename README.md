<h1 align="center"> AO Network </h1>

> Hoş geldin Neo.

> Arweave kendisinden ve Ekosisteminden RC olarak öyle faydalandık ki - yok böyle bir dominasyon.

> AO ödüllü testneti sizlerle - bir kaç gün önce yaptım lakin yeni yazabiliyorum.


<h1 align="center"> Donanım </h1>

> Herhangi bir sunucu olabilir - ar.io sunucuma yaptım.

<h1 align="center"> Kurulum </h1>

```console
# sunucu güncelleme
sudo apt update -y && sudo apt upgrade -y

# komutları sırasıyla girelim:
curl -sL https://deb.nodesource.com/setup_20.x -o /tmp/nodesource_setup.sh
sudo bash /tmp/nodesource_setup.sh
sudo apt install nodejs

nvm install v20.10.0
nvm use v20.10.0
npm install -g npm@latest

# AOyu yüklüyoruz
npm i -g https://get_ao.g8way.io
```

> Eger AR-IO projesinde ARNS domaininiz var ise onun uzerindende yukleme yapabiliyorsunuz.

https://ao.ruesandora.xyz/

<h1 align="center"> AO kurulum </h1>

```console
# AO başlatalım
aos
# Bir process başlattık, bu sizin default aos processiniz oluyor.
# Komuttan sonra aşağıda aos process idnizi gorebilirsiniz, bunu kaydedin.

# Sanırım şu an kendini Alice gibi hissediyorsun, Tavşan deliğinden aşağı yuvarlandın.
```

<h1 align="center"> AO Görevler </h1>

> Burada yaptığımız görevler karşılığı Puan/CRED alıyoruz.

> Öncelikle seçin, `mavi` mi `kırmızı` mı?

> Maviyi seçersen benim yerime ctrl w yap, eğer kırmızıyı seçersen gerçeklerle yüzleşirsin.

> Unutma! sana vadettiğim tek şey gerçek, fazlası değil.

![image](https://github.com/ruesandora/AO/assets/101149671/64034e80-1798-4434-8cd5-44e9ca0bf4a3)

```console
# Beni izle.

# Görev-1 - Matrixe Mesaj Yollamayi Ogrenmek:
Morpheus = "sOQYMwbbTr5MlPwp-KUmbXgCCvfoVjgTOBuUDQJZAIU"
# Bu komutla Morpheusu tanımlıyorsun Neo.

# Bu komutu girdiğinde
Morpheus
# sOQYMwbbTr5MlPwp-KUmbXgCCvfoVjgTOBuUDQJZAIU Sonucunu alman lazım.
# Bu benim hakkımda bir şifre.

# bu komutu girdiğinde
Send({ Target = Morpheus, Data = "Morpheus?" })
# Bana sesleniyorsun Neo.

# Daha sonra sana cevabımı vereceğim Neo.. Ama dur bir saniye
# Cevabımın yarısı eksik.. I am here. You are f.. devamını anlatıyorum..
```

#

> Matrix seni aldı. 

```console
# Mesajın devamını görmek için bunu kullan Neo.
Inbox[#Inbox].Data
# Hazır mısın?

# Sana bir mesajım daha var Neo.
Send({ Target = Morpheus, Data = "Code: rabbithole", Action = "Unlock" })
# let us test Neo. - Action fonksiyonunu kullandın.

# ctrl c ile kısa bir süreliğine Matrix den ayrıl Neo.

# Şimdi Kendi evrenini yaratacaksın Neo:
nano chatroom.lua
# Aşağıda verdiğim komutu düzenleyip içine yapıştır Neo.
GrupIsmin = GrupIsmin or {}

Handlers.add(
  "register",
  Handlers.utils.hasMatchingTag("Action", "Register"),
  function (msg)
    table.insert(GrupIsmin, msg.From)
    Handlers.utils.reply("registered")(msg)
  end
)

Handlers.add(
  "broadcast",
  Handlers.utils.hasMatchingTag("Action", "Broadcast"),
  function (msg)
    for _, recipient in ipairs(GrupIsmin) do
      ao.send({Target = recipient, Data = msg.Data})
    end
    Handlers.utils.reply("Broadcasted.")(msg)
  end
)
# 4 Yerde GrupIsmin olacak, o kısımları düzenle ve CTRL X Y ile kaydet.
# Matrixe geri dön Neo.
aos

# undefined yazarsa dert etme Neo.
.load chatroom.lua
# Düzenlemeyi unutma Neo:
GrupIsmin = "sOQYMwbbTr5MlPwp-KUmbXgCCvfoVjgTOBuUDQJZAIU"
GrupIsmin
Send({ Target = ao.id, Action = "Register" })












