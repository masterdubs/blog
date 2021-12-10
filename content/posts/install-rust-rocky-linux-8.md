---
title: "Install Rust on Rocky Linux 8"
date: 2021-12-10T22:30:19+04:00
draft: False
---


# How to install Rust programing language on Rocky linux 8

### Update and install all the dependencies:
```
sudo dnf update -y
sudo dnf install -y epel-release
sudo dnf install cmake gcc make curl clang -y
```


### Install rustup, nightly release and the nightly WebAssembly 
```
curl https://sh.rustup.rs -sSf | sh
source ~/.cargo/env
rustup default stable
rustup update
rustup update nightly
rustup target add wasm32-unknown-unknown --toolchain nightly
```

### Check if all is correct
```
rustc --version
rustup show
```

