# explodeTree
PHP function to transform arrays/tables into trees

None of this code is my work, all credit goes to (kvz.io blog)[http://kvz.io/blog/2007/10/03/convert-anything-to-tree-structures-in-php/].

I just have cloned those scripts to keep they with me for my personal use and study. It's a complex task that is performed pretty well (and fairly fast) with these scripts.

You can use it as this:
```php
<?php
# To create an long array of directories and subdirectories
if(exec("find /etc/php5", $files)){
    // the $files array now holds the path as it's values,
    // but we also want the paths as keys:
    $key_files = array_combine(array_values($files), array_values($files));

    // show the array
    print_r($key_files);
}

# to explode the array into a tree structure
// let '/' be our delimiter
$tree = explodeTree($key_files, "/");
// show the array
print_r($tree);
?>
```

The result of `print_r($tree)` should be this:
```php
Array
(
    [etc] => Array
        (
            [php5] => Array
                (
                    [cli] => Array
                        (
                            [conf.d] => /etc/php5/cli/conf.d
                            [php.ini] => /etc/php5/cli/php.ini
                        )
                    [conf.d] => Array
                        (
                            [mysqli.ini] => /etc/php5/conf.d/mysqli.ini
                            [curl.ini] => /etc/php5/conf.d/curl.ini
                            [snmp.ini] => /etc/php5/conf.d/snmp.ini
                            [gd.ini] => /etc/php5/conf.d/gd.ini
                        )

                    [apache2] => Array
                        (
                            [conf.d] => /etc/php5/apache2/conf.d
                            [php.ini] => /etc/php5/apache2/php.ini
                        )
                )
        )
)
```

And if you use `plotTree($tree)` instead, you'll get this:
```php
start
O etc ()
  + php5 (/etc/php5)
    + cli (/etc/php5/cli)
      - conf.d (/etc/php5/cli/conf.d)
      - php.ini (/etc/php5/cli/php.ini)
    + conf.d (/etc/php5/conf.d)
      - mysqli.ini (/etc/php5/conf.d/mysqli.ini)
      - curl.ini (/etc/php5/conf.d/curl.ini)
      - snmp.ini (/etc/php5/conf.d/snmp.ini)
      - gd.ini (/etc/php5/conf.d/gd.ini)
    + apache2 (/etc/php5/apache2)
      - conf.d (/etc/php5/apache2/conf.d)
      - php.ini (/etc/php5/apache2/php.ini)
end
```
