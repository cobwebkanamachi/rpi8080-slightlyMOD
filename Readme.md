clone of https://github.com/erfan-khadem/rpi8080 slightly mod.

<PRE>
 diff main.c ../../main.c
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
