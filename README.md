# Smoothie on Debian

## Getting Started
Let's do a basic rundown of the items, we are downloading and installing:
1. Vapoursynth
2. SVPFlow
3. VS-Frameblender
4. FFmpeg
5. Smoothie & VS-Frameblender Repositories

## Installing Vapoursynth
You will first need to add https://deb-multimedia.org/ to our sources list.

In your terminal:
```bash
sudo nano /etc/apt/sources.list
```

Add `deb [trusted=yes] https://www.deb-multimedia.org bullseye main non-free`
```
deb http://deb.debian.org/debian bullseye main
deb http://deb.debian.org/debian bullseye-updates main
deb http://security.debian.org/debian-security bullseye-security main
deb http://ftp.debian.org/debian bullseye-backports main
deb [trusted=yes] https://www.deb-multimedia.org bullseye main non-free
```
Adding `[trusted=yes]` makes any added repository trusted by `apt`.

Save the file.

Now install the repository's GPG key.
`sudo apt-get install deb-multimedia-keyring`

Now run `sudo apt update` and upgrade any packages, if needed.

Finally -> `sudo apt install vapoursynth`.

## Setting up the Dependencies

### Downloading
Make sure to install `git, ffmpeg & curl` first. (`sudo apt install git ffmpeg curl`)       
Make a new directory for Smoothie and any files related to it, so its easier to manage.             
        
First clone the following repositories:
```
git clone https://github.com/couleur-tweak-tips/smoothie      
git clone https://github.com/couleurm/vs-frameblender
```

After that download SVPFlow: https://www.svp-team.com/files/gpl/svpflow-4.3.0.168.zip               
Create a new directory with the name of `plugins` in the Smoothie folder.

Then unzip `svpflow-4.3.0.168.zip` and dump the .so files present in `lib-linux`.      
In the `plugins` directory run: 
```
curl https://github.com/couleurm/vs-frameblender/releases/download/1.2/vs-frameblender-1.2.so -o vs-frameblender-1.2.so
```

### Setting up Vapoursynth's conf file       
We will need to specify a directory from which vapoursynth will auto-load our dependencies from.       

Begin by: `sudo nano ~/.config/vapoursynth/vapoursynth.conf`    
The file should look like this:          
```
UserPluginDir=/home/user/vapoursynth
```
Note: `Path to the 'plugins' directory, you created. (Provide the absolute path.)`        
Save the file.   
                  
## Running Smoothie
To use Smoothie use the following command in the cloned repository's directory: `python3.9 ./smoothie.py`

Example Usage: `python3.9 ./smoothie.py -i video.mp4`

Edit the config file present in `/settings/recipe.ini`.

## Troubleshooting
1. VS-Frameblender not being imported/detected by Vapoursynth.      
    > I actually encountered this issue when setting up Smoothie on a WSL instance initally.   
    Incase if VS-Frameblender isn't being detected, you might need to compile it on your machine.
    1. Install `clang` | `sudo apt install clang`
    2. Then in the cloned repository of vs-frameblender run: 
    ```
    clang++ main.cpp -shared -std=c++17 -I vapoursynth -o foo.so -fPIC`
    ```
    3. Copy `foo.so` to the vapoursynth plugins directory.


