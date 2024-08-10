# Nickname Validator
API ini dibuat untuk mencari nickname in-game menggunakan ID player, data dari API ini diambil dari [Codashop](https://www.codashop.com/).

Awal bermula nya projek ini saat saya mengunjungi web phising yang menggunakan sistem validasi ID pada situsnya (ironis, padahal masih bayak web topup yang belum implementasi beginian), jadi kalo ID nya tidak valid maka data tidak bisa disubmit.

Karena dari Codashop request dan parsing data nya lebih ribet, maka dibuatlah API ini.

## Self Deploy
Kamu bisa langsung fork aja repo ini, atau bisa tekan tombol dibawah ini (jangan lupa github secrets nya di seting)

[![Deploy to Cloudflare Workers](https://deploy.workers.cloudflare.com/button)](https://deploy.workers.cloudflare.com/?url=https://github.com/ihsangan/valid)
## Endpoint
```
https://validator.hermantabd.workers.dev
```
## Output
application/json; charset=utf-8 ([RFC4627](https://datatracker.ietf.org/doc/html/rfc4627))
```ts
interface Result {WEB
  success: boolean;
  game?: string;
  id?: number | string;
  zoneId?: number;
  server?: string,
  name?: string;
  message?: string;
}
```
# Daftar game
Berikut adalah daftar game yang didukung oleh API ini.
### Genshin Impact (America, Asia, Europe, SAR) [CENSORED]
GET `/gi?id=PLAYER_ID`

**Contoh:** [600000000](https://validator.hermantabd.workers.dev/gi?id=600000000)
### Honkai Impact 3rd [CENSORED]
GET `/hi?id=PLAYER_ID`

**Contoh:** [10000001](https://validator.hermantabd.workers.dev/hi?id=10000001)
### Honkai: Star Rail (America, Asia, Europe, SAR) [CENSORED]
GET `/hsr?id=PLAYER_ID`

**Contoh:** [600000001](https://validator.hermantabd.workers.dev/hsr?id=600000001)
### LifeAfter
GET `/la?id=PLAYER_ID&zone=SERVER_NAME`

SERVER_NAME bersifat case-insensitive, untuk daftarnya ada [di sini](https://github.com/ihsangan/valid/blob/main/src/router/la.ts).

**Contoh:** [?id=22512309&zone=milestone](https://validator.hermantabd.workers.dev/la?id=22512309&zone=milestone)
### Point Blank
GET `/pb?id=ZEPETTO_ID`

**Contoh:** [wakwaw55](https://validator.hermantabd.workers.dev/pb?id=wakwaw55)
### Punishing: Gray Raven (AP, EU, NA)
GET `/pgr?id=ID&zone=SERVER_ID`

Case-insensitive, keterangan untuk identifikasi server: AP(Asia-Pasifik), EU(Europe), NA(North America)

**Contoh:** [?id=16746755&zone=AP](https://validator.hermantabd.workers.dev/pgr?id=16746755&zone=AP)
### Sausage Man
GET `/sm?id=PLAYER_ID`

**Contoh:** [5sn9jf](https://validator.hermantabd.workers.dev/sm?id=5sn9jf)
### Super Sus
GET `/sus?id=SPACE_ID`

**Contoh:** [15916600](https://validator.hermantabd.workers.dev/sus?id=15916600)
### Valorant
GET `/valo?id=URISafeRiotIdAndTag`

**Contoh region ID :** [yuyun%23123](https://validator.hermantabd.workers.dev/valo?id=yuyun%23123)

**Contoh region non ID :** [Westbourne%23USA](https://validator.hermantabd.workers.dev/valo?id=Westbourne%23USA)
### Zenless Zone Zero (America, Asia, Europe, SAR) [CENSORED]
GET `/zzz?id=PLAYER_ID`

**Contoh:** [1000000100](https://validator.hermantabd.workers.dev/zzz?id=1000000100)
## ID-REG-ONLY
Dibawah ini adalah daftar game yang hanya bisa dipakai menggunakan ID yang terdaftar dari region Indonesia/SEA
### Arena of Valor
GET `/aov?id=PLAYER_OR_OPEN_ID`

**Contoh:** [124590895269021](https://validator.hermantabd.workers.dev/aov?id=124590895269021)
### Call Of Duty
GET `/cod?id=PLAYER_OR_OPEN_ID`

**Contoh:** [243402956362890880](https://validator.hermantabd.workers.dev/cod?id=243402956362890880)
### Free Fire
GET `/ff?id=PLAYER_ID`

**Contoh:** [225009777](https://validator.hermantabd.workers.dev/ff?id=225009777)
### Mobile Legends: Bang Bang
GET `/ml?id=PLAYER_ID&zone=ZONE_ID`

**Contoh:** [?id=1114917746&zone=13486](https://validator.hermantabd.workers.dev/ml?id=1114917746&zone=13486)
## Parameter Opsional
Kamu dapat menambah parameter `decode` dan mengisi value ke `false` (default ke `true`).

Ketika value diatur ke `false` maka data nickname akan ditampilkan dala URL encoded dan untuk membacanya memerlukan function seperti `decodeURIComponent()` (dalam javascript) atau sejenisnya, saya juga lebih merekomendasikan untuk menggunakan `?decode=false`.

Sementara jika value adalah `true` maka data akan bisa dibaca secara langsung tapi kemungkinan error dan gagal dalam pembacaan data akan muncul.

Berikut adalah contoh penggunaan `?decode=false`

[ml?id=1007909047&zone=13044&decode=false](https://validator.hermantabd.workers.dev/ml?id=1007909047&zone=13044&decode=false)

Contoh penggunaan `?decode=true`

[ml?id=1007909047&zone=13044&decode=true](https://validator.hermantabd.workers.dev/ml?id=1007909047&zone=13044&decode=true) atau [ml?id=1007909047&zone=13044](https://validator.hermantabd.workers.dev/ml?id=1007909047&zone=13044) (sama saja).
## Monitoring
API monitoring [UptimeRobot](https://stats.uptimerobot.com/s9axzR77Fm)
# Copyright
© Projek ini dibawah lisensi: [CC BY-NC 4.0](https://creativecommons.org/licenses/by-nc/4.0/), tidak terafiliasi dengan Codashop.
