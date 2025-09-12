# Switch JDK environment
## Install JDK11
```
brew install openjdk@11
sudo ln -sfn /opt/homebrew/opt/openjdk@11/libexec/openjdk.jdk /Library/Java/JavaVirtualMachines/openjdk-11.jdk
```

## Install JDK8
```
brew install --cask temurin@8
==> Caveats
temurin@8 is built for Intel macOS and so requires Rosetta 2 to be installed.
You can install Rosetta 2 with:
  softwareupdate --install-rosetta --agree-to-license
Note that it is very difficult to remove Rosetta 2 once it is installed.

==> Downloading https://github.com/adoptium/temurin8-binaries/releases/download/jdk8u422-b05/OpenJDK8U-jdk_x64_mac_hotspot_8u422b05.pkg
==> Downloading from https://objects.githubusercontent.com/github-production-release-asset-2e65be/372924428/3b293381-a815-4340-8f67-1d7ea1699d96?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=releaseassetproduction%2F20240726%2Fus-east
####################################################################################################################################################################################################################################### 100.0%
==> Installing Cask temurin@8
==> Running installer for temurin@8 with sudo; the password may be necessary.
Password:
installer: Package name is Eclipse Temurin
installer: Installing at base path /
installer: The install was successful.
🍺  temurin@8 was successfully installed!
```

## Install Jenv
```sh
brew install jenv
==> Downloading https://formulae.brew.sh/api/formula.jws.json
#=O#-    #        #                                                                                                                                                                                                                          
==> Downloading https://formulae.brew.sh/api/cask.jws.json
#=O#-    #        #                                                                                                                                                                                                                          
==> Downloading https://ghcr.io/v2/homebrew/core/jenv/manifests/0.5.7
####################################################################################################################################################################################################################################### 100.0%
==> Fetching jenv
==> Downloading https://ghcr.io/v2/homebrew/core/jenv/blobs/sha256:35224b1400c377abd56e99f5e6caec0b48672a935cd3eb250046cf5ab107948e
####################################################################################################################################################################################################################################### 100.0%
==> Pouring jenv--0.5.7.all.bottle.tar.gz
==> Caveats
To activate jenv, add the following to your shell profile e.g. ~/.profile
or ~/.zshrc:
  export PATH="$HOME/.jenv/bin:$PATH"
  eval "$(jenv init -)"
==> Summary
🍺  /opt/homebrew/Cellar/jenv/0.5.7: 87 files, 80.6KB
==> Running `brew cleanup jenv`...
Disable this behaviour by setting HOMEBREW_NO_INSTALL_CLEANUP.
Hide these hints with HOMEBREW_NO_ENV_HINTS (see `man brew`).
```

### Config zsh for jenv
```sh
export PATH="/opt/homebrew/opt/scala@2.12/bin:$PATH" >> ~/.zshrc
eval "$(jenv init -)" >> ~/.zshrc
source ~/.zshrc 
jenv enable-plugin export
# add JDK
jenv add /Library/Java/JavaVirtualMachines/temurin-8.jdk/Contents/Home
jenv add /Library/Java/JavaVirtualMachines/openjdk-11.jdk/Contents/Home
```

### How to use jenv
```sh
jenv versions
* system (set by /Users/xavierzyxue/.jenv/version)
  1.8
  1.8.0.422
  11
  11.0
  11.0.24
  openjdk64-11.0.24
  temurin64-1.8.0.422

jenv global 1.8
java -version
openjdk version "1.8.0_422"
OpenJDK Runtime Environment (Temurin)(build 1.8.0_422-b05)
OpenJDK 64-Bit Server VM (Temurin)(build 25.422-b05, mixed mode)
```

# Ref
`https://www.yhz.me/posts/ma-java-multiple-versions/`
`https://blog.csdn.net/Wbl752134268/article/details/128417866`