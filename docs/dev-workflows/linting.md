# Code Linting

## Deployment

The deployment process includes automatic linting by VIP Bot. It applies the WordPress-VIP-Go standard not only to PHP files, but also JS files.

## Local linting

To lint automatically with VS Code:

1. Make sure Composer is installed: `composer -v` on the command line to check. If it's installed, you will see version information and a help menu. You need version 2.x.x - not 1.x.x.
    * If it is not installed, follow [Composer's documentation](https://getcomposer.org/doc/00-intro.md) to install it globally on your computer.
2. Install PHP CodeSniffer (phpcs): `composer global require "squizlabs/php_codesniffer=*"`.
3. Install WPVIP coding standards:
 ```
 composer g config allow-plugins.dealerdirect/phpcodesniffer-composer-installer true
 composer g require automattic/vipwpcs
 ```
    * If prompted do you want to move this requirement, say no.
    * If prompted do you want to re-run the command with --dev, say no.
4. Check your installed standards by running `phpcs -i`. If everything is set up correctly, it will say
 ```
 The installed coding standards are MySource, PEAR, PSR1, PSR2, PSR12, Squiz, Zend, WordPress-VIP-Go, WordPressVIPMinimum, VariableAnalysis, WordPress, WordPress-Core, WordPress-Docs and WordPress-Extra
 ```
    * Mac only: if the command doesn't work, or if you are missing some of these standards, try installing iTerm 2 and editing its config file. Type `sudo nano ~/.zshrc` and add the line `export PATH=~/.composer/vendor/bin:$PATH`. Control-x to exit, Y to save modified buffer, Enter to keep the same file name. You will then have to completely quit iTerm 2 and then reopen it so it applies the new setting. Then check the standards again with `phpcs -i`.
    * If the standards still aren't showing, try re-running #3, then check with `phpcs -i` again.
5. Now in VS Code, install the [PHP Sniffer extension](https://marketplace.visualstudio.com/items?itemName=wongjn.php-sniffer).
6. Update your VS Code settings. The quickest way is to open settings, then use the icon in the top right corner that says "Open Settings JSON". Update or add the following settings:
 ```
 {
   "[php]": {
     "editor.defaultFormatter": "wongjn.php-sniffer",
     "editor.tabSize": 4
   },
   "phpSniffer.extraFiles": [
     "**/*.{js}"
   ],
   "phpSniffer.standard": "WordPressVIPMinimum",
   "phpSniffer.executablesFolder": "/Users/yourusernamehere/.composer/vendor/bin/"
 }
 ```
    * Note: You will need to edit the last setting for the executables folder. You can re-run step 3 (the two lines to install the VIP coding standards) and your terminal should say `Changed current directory to` your Composer directory. For example, Elaine's is `/Users/elaineshannon/.composer`. Add `/vendor/bin/` to the end, so for Elaine's the full path for phpSniffer.executablesFolder is `/Users/elaineshannon/.composer/vendor/bin/`.
    * Similarly on Windows, Elaine's Composer path is `C:\Users\elaine\AppData\Roaming\Composer`. Since a backslash is a special character in JSON, escape each one with a duplicate backslash, and also add the `\vendor\bin\` folder at the end - so Elaine's Windows full path for phpSniffer.executablesFolder is `C:\\Users\\elaine\\AppData\\Roaming\\Composer\\vendor\\bin\\`.
7. Completely close and re-open VS Code. Now when a PHP or JS file has focus, you'll see the most recently saved standards warnings in the Problems view. (Click the x and caution icons at the bottom left of your screen, or choose View > Problems from the top menu, to show this view.)
    * It's a good idea to save your work frequently. Each time you save, linting will run again. (It is possible to change this so it lints as you type, but that tends to overload VS Code.)
    * If for some reason you open a file and you're not seeing the linting warnings that you're sure should be there, try closing the file and reopening it.

- Related: [wpVIP documentation on using PHP CodeSniffer](https://docs.wpvip.com/how-tos/php_codesniffer/)

@TODO: Determine a CSS/SCSS standard and apply linting for it as well.