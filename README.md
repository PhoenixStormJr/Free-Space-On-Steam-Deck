# Free-Space-On-Steam-Deck
This short script deletes cache, logs, temporary files, everything I could find that is not necessary. 

WARNING, IT WILL DELETE YOUR SCREENSHOTS TOO!!!

I tested this script on my machine, it freed up space and I didn't lose any save files for any games.

#!/bin/bash
echo "deleting cache"
rm -rf ~/.cache/*
echo "deleting app cache"
rm -rf ~/.local/share/Steam/appcache/*
echo "deleting logs"
rm -rf ~/.local/share/Steam/logs/*
echo "deleting screenshots"
rm -rf ~/.local/share/Steam/screenshots/*
echo "deleting thumbnails"
rm -rf ~/.thumbnails/*
echo "deleting cached thumbnails"
rm -rf ~/.cache/thumbnails/*
echo "deleting shader cache"
rm -rf ~/.local/share/Steam/steamapps/shadercache/*
rm -rf ~/.local/share/Steam/steam/cached/*
echo "deleting steam cache"
rm -rf ~/.steam/steam/appcache/*
rm -rf ~/.steam/steam/depotcache/*
rm -rf ~/.steam/steam/logs/*
rm -rf ~/.steam/steam/steamapps/shadercache/*
rm -rf ~/.steam/steam/steam/cached/*
echo "deleting temporary files I found luckily"
rm -rf ~/.local/share/Steam/steamapps/workshop/temp/*
rm -rf ~/.local/share/Steam/steamapps/temp/*
echo "Deleting cache I found luckily"
rm ~/.local/share/mime/mime.cache
rm -rf ~/.local/share/flatpak/repo/tmp/cache/*
rm -rf ~/.local/share/Steam/config/htmlcache/*
rm -rf ~/.local/share/Steam/depotcache/*
rm -rf ~/.local/share/Steam/userdata/1928087934/config/licensecache/*
STEAM_PROTON_DIR="$HOME/.local/share/Steam/steamapps/common"
echo "Searching for __pycache__ folders in Proton installations..."
# Find all __pycache__ directories and delete their contents
find "$STEAM_PROTON_DIR" -type d -name "__pycache__" | while read -r dir; do
    echo "Deleting contents of $dir"
    rm -rf "$dir"/*
done
echo "All Proton __pycache__ folders cleaned."
STEAM_USERDATA_DIR="$HOME/.local/share/Steam/userdata"
echo "Searching for librarycache folders..."
# Find all librarycache directories inside user IDs and delete them
find "$STEAM_USERDATA_DIR" -type d -name "librarycache" | while read -r dir; do
    echo "Deleting contents of $dir"
    rm -rf "$dir"/*
done
echo "All Steam librarycache folders cleaned."
STEAM_USERDATA_DIR="$HOME/.local/share/Steam/userdata"
echo "Searching for ugcmsgcache folders..."
# Find all ugcmsgcache directories inside user IDs and delete their contents
find "$STEAM_USERDATA_DIR" -type d -name "ugcmsgcache" | while read -r dir; do
    echo "Deleting contents of $dir"
    rm -rf "$dir"/*
done
echo "All Steam ugcmsgcache folders cleaned."
echo "doing flatpak cleaning"
flatpak uninstall --unused -y
#Optionally delete flatpak user data. But may be too risky so I blacked it out.
#flatpak remove --delete-data
flatpak repair
echo "deleting sneaky logs"
find ~/.local/share -name "*.log" -type f -delete
