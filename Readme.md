clone of https://github.com/erfan-khadem/rpi8080 slightly mod.
<PRE>
usage: 
1) put uf2 into pico under bootsel mode.
2) open serial (ex. teraterm etc).
3) test type something into keyboard then callbacks.
4) type q for exiting callback test.
5) type help -> same as original.
you could entry memory something after reboot with R command.

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
