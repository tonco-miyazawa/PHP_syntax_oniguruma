# How to test Oniguruma 6.9.10 with PHP 8.4.6

First, install [Oniguruma 6.9.10](https://github.com/kkos/oniguruma/releases/tag/v6.9.10) or [the Oniguruma's current master branch](https://github.com/kkos/oniguruma/archive/refs/heads/master.zip) etc.. See [Oniguruma: Install](https://github.com/kkos/oniguruma?tab=readme-ov-file#install) .
  
  
Apply [add_option_o.patch](https://github.com/tonco-miyazawa/PHP_syntax_oniguruma/blob/main/add_option_o.patch) to [php-8.4.6/ext/mbstring/php_mbregex.c](https://github.com/php/php-src/blob/php-8.4.6/ext/mbstring/php_mbregex.c) .  
`$ patch -u < add_option_o.patch` 

This patch makes option '`o`' means `ONIG_SYNTAX_ONIGURUMA`.  

This patch only enables the following three encodings:  

```
OnigEncoding encs[3];
encs[0] = ONIG_ENCODING_UTF8;
encs[1] = ONIG_ENCODING_UTF16_BE;
encs[2] = ONIG_ENCODING_UTF16_LE;
```

Add the encoding you need. See [oniguruma/doc/API: enc](https://github.com/kkos/oniguruma/blob/09604e72328401a28aab08020b13ffc5ac828833/doc/API#L107-L140) and [PHP: Supported Character Encodings](https://www.php.net/manual/en/mbstring.supported-encodings.php) .
  
  
  
Enable `mbstring` when installing [PHP 8.4.6](https://www.php.net/downloads.php).  
`$ ./configure --enable-mbstring`  
  
  
Run the test file [mytest](https://github.com/tonco-miyazawa/PHP_syntax_oniguruma/blob/main/mytest).  
`$ php ./mytest`
  
  
(Note) If your PHP is loading an old version of Oniguruma, please replace the library file with the new one.  
  
example:  
  
Path of Oniguruma old library file: `/usr/lib/x86_64-linux-gnu/libonig.so.5.4.0`  
Path of Oniguruma new library file: `/usr/local/lib/libonig.so.5.4.0`  
  
And update Oniguruma library cache files.  
`$ sudo ldconfig`  


## Links:

Oniguruma (Owner: K.Kosako) [https://github.com/kkos/oniguruma](https://github.com/kkos/oniguruma)  
[PHP: github](https://github.com/php/php-src)  
[PHP: web](https://www.php.net/)

[mb_ereg()](https://www.php.net/manual/en/function.mb-ereg.php)  
[mb_ereg_match()](https://www.php.net/manual/en/function.mb-ereg-match.php)  
[mb_ereg_search_init()](https://www.php.net/manual/en/function.mb-ereg-search-init.php)  
[mb_ereg_search_pos()](https://www.php.net/manual/en/function.mb-ereg-search-pos.php)  
[mb_ereg_search_regs()](https://www.php.net/manual/en/function.mb-ereg-search-regs.php)  
[mb_regex_set_options()](https://www.php.net/manual/en/function.mb-regex-set-options.php)  
[mb_check_encoding()](https://www.php.net/manual/en/function.mb-check-encoding.php)  
[PHP: Supported Character Encodings](https://www.php.net/manual/en/mbstring.supported-encodings.php)  

-------------------------

## Contributors

Anonymous awesome PHP engineers.  
https://mevius.5ch.net/test/read.cgi/tech/1663659983/947-  
https://mevius.5ch.net/test/read.cgi/tech/1730202739/1-47  
(Note) Beware of sexual ads.  
