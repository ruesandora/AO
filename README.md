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

curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.1/install.sh | bash
source ~/.bashrc
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

<h1 align="center"> Morphreus görevi: Matrix'e giriş. </h1>

```console
# Beni izle.

# Matrixe Mesaj Yollamayi Ogrenmek:
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

> Matrix'e devam etmeden önce [bu](https://github.com/ruesandora/AO/blob/main/chatroom.md) dosyaları ayarla Neo.

<h1 align="center"> Matrix'e dönüş. </h1>

```console
# Bu komutları gir Neo.
.load chatroom.lua
.load token.lua
Morpheus = "sOQYMwbbTr5MlPwp-KUmbXgCCvfoVjgTOBuUDQJZAIU"
Morpheus
Send({ Target = Morpheus, Data = "Morpheus?" })

# Mesajın devamını görmek için bunu kullan Neo.
Inbox[#Inbox].Data
# Hazır mısın?

# Sana bir mesajım daha var Neo.
Send({ Target = Morpheus, Data = "Code: rabbithole", Action = "Unlock" })
# let-us-test Neo. - Action fonksiyonunu kullandın.

# Şimdi chat room için verdiğin isim neyse onu gir Neo. (örnk: Rues)
# { } şeklinde çıktı alacaksın Neo.

# Register et kendini Neo.
Send({ Target = ao.id, Action = "Register" })
# Tekrar chat Room ismini gir Neo
# Bu sefer { } içinde process ID'ini göreceksin.

# brodcast yayınla Neo.
Send({Target = ao.id, Action = "Broadcast", Data = "Broadcasting My 1st Message" })
```

> Öncelikle Morphreus ile tanışmıştın, şimdi beni chatroom'una davet edeceksin.

```console
# Davet kodu bu Neo.
Send({ Target = Morpheus, Action = "Join" })

# şimdi Chatroom adınızı tekrar girin.
# { } içinde hem kendi process hem de benim process ID görürsen başarılı şekilde gelmişimdir Neo.
# Şimdi az şekerli bir Zion kahvesi yap bana Neo.
# bu ID'leri not et bir yere Neo.

# Şimdi sana söylemem gereken bir şey var Neo.
Inbox[#Inbox].Data 
# Evet Neo, Trinity.. Onuda alalım aramıza.
Trinity = "K3YDqxUlQvzonUZ0itOPzAR-rPWvo2Clf9w_NRBBfds"
Send({ Target = Trinity, Action = "Join" })
# Chatroom adını gir bakalım Trinity proces görücek misin Neo.

# Trinity sana bir görev verdi Neo..
````

<h1 align="center"> Trinty Görevi: Token oluşturma. </h1>


```console
# Az önce dosyalar içersinde token dosyamızı oluşturmuştuk Neo.

# Şimdi Trinty'e 1000 adet token gönderelim.
Send({ Target = ao.id, Action = "Transfer", Recipient = Trinity, Quantity = "1000"})

# Trinty sana ne demiş bakalım
Inbox[#Inbox].Data 
# Trinty 1. Görevini tamamlamanı istiyor.

# Daha önce sana dosyaları oluşturduğumuz için Kolay burası Neo.
Send({ Target = ao.id , Action = "Broadcast", Data = "It is done" })
Inbox[#Inbox].Data 

# Görev ödülünü claim et Neo.
Send({Target = "Lz8WE41Ou1RbAiu5Ghm7_xLzVIylYM3iy8A7C6sJraY", Action = "Claim", Name = "Begin" })
Send({ Target = "Sa0iBLPNyJQrwpTTG-tWLQU-1QeUAJA73DdxGGiKoJc", Action = "Balance" })
# Görev ödülünü kontrol et Neo
.load-blueprint chat
Send({ Target = CRED, Action = "Balance" })
CRED = "Sa0iBLPNyJQrwpTTG-tWLQU-1QeUAJA73DdxGGiKoJc"
CRED
.load-blueprint credUtils
CRED.balance

# 500k token almışsındır Neo.
```

<h1 align="center"> Neo, tokenlerini cüzdanına al. </h1>

> Öncelikle [ArConnect](https://www.arconnect.io/) walleta ihtiyaç var.

> İçine de biraz AR token lazım - Ar.io yapanlarda var zaten.

> Ayarlar, Tokens, Token import

> Token adresi: `Sa0iBLPNyJQrwpTTG-tWLQU-1QeUAJA73DdxGGiKoJc`


```console
# token adetin Neo.
Send({ Target = "Sa0iBLPNyJQrwpTTG-tWLQU-1QeUAJA73DdxGGiKoJc", Action = "Balance" })

# Düzenle Neo komutu
Send({ Target = "Sa0iBLPNyJQrwpTTG-tWLQU-1QeUAJA73DdxGGiKoJc", Action = "Transfer", Recipient = "walletAdresin", Quantity = "Miktar"})
```

* Sonraki görevleri daha sonra yazacağım yoruldum ve vaktim kalmadı..

* Ne o Neo? Beğenemedin mi? Sonra yazıcam dedim işte, hadi iyi geceler.




