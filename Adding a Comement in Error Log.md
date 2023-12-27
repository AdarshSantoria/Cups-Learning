
# Adding a Comement in Error Log.md
## Steps
- Locate the log.c file in scheduler directory of cups.
- Locate the line `cupsFilePrintf(ErrorFile, "%c %s %s\n", levels[level], cupsdGetDateTime(NULL, LogTimeFormat), message);` and modify it with `cupsFilePrintf(ErrorFile, "%c %s %s\n Hey, I am adding a comment\n", levels[level], cupsdGetDateTime(NULL, LogTimeFormat), message);` in the file.
- - `cupsFilePrintf`: Defined Function in log.c used for printing in log.c.
  - `ErrorFile` : Defines the file to print the log. If replaced with `AccessFile`, it will print in access_log file.
- Rebuild the CUPS system to apply the changes and print something, Now we will find  this comment `Hey, I am adding a comment\n` inside the error_log file in `/home/adarsh/cups/build/var/log/cups`.

Here is the log with comments.
```
W [27/Dec/2023:18:37:57 +0530] [Job 1] The printer is unreachable at this time.
 Hey, I am adding a comment
```
