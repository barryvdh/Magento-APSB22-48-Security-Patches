**!!We're still analyzing the released patch and are in no means sure that these patches cover the entire solution for the newly found security vulnerabilities, use at your own risk. The best way to keep your Magento shop secure is to upgrade to the latest version.!!**

# Security patches for APSB22-48

This repository contains Magento 2 Patch Files for the recently found security issues on 12-10-2022.
The patch files aim to fix the CVE-2022-35698 and CVE-2022-35689 vulnerabilities.

There is not much information about the exact fix which has been released in the newly released patch versions of Magento. 
To create these patch files we've tried our best to inspect the [2.4.4-p1...2.4.4-p2 diff](https://github.com/magento/magento2/compare/2.4.4-p1...2.4.4-p2.diff) and extract the possible security fixes which seems to be in the Magento template directives.

## Contents

As of now the patch only applies a few fixes in the `Magento/Framework/Filter` namespace which have been extracted from the following commit: [Patch Commit](https://github.com/magento/magento2/commit/11846a1a10539470f2fe1522030ff42d62daa562#diff-adf392bf8e6a1c22dc920c482055f9611acb6b8d5940397d5281e53354230ed8)
While inspecting this commit there also seem to be a lot of fixes in the `Magento/Customer` module, we're currently working on applying these changes aswell.

The `magento/module-customer` patch applies a fix to the Webapi for Customer creation and Customer Confirmation Controller.
- The Webapi patch fixes an issue where it used to be possible to send multiple keys with different capitalized key fields thus possibly ignoring any validation made by Magento.
- The Confirmation Controller is changed to cast a `id` POST parameter to an integer.

The `magento/framework` patch applies a fix to the CMS template directive parsing, a signature is added and a depth check.
We think the cause could be issues with nested CMS directives in Magento 2 and certain customer data being exposed to a XSS attack.

## Installation

Use a package such as [cweagans/composer-patches](https://github.com/cweagans/composer-patches) or [vaimo/composer-patches](https://github.com/vaimo/composer-patches) to apply the correct patch file to your Magento shop.
The patches are to be applied to the `magento/framework` and `magento/module-customer` package.
The correct patch file can be found within the folder corresponding to your Magento 2 version.

## Contributing

Feel free to create missing patch files for your Magento 2 version and create a Pull Request!