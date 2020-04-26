# flutter-without-android-studio
this is a step by step documentation on how to use flutter from scratch without android studio

**DISCLAIMER:** this method meant for those who have very low-end PCs and those who love playing with command-line tools, if you can't find yourself there i highly encourge you to stop here and use the official and the well-supported Android Studio method.

## What do we need?
* **android-sdk** package (from your repo package manager for example) to provide the basic directory structure, for ubuntu users you can use aptitude to install it `sudo apt install android-sdk`
* [sdkmanager](https://developer.android.com/studio/command-line/sdkmanager) download it from [here](https://developer.android.com/studio#downloads) and seach for `command-line-tools` 
* **Flutter-sdk** download it from [here](https://flutter.dev/docs/get-started/install/linux#get-sdk) 
* [vim](https://github.com/vim/vim) / [neovim](https://github.com/neovim/neovim) or [vscode](https://github.com/microsoft/vscode) or any text editor of your choise, i will use neovim as my text-editor, but you don't really have to
* For (neo)vim users i recommend installing a plug-ins manager (i.e. vim-plug) [coc](https://github.com/neoclide/coc.nvim) then [coc-flutter](https://github.com/iamcco/coc-flutter) very useful plugins while dealing with flutter
* For vs-code users install Flutter plug-in

## Steps:
### Step 1 (perpare your directory structure):
Assuming you had followd the [What do we need]() section above you will have `/usr/lib/android-sdk` directory, create cmdline-tools directory inside it 
```bash
sudo mkdir /usr/lib/android-sdk/cmdline-tools
# unzip the content of command line tools to that folder
sudo unzip /path/for/your/command-line/tools/zip/commandlinetools-linux-*.zip /usr/lib/android-sdk/cmdline-tools
# link the content of /usr/lib/android-sdk/cmdline-tools/tools/bin to /usr/lib/android-sdk/tools/bin 
# because flutter will seach for "/usr/lib/android-sdk/tools/bin" when it need the sdkmanager
sudo ln -s /usr/lib/android-sdk/cmdline-tools/tools/bin/* /usr/lib/android-sdk/tools/bin
# define the environmental variables and add the command line tools to path
# NOTE: i will use ~/.profile but for a matter of preference but most people will prefer using .xrc (where x is (zsh, bash, ...etc) 
echo -e "export ANDROID_SDK_ROOT=/usr/lib/android-sdk\nexport PATH=\$ANDROID_SDK_ROOT/cmdline-tools/tools/bin:\$PATH" >> ~/.profile
```
## Step 2 (Download android-sdk):
This is a list of the very essential packages you should have to be able to run you app
**NOTE:** you will definitely need more than these packages for production (i.e. the google play packages)
```
  Path                        | Version | Description                    | Location                    
  -------                     | ------- | -------                        | -------                     
  build-tools;28.0.3          | 28.0.3  | Android SDK Build-Tools 28.0.3 | build-tools/28.0.3/         
  extras;android;m2repository | 47.0.0  | Android Support Repository     | extras/android/m2repository/
  extras;google;m2repository  | 58      | Google Repository              | extras/google/m2repository/ 
  patcher;v4                  | 1       | SDK Patch Applier v4           | patcher/v4/                 
  platform-tools              | 30.0.0  | Android SDK Platform-Tools     | platform-tools/             
  platforms;android-28        | 6       | Android SDK Platform 28        | platforms/android-28/       
  tools                       | 25.0.0  | Android SDK Tools              | tools/                    
  ```
  so you will download these packages 
  ```bash
  # the packages i have ignored should already exist in on your machine
  # Notice that i didn't installed the latest versions it won't work it's a known issue and flutter's team is working on it
  sdkmanager "build-tools;28.0.3" "extras;android;m2repository" "extras;google;m2repository" "platform-tools" "platforms;android-28"
  ```
  ## Step 3 (The flutter side):
  
