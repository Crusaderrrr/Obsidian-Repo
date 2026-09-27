**grep** is a command-line tool for *searching text* using patterns (including regular expressions). Given a pattern and a set of files (or piped input), it prints the lines that match.

*Example*:
```bash
grep "TODO" src/main.py          # find lines containing "TODO" in one file
grep -r "TODO" src/               # recursive: search every file under src/
grep -rn "TODO" src/              # -n adds line numbers
grep -ri "todo" src/              # -i = case-insensitive
grep -rl "TODO" src/              # -l = just list filenames, not the matching lines
grep -rE "TODO|FIXME" src/         # -E enables extended regex (alternation, etc.)
grep -v "TODO" src/main.py        # -v = invert match, show lines that DON'T match
grep -w "log" src/main.py         # -w = match whole word only, not "logger" etc.
grep -A 3 -B 2 "def parse" file.py  # show 3 lines After and 2 lines Before each match
```