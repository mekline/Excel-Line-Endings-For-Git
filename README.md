# Excel-Line-Endings-For-Git

For reasons unknown, Excel for Mac saves CSV files with a deprecated line ending (\\r). What a pain.

This is a quick & dirty solution inspired by <a href="http://nicercode.github.io/blog/2013-04-30-excel-and-line-endings/">this post</a>. Edit & install this pre-commit hook to fix up line endings in a problematic file before allowing a commit, ensuring that only bare \\n line endings are every committed to the repository.  

It's also the first git hook I wrote, so it's a straightforward example of how hooks work before interesting git checks get involved.  It works in the GithubForMac GUI (allowing the nice red/green line-by-line change highlighting to work properly!!!) 

Usage: 
Copy the file into .git/hooks/ in your repository folder. (Unhide hidden files if you can't find the .git folder.)  Every user must do this, hooks don't sync with repositories!

If some simple search-replaces of line endings diff the file at all, the cleaned-up file is saved over the broken one, the commit fails and you get a warning message reminding you of the annoying Excel workaround too.  Since the file has been updated nicely, the subsequent commit should go through.

Bugs I know about:
* In GithubForMac, sometimes after throwing the error the preview window doesn't show the updated file (i.e. it still shows all lines being deleted and replaced by the ugly single-line file.)  However, if you commit and then check the revision history, the correct/actual commit (of just the lines you really changed) is intact.  Clicking on any other repository and then back into the one your working in refreshes the display for whatever reason.

* Once during testing the search-replace routine produced a file with ugly \\n\\n sequences, and I'm not sure why (probably accidentally and silently reencoded in a text editing program?)
