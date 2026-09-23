## Bioinformaticians are not software engineers

Lawlor B, Walsh P. Engineering bioinformatics: building reliability, performance and productivity into bioinformatics software. Bioengineered. 2015

<https://pmc.ncbi.nlm.nih.gov/articles/PMC4601517/>

"Although biologists and especially bioinformaticians possess programming skills, and use those skills as part of their day to day work, they do so in a way that is unstructured and not in line with modern standards of software engineering."

Bioinformaticians have programming skills but lack of software engineering infrastructure and techniques.

Segal points out that the “lack of any disciplined testing procedure” is a characteristic of any development practice where the end user is also the developer.^[3](https://pmc.ncbi.nlm.nih.gov/articles/PMC4601517/#cit0003)^

Authors have suggested that the 2 contexts (scientific vs commercial) are “fundamentally different” for reasons of subject domain complexity, requirements volatility and budgetary constraints. These differences make it problematic to “impose software engineering techniques on scientists.

-   **Subject Domain Complexity.** Segal & Morris assert that in the case of scientific software development the subject matter is simply too complex for the “average developer." In a similar vein, Hannay suggests that “developers are much less likely to need to be domain experts” in “regular” software development compared to scientific.^[11](https://pmc.ncbi.nlm.nih.gov/articles/PMC4601517/#cit0011)^

-   **Requirements Volatility.** According to Segal & Morris, “full up-front requirement specifications are impossible” where scientists are concerned, and that requirements rather “emerge” on an ongoing basis. The suggestion is that this is a distinctive feature of scientific programming, which makes the application of software engineering techniques more difficult.

-   **Budget and Resources.** Verma et al. and Umarji et al. cite tighter budget and timetable constraints as a differentiating factor of bioinformatic software development, and therefore as one possible cause of a lack of software engineering best practices in that field.

The elements of software engineering practice that are often absent from bioinformatic teams correspond to those elements which are typically learned by the software engineering apprentice (source control, build systems, unit testing etc).

### Figure 1. Key Components of Software Engineering.

![Figure 1.](https://cdn.ncbi.nlm.nih.gov/pmc/blobs/91c1/4601517/f7d3e2e206f5/kbie-06-04-1050162-g001.jpg){alt="Figure 1."}

The entire field of software engineering is too large to incorporate into the skillset of bioinformatics, and much of it is of no interest to the bioinformatician in the first place. Nobody expects him to build, or even understand the inner workings of the centrifuges and mass spectrometers that are so essential to research. Why then should we expect him to master the art of building large-scale, performant and production-ready software systems?

The point we are making in distinguishing the role of Bioinformatics Engineer can be summarized as follows: Software Engineering is vital to the discipline of bioinformatics *without being a core skill of that discipline*. This question of specialization is a logistic or even economic one which finds echoes in Ricardo's Law of Comparative Advantage: Even if it were possible for bioinformaticians to subsume the entire discipline of software engineering into their body of knowledge, it would not be desirable.^[20](https://pmc.ncbi.nlm.nih.gov/articles/PMC4601517/#cit0020)^ It would simply represent bad value. A bioinformatician investing the necessary time in engineering skills would pay a heavy price in terms of Opportunity Cost - the time *not* spent on study and research in core biological questions. Much better to lean on an engineering specialist in those key moments of research and development when engineering skills come to the fore.

**Figure 7** categorizes the kinds of software development that would typically take place in a research team into 4 quadrants, based on 2 variables: Whether the work is core or peripheral to the team's output (focus) eg. scientific problem/question, and whether the resulting software should be considered temporary or permanent (durability). We can use these variables to pinpoint the phases of research where bioinformaticians could increase their productivity by handing over to bioinformatic engineers, or at the very least, “change hat” and temporarily adopt an engineering approach.

![Figure 7.](https://cdn.ncbi.nlm.nih.gov/pmc/blobs/91c1/4601517/d501f12b73ed/kbie-06-04-1050162-g007.jpg){alt="Figure 7."}

Projects that weave software engineering best practices into bioinformatics research and *in silico* experimentation reap concrete rewards. By employing software engineering techniques such as a layered architecture, explicit development models and a rigorous requirements-gathering approach, Walsh et al.^[22](https://pmc.ncbi.nlm.nih.gov/articles/PMC4601517/#cit0022)^
