---
tags:
  - personal
  - personal/pkm
created:
modified: 2026-08-02T10:39
published:
sources:
topics:
authors:
  - Jakub
ai-assisted:
hidden:
public: true
---
# Data Folder Desing
- This is a folder where external folders are mounted via [[Folder Bridge Plugin]]
- It currently does not work to move files from vault folder to mounted folders via Obsidian UI
	- Also, some plugins struggle to work with mounted folders like [[Book Search Plugins]]
- Therefore, all the media files are temporarily set to be copied into `temp_data` folder
	- Then Python or AI is used to move this files into mounted folders
- AI is instructed by default to use mounted folders directly without `temp_data`
	- For this it needs to additionally have access to the mounted directory on your system