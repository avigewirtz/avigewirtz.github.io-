# Identifying Build Errors



* preprocessor maro (like PI) used in testcircle.c, where it isn't defined



Preprocessor errors



* \#include "nonexistentfile.h"

\~> gcc main.c

main.c:4:10: fatal error: 'nonexistentfile.h' file not found

\#include "nonexistentfile.h"

&#x20;        ^\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~\~

1 error generated.

\~>&#x20;





* no prototype - compilation error
