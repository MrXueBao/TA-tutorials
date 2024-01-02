# RC0 - Basic Mac Setup

MacOS comes with a terminal and can run most of the same commands as Linux directly. By default the `zsh` shell which was introduced in my last section is used and you can follow the same instructions as Linux to install `oh-my-zsh` and `powerlevel10k` and other plugins to get a nice terminal experience.

This tutorial will cover some basic setup for MacOS and some useful tools to install.

## Compiler

To install a compiler on MacOS, run the following command:

```bash
xcode-select --install
```

The function of this command is similar to `sudo apt install build-essential` on Linux. It will install the `clang` compiler and other tools.

You can verify if it is installed by running `g++ --version` in the terminal. The output should look like this:

```bash
g++ --version
Apple clang version 15.0.0 (clang-1500.1.0.2.5)
Target: arm64-apple-darwin23.0.0
Thread model: posix
InstalledDir: /Library/Developer/CommandLineTools/usr/bin
```

## Homebrew package manager

Homebrew is a package manager for MacOS. It is similar to `apt` on Linux and can be used to install useful command line tools and applications. To install Homebrew, run the following command:

```bash
/bin/bash -c "$(curl -fsSL  https://gitee.com/ineo6/homebrew-install/raw/master/install.sh)"
```

Note that this command is installed from a mirror in China. You may also refer to [tuna mirror](https://mirrors.tuna.tsinghua.edu.cn/help/homebrew/) for more information. The official installation command is as follows:

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

Then, you may run the following command to verify that it is installed, your version may be different:

```bash
brew --version
Homebrew 4.2.2
```

And to fasten the download speed of Homebrew, you may also use [tuna mirror](https://mirrors.tuna.tsinghua.edu.cn/help/homebrew/) to replace the default mirror, the tutorial is in the link.

Then you may install some useful tools with Homebrew:

```bash
brew install orbstack # Install applications
brew install tldr # Install command line tools
```

## Terminal Emulator

The default terminal emulator on MacOS is `Terminal`, which is somewhat outdated. There're many feature-rich terminal emulators on MacOS, such as `iTerm2`, `Alacritty`, `Kitty`, etc. I personally use `warp`, a terminal emulator written in rust. It doesn't need much configuration and has a built-in `Warp AI`. Most of terminal emulators are available on Homebrew, you may install them with the following command:

```bash
brew install --cask iterm2
brew install --cask warp
brew install --cask kitty
```

You may search for detailed instructions on the Internet if you want to use them. Note that if you finished configuration of `oh-my-zsh`, you don't need to configure it again for the new terminal emulator.

## Spotlight Replacement

Spotlight is a built-in search tool on MacOS and is very useful. However, its replacements are even more powerful. Here I recommend `Alfred` and `Raycast`. They are both available on Homebrew:

```bash
brew install --cask alfred
brew install --cask raycast
```

I'm currently using `Raycast`. I don't think I need to introduce it in detail, because its built-in tutorial upon installation is very detailed and easy to understand. You may also search for tutorials on the Internet if you want to use `Alfred`, their functions are similar.

## References

- [Homebrew](https://brew.sh/)
- [Homebrew Tuna Mirror](https://mirrors.tuna.tsinghua.edu.cn/help/homebrew/)
- [Homebrew zhihu tutorial](https://zhuanlan.zhihu.com/p/341831809)
- [iTerm2](https://iterm2.com)
- [kitty](https://sw.kovidgoyal.net/kitty/)
- [Warp](https://www.warp.dev)
- [Raycast](https://www.raycast.com)
- [Alfred](https://www.alfredapp.com)
