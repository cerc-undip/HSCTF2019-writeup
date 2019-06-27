# Chicken Crossing
**Category:** forensic <br>
**Point:** 51

> Written by: Jeremy Hui
> 
> Keith is watching chickens cross a road in his grandfather’s farm. He once heard from his grandfather that there was something significant about this behavior, but he can’t figure out why. Help Keith discover what the chickens are doing from this seemingly simple behavior.

file : [hsctf-chicken_crossing.jpg](https://ctf.hsctf.com/files/be1cda99d1a10beae910f00fb95c8fbe/hsctf-chicken_crossing.jpg?token=eyJ0ZWFtX2lkIjoxODMyLCJ1c2VyX2lkIjoyODY3LCJmaWxlX2lkIjo2OX0.XRTprw.qluRCPejW2SmbpssUGQt_WFHWsM)

---

![](./hsctf-chicken_crossing.jpg)

Pada challenge kali ini kita diberikan sebuah file gambar berekstensi `.jpg` dengan gambar 2 buah ayam yang mungkin sedang "ingin menyeberang jalan". Tapi siapa peduli dengan ayam-ayam itu. Mari kita selesaikan challenge ini dengan smooth dan hati yang tenang.

Challenge jenis ini sangat mudah untuk diselesaikan dan sangat umum untuk challenge CTF, karena kita hanya perlu melihat _string_ yang ada dalam gambar ini. Karena file `.jpg` adalah file _binary_, maka kita lakukan ekstraksi untuk menampilkan hanya yang merupakan _string_ saja. Kita bisa menggunakan command `strings`.

```bash
strings hsctf-chicken_crossing.jpg | grep -i hsctf
```

flag : `hsctf{2_get_2_the_other_side}`