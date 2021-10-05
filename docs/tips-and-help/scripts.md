# Scripts
Small bits of code to automate or speed up your tasks.

## NPM
- Install an [NPM updater](https://www.npmjs.com/package/npm-check-updates) globally `npm i -g npm-check-updates` and run it every other week. This can executed as `ncu -g` and it will give you a command to update your global packages.
- To _view_ globally installed packages: `npm list -g --depth=0`

## Aliases (bash/shell)
A list of shorthand aliases for multiple commands.
```bash
# A fresh build in our builds.
alias npmfresh='rm -rf node_modules/ && npm i && npx gulp build';

# Concatenate a series of sql files (handy when importing DB dumps).
alias sqlall='cat *.sql > all_files.sql';

# Handy for when installing/updating dependabot related composer branches. gcu = gitcomposerupdate
alias gcu='rm -rf vendor && composer clearcache && composer install';

# Update vendor autoload for composer.
alias cdo='composer dump-autoload -o'

# Hard drive filling up due to all those `node_modules` folders? Delete all node_modules folders inside current folder.
alias dumpnodemodules="find . -name 'node_modules' -type d -prune -print -exec rm -rf '{}' \;";
```

## Functions (bash/shell)
```bash
# Load the shell dotfiles, and then some!
# * Basically...split your .bash_profile or .zshrc file(s) into multiple files to keep things organized.
# * ~/.path can be used to extend `$PATH`.
# * ~/.extra can be used for other settings you don’t want to commit.
for file in ~/.{path,bash_prompt,exports,aliases,functions,extra}; do
  [ -r "$file" ] && source "$file"
done
unset file

# `cd` into any of your local vagrant/vvv local sites.
# * It accepts a parameter as an alternate folder for the default `public_html`.
cdvvv() {
  if [ -z "$2" ]; then
    files_folder="public_html"
  else
    files_folder="$2"
  fi

  cd ~/vagrant-local/www/$1/$files_folder/wp-content/
}

# Update all your WPVIP "mu-plugin" folders at once!
# @TODO Functionality if `public_html` is not the default folder.
updatevipmu() {
  RED='\033[01;31m'
  BLUE='\033[01;34m'
  NC='\033[00m' # No color
  sites=( "site1" "site2" "site3" ); # site-slugs in your config.yml for VVV

  for i in "${sites[@]}"
  do
    echo -e "${BLUE}Updating mu-plugins for${NC} ${RED}'${i}'${NC}"
    cd ~/vagrant-local/www/$i/public_html/wp-content/mu-plugins/
    git pull
  done
}

# Requires vassh, which at the time or writing is only available for Mac.
updatewpcores() {
  RED='\033[01;31m'
  BLUE='\033[01;34m'
  NC='\033[00m' # No color
  sites=( "site1" "site2" "site3" ); # site-slugs in your config.yml for VVV

  for site in "${sites[@]}"
  do
    echo -e "${BLUE}Updating WP core for${NC} ${RED}'${site}'${NC}"
    cd ~/vagrant-local/www/$site/public_html/
    vassh wp core update
  done
}

```
