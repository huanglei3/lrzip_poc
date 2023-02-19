run it:

./lrzip -t file

result:

Decompressing...
AddressSanitizer:DEADLYSIGNAL		2:21%  
=================================================================
==2768766==ERROR: AddressSanitizer: SEGV on unknown address 0x625000010000 (pc 0x7f0bcc1e3d35 bp 0x7f0bc8ae1650 sp 0x7f0bc8ae0db8 T2)
==2768766==The signal is caused by a WRITE memory access.
    #0 0x7f0bcc1e3d34  (/lib/x86_64-linux-gnu/libc.so.6+0xbbd34)
    #1 0x7f0bcc79b37e in __interceptor_memcpy ../../../../src/libsanitizer/sanitizer_common/sanitizer_common_interceptors.inc:790
    #2 0x56108414631a in bufWrite::write(char const*, int) ../libzpaq/libzpaq.h:513
    #3 0x56108410a9ef in libzpaq::ZPAQL::flush() ../libzpaq/libzpaq.cpp:399
    #4 0x561084140dca in libzpaq::ZPAQL::outc(int) ../libzpaq/libzpaq.h:171
    #5 0x561084140dca in libzpaq::PostProcessor::write(int) ../libzpaq/libzpaq.cpp:1188
    #6 0x5610841422ba in libzpaq::Decompresser::decompress(int) ../libzpaq/libzpaq.cpp:1316
    #7 0x561084142c5c in libzpaq::decompress(libzpaq::Reader*, libzpaq::Writer*) ../libzpaq/libzpaq.cpp:1366
    #8 0x561084143171 in zpaq_decompress ../libzpaq/libzpaq.h:539
    #9 0x5610840d3bb6 in zpaq_decompress_buf ../stream.c:446
    #10 0x5610840d3bb6 in ucompthread ../stream.c:1566
    #11 0x7f0bcc670608 in start_thread /build/glibc-SzIz7B/glibc-2.31/nptl/pthread_create.c:477
    #12 0x7f0bcc247132 in __clone (/lib/x86_64-linux-gnu/libc.so.6+0x11f132)

AddressSanitizer can not provide additional info.
SUMMARY: AddressSanitizer: SEGV (/lib/x86_64-linux-gnu/libc.so.6+0xbbd34) 
Thread T2 created by T0 here:
    #0 0x7f0bcc73a815 in __interceptor_pthread_create ../../../../src/libsanitizer/asan/asan_interceptors.cc:208
    #1 0x5610840d5fbb in create_pthread ../stream.c:125

==2768766==ABORTING



