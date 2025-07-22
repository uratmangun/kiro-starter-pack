---
description: Synchronizes hook filenames to match their internal 'name' values, converting spaces to dashes and ensuring uppercase format
---
Please synchronize all hook filenames in the .kiro/hooks directory to match their internal 'name' values. For each .kiro.hook file:

1. Read the JSON content of each hook file
2. Extract the 'name' value from the JSON
3. Convert the name to the proper filename format:
   - Replace spaces with dashes
   - Keep uppercase format
   - Add .kiro.hook extension
   - Example: "GIT PUSH AUTO" becomes "GIT-PUSH-AUTO.kiro.hook"
4. If the current filename doesn't match the expected filename based on the name value, rename the file
5. Report which files were renamed and their new names

Process all hook files in the .kiro/hooks directory and ensure consistency between internal names and filenames.