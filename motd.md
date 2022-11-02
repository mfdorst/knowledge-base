# Make a cool looking ASCII art MOTD
_Note: Works on Ubuntu, may or may not break on other systems_

Install `figlet`.

Edit `/etc/update-motd.d/00-header`:
```
echo "\n\e[32mWelcome to"
figlet $(hostname) -f slant
printf "\n\e[34m%s (%s %s %s)\e[0m\n" "$DISTRIB_DESCRIPTION" "$(uname -o)" "$(uname -r)" "$(uname -m)"
```

This should result in something like this:
```
Welcome to
    ____  _                     __    
   / __ \(_)________ __________/ /___ 
  / /_/ / / ___/ __ `/ ___/ __  / __ \
 / _, _/ / /__/ /_/ / /  / /_/ / /_/ /
/_/ |_/_/\___/\__,_/_/   \__,_/\____/ 
                                      

Ubuntu 22.04.1 LTS (GNU/Linux 5.15.0-52-generic x86_64)
```
