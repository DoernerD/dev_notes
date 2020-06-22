# Everything bash/zsh related

## Starting applications

    sh ./<application name>

## Writing bash scripts

## Batch renaming of files

Just needed to rename all timestamps from 17:23:18 to 17\_23\_18 (ignore the escape \ ) (thanks Windows... .\m/.). Figured out, that it's a 1.5 liner in zsh
    
    autoload zmv
    zmv -Qwn '**/*(*)' '$1${2//:/_}'

The first line loads zmv, the second line replaces all files according the the specified rules.
Q enables globbing, w the wildcards and n is for testing purpose. The command writes the results to the console without executing it, so we can check the results. 

    '**/*(*)' 

iterates through all directories and subdirectories and looks at each file

    '$1${2//:/_}'

denotes the way we want to change the file name. Since we use two globs, we need $1 for the path and $2 for the filename. The argument in the brackets says, that we take the filename and replace : with \_. 
Run in your desired root directory and all files in all subdirectories will be renamed within seconds. Took a while to find the command, but execting it was a breeze :)

## Renaming Filenames with for loop

    for FILENAME in *; do mv $FILENAME Unix_$FILENAME; done 
    
Also prettu straight forward. (the \$ is not escaped in above line...)

## Running Bash Script in Several Directories

Imagine you want to run your bash script in several sub or subsubdirectories. One option is

    for d in **/*; do
        if [ -d "$d" ]; then
            ( cd "$d" && ../../mycommand.sh )
        fi
    done

This loops through all the directories, cd's into them and executes mycommand.sh. There are
several things to consider:

    1.) Adjust **/* to the depth level you need
    2.) The easiest way to check is with replacing the ( ) with

            echo "$d"

        Then you get the directories in which the command will operate.
    3.) As you adjust **/*, you also need to adjust the path to mycommand.sh accordingly.
    4.) **/* can be also replaced by known folders, e.g. 
    
            in a b; do

        This also supports globs, e.g.

            in *pattern/*; do

        will go into all subdirectories of all directoreies with the ending model_HRN.

## Replacing Strings using sed

This time I wanted to replace the content of line 19 in a file.

    sed -i '19s/ymin.*/ymin=-5,/' file.txt

This replaces the line 19 with ymin=-5, if it fits the pattern. Since I don't know
what's after ymin in the original file, I have to use the wildcard .\* (the asteriks
needs to be escaped in markdown, hence the backslash).

## Comparing 

That's also a fun one. Imagine you've two large directories, e.g. HDD backups to
compare. Using diff or meld directly won't work, because they usually tend to
load both files/directories in the RAM, which with 200+GB directories doesn't
work. So, what to do?

    cd dir1
    du -ah > dir1.txt
    cd dir2
    du -ah > dir2.txt
    diff dir1.txt dir2.txt > dir12_diff.txt
    
You go into each directory and use du -ah to list the content. Pipe the output
directly in a text file and then compare the contents of each text file. You'll
see the difference might be the date, but that's about it, depending on how you
copied the files. 
    
