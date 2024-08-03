![Ticket System](https://media.discordapp.net/attachments/1269039649284690023/1269039862246412499/Tickets_md-removebg-preview.png?ex=66ae9cf8&is=66ad4b78&hm=84d07e84e06d0e8243a4cecd613273b41a158c6433c754117c712fe6311a2c32&=&format=webp&quality=lossless&width=703&height=227)
# Config
**Bu dosyayı okumadan önce readme.md dosyasını okuduğunuzdan emin olun.**
## Config Kurulumu ve açıklamaları
_**Config ilk olarak "system" ve "guild" olmak üzere 2 ayrı kümeden oluşur, biz system kümesini ele alacağız**_
- Küme Yapısı:
```json
"system": {
    "ticket_embed": {},
    "ticket_embed_button": {},
    "ticket_categories": [],
    "ticket_category_permissions": {},
    "ticket_opening_settings": {},
    "ticket_closing_settings": {},
    "ticket_logs": {},
    "commands": {},
    "voice": {}
}
```
Basitten karmaşığa doğru gitmek istiyorum o yüzden en kolaylarıyla başlayalım
## system.voice
```json
"voice": {
    "enabled":true,
    "channel":"CHANNEL_ID"
}
```
Voice kümesi bot sunucunuzda başladığında bir nevi gösteriş amaçlı bir ses kanalında öylece durmasını sağlar herhangi bir amacı yoktur eğer enabled değerini `true` yaparsanız bot `channel` kanalına bağlanmaya çalışacaktır. Eğer kanal sunucunuzda varsa bot oraya bağlanır ve öylece bekler.
## system.ticket_setup_command
```json
"ticket_setup_command": ".setupTickets"
```
Çok fazla açıklamaya gerek yok bunu yazarsanız belirtilen kanala `Bilet Oluştur` embedi gönderilir yani bir nevi görsel setup
## system.ticket_setup_channel
```json
"ticket_setup_channel":"CHANNEL_ID"
```
Asıl önemli olan kısım aslında burasıdır, buraya setup komutunu kullandığınız veya kullanacağınız kanalın idsini girmeniz gerekmektedir.
## system.ticket_setup_command_required_role
```json
"ticket_setup_command_required_role":"ROLE_ID"
```
Ve evet o komutu kullanmak için gereken rol burada belirlenir.
## system.ticket_logs
```json
"ticket_logs": {
    "enable":true,
    "Auto_Log_Channels":900000

},
```
Ticketların kapatıldıktan sonra dosya olarak dışarıya çıkartılması olayını kontrol edersiniz `enable` değeri `true` iken her `Auto_Log_Channels` milisaniyede 1 bot kategori içeriğini temizler ve dosyalara taşır logları. Dakikayı kolay hesaplamak isterseniz<br>
`MINUTES * 60 * 1000` formülünü kullanabilirsiniz. size o dakikanın `milisaniye` cinsinden karşılığını verir.
# Eğlenceli kısım başlıyor
## system.ticket_embed
```json
"ticket_embed": {
    "Title":"Destek Sistemi",
    "Description":"Bilet oluşturmak için alttaki butona tıkla !",
    "color":"#00FF00",
    "fields": {},
    "Images": {}
},
```
`ticket_setup_command` kullanıldığında hangi embedin gönderileceği burada detaylıca hazırlanıp düzenlenebilir ama sadece metinleri değil bu embedin tam anlamıyla her şeyi düzenlenebilir.
### system.ticket_embed.fields
```json
"ticket_embed": {
    "fields": {
        "status":true,
        "name":"Aşağıdaki örnek durumlarda ticket açabilirsiniz;",
        "value":"- Bir yetkilinin hatası olduğunda,\n- Bir oyuncuyu bildirmek için,\n- Bir görüş veya öneriniz olduğunda...",
        "inline":false
    }
}
```
`status` değeri `true` veya `false` olabilir eğer `false` yaparsanız embed içeriğinde bir field açılmaz ve sadece Title & Description olarak gönderilir. `true` yaparsanız bunlar aktif edilir.
- `inline` çok önemli bir değer değil şuanki durum için o yüzden es geçiyorum
### system.ticket_embed.Images
```json
"ticket_embed": {
    "Images": {
        "thumbnail": {
            "status":true,
            "url":"LINK_TO_PNG"
        },
        "img": {
            "status":true,
            "url":"LINK_TO_PNG"
        }
    }
}
```
`thumbnail` ve `img` olarak 2 ayrı bölümü vardır, her bölümü kendi içerisindeki `status` kısmını `true` veya `false` yaparak kullanabilirsiniz tahmin edeceğiniz üzere `true` yaparsanız koyduğunuz `url` embed'e eklenecektir.
- bunların hangisinin hangisi olduğunu şöyle ayırt edebilirsiniz:
![embed](https://media.discordapp.net/attachments/1269039649284690023/1269107955505041509/image.png?ex=66aedc63&is=66ad8ae3&hm=c782bba2a86dea0d98ac1e9cf493ca0dc11c6b3b9453f82fc9b6a2a9b967a2ea&=&format=webp&quality=lossless&width=822&height=460)<br>
Bu embed örneğinde
- `SMILE` yazan kısım `img`
- `LOREM` yazan kısım `thumbnail`
olarak ayırt edilebilir.
## system.ticket_embed_button
```json
"ticket_embed_button": {
    "Label":"Ticket Aç!",
    "emoji":{
        "status":true,
        "emoji":"<:konrul_mail:1248248920828678144>"
    }
}
```
Ve burasıda yukarıda hazırladığınız embedinizin altında olacak olan `ticket_creation_button` dediğimiz Bilet oluşturma butonu, kendisinin üzerindeki yazıyı ve emoji koymak isterseniz `emoji.status` kısmını `true` yapıp belirtilen yere doğru formatta bir emoji koymalısınız.
- Doğru formatta emojiyi nasıl alıcam ?<br>
Bunu yapmak çok kolay aslında discord'da dümdüz emojiyi yazın örneğin `:x:` discord bunu otomatik olarak resme dönüştürüyor sohbet kutusunda tek yapmanız gereken bir karakter soluna gelip `\` koymak:<br>
`\:x:` bunu `enter` bastığınızda yukarıdaki gibi bir kod alıcaksınız. burayı iyi öğrenin birazdan aşağıda bol bol kullanıcaz.
## system.ticket_categories
```json
"ticket_categories": [
    { "label": "Category Name 1", "value": "category1", "emoji": "<:superemoji:1010>" },
    { "label": "Category Name 2", "value": "category2", "emoji": "<:superemoji:1010>" }
],
```
`label` kısmı oyuncunun kategori seçerken göreceği kısımdır ve boşluk bırakıp istediğinizi yapabilirsiniz.<br>
`value` kısmı ise kategori izinlerindede bize lazım olacak ve ismi `boşluk,'-'` içermeyerek `.js` formatı dışına çıkabilecek herhangi bir `key_name` olmamalıdır.<br>
`emoji` kısmınada yine yukarıdan öğrendiğiniz şekilde emoji koyabilirsiniz.
## system.ticket_category_permissions
```json
"ticket_category_permissions": {
    "category1": ["ROLE_ID_HERE", "ROLE_ID_HERE"],
    "category2": ["ROLE_ID_HERE"],
}
```
Bu sefer yukarıda seçilen kategoriyi hangi `rollerin` görebileceğini seçiyoruz, `[]` içerisine `["ROLE","ROLE"]` formatında dilediğiniz kadar `ROLE_ID` koyabilirsiniz bot algılayacaktır tek kilit nokta yukarıda belirlenen her `key_name` yani `value` için burada bir karşılık olmasıdır.
# system.ticket_opening_settings
Bu küme Biletin ilk oluşturulduğu anı ve nerede oluşturulacağı gibi durumları ele alır.
## system.ticket_opening_settings.tags
```json
"ticket_opening_settings": {
    "tags": "ROLE_ID",
}
```
Ticket ilk açıldığında embedin yanında hangi rolü tagleyecek ? *Yetkili veya moderatör ekibi gibi genel bir rol yazmanız önerilir.*
## system.ticket_opening_settings.timelimitation
```json
"ticket_opening_settings": {
    "timelimitation": {
        "enabled": true,
        "start_hour": 11,
        "end_hour": 2,
        "message": "Sadece mesai saatleri (11:00 - 02:00) arasında Bilet oluşturabilirsiniz."
    }
}
```
Bunu açıp açmamak tamamen size kalmış ticketların belirli saat aralığında açılmasına izin verir sadece, `0-24` saat aralığını kullanabilirsiniz eğer isterseniz. kullanmak istemezseniz `enabled` - `false` yapıp geçin
## system.ticket_opening_settings.ticket_create
```json
"ticket_opening_settings": {
    "ticket_create": {
        "category": "CATEGORY_ID"
    }
}
```
Ticketlar açıkken hangi kategori altına açılacaksa onu buraya yazıyoruz.
## system.ticket_opening_settings.first_embed
```json
"ticket_opening_settings": {
    "first_embed": {
        "Title":"Destek Talebi",
        "Description":"Biletini açtığın yetkililere bildirildi en kısa sürede seninle ilgileneceklerdir",
        "Color":"#00FF00",
        "fields": {
            "status":false,
            "name":"",
            "value":"",
            "inline":false
        },
        "Images": {
            "thumbnail": {
                "status":false,
                "url":"url"
            },
            "img": {
                "status":false,
                "url":"url"
            }
        }
    }
}
```
`Images` ve `fields` ile ilgili yukarıdaki açıklamaları okuduğunu varsayaraktan bunun ne olduğunu kolayca anlarsın diye düşünüyorum,<br>
Ticket açıldığında ilk mesaj olarak kullanıcıyı bilgilendirmek için bu embed gönderilecektir.
## system.ticket_closing_settings
```json
"ticket_closing_settings": {
    "category_error": {
        "msg":"Bu komut sadece Konrul Tickets kategorisi altında kullanılabilir.",
        "embed":true,
        "ephemeral":true
    },
    "log_category": "CATEGORY_ID",
    "action_logs": "CHANNEL_ID"
}
```
- `category_error` bölümü komutun Ticketlar için ayırdığınız kategori dışında kullanılması sonucu oluşacak hatayı temsil eder. <br> `category_error.embed` değeri ise bu mesajın bir embed olarak gönderilmesi olayını kontrol eder,<br> `category_error.ephemeral` ise bu gönderilecek mesajın sadece komutu kullanan kullanıcıya görünmesi olayını kontrol eder.
`log_category` Değeri biletler kapatıldığında hangi kategori altına taşınacaklarını kontrol eder.<br>
- NOT: **Ticketlar kapatıldığında belirlenen kategorinin izinleri ile kendilerini `senkronize` ederler bu yüzden `log_category` izinlerini ne yaparsanız altındaki kanallar içinde geçerli olucaktır.**
`action_logs` kısmı ise Ticket kapatma işlemlerini loglar yani metinsel olarak şu şunu yaptı diye, bir kanal belirlemeniz gerekir.
## system.commands
Bu bölüm içerisinde fazla komut olduğu için hepsini buraya yazamıyorum ama bilmeniz gereken bilgiler<br>
```json
"commandName":{
    "required_role": "ROLE_ID",
    "permission_error":{
        "msg":"Bu komutu kullanmak için yeterli izniniz yok.",
        "embed":true,
        "ephemeral":true
    }
},
```
Bu genel bir komut örneğini ele alalım
- `required_role` Komutu kullanmak için gereken rol
- `permission_error` ise izni yoksa karşısına çıkacak mesaj, `embed` ve `ephemeral` kısımlarını atlıyorum yukarıda bahsettim.
**Ayrıca lafı geçmişken `system.ticket_claim_command` da komutlara dahildir yani burada ne görüyorsan orasıda hemen hemen aynı**
