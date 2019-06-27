# Cool Image
**Category:** forensic <br>
**Point:** 101

> Written by: cppio
> 
> My friend told me he found a really cool image, but I couldn't open it. Can you help me access the image?

file : [cool.pdf](https://ctf.hsctf.com/files/81da3c85ccd0a37505a994cc749a1fbe/cool.pdf?token=eyJ0ZWFtX2lkIjoxODMyLCJ1c2VyX2lkIjoyODY3LCJmaWxlX2lkIjo4fQ.XRTrhA.rWGsQGQcCU4wLOTlYb7x91-7x7s)

---

Pada challenge ini kita diberikan 1 buah file berekstensi `.pdf`. Namun ketika dibuka menggunakan PDF Viewer kita mendapatkan error, setelah dicek, ternyata file tersebut bukanlah file PDF melainkan PNG.

```
cool.pdf: PNG image data, 1326 x 89, 8-bit/color RGBA, non-interlaced
```

Kita ubah ekstensinya dari `.pdf` menjadi `.png`.
```bash
cp cool.pdf cool.png
eog cool.png
```

![](./cool.png)

flag : `hsctf{who_uses_extensions_anyways}`