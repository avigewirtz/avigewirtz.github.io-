# Quoting

Quoting is a method used to control how Bash interprets and processes special characters and whitespace in strings and commands. There are three types of quoting in Bash: single quotes (' '), double quotes (" "), and backslashes ().

1. Single quotes (' '): Enclosing a string within single quotes (' ') preserves the literal value of each character within the quotes. No variable substitution or command substitution will occur, and all special characters lose their special meaning. For example:
2. Double quotes (" "): Enclosing a string within double quotes (" ") allows variable substitution and command substitution to occur, while preserving the literal value of other characters, including whitespace. For example:
3. Backslash (/): Used as an escape character to remove the special meaning of the following character. It is useful when you want to include a single quote, double quote, or other special characters in a string without invoking their special behavior. For example:
