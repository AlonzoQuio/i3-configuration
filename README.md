# start i3
startx

# ibus
To change keyboard layout

# i3blocks
sudo apt install i3blocks

# Save layout
i3-msg "workspace 2: Programming; append_layout /home/alonzo/.config/i3/layouts/programming.json"

# Load layout
i3-msg "workspace 1: Navigation; append_layout /home/alonzo/.config/i3/layouts/workspace-1.json"

# Rearrange
```bash
function apply-layout-to-workspace
  i3-msg append_layout ~/.config/i3/layouts/$argv.json
  sleep 0.05
  while windows-list | gr "N/A N/A" 
    xdotool search --all --onlyvisible --desktop (xprop -notype -root _NET_CURRENT_DESKTOP | cut -c 24-) "" windowunmap windowmap
    sleep 0.05
  end
end
```

https://www.reddit.com/r/i3wm/comments/808685/create_your_own_i3_layouts_that_are_actually/


# Swap workspaces
```bash
#!/usr/bin/env bash
# requires jq

IFS=:
INITIAL_WORKSPACE=$(i3-msg -t get_workspaces \
  | jq '.[] | select(.focused==true).name' \
  | cut -d"\"" -f2)

i3-msg -t get_outputs | jq -r '.[]|"\(.name):\(.current_workspace)"' | grep -v '^null:null$' | \
while read -r name current_workspace; do
    echo "moving ${current_workspace} right..."
    i3-msg workspace "${current_workspace}"
    i3-msg move workspace to output right   
done
```

# GMRUN
edit 
/etc/gmrunrc
add command
URL_l = ${TermExec} 'bash /home/alonzo/.config/i3/layouts/%s'

# keyword manager
sudo apt install ibus
ibus-setup


# Solve opera problems
```console
curl -L -O https://github.com/iteufel/nwjs-ffmpeg-prebuilt/releases/download/0.47.2/0.47.2-linux-x64.zip
unzip 0.47.2-linux-x64.zip
sudo mv libffmpeg.so /usr/lib/x86_64-linux-gnu/opera/
```
https://forums.opera.com/topic/34659/opera-linux-browser-h-264-support-through-x264-open-source-codec/14

# Set theme using gtk3
Download and copy theme folder to
/usr/share/themes

Edit the file ~/.config/gtk-3.0/settings.ini
[Settings]
...
gtk-theme-name=Kripton 
