[![Build Status](https://travis-ci.org/wormhit/InstallScripts.png?branch=master)]
(https://travis-ci.org/wormhit/InstallScripts)
[![Scrutinizer Quality Score](https://scrutinizer-ci.com/g/wormhit/InstallScripts/badges/quality-score.png?s=bd189bbfc713619cacd5f6d1e1d37caca046a70f)]
(https://scrutinizer-ci.com/g/wormhit/InstallScripts/)
[![Code Coverage](https://coveralls.io/repos/wormhit/InstallScripts/badge.png?branch=master)]
(https://coveralls.io/r/wormhit/InstallScripts?branch=master)

InstallScripts
==============

Module for Zend Framework 2 to perform script execution

It allow you to create scripts that needs to be executed from terminal.



Setup
-----

Install using composer.
---

``` xml
    "require": {
        "wormhit/InstallScripts": "*"
    },
    "repositories": [
        {
            "type": "git",
            "url":  "https://github.com/wormhit/InstallScripts.git"
        }
    ]
```

```sh
php composer.phar update
```


Enable module
---

config/application.config.php
``` php

<?php
return array(
    'modules' => array(s
        '...',
        'InstallScripts'
    ),
);

```


Usage
-----

Setup InstallScripts configuration
---

config/autoload/instal.global.php
``` php
<?php

return array(
    'InstallScripts' => array(
        'StorageAdapter' => array(
            'Adapter' => 'InstallScripts\StorageAdapter\FileStorageAdapter',
            'Options' => array(
                'file' => __DIR__ . '/../../data/install.json', // make sure directory is writable
            )
        ),
        'Scripts' => array(
            // namespace => array( script files )
            'Application' => array(
                'Install\Transactions',
            )
        ),
    )
);

```


Create first script
---

module/Application/src/Application/Install/Transactions.php
``` php
<?php

namespace Application\Install;

use InstallScripts\Script;


class Transactions extends Script
{
    public function __construct()
    {
        set_time_limit(0);
    }

    /**
     * @return array
     */
    public function getVersions()
    {
        return array(
            '0.0.1' => 'MoveDatabase',
            '0.0.2' => 'SomethingElse',
        );
    }

    /**
     * Do some stuff
     */
    public function MoveDatabase()
    {
        $e = $this->getMvcEvent();

        // execute something
        return true;
    }

    /**
     * Do some other stuff
     */
    public function SomethingElse()
    {
        return true;
    }

}

```


Use script
---

![ScreenShot](http://i.imgur.com/aNJcMK5.png)

![ScreenShot](http://i.imgur.com/m6M6r3m.png)

![ScreenShot](http://i.imgur.com/v2LnocW.png)

