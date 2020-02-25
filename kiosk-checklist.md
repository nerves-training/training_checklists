# Kiosk Training Prep

We'll be using a few programs in the training class. Please try to install these
beforehand to save time.

Here's the short list of what's needed:

1. Erlang 22 and Elixir 1.9.4
2. [Qt](https://www.qt.io/)
3. The Nerves archive and required host packages
4. The Phoenix archive

The following checklists should get this done with minimal pain. First work
through the checklist for your OS and then skip to the Erlang checklist.

Many people have had success with [asdf](https://asdf-vm.com/) for managing
Erlang and Elixir versions so the following instructions use it. It's fine to
use other tools.

## OSX checklist

The recommended OSX setup uses Homebrew.

1. Install Xcode from the App Store if you haven't already
2. Setup the Xcode command-line tools:

    ```sh
    xcode-select --install
    ```

3. Install Homebrew from [brew.sh](https://brew.sh)
4. Install required packages for `asdf`, Nerves, and Erlang

    ```sh
    brew install coreutils automake autoconf openssl libyaml readline libtool fwup squashfs wxmac xz picocom
    ```

5. Install Qt

    ```sh
    brew install qt
    ```

6. Go to the Erlang installation checklist

## Linux checklist

1. Use your OS package manager to install required packages for `asdf`, Nerves,
   and Qt

    ```sh
    sudo apt install ssh-askpass squashfs-tools git build-essential libssl-dev libncurses5-dev \
       bc m4 make unzip cmake python autoconf libwxgtk3.0-dev picocom libmnl-dev
    ```

2. Install `fwup` by downloading the .deb or .rpm file from
   [github.com/fhunleth/fwup/releases](https://github.com/fhunleth/fwup/releases).
   Nerves uses this tool as part of the software packaging process.

   ```sh
   sudo dpkg -i ~/fwup_1.5.1_amd64.deb
   ```

3. Install Qt

   ```sh
   sudo apt install qtmultimedia5-dev qtwebengine5-dev qt5-default
   ```

4. Go to the Erlang installation checklist.

## Windows checklist

While some users have had success with Windows Subsystem for Linux, it still
seems like the least painful route is to use Linux VM inside Virtual Box or
VMWare.

1. Verify that USB devices can be made accessible in the Linux VM. The Nerves
   devices used in the class look like an Ethernet interface and it's easiest if
   the Linux VM sees them directly.
2. Follow the Linux checklist.

## Erlang checklist (everyone)

This section uses `asdf` to install Erlang, Elixir, and some archives. You don't
have to use `asdf`, but try to come close on the versions.

1. Install `asdf`. These instructions are copied from
   [asdf-vm.com](https://asdf-vm.com/#/core-manage-asdf-vm), so if there's an
   issue, check there.

    ```sh
    git clone https://github.com/asdf-vm/asdf.git ~/.asdf --branch v0.7.6
    # The following steps are for Bash. If you’re using something else,
    # check asdf-vm.com or adjust accordingly.
    echo -e '\n. $HOME/.asdf/asdf.sh' >> ~/.bashrc
    echo -e '\n. $HOME/.asdf/completions/asdf.bash' >> ~/.bashrc
    # Restart your shell to update the environment - e.g., open a new tab
    ```

2. Install Erlang. OTP 22.2 is recommended.

    ```sh
    asdf plugin-add erlang
    asdf install erlang 22.2.6
    asdf global erlang 22.2.6
    ```

3. Install Elixir 1.9.4. Elixir 1.10 won't work yet.

    ```sh
    asdf plugin-add elixir
    asdf install elixir 1.9.4-otp-22
    asdf global elixir 1.9.4-otp-22
    ```

4. Verify that Erlang and Elixir work by running observer:

    ```sh
    $ iex
    iex(1)> :observer.start
    ```

5. Make sure that `mix` has downloaded the `hex` archive:

   ```sh
   mix local.hex
   ```

6. Install the Nerves archive:

   ```sh
   mix archive.install hex nerves_bootstrap
   ```

7. Install the Phoenix archive:

   ```sh
   mix archive.install hex phx_new
   ```

## What to bring

IMPORTANT: If you're bringing a work laptop, please double check that a corporate firewall
doesn't interfere with using the USB ports.

Also bring:

1. A wired Ethernet adapter if your laptop doesn't have a built-in port. We will be supplying short Ethernet cables.
2. A MicroSD card reader/writer. If your laptop has a built-in SDCard reader, that will work with a MicroSD card adapter.
