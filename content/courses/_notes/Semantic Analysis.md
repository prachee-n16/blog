- once sentence structure is understood, we can try to understand the meaning of the sentence
	- however, understanding meaning of programs automatically is too hard

Example: `I saw a man on a hill with a telescope.`
- Interpretation 1: There's a man on a hill, I am watching him with my telescope
- Interpretation 2: There's a man on a hill, I see him and he has a telescope
- Interpretation 3: There's a man, and he's on a hill that also has a telescope

Example: `Jack said Jack left his assignment at home.`
- How many Jacks are we referring to? Is he referring to himself?

To avoid these ambiguities, programming languages define strict rules.
```
{
	int Jack = 3;
	{
		int Jack = 4;
		cout << Jack;
	}
}
```
- In C++, the C++ code prints 4 because it uses the definition of the variable within the scope of the statement. Here, scope is defined by `{}`
This stage results in an '[[Intermediate Languages|Intermediate Representation]]' which moves to the next stage.
