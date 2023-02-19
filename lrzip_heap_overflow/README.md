lrzip v0.651(latest)

poc:https://github.com/huanglei3/lrzip_poc/blob/main/lrzip_heap_overflow/overflow

execution:./lrzip -t overflow

result:  reference : https://github.com/huanglei3/lrzip_poc/blob/main/lrzip_heap_overflow/overflow.png


Decompressing...
=================================================================
==3510675==ERROR: AddressSanitizer: heap-buffer-overflow on address 0x6140000001ec at pc 0x55f6c66defd6 bp 0x7fa7db9e16d0 sp 0x7fa7db9e16c0
WRITE of size 1 at 0x6140000001ec thread T2
    #0 0x55f6c66defd5 in libzpaq::PostProcessor::write(int) ../libzpaq/libzpaq.cpp:1208
    #1 0x55f6c66e01b3 in libzpaq::Decompresser::decompress(int) ../libzpaq/libzpaq.cpp:1311
    #2 0x55f6c66e0c5c in libzpaq::decompress(libzpaq::Reader*, libzpaq::Writer*) ../libzpaq/libzpaq.cpp:1366
    #3 0x55f6c66e1171 in zpaq_decompress ../libzpaq/libzpaq.h:539
    #4 0x55f6c6671bb6 in zpaq_decompress_buf ../stream.c:446
    #5 0x55f6c6671bb6 in ucompthread ../stream.c:1566
    #6 0x7fa7df503608 in start_thread /build/glibc-SzIz7B/glibc-2.31/nptl/pthread_create.c:477
    #7 0x7fa7df0da132 in __clone (/lib/x86_64-linux-gnu/libc.so.6+0x11f132)

0x6140000001ec is located 0 bytes to the right of 428-byte region [0x614000000040,0x6140000001ec)
allocated by thread T2 here:
    #0 0x7fa7df6a0a06 in __interceptor_calloc ../../../../src/libsanitizer/asan/asan_malloc_linux.cc:153
    #1 0x55f6c66e5606 in libzpaq::Array<unsigned char>::resize(unsigned long, int) ../libzpaq/libzpaq.h:114

Thread T2 created by T0 here:
    #0 0x7fa7df5cd815 in __interceptor_pthread_create ../../../../src/libsanitizer/asan/asan_interceptors.cc:208
    #1 0x55f6c6673fbb in create_pthread ../stream.c:125

SUMMARY: AddressSanitizer: heap-buffer-overflow ../libzpaq/libzpaq.cpp:1208 in libzpaq::PostProcessor::write(int)
Shadow bytes around the buggy address:
  0x0c287fff7fe0: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
  0x0c287fff7ff0: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
  0x0c287fff8000: fa fa fa fa fa fa fa fa 00 00 00 00 00 00 00 00
  0x0c287fff8010: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
  0x0c287fff8020: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
=>0x0c287fff8030: 00 00 00 00 00 00 00 00 00 00 00 00 00[04]fa fa
  0x0c287fff8040: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x0c287fff8050: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x0c287fff8060: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x0c287fff8070: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x0c287fff8080: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
Shadow byte legend (one shadow byte represents 8 application bytes):
  Addressable:           00
  Partially addressable: 01 02 03 04 05 06 07 
  Heap left redzone:       fa
  Freed heap region:       fd
  Stack left redzone:      f1
  Stack mid redzone:       f2
  Stack right redzone:     f3
  Stack after return:      f5
  Stack use after scope:   f8
  Global redzone:          f9
  Global init order:       f6
  Poisoned by user:        f7
  Container overflow:      fc
  Array cookie:            ac
  Intra object redzone:    bb
  ASan internal:           fe
  Left alloca redzone:     ca
  Right alloca redzone:    cb
  Shadow gap:              cc
==3510675==ABORTING


