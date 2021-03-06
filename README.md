Finds all the gettext calls that have an inline fallback and moves that fallback
into the messages.po file.  Thus, you can use `___('msgid', 'msgstr')` when you're
writing new code and use this script to clean up afterwards.

poboy won't edit any code files.  Instead, it prints out a unified diff that you
can check for correctness and send to patch.  I didn't want to deal with
rewriting files safely.

### How I use it

Find all the strings that have a fallback:

    poboy locale/en_US/LC_MESSAGES/messages.po --find

Find the strings with a fallback that aren't already in messages.po:

    poboy locale/en_US/LC_MESSAGES/messages.po -an

That's `-a` for `--add` (to the .po file) and `-n` for `--dry_run`.

Show the strings that will be added and the cleanup patch:

    poboy locale/en_US/LC_MESSAGES/messages.po -n

And the fun one, add the strings to messages.po and generate a cleanup patch:

    poboy locale/en_US/LC_MESSAGES/messages.po > poboy.patch


Testing the service hook