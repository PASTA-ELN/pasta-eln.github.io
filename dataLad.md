# DataLad
The raw data is the origin of scientific work and has to follow the FAIR principles to be trusted. PASTA uses **DataLad** for the raw data and simplifies it to the typical use of experimental material scientists.

- Each project is a dataset that can be shared, etc. Nesting of datasets is possible in DataLad but not part of the PASTA database implementation.
- Files that end with .md, .rst, .org files are stored in plain-Git. Which implies they are not locked and can be easily changed. (see more below)
- All other files are considered data and stored as git-annex. These files are locked and cannot be changed. But they can be moved, deleted, copied.
- The git-shasum is used to trace a file, if it is moved/copied by the user.

## Unlocked files
Some files can be easily edited, e.g. procedures, while other files are locked to prevent accidental or purposeful manipulation.
- Locked files can be copied, then changed and the original can be destroyed though.

Locked files (protected from editing) are the default and the following list shows the unlocked files (can be edited by the user and these changes will be noticed by PASTA). See DataLad and git-annex for more details.
Unlocked files:
- Markdown files: .md, .rst, .org
- Latex files: .tex
- JSON files: .id_pasta.json (used for PASTA bookkeeping)