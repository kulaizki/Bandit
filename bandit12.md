# Bandit 12

We are given a file named data.txt, which is a `hexdump` file that has been repeatedly compressed.

With that, it would be a good idea to create a new directory wherein we can save our progress
in decompressing the file multiple times.
```bash
bandit12@bandit:~$ mkdir /tmp/123
bandit12@bandit:~$ cd /tmp/123
bandit12@bandit:/tmp/123$ cd ~
bandit12@bandit:~$ cp data.txt /tmp/123
bandit12@bandit:~$ cd /tmp/123
```
```bash
bandit12@bandit:/tmp/123$ ls
data.txt
bandit12@bandit:/tmp/123$ cat data.txt
00000000: 1f8b 0808 6855 1e65 0203 6461 7461 322e  ....hU.e..data2.
00000010: 6269 6e00 013d 02c2 fd42 5a68 3931 4159  bin..=...BZh91AY
00000020: 2653 5948 1b32 0200 0019 ffff faee cff7  &SYH.2..........
00000030: f6ff e4f7 bfbc ffff bff7 ffb9 39ff 7ffb  ............9...
00000040: bd31 eeff b9fb fbbb b9bf f77f b001 3b2c  .1............;,
00000050: d100 0d03 d200 6868 0d00 0069 a00d 0340  ......hh...i...@
00000060: 1a68 00d0 0d01 a1a0 0001 a680 0003 46d4  .h............F.
00000070: 6434 3234 611a 340d 07a4 c351 068f 5000  d424a.4....Q..P.
00000080: 069a 0680 0000 0006 8006 8da4 681a 6868  ............h.hh
00000090: 0d06 8d00 6834 3400 d07a 9a00 01a0 0341  ....h44..z.....A
000000a0: ea1e a190 da40 3d10 ca68 3468 6800 00c8  .....@=..h4hh...
000000b0: 1a1a 1b50 0683 d434 d069 a0d0 3100 d000  ...P...4.i..1...
000000c0: 001e a680 00d0 1a00 d0d0 6864 d0c4 d0d0  ..........hd....
000000d0: 000c 8641 7440 0108 032e 86b4 4cf0 22bb  ...At@......L.".
000000e0: 6682 2b7e b3e2 e98d aa74 dacc 0284 330d  f.+~.....t....3.
000000f0: bbb2 9494 d332 d933 642a 3538 d27e 09ce  .....2.3d*58.~..
00000100: 53da 185a 505e aada 6c75 59a2 b342 0572  S..ZP^..luY..B.r
00000110: 249a 4600 5021 25b0 1973 c18a 6881 1bef  $.F.P!%..s..h...
00000120: 3f9b 1429 5b1d 3d87 68b5 804f 1d28 42fa  ?..)[.=.h..O.(B.
00000130: 16c2 3241 98fb 8229 e274 5a63 fe92 3aca  ..2A...).tZc..:.
00000140: 70c3 a329 d21f 41e0 5a10 08cb 888f 30df  p..)..A.Z.....0.
00000150: f3da ce85 418b 0379 6a65 cfa2 eeb7 9f01  ....A..yje......
00000160: 782c da0e 288b e0c3 fe13 7af5 45ab 2b22  x,..(.....z.E.+"
00000170: a432 bf2f e32d b9e6 1465 2296 d805 a45e  .2./.-...e"....^
00000180: d1c1 eacb 7483 6aac ca0e cf24 8864 bd40  ....t.j....$.d.@
00000190: 118c 644a 1dc6 a127 375c b7a6 c124 bdae  ..dJ...'7\...$..
000001a0: 6d31 63a0 a223 3ea0 61d4 bdf0 450f 56fb  m1c..#>.a...E.V.
000001b0: a546 8d34 08a2 4f1d 43d3 9063 404d dd43  .F.4..O.C..c@M.C
000001c0: b4f2 e65d bcb7 5932 0f5e 6802 3892 a988  ...]..Y2.^h.8...
000001d0: 443d 8e89 7e09 4fb0 499d ee4e 4470 46c0  D=..~.O.I..NDpF.
000001e0: 2ba6 7c62 234a 7f76 151b aec0 23ee 4a97  +.|b#J.v....#.J.
000001f0: bc64 e34c de8a 5724 a1c3 9b89 cd96 1879  .d.L..W$.......y
00000200: d560 0cbb 5c26 09e4 efaf 5b94 402a 7780  .`..\&....[.@*w.
00000210: 4d87 30ce b8a3 946e 72c1 a643 1db7 a060  M.0....nr..C...`
00000220: 6524 629c 0c7e 8e7b e0f8 820c d5cb 60a0  e$b..~.{......`.
00000230: 003c a584 d4c1 61ef eb02 3f65 3a54 a3a2  .<....a...?e:T..
00000240: a565 c154 34c2 b162 d206 1ff8 bb92 29c2  .e.T4..b......).
00000250: 8482 40d9 9010 b3a9 e478 3d02 0000       ..@......x=...
```

First, since it's a hexdump we used `xxd -r` to `reverse` the hexdump or convert it to binary.
We save the converted file into `crack1.txt` so we can easily decompress it further.
```bash
bandit12@bandit:/tmp/123$ xxd -r data.txt compressed_data
bandit12@bandit:/tmp/123$ ls
compressed_data  data.txt
bandit12@bandit:/tmp/123$ cat compressed_data
�h44�z��A����@=�h4hh�������hd�������������9��1�������;,�
�����2�3d*58�~	�S�ZP^��luY��Br$�FP!%�s��h�?�)[=�h��O(B��2A��)�tZc��:�pã)�A�ˈ�0���΅A�yjeϢx,�(����z�E�+"�2�/�-��e"���^����t�j���$�d�@�dJơ'7\���$��m1c��#>�aԽ�EV�F��OCӐc@M�C���]��Y2^h8���D=��~	O�I��NDpF�+�|b#Jv�#�J��d�LފW$�Û�͖y�`
                                                                                                            �\&	��[�@*w�M�0θ��nr��C��`e$b�
                 ~�{��
                      ��`�<����a��?e:T���e�T4±b��)�@ِ���x=bandit12@bandit:/tmp/123$ ^C
```
Since we'll be **decompressing multiple files** with potentially `varying formats`, 
we need to use the `file` command to identify their types before decompression.
Here we notice that the file is `gzip compressed data`, which means we have to decompress it using 
`gzip -d`. But before that, we have to add the `.gz` suffix to our file using `mv`, because gzip can only
work with files with that suffix.
```bash
bandit12@bandit:/tmp/123$ file compressed_data
compressed_data: gzip compressed data, was "data2.bin", last modified: Thu Oct  5 06:19:20 2023, max compression, from Unix, original size modulo 2^32 573
bandit12@bandit:/tmp/123$ mv compressed_data compressed_data.gz
bandit12@bandit:/tmp/123$ gzip -d compressed_data.gz
bandit12@bandit:/tmp/123$ ls
compressed_data  data.txt
bandit12@bandit:/tmp/123$ cat compressed_data
�h44�z��A����@=�h4hh���4�i��1������hd����,�
�����2�3d*58�~	�S�ZP^��luY��Br$�FP!%�s��h�?�)[=�h��O(B��2A��)�tZc��:�pã)�A�ˈ�0���΅A�yjeϢx,�(����z�E�+"�2�/�-��e"���^����t�j���$�d�@�dJơ'7\���$��m1c��#>�aԽ�EV�F��OCӐc@M�C���]��Y2^h8���D=��~	O�I��NDpF�+�|b#Jv�#�J��d�LފW$�Û�͖y�`
                                                                                                            �\&	��[�@*w�M�0θ��nr��C��`e$b�
                 ~�{��
                      ��`�<����a��?e:T���e�T4±b��)�@ِbandit12@bandit:/tmp/123$ ^C
```

Here we have `bzip2 compressed data`, we can decompress this using `bzip2 -d`.
Similarly to `gzip`, we must change the suffix to `.bz2` for bzip2 to work.
```bash
bandit12@bandit:/tmp/123$ file compressed_data
compressed_data: bzip2 compressed data, block size = 900k
bandit12@bandit:/tmp/123$ mv compressed_data compressed_data.bz2
bandit12@bandit:/tmp/123$ ls
compressed_data.bz2  data.txt
bandit12@bandit:/tmp/123$ bzip2 -d compressed_data.bz2
bandit12@bandit:/tmp/123$ ls
compressed_data  data.txt
bandit12@bandit:/tmp/123$ cat compressed_data
hUedata4.bin���Ka��qDte���A�g���E��	["��AS\ZWO��*�J�FI
�                                                         �
 B�.!�Y���<����jʛ����_�ϗ�y.���R�Y���%���7�?�8���{�����n�ι��Q+��8=�)+��d"�:�ݿ�/��ӿ�\�״��W���������X՝�+��s!�~nm4��w��m���Q ���.1)�gE7<��iY�?��U�P�v��J�Q�LWVs!u($
                                      ��fǾ�,١�'p��j�
                                                    -W�D��7r�����l��7"��u��T���JcC��D��ȵ��z�������77���Wݾ��/�S��╊ftamo��G�ӮO��m�ww>��^����d] �9^�p~G0�Pbandit12@bandit:/tmp/123$ ^C
```

Now we just repeat the same process here.
```bash
bandit12@bandit:/tmp/123$ file compressed_data
compressed_data: gzip compressed data, was "data4.bin", last modified: Thu Oct  5 06:19:20 2023, max compression, from Unix, original size modulo 2^32 20480
bandit12@bandit:/tmp/123$ mv compressed_data compressed_data.gz
bandit12@bandit:/tmp/123$ gzip -d compressed_data.gz
bandit12@bandit:/tmp/123$ ls
compressed_data  data.txt
bandit12@bandit:/tmp/123$ cat compressed_data
data5.bin0000644000000000000000000002400014507452550011247 0ustar  rootrootdata6.bin0000644000000000000000000000033114507J!�1����&�2i6��I�P2���@�@4��k�ʀ@��8M|�V1@��P����2[j�.�v'�1�s���TTI��V�*�A�^O
�⛝���5P�����a��'1�U^Gl~BH��rE8P���bandit12@bandit:/tmp/123$ ^C
```

Here we see a new file type which is `tar`, we can use `tar -xf` to `extract` the file.
```bash
bandit12@bandit:/tmp/123$ file compressed_data
compressed_data: POSIX tar archive (GNU)
bandit12@bandit:/tmp/123$ mv compressed_data compressed_data.tar
bandit12@bandit:/tmp/123$ tar -xf compressed_data.tar
bandit12@bandit:/tmp/123$ ls
compressed_data.tar  data5.bin  data.txt
bandit12@bandit:/tmp/123$ file data5.bin
data5.bin: POSIX tar archive (GNU)
bandit12@bandit:/tmp/123$ tar -xf data5.bin
bandit12@bandit:/tmp/123$ ls
compressed_data.tar  data5.bin  data6.bin  data.txt
bandit12@bandit:/tmp/123$ file data6.bin
data6.bin: bzip2 compressed data, block size = 900k
bandit12@bandit:/tmp/123$ mv data6.bin data6.bz2
bandit12@bandit:/tmp/123$ bzip2 -d data6.bz2
bandit12@bandit:/tmp/123$ ls
compressed_data.tar  data5.bin  data6  data.txt
bandit12@bandit:/tmp/123$ cat data6
data8.bin0000644000000000000000000000011714507452550011255 0ustar  rootroohUedata9.bin
                                                                                      �HU(H,..�/JQ�,V(O
O�q�p�,2qNt��I
              �H,-��7+(�-r)���uG1bandit12@bandit:/tmp/123$ ^C
bandit12@bandit:/tmp/123$ file data6
data6: POSIX tar archive (GNU)
bandit12@bandit:/tmp/123$ mv data6 data6.tar
bandit12@bandit:/tmp/123$ tar -xf data6.tar
bandit12@bandit:/tmp/123$ ls
compressed_data.tar  data5.bin  data6.tar  data8.bin  data.txt
bandit12@bandit:/tmp/123$ cat data8.bin
hUedata9.bin
            �HU(H,..�/JQ�,V(O
O�q�p�,2qNt��I
              �H,-��7+(�-r)���uG1bandit12@bandit:/tmp/123$ ^C
```

Finally, we cracked the password after decompressing the file one last time.
```bash
bandit12@bandit:/tmp/123$ file data8.bin
data8.bin: gzip compressed data, was "data9.bin", last modified: Thu Oct  5 06:19:20 2023, max compression, from Unix, original size modulo 2^32 49
bandit12@bandit:/tmp/123$ mv data8.bin data8.gz
bandit12@bandit:/tmp/123$ gzip -d data8.gz
bandit12@bandit:/tmp/123$ ls
compressed_data.tar  data5.bin  data6.tar  data8  data.txt
bandit12@bandit:/tmp/123$ cat data8
The password is wbWdlBxEir4CaE8LaPhauuOo6pwRmrDw
```
