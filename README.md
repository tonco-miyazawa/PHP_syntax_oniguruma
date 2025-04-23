# How to test Oniguruma 6.9.10 with PHP 8.4.6

First, install [Oniguruma 6.9.10](https://github.com/kkos/oniguruma/releases/tag/v6.9.10).

Apply [add_option_o.patch](https://github.com/tonco-miyazawa/PHP_syntax_oniguruma/blob/main/add_option_o.patch) to [php-8.4.6/ext/mbstring/php_mbregex.c](https://github.com/php/php-src/blob/php-8.4.6/ext/mbstring/php_mbregex.c) . `$ patch -u < add_option_o.patch`

Enable `mbstring` when installing [PHP 8.4.6](https://www.php.net/downloads.php). `$ ./configure --enable-mbstring`

Run the [test file](https://github.com/tonco-miyazawa/PHP_syntax_oniguruma/blob/main/mytest). `$ php ./mytest`

(Note) If your PHP is loading an old version of Oniguruma, please overwrite the library file with the new one.  

This patch only enables the following three encodings:
`ONIG_ENCODING_UTF8`, `ONIG_ENCODING_UTF16_BE`, `ONIG_ENCODING_UTF16_LE`.  
Add the encoding you need.

-------------------------
## Contributors

Anonymous awesome PHP engineers  
https://mevius.5ch.net/test/read.cgi/tech/1663659983/947-  
https://mevius.5ch.net/test/read.cgi/tech/1730202739/1-47  
(Note) Beware of sexual ads.





