## What is rule based cracking in hashcat?
- Sometimes standard wordlist like rockyou is not enough to crack a hash.
- We can use a rule to change the wordlist and rules to it in order to crack a hash.
	- A rule list works by having a set of rules that can append characters to a password, attach characters and subsitutute words with characters.


**`Append Rule`**
- appending a word using a `$` operator before the characters to append with.

Example - `$1, $2 and $a`

**`Attach Rule`**
- attaching a word use a `^` operator before the character to attach with.

Example - `^1, ^2 and ^a`

**`Substitute Rule`**
- Substituting a word or character uses an `s`, followed by the character you want to substitute, followed by the character to be substituted.

Example - `sa@, sa4, sl1`


To make rule based attacks easier you can use a pre-compiled rule list. The one we will run the demo with is OneRuleToRuleThemAll, it is a large rule list that contains more 50,000 rules making it much more effective than creating your own list. 

Some good rules for hashcat hash cracking can be found here - [Hashcat Rules](https://github.com/NotSoSecure/password_cracking_rules/blob/master/OneRuleToRuleThemAll.rule)


## Hashcat with rules
```
hashcat -m 5600 hash.txt rockyou.txt -r rules/OneRuleToRuleThemAll.rule --debug-mode=1 --debug-file=matched.rule
```
