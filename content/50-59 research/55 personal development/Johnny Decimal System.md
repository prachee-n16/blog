The file organization system I maintain internally is not exposed to the public; it's both to avoid judgement from your discerning eyes and to hide my less-than-perfect attempt at using the Johnny Decimal system. But hey, it works for me! So, here's a little on how I do it:

The process of setting this up is borrowed from: https://johnnydecimal.com/ 

**I have ten shelves, and in each shelf, I could keep at most 10 boxes**; keeping this principle in mind, here we go:
- `10-19 life admin`
	- `11 _notes`
	- `12 me`
	- `13 plans`
	- `14 money`
	- `15 travel`
	- `16 home`
	- `17 health`
	- `18 work`
	- `19 education`
- `20-29 work`
	- `21 _notes`
	- `22 job search`
	- `23 portfolio`
- `30-39 education`
	- `31 _notes`
	- `32 course xx` and so on..
- `40-49 hobbies`
	- `41 reading`
	- `42 puzzles`
- `50-59 research`
	- `51 maths`
	- `52 physics`
	- `53 computer science`
	- `54 data science`

I used https://johnny-decimal-generator.netlify.app/ to help organize this structure initially, and then let it organically grow over time.

A few caveats:
- Education is where I keep notes from courses currently in-progress; Since this is an area I use a lot over study terms, the organization in these folders breaks the usual Johnny Decimal setup. Instead, it mimics how the professor has it organized in Learn
- Eventually, at the end of each study term, I migrate my notes from education to research
- How do I handle **asset management** i.e. screenshots, photos? I dump them all in an \_assets folder that lives in the root level. I don't bother to organize this since I don't ever access them directly (usually, these are media embedded into notes)

