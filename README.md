## Froyocomb Testbed


> [!CAUTION]
> These builds are not to be documented until they reach completion and the manifest and patches are moved into their appropriate folder. Upon completion, they will be upstreamed into the Froyocomb project.

The build that is currently being worked on in this repo is: **MIY71B**

#### Notes:
- Breakpad has a bad example project which must be removed from the source tree.
`rm -rf external/google-breakpad/Android/sample_app/`
- Address sanitation is totally messed up here due to tons of mismatches with upstream Clang. Patches for various Android.mk files will be included.
- This build will ONLY work on arm32 for the time being.
- IFDEF for various libc functions go missing and will be correctly stubbed. Instructions will come later.

> [!TIP]
> Builds like these create a lot of artifacts. If you run into problems related to artifacts after running make clean, run make clobber instead.

#### Setup:

 1. Grab an Ubuntu 14.04 ISO, flavor does not matter here.
 2. Install packages required for building:
```
sudo apt-add-repository ppa:git-core/ppa
sudo apt update
sudo apt upgrade --yes
sudo apt install bc bison build-essential ccache curl flex g++-multilib gcc-multilib git gnupg gperf imagemagick protobuf-compiler lib32readline-dev lib32z1-dev libdw-dev libelf-dev libgnutls28-dev libsdl1.2-dev libssl-dev libwxgtk2.8-dev libxml2 libxml2-utils openjdk-7-jdk pngcrush rsync schedtool squashfs-tools xsltproc zip zlib1g-dev --yes
```
 3. Compile Python 3.6:
```
wget https://www.python.org/ftp/python/3.6.15/Python-3.6.15.tgz
tar -xvf Python-3.6.15.tgz && cd Python-3.6.15
sudo ./configure --enable-optimizations
sudo make -j6 && sudo make install
```
 4. Create directories:
```
mkdir -p ~/bin
mkdir -p ~/android/system
```
 5. Install `repo`:
```
curl https://storage.googleapis.com/git-repo-downloads/repo > ~/bin/repo
chmod a+x ~/bin/repo
```
 6. Edit your shell config (place at the end of .bashrc):
```
if [ -d "$HOME/bin" ] ; then
    PATH="$HOME/bin:$PATH"
fi
```
Then run `source ~.bashrc`.

 7. Initialize repository:
```
cd ~/android/system
repo init -u https://github.com/laniku/froyoc-testbed.git -b main MIY71B.xml --depth=1
repo sync --no-tags --no-clone-bundle -c
```
