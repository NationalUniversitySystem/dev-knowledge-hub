# Code Linting

## Deployment

The deployment process includes automatic linting by VIP Bot. It applies the WordPress-VIP-Go standard not only to PHP files, but also JS files.

## Local linting

To lint automatically with VS Code:

- Follow the instructions in the [wpVIP documentation on using PHP CodeSniffer](https://docs.wpvip.com/how-tos/php_codesniffer/). This will get the correct standards installed.
- Install the [PHP Sniffer extension](https://marketplace.visualstudio.com/items?itemName=wongjn.php-sniffer).
- Add to your VS Code settings file:
```
"phpSniffer.extraFiles": [
"**/*.{js}"
]
```
- Restart VS Code. When a PHP or JS file has focus, you'll now see errors and warnings automatically in the Problems view. (Click the x and caution icons at the bottom left of your screen, or choose View > Problems from the top menu, to show this view.)

@TODO: Determine a CSS/SCSS standard and apply linting for it as well.