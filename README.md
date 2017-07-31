Custom function for generating a cross-platform compatible fmpurl for opening files and running scripts via the Open URL script step.

This file mostly exists due to [this bug](http://thefmkb.com/11358) and my wanting to do cross-platform testing to confirm I can open/close files and run scripts via fmpurl.


## fmpurl protocol facts

These facts were observed based on tests done by the fmpurl-protocol-tests file on multiple platforms/versions. These were _only_ tested with the `Open URL` script step with the specified file in Documents directory.

1. Account and password cannot be urlencoded
2. Account cannot contain any special characters or text with accents, but a space is fine.
3. Password can only contain these special characters ,;:()$ (of the one's I tested, at least).
   * FM Go is the most restrictive; FM Pro accepted other special characters.
4. Password cannot contain text with accents.
5. The work-around for a bug in iOS 6, 7, and 8 (http://thefmkb.com/11358) will fail if the filename contains spaces (only tested on iOS 9 and 10).
6. Filename cannot be urlencoded.
7. Filename can contain text with accents, spaces, and special characters (I only tested @).
8. If a script name is urlencoded, it can contain any character (of the set tested, at least). Many characters don't even need to be urlencoded, but results will vary across platforms.
   * same applies to script parameter
   * same applies to variable values
9. Variable names were not tested since I never use spaces, special characters, or accents in my variable names.

## Tests that should still be done

1. Re-login to an already open file.
2. Login as [Guest].
3. Login to account without password.
4. Resolve, or document failing tests in fmpurl.fmp12 file, when run from FMGo.
