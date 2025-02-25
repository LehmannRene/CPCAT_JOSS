---
title: 'CPCAT: A package for multiple comparisons of (generalized) Poisson distributed data'

tags:
  - R
  - ecotoxicology
  - economics
  - count data
  - control vs. treatment
  - no/lowest observed (adverse) effect contration/treamt
  - closure principle (CP)
  - computational approach test (CAT)
authors:
  - name: René Lehmann
    orcid: 0000-0003-4145-8272
    corresponding: true
    affiliation: "1, 2" # (Multiple affiliations must be quoted)
affiliations:
 - name: FOM University of Applied Science, Essen, Germany
   index: 1
 - name: Otto von Guericke University, Magdeburg, Germany
   index: 2
date: 24 February 2025
bibliography: paper.bib
---

# Summary

Many scientific fields consider grouped count data to reveal effects between variables. For example, in ecotoxicology, species reproduction tests based on the number of juveniles are widespread. These tests are used to assess the effects of chemical substances on species reproduction (e.g., on the numbers of juvenile Daphnia magna or the number of new fronds of Lemna minor L.). In economics, the testing of economic indicators (e.g., the number of impulse purchases or the number of cars owned) dependent on income, education, or the intensity of marketing measures is considered.

While normal approximation of the data is often a minor problem, the requirement of variance homogeneity is frequently not fulfilled. Variance homogeneity is necessary to ensure the proper application of statistical procedures such as pairwise t-tests [@Welch1938; @Welch1947; @Welch1951], Dunnett's t-test [@Dunnett1955; @Dunnett1964], and Williams' t-test [@Williams1971; @Williams1972]. A Poisson model can solve this issue, preserving meaningful results and rendering statistical analysis more reliable [@Lehmann2016]. Moreover, the sequential application of pairwise statistical 'control vs. treatment' tests is a drawback concerning $\alpha$-inflation. The closure principle (CP) [@Bretz2011] for hypothesis testing is used to generate a step-wise approach for detecting the no/lowest observed (adverse) effect level (NOEL,LOEL,NOAEL,LOAEL) using the computational approach test (CAT)[@Chang2010]. The combined approach is called CPCAT [@Lehmann2018].

While @Chang2010 provides the mathematical details of the CAT, @Bretz2011 offers a proper introduction to the CP and its applications. @Lehmann2016 develops the mathematical arguments behind the CPCAT. The simulation study by @Lehmann2018 provides deeper insights into the
behavior and statistical power of the CPCAT in various scenarios

# Statement of need

`CPCAT` is an R package for computing NOEL,LOEL,NOAEL,LOAEL in the framework of multiple testing of (generalized) Poisson distributed grouped count data using the CPCAT procedure. Being considered for the OECD Guidance Document on statistical procedures [@OECD2006a] there is a need to ensure user-friendly and easy applicability. Beside the CPCAT, practioners also need support in automatically generating intersection hypotheses and single computations of the CAT.

# Mathematics
Consider an exemplary multiple testing problem consisting of one control group ("0") and three treatment groups ("1", "2", "3") at a significance level $\alpha\in(0;1)$. To find the NOEL (NOAEL, LOEL, LOAEL), we test for equality/inequality of means iteratively. We compare the control group with each treatment $i$ by testing the null hypothesis $H_{0i}:\ \mu_0=\mu_i$, where $\mu$ denotes a population mean ($i=1,2,3$). This process, however, causes $\alpha$-inflation. The Closure Principle (CP) dictates testing all intersection hypotheses associated with a main hypothesis $H_{0i}$. For example, when testing $H_{01}:\ \mu_0=\mu_1$, we test all intersection hypotheses involving $\mu_0$ and $\mu_1$, i.e., $H_{0123}:\ \mu_0=\mu_1=\mu_2=\mu_3$, $H_{012}:\ \mu_0=\mu_1=\mu_2$, $H_{013}:\ \mu_0=\mu_1=\mu_3$, and $H_{01}:\ \mu_0=\mu_1$. The corresponding p-value $p_i$ is obtained by selecting the maximum p-value of all associated intersection hypotheses [@Bretz2011]. In the above example, we have $p_1=\max{p_{0123},p_{012},p_{013},p_{01}}$. Then, $H_{0i}$ is rejected if $p_i<\alpha$. While the CP increases the number of hypotheses to be tested, it prevents $\alpha$-inflation.

The CAT is used to test any intersection hypothesis. Combining the CP and the CAT yields the CPCAT. @Chang2010 describes the CAT in detail, while @Lehmann2016 provides an algorithmic representation.

A Poisson-distributed data generating process (DGP) postulates an equality of the population mean $\mu$ and the population variance $\sigma^2$, i.e., $\mu=\sigma^2$. This property, however, can make a Poisson model unsuitable in practice. A generalized Poisson model allows for differences in $\mu$ and $\sigma^2$. Although the CAT is designed to test the equality/inequality of several Poisson means $\mu_0,\mu_1,\mu_2,\ldots$, @Lehmann2018 provides evidence that it also works satisfactorily if the DGPs are generalized Poisson distributed.


# References

