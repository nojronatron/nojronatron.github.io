# Class08 Reading Notes

## References

The [Rule of Three (Computer Programming)](https://en.wikipedia.org/wiki/Rule_of_three_(computer_programming))

YAGNI [You Aren't Gonna Need It](https://en.wikipedia.org/wiki/You_aren%27t_gonna_need_it)

MVP [Minimum Viable Product](https://en.wikipedia.org/wiki/Minimum_viable_product)

DRY [Don't Repeat Yourself](https://en.wikipedia.org/wiki/Don%27t_repeat_yourself)

## The Rule of Three

"Three Strikes and Refactor!"  
When developing code, the 3rd time that similar code is written, it should be a candidate for code within a helper function.  
On the flip-side, refactoring code *to early* can cause more code problems in the future when requirements change or are added.  
Two instances of similar code is probably fine, three instances is time to reconsider, more than 3 => a refactoring plan should be put in place.  

## You Aren't Gonna Need It

Saying arose from Extreme Programming (XP).  
Basically *do not add functionality until it is absolutely necessary*.  
"Do the simplest thing that could possibly work".  

## Minimum Viable Product

An MVP is a product "...with just enough features to the usable..." *[Wikipedia, accessed 25-May-22, see References above]*  
Purpose is to provide a working product that can be used and from which feedback can be drawn to determine the next phase of development neededd to meet end-users needs.  
Validate a business hypothysis through experimenting...with ann App.  

- Use minimal resources  
- Only the least amount of functionality is necessary  
- Get product to customers as early in the development cycle as possible  
- Can help find a base for other Apps/products  
- Validate builder's capabilities / Readiness to develop the product  
- Rapidly build a brand  

Steve Blank said (paraphrased) "Sell the vision, deliver the mvp to visionaries."  

### Critisism

Releasing an MVP too early or as a copy-cat can actually injure the reputation of the developer / company.  
Releasing an MVP that is TOO MINIMAL injures the company, team, and product as it is incomplete and does not meet user expectations.  
Testing ideas in the market is risky business especially in areas where Intellectual Property is a major concern.  

MVE - Minimum Viable Experiment - and MAP - Minimum Awesome Product - are two new approaches that have surfaced through criticism of MVP.  

## Don't Repeat Yourself

Reduce repetition in software development patterns through reuse and advanced software development techniques and principles.  

- Utilize abstractions
- Apply [data normalization techniques](https://en.wikipedia.org/wiki/Canonical_form#Computing)
- Develop functions that are easily reused  
- Arrange the object hierarchy so inheritance members can be automatically applied and overridden when needed  

Take a peek at [this book by Andrew Hunt and David Thomas (Addison Wesley)](https://en.wikipedia.org/wiki/The_Pragmatic_Programmer)  

### When Applied Properly

Modifications are only necessary in the directly-affected portions of the system, and not beyond.  
Less code is written and commonly-used logic is modularized and reused.  
Related elements are kept in sync and change predictably.  

### Challenges with DRY

Simply applying DRY because it exists might not be the right solution for a project.  
Forcing abstractions at every turn can cause a codebase to become rigid and difficult to refactor (rising costs as it ages).  
There are arguments that principles of abstraction and DRY should be applied *when not doing so becomes a barrier to the product*.  
Kent C. Dodds coined the acronym AHA - Avoid Hasty Abstractions - that talks to the previous statements.  

## Footer

Return to [Parent Readme.md](../README.html)  
