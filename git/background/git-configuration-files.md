# Git configuration files

Git configuration files are all simple text files in the style of .ini files. The configura‐ tion files are used to store preferences and settings used by multiple git commands. Some of the settings represent personal preferences (e.g., should a color.pager be used?), others are important for a repository to function correctly (e.g., core



Hierarchy of configuration files

Figure 1-6 represents the Git configuration files hierarchy in decreasing precedence:

.git/config

Repository-specific configuration settings manipulated with the --file option or by default. You can also write to this file with the --local option. These settings have the highest precedence.

\~/.gitconfig

User-specific configuration settings manipulated with the --global option.

/etc/gitconfig

System-wide configuration settings manipulated with the --system option if you have proper Unix file write permissions on the gitconfig file. These settings have the lowest precedence. Depending on your installation, the system settings file might be somewhere else (perhaps in /usr/local/etc gitconfig) or may be absent entirely.
