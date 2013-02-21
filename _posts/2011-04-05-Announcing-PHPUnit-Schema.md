---

layout: post
title: Announcing PHPUnit Schema
tags: [php, testing, phpunit, xml, tools]

---

When working with [PHPUnit's XML Config file][1], it can be somewhat tedious to remember all the possible configuration elements and how they should be written. For this purpose, I have assembled a PHPUnit Schema file to assist in authoring PHPUnit configuration files. And since I figured I am not the only one who could find that useful, I decided to share with you. [The PHPUnit-Schema is available on GitHub][2]. Contributions and corrections are welcome. If you want to participate in maintaining and/or improving the file, feel free to fork at will. Pull requests are always welcome.

## Usage
To apply the Schema to a configuration file, you have to declare the Schema Namespace and the location of the Schema file in the phpunit.xml file. Since PHPUnit does not use a dedicated namespace for the configuration file, the following two lines are all that is required:

{:.prettyprint .linenums .lang-xml}
    <?xml version="1.0" encoding="UTF-8">
    <phpunit
        xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:noNamespaceSchemaLocation="location of xsd file"
    …

Assuming you are working with a Schema-aware editor (like Eclipse) you should get Content Assist and limited Code Completion then:

![PHPUnit Code Completion in Zend Studio][3]

## Notes

The Schema file is currently split into multiple smaller files. This eases maintaining the Schema file during development for me. But it's somewhat inconvenient, if you just want the Schema file for Content Assist. For this purpose, you can create a single phpunit.xsd with the PHP script given in the tools folder:

    $ php generate-schema.php
    Created new validated Schema file at:
    F:\Work\code\PHPUnit-Schema\tools\phpunit.xsd.1301999633


  [1]: http://www.phpunit.de/manual/current/en/appendixes.configuration.html
  [2]: https://github.com/gooh/phpunit-schema
  [3]: {{ JB.POST_ASSET_PATH }}/2011-04-05/ContentAssist.png
