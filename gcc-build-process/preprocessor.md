# Preprocessor

When C came out, it had no preprocessor. The build process began with the compilation. In The Development of The C Language, Dennis Ritchie, one of the founders of C, states the following:

> Many other changes occurred around 1972-3, but the most important was the introduction of the preprocessor, partly at the urging of Alan Snyder \[Snyder 74], but also in recognition of the utility of the the file-inclusion mechanisms available in BCPL and PL/I. Its original version was exceedingly simple, and provided only included files and simple string replacements: #include and #define of parameterless macros. Soon thereafter, it was extended, mostly by Mike Lesk and then by John Reiser, to incorporate macros with arguments and conditional compilation. The preprocessor was originally considered an optional adjunct to the language itself. Indeed, for some years, it was not even invoked unless the source program contained a special signal at its beginning. This attitude persisted, and explains both the incomplete integration of the syntax of the preprocessor with the rest of the language and the imprecision of its description in early reference manuals.

As is evident, C preprocessor was added for convenience purposes, to extend the functionality of C. Most commonly used for file inclusion, macro expansion, and conditional compilation.&#x20;
