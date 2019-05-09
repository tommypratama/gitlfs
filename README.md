# Git LFS Tutorial

## Installation

Khusus untuk ubuntu

```bash
wget -O - https://raw.githubusercontent.com/tommypratama/dotfiles/master/gitlfs/ubuntu/install.sh | sudo bash
```

Untuk OS lainnya, silahkan ikuti tutorial berikut [https://github.com/git-lfs/git-lfs/wiki/Tutorial](https://github.com/git-lfs/git-lfs/wiki/Tutorial)

## Tutorial

### Buat Repositori Github

1. Membuat Repositori di https://github.com/new
2. Membuat file `README.md`

```bash
git init .
echo Hello World > README.md
git add README.md
git commit -m "Initial commit"
```

3. Pastikan sudah menginstal git-lfs. Untuk memastikan bahwa git-lfs diatur dengan benar dalam file konfigurasi git Anda, gunakan perintah install git lfs:

```bash
git lfs install
```

Output 

```bash
Git LFS initialized.
```

4. Sekarang mari kita tambahkan beberapa file besar untuk dilacak oleh git-lfs:

```bash
head -c 1M /dev/urandom > cat.bin
head -c 1M /dev/urandom > dog.bin
```

5. Tentukan file yang ingin dilacak oleh git-lfs, misalkan `.bin`, `.csv`, dll dengan perintah berikut:

```bash
git lfs track '*.bin'
```

Perintah di atas akan membuat file otomatis `.gitattributes` yang di dalamnya berisi `*.bin filter=lfs diff=lfs merge=lfs -text`. Silahkan cek untuk memastikan :

```bash
cat .gitattributes
```

Output

```bash
*.bin filter=lfs diff=lfs merge=lfs -text
``` 

Untuk melihat format file apa saja yang dilacak/ditrack oleh git-lfs, gunakan perintah:

```bash
git lfs track
```

Output

```bash
Listing tracked patterns
    *.bin (.gitattributes)
Listing excluded patterns
```

> **CATATAN**: Perintah `'*.bin'` akan melacak semua file di dalam direktori yang ber ekstensi `.bin` menjadi file git-lfs

6. Tambahkan file `.gitattributes` , `cat.bin` dan `dog.bin` ke dalam Git.

```bash
git add .gitattributes
git add "*.bin"
```

6. Cek status

```bash
git status
```

Output

```bash
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        new file:   .gitattributes
        new file:   bar.txt
        new file:   cat.bin
        new file:   dog.bin
        new file:   foo.txt
```

7. Terakhir, commit semua file

```bash
git commit -m "Add files"
```

8. Sekarang, coba jalankan `git lfs ls-files` dan kita dapat melihat file apa saja yang dilacak git-lfs:

```bash
a1c119ccc2 * cat.bin
62a01ce9d4 * dog.bin
```

### Kesimpulan

Repositori Github biasa ( tanpa git-lfs ) mempunyai batasan limit `100mb`, jika Anda mengupload file lebih dari 100mb ke Github ,maka akan ditolak. Git-lfs disini berfungsi untuk menangani file yang memiliki size besar.


### Sumber

* https://github.com/git-lfs/git-lfs/wiki/Tutorial
* https://github.com/git-lfs/git-lfs/wiki/Installation
* https://www.atlassian.com/git/tutorials/git-lfs
* https://www.youtube.com/watch?v=uLR1RNqJ1Mw




