
# System setup.sh 🐚

### Prerequisites

> [!NOTE]
> 1. You need to install Xcode from the App Store or https://xcodereleases.com/ first
> 2. Install Docker from the official website (homebrew does not install the arm version by default) **(Optional)**

### Installation script

> [!CAUTION]
> Don’t forget to change `<your_username>` to your actual username on your mac.
> 
> To find this run:
> ```bash
> cd ~ && pwd
> ```

After you’ve substituted with your specific path, just run the below script

```bash
USER_DIR=/Users/indrajitroy
# Create the .zprofile & .zshrc files
echo >> $USER_DIR/.zprofile
echo >> $USER_DIR/.zshrc

# Install Xcode from App Store or `https://xcodereleases.com/` !!!
# Install Docker from the official website (homebrew does not install the arm version by default)

# Install homebrew
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
## Add homebrew shellenv evalutaion to the top of the .zprofile
## This will help homebrew setup the $PATH before the shell starts
'eval "$(/opt/homebrew/bin/brew shellenv)"' >> $USER_DIR/.zprofile
## Run this to get the homebrew packages available in the current terminal session
eval "$(/opt/homebrew/bin/brew shellenv)"

# Install ruby
brew install ruby
'export PATH="/opt/homebrew/opt/ruby/bin:$PATH"' >> ~/.zshrc
'export GEM_HOME=$HOME/.gem' >> ~/.zshrc
'export PATH=$GEM_HOME/bin:$PATH' >> ~/.zshrc
# If xcode command line tools fails during pos install, run
# sudo xcode-select --reset

# To manage different ruby versions
brew install rbenv

# To manage different flutter versions
brew tap leoafarias/fvm
brew install fvm
fvm install stable
fvm global stable
fvm flutter doctor

# Install VSCode
brew install --cask visual-studio-code
# Install Cursor
brew install --cask cursor
# Install MongoDB Compass
brew install --cask mongodb-compass
# Install Pritunl
brew install --cask pritunl

# Install JetBrains Toolbox
brew install --cask jetbrains-toolbox
## Set JetBrains' toolbox scripts in PATH
'export PATH="$HOME/Library/Application Support/JetBrains/Toolbox/scripts:$PATH"' >> $USER_DIR/.zshrc

## Install the latest Android Studio from the toolbox and install the JBR Java version 11 || 17
## Set JAVA_HOME from JetBrains runtime (make sure to install the `jbr-17.0.14` version from Android Studio)
'export JAVA_HOME="$HOME/Library/Java/JavaVirtualMachines/jbr-17.0.14/Contents/Home"' >> $USER_DIR/.zshrc

## Set Android related env PATHS
'export ANDROID_HOME="$HOME/Library/Android/sdk"' >> $USER_DIR/.zshrc
'export PATH="$PATH:$ANDROID_HOME/platform-tools"' >> $USER_DIR/.zshrc
'export PATH="$PATH:$ANDROID_HOME/tools"' >> $USER_DIR/.zshrc
'export PATH="$PATH:$ANDROID_HOME/tools/bin"' >> $USER_DIR/.zshrc
'export PATH="$PATH:$ANDROID_HOME/emulator"' >> $USER_DIR/.zshrc

# Install Volta
brew install volta
## Set Volta bin in PATH
'export PATH="$HOME/.volta/bin:$PATH"' >> $USER_DIR/.zshrc

# Install Go
brew install go
## Set GOPATH and add go installations to bin
export GOPATH="$HOME/go"
export PATH="$PATH:$GOPATH/bin"
```

> [!NOTE]
> When changing the location of the above setup, please remember to update the [master doc](https://docs.google.com/document/d/1RH1MY--qGnjWJUDGOk4roouI2Si2U9dcbmA4wWa08UY/edit?tab=t.tdacod3gtocz#heading=h.nmgq5tlz1i6w).
