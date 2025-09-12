# Install Iterm2
```sh
brew info iterm2
==> iterm2: 3.5.3 (auto_updates)
https://iterm2.com/
Not installed
From: https://github.com/Homebrew/homebrew-cask/blob/HEAD/Casks/i/iterm2.rb
==> Name
iTerm2
==> Description
Terminal emulator as alternative to Apple's Terminal app
==> Artifacts
iTerm.app (App)
==> Analytics
install: 22,961 (30 days), 71,146 (90 days), 282,092 (365 days)
xavierzyxue@xue work % brew install iterm2
==> Downloading https://iterm2.com/downloads/stable/iTerm2-3_5_3.zip
####################################################################################################################################################################################################################################### 100.0%
==> Installing Cask iterm2
==> Moving App 'iTerm.app' to '/Applications/iTerm.app'
🍺  iterm2 was successfully installed!
```

# Install [oh-my-zsh](https://github.com/ohmyzsh/ohmyzsh)
```sh
sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
zsh: command not found: #
Cloning Oh My Zsh...
remote: Enumerating objects: 1397, done.
remote: Counting objects: 100% (1397/1397), done.
remote: Compressing objects: 100% (1335/1335), done.
remote: Total 1397 (delta 41), reused 813 (delta 33), pack-reused 0
Receiving objects: 100% (1397/1397), 3.19 MiB | 3.06 MiB/s, done.
Resolving deltas: 100% (41/41), done.
From https://github.com/ohmyzsh/ohmyzsh
 * [new branch]      master     -> origin/master
branch 'master' set up to track 'origin/master'.
Already on 'master'
/Users/xavierzyxue

Looking for an existing zsh config...
Found /Users/xavierzyxue/.zshrc. Backing up to /Users/xavierzyxue/.zshrc.pre-oh-my-zsh
Using the Oh My Zsh template file and adding it to /Users/xavierzyxue/.zshrc.

         __                                     __
  ____  / /_     ____ ___  __  __   ____  _____/ /_
 / __ \/ __ \   / __ `__ \/ / / /  /_  / / ___/ __ \
/ /_/ / / / /  / / / / / / /_/ /    / /_(__  ) / / /
\____/_/ /_/  /_/ /_/ /_/\__, /    /___/____/_/ /_/
                        /____/                       ....is now installed!


Before you scream Oh My Zsh! look over the `.zshrc` file to select plugins, themes, and options.

• Follow us on X: @ohmyzsh
• Join our Discord community: Discord server
• Get stickers, t-shirts, coffee mugs and more: Planet Argon Shop
```

# Install fonts `https://github.com/powerline/fonts`
```
# clone
git clone https://github.com/powerline/fonts.git --depth=1
# install
cd fonts
./install.sh
# clean-up a bit
cd ..
rm -rf fonts
```

# Change the theme
```sh
vim ~/.zshrc
ZSH_THEME="agnoster"
```

# Ref
`https://github.com/sirius1024/iterm2-with-oh-my-zsh`