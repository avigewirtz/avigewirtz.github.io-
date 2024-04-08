# Merging two branches

Consider the graph of commits shown below.&#x20;

<figure><img src="../../.gitbook/assets/Group 47 (1).png" alt="" width="563"><figcaption></figcaption></figure>

```bash
~> mkdir mergePractice
~> cd mergePractice/
~/mergePractice> printf "Alice\nBob\nCharlie\nEvan" > names.txt
~/mergePractice> git init
~/mergePractice> git add .
~/mergePractice> git commit -m "first commit"
[master (root-commit) 1079992] first commit
 1 file changed, 4 insertions(+)
 create mode 100644 names.txt
~/mergePractice> git branch test
~/mergePractice> git checkout test
Switched to branch 'test'
~/mergePractice> 

```
