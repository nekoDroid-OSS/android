<p align="center">
  <img src="https://github.com/user-attachments/assets/6c006108-f5ba-4449-9736-b5fe04896af7">
</p>

<h1 align="center">nekoDroid</h1>
<p align="center"><i>A simple, feature packed Android ROM.</i></p>

---

# Welcome!
This is nekoDroid's manifest where you use Source Control Tools to fetch and build nekoDroid.

# Minimum requirements
If you want to build Android, your gonna need a somewhat beefy machine. nekoDroid recommends:

- A distro with glibc version 2.17 or later
- 32GB RAM with a 24GB swapfile
- A somewhat modern CPU with 12c/24t
- Atleast 400GB of space

> [!NOTE]
> You shouldn't be building as the `root` user. If you are, please switch to another to avoid conflicts.

Anything above this will work great. nekoDroid Build Servers use 128GB RAM and a CPU with 24c/48t.

## 1. Make your directories
You need to make directories to place the nekoDroid source somewhere. Here's what you need to run:

```sh
mkdir ~/android/neko
mkdir ~/bin
```

## 1.1 Installing dependencies and Repo
For nekoDroid the dependencies you'll need is:

```
bc bison build-essential ccache curl flex g++-multilib gcc-multilib git git-lfs gnupg gperf imagemagick lib32readline-dev lib32z1-dev libelf-dev liblz4-tool libsdl1.2-dev libssl-dev libxml2 libxml2-utils lzop pngcrush rsync schedtool squashfs-tools xsltproc zip zlib1g-dev
```

If you are something like Debian or Ubuntu you can run:

```sh
sudo apt install bc bison build-essential ccache curl flex g++-multilib gcc-multilib git git-lfs gnupg gperf imagemagick lib32readline-dev lib32z1-dev libelf-dev liblz4-tool libsdl1.2-dev libssl-dev libxml2 libxml2-utils lzop pngcrush rsync schedtool squashfs-tools xsltproc zip zlib1g-dev
```

If you are on Ubuntu 23.10 install libncurses5 from 23.04 like:
```sh
wget http://archive.ubuntu.com/ubuntu/pool/universe/n/ncurses/libtinfo5_6.4-2_amd64.deb && sudo dpkg -i libtinfo5_6.4-2_amd64.deb && rm -f libtinfo5_6.4-2_amd64.deb
wget http://archive.ubuntu.com/ubuntu/pool/universe/n/ncurses/libncurses5_6.4-2_amd64.deb && sudo dpkg -i libncurses5_6.4-2_amd64.deb && rm -f libncurses5_6.4-2_amd64.deb
```

While for older versions of Ubuntu just install `lib32ncurses5-dev libncurses5 libncurses5-dev` normally.

If you are on Ubuntu 20.04 or older install `libwxgtk3.0-dev` and if you are on Ubuntu 16.04 or older install `libwxgtk2.8-dev`.

### Java
For nekoDroid you will need OpenJDK 11 which will be included in the source download.

### Python
For nekoDroid you will need python3. Install `python-is-python3`.

### Install repo
Enter the following to install the `repo` binary and make it executable:

```sh
curl https://storage.googleapis.com/git-repo-downloads/repo > ~/bin/repo
chmod a+x ~/bin/repo
```

Now, put the `~/bin` directory in your PATH:

```sh
# set PATH so it includes user's private bin if it exists
if [ -d "$HOME/bin" ] ; then
    PATH="$HOME/bin:$PATH"
fi
```

Then run `source ~/.profile` to update your env.

You have successfully installed the dependencies and repo!

## Configure git
Repo requires you to identify yourself to sync Android. Run the following commands to configure your git identity:

```sh
git config --global user.email "you@example.com"
git config --global user.name "Your Name"
```

Due to the size of some repos, they are configured for `lfs` or `Large File Storage`. To make sure repo is prepared for this run:

```sh
git lfs install
```

## Enabling caching to speed up building
If you want faster builds you might want to turn on `ccache`. To enable it run:
sh
```
export USE_CCACHE=1
export CCACHE_EXEC=/usr/bin/ccache
```

Then you need to specify how much cache you want. For example, we will enable 50GB cache by running:

```sh
ccache -M 50G
```

50G corresponds to 50GB.

## Initialize nekoDroid source
Now that we have all of that covered we can finally fetch nekoDroid's source. Run:

```sh
cd ~/android/neko
repo init -u https://github.com/nekoDroid-OSS/android.git -b fourteen-cat --git-lfs
```

## Download the source
Now to download the source, run:

```
repo sync -c --no-clone-bundle --optimized-fetch --prune --force-sync -j$(nproc --all)
```

> [!NOTE]
> This may take a while depending on your ISP's speed. Just sit back, relax, make your self a cup of coffee/tea/beer and or have a nap in the meantime.

## What's next?
Well now that you have the nekoDroid source, you can go over to the wiki, find your device and find the specific build instructions for your device. 

Once you have done that and have successfully built nekoDroid you can now call your self an elite Android Builder. Enjoy!

# Credits
- [LineageOS](https://lineageos.org)
- [risingOS](https://github.com/RisingTechOSS)
- [crDroid](https://crdroid.net)
- [DerpFest](https://derpfest.org/)
- [Evolution-X](https://evolution-x.org)
- [PixelOS](https://pixelos.org)
