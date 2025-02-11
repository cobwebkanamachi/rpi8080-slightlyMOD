clone of https://github.com/erfan-khadem/rpi8080 slightly mod.
<PRE>
usage: 
1) put uf2 into pico under bootsel mode.
2) open serial (ex. teraterm etc).
3) test type something into keyboard then callbacks.
4) type q for exiting callback test.
5) you could entry memory.
   like EE 01(enter) -> 01 address is EE value.
5) type help -> same as original.
6) reboot with R command(same as original).
7) m 0000 -> memory dump (entry check).

I build this with wsl2(Ubuntu).

diff main.c ../../main.c
main.c is original.
../../main.c is mine
163,164c163,175
<
<     stdio_usb_init();
---
>     /*stdio_usb_init();*/
>     stdio_init_all();
>     while (!stdio_usb_connected()) {
>         sleep_ms(100);
>     }
>     printf("Started\n");
>     while (true) {
>         char c = getchar();
>         printf("You typed 0x%02x (%d)\n", c, c);
>       if(c=='q'){
>          break;
>         }
>     }
189a201
>         //int scanf_result = scanf("%x %x", &memory_value, &memory_address);
197c209,210
<             reset_usb_boot(1 << LED_PIN, 0);
---
>             //reset_usb_boot(1 << LED_PIN, 0);
>             break;
</PRE>

Enjoy!
<PRE>>boot -> callback (aiuq entered) -> memory entry(FF 00(enter) FE 01(enter) FD 02(enter)q -> m_0000(enter)</PRE>
<a><img src="https://github.com/cobwebkanamachi/rpi8080-slightlyMOD/raw/main/1.png"></a><BR>
<PRE>after m_0000(enter)</PRE>
<a><img src="https://github.com/cobwebkanamachi/rpi8080-slightlyMOD/raw/main/2.png"></a>
