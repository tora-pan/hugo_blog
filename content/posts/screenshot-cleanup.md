+++
title = 'Screenshot Cleanup'
date = 2024-04-29T05:32:33-07:00
draft = false
+++
# Time to automate a bit of your desktop cleanup.

Ah, the cluttered desktop syndrome — a tale as old as time, or at least as old as screens and shots have mingled on our desktops. If you're anything like me, you've ventured into the realm of organizing screenshots, diligently renaming them and ushering them to their rightful places. But alas, time's relentless flow can turn even the most orderly desktop into a labyrinth of scattered images.

Fear not, for I present to you a humble script, a beacon of tidiness amidst the chaos. With it, you can reclaim your desktop serenity. Simply run it as needed or let it dance with the weekly rhythm of a cron job. This script, crafted for our beloved Mac desktops, scours the expanse of your screen for files bearing the familiar mark of screenshots. With grace and precision, it creates subfolders adorned with the timeless attire of year-month and gently guides your images to their cozy abodes within.

Simply save the script below and give it a try for yourselves!

### Script
```python
import os
import re
import shutil


def extract_month_year(filename):
    match = re.search(r'(\d{4})-(\d{2})', filename)
    if match:
        return match.group(1, 2)
    else:
        return None, None


def create_folder_if_not_exists(folder):
    if not os.path.exists(folder):
        os.makedirs(folder)


def move_file(source, destination):
    shutil.move(source, destination)


desktop_path = os.path.join(os.path.expanduser("~"), "Desktop")
files = os.listdir(desktop_path)
screenshots_path = os.path.join(desktop_path, "screenshots")

for file in files:
    if file.startswith('Screenshot'):
        year, month = extract_month_year(file)
        if year and month:
            folder_name = f'{year}-{month}'
            destination_folder = os.path.join(screenshots_path, folder_name)
            create_folder_if_not_exists(destination_folder)
            move_file(os.path.join(desktop_path, file), destination_folder)
```

_Happy Hacking!_
