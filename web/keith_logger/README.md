# Keith Logger
**Category:** web <br>
**Point:** 157

> Written by: dwang
> 
> Keith is up to some evil stuff! Can you figure out what he's doing and find the flag?
> 
> Note: nothing is actually saved

File : [extension.crx](https://ctf.hsctf.com/files/06b639a54f7c556d3462a44f2fbecc84/extension.crx?token=eyJ0ZWFtX2lkIjoxODMyLCJ1c2VyX2lkIjoyODY3LCJmaWxlX2lkIjo1fQ.XRTiMw.lhSoGlLbLX6DexSRRm2C_nvNdUI)

---

Pada challenge ini kita diberikan sebuah file `.crx`, file ini merupakan file untuk yang berisi fitur yang dapat di-instal pada browser Chrome.

```
extension.crx: Google Chrome extension, version 3
```

Untuk membuka file yang di dalamnya kita _extract_ menggunakan `unzip`.

```console
┌─[haz@haz]─[~/Programming/CTF/hsctf2019/web/keith_logger]
└──╼ $unzip extension.crx
Archive:  extension.crx
warning [extension.crx]:  593 extra bytes at beginning or within zipfile
  (attempting to process anyway)
  inflating: jquery-3.3.1.min.js     
  inflating: manifest.json           
  inflating: content.js
```

Setelah di-_extract_ maka terdapat 3 buah file, kita buka file Javascript bernama `content.js`. Fokus pada bagian

```javascript
xhr.open(
  "GET",
  "https://keith-logger.web.chal.hsctf.com/api/admin",
  true
);
```

Action akan mengirimkan AJAX ke alamat tersebut, ketika url diatas dibuka menggunakan browser maka kita akan dapatkan pesan dengan _credential_ khusus. _Credential_ ini merupakan kunci untuk masuk kedalam server database MongoDB. Langkah selanjutnya adalah kita _connect_-kan dengan server tersebut menggunakan `mongo`. Untuk melakukan koneksi silahkan baca pada website dokumentasi [disini](https://docs.mongodb.com/manual/mongo/).

<pre>
┌─[haz@haz]─[~/Programming/CTF/hsctf2019/web/keith_logger]
└──╼ $mongo --username admin --password keithkeithkeith --authenticationDatabase "admin" keith-logger-mongodb.web.chal.hsctf.com:27017
```

Kemudian kita berhasil terkoneksi dengan server database mongo. Selanjutnya kita cek semua _database_ dan _collection_ yang ada untuk menemukan flag-nya.

> Jika belum mengetahui perintah pada MongoDB, silahkan baca pada tutorial [berikut](https://dzone.com/articles/top-10-most-common-commands-for-beginners) atau melalui [Official Quick Reference](https://docs.mongodb.com/manual/reference/mongo-shell/).

```shell
MongoDB shell version v3.6.3
connecting to: mongodb://keith-logger-mongodb.web.chal.hsctf.com:27017/test
MongoDB server version: 4.0.10
WARNING: shell and server versions do not match
> show dbs
database  0.000GB
> use database
switched to db database
> show collections
collection
> db.collection.find()
{ "_id" : ObjectId("5cf0512d464d9fe1d9915fbd"), "text" : "are kitties cool", "url" : "https://keith-logger.web.chal.hsctf.com/", "time" : "21:54:53.925045" }
{ "_id" : ObjectId("5cf051a95501f2901a915fbd"), "text" : "because i think they are", "url" : "https://keith-logger.web.chal.hsctf.com/", "time" : "21:56:57.974856" }
{ "_id" : ObjectId("5cf051b3464d9fe1d9915fbe"), "text" : "meow! :3", "url" : "https://keith-logger.web.chal.hsctf.com/", "time" : "21:57:07.295378" }
{ "_id" : ObjectId("5cf0520b464d9fe1d9915fbf"), "text" : "meow! :3", "url" : "https://keith-logger.web.chal.hsctf.com/", "time" : "21:58:35.030635" }
{ "_id" : ObjectId("5cf05212464d9fe1d9915fc0"), "text" : "if you're looking for the flag", "url" : "https://keith-logger.web.chal.hsctf.com/", "time" : "21:58:42.170470" }
{ "_id" : ObjectId("5cf0521b5501f2901a915fbe"), "text" : <b>"it's hsctf{watch_out_for_keyloggers}"</b>, "url" : "https://keith-logger.web.chal.hsctf.com/", "time" : "21:58:51.359556" }
> 
</pre>

flag : `hsctf{watch_out_for_keyloggers}`