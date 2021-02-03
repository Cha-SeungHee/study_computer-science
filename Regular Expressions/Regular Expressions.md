```
abc…	Letters
123…	Digits
\d	Any Digit
\D	Any Non-digit character
.	Any Character
\.	Period
[abc]	Only a, b, or c
[^abc]	Not a, b, nor c
[a-z]	Characters a to z
[0-9]	Numbers 0 to 9
\w	Any Alphanumeric character
\W	Any Non-alphanumeric character
{m}	m Repetitions
{m,n}	m to n Repetitions
*	Zero or more repetitions
+	One or more repetitions
?	Optional character
\s	Any Whitespace
\S	Any Non-whitespace character
^…$	Starts and ends
(…)	Capture Group
(a(bc))	Capture Sub-group
(.*)	Capture all
(abc|def)	Matches abc or def
```


```
Q1. 
Match	cat.	
Match	896.	
Match	?=+.	
Skip	abc1. 

...\.


Q2. 
Match	can	
Match	man	
Match	fan	
Skip	dan	
Skip	ran	
Skip	pan

[cmf]an


Q3. Not
Match	hog	
Match	dog	
Skip	bog

[^b]og


Q4. Range
Match	Ana	
Match	Bob	
Match	Cpc	
Skip	aax	
Skip	bby	
Skip	ccz

[A-Z][^a-c][^x-z] (Or [A-C][n-p][a-c])


Q5. Repetitions
Match	wazzzzzup	
Match	wazzzup	
Skip	wazup

waz{3,5}up
- a{3} will match 'a' exactly three times
- a{1,3} will match 'a' no more than 3 times, no less than once


Q6. Repetitions 2
Match	aaaabcc	
Match	aabbbbc	
Match	aacc	
Skip	a

a+b*c+
- *: zero or more repetitions
- +: one or more repetitions


Q7. Optional Character
Match	1 file found?	
Match	2 files found?	
Match	24 files found?	
Skip	No files found.

\d+ files? found\?


Q8. White space
Match	1.   abc	
Match	2.	abc	
Match	3.           abc	
Skip	4.abc

\d\.\s+abc


Q9. Starts and ends
Match	Mission: successful
Skip	Last Mission: unsuccessful
Skip	Next Mission: successful upon capture of target

^Mission: successful$


Q10. Capture
Capture	file_record_transcript.pdf	file_record_transcript	
Capture	file_07241999.pdf	file_07241999	
Skip	testfile_fake.pdf.tmp

^(file.+)\.pdf$


Q11. Nested groups
Capture	Jan 1987	Jan 1987 1987	
Capture	May 1969	May 1969 1969	
Capture	Aug 2011	Aug 2011 2011	

(\w+ (\d+))


Q12. Matching Nested Groups
Capture	1280x720	1280 720	
Capture	1920x1600	1920 1600	
Capture	1024x768	1024 768	

(\d+)x(\d+)


Q13.
Match	I love cats	
Match	I love dogs	
Skip	I love logs	
Skip	I love cogs

I love (cat|dog)s
```
