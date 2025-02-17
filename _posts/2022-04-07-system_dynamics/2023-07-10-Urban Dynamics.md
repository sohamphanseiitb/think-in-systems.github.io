---
layout: page
title: "Urban Dynamics"
author: "Soham Phanse"
categories: journal
tags: [documentation,sample]
---

Hey folks! We are back again; this time, we will analyze an exciting and complex system - a city, better called Urban Dynamics. We will try to model this system - it contains very interesting elements like housing, jobs, economic development, and a lot more.

> **Acknowledgement**: This case study has been borrowed from the course IE604 System Dynamics Modeling and Analysis from the semester of Fall 2022 taught by Prof. Jayendran Venkateswaran at IIT Bombay. 

# Problem Statement
New town development drives urbanization, especially in developing countries. These new towns can be different designs, functions, and populations; there can be interesting dynamic parallels in their evolution. Prof. Jay W. Forrester, in his now classical work on Urban Dynamics, showed that SD is an appropriate method to understand new town structures and dynamics and to test policies. The description below simplifies and highlights some essential interactions found in Urban
Dynamics. The critical sectors represented are the Population, Housing, and Business Structures, with interactions including population-housing interactions, population-business interactions, and business-housing interactions. Land as a fixed limited resource affects housing and business constructions; the Population provides the labor for doing the jobs that are created by the Businesses. The model, when completed, should be able to trace the area’s growth from an early undeveloped stage to a growth stage and into an equilibrium stage within a 50-100 year time horizon. 

## Part 1
Consider a fixed geographical area that might represent a new town or suburb. Aside from location & climate, housing availability, and job availability are the primary determinants of population growth in the town. The population experiences annual growth driven by births (3% per year) and deaths (1.5% per year) in the town. Also, the town’s housing attractiveness brings new people in at a normal rate of 10% per year (in-migration). Town residents also leave at the rate of 7% per year for various reasons (out-migration). The population drives the desired housing proportionally.

Housing construction continues as long as plenty of land is available for housing. Under these conditions, the housing construction rate will equal 7% per year. As the fraction of landfills up, house construction ceases. Also, when surplus housing exists, builder cut back on construction, and when a shortage of housing is there, the construction rate increases to meet demand. Since the average lifetime of housing units equals ~50 years, the annual demolition rate equals 2%.

The business (or business structures) in the area also responds to land availability. New business constructions/ establishments continue as long as plenty of land is available. Under these conditions, the business construction rate will equal 7% per year. As the fraction of land occupied fills up, business structure construction ceases. Since the average lifetime of business units equal ~40 years, the annual demolition rate equals 2.5%. Businesses (or business structures) provide jobs in proportion to the number of businesses. A fraction of the population will be the labor force. The above description treats each sector independently. That is, it doesn’t really connect the sectors.

## Model Description

| Sr. No | Component Name | Component type | Explanation | Initial Value | Corresponding Flows | Units |
| ------ | -------------- | -------------- | ----------- | ------------- | ------------------- | ----- |
| 1 | Population | stock | number of people in the city | 50000 | Births, Deaths, Inmigration, Outmigration | persons |
| 2 | Houses | stock | number of houses in the city | 14000 | Housing Construction (HC), Housing Demolition (HD) | house |
| 3 | Business Structures | Organization doing economic activity and employing people | 1000 | Business Construction (BC), Business Demolition (BD) | business |

| Sr. No | Component Name | Component Type | Explanation | Expression | Units |
| ------ | -------------- | -------------- | ----------- | ---------- | ----- |
| 1 | area per business structure | variable | amount of area required by each business structure | 0.2 | acre/business |
| 2 | area per house | variable | amount of area required to build 1 house | 0.05 | acre/house | 
| 3 | Jobs per business structure | variable | number of jobs generated by each business | 18 | jobs/business |
| 4 | labor fraction | variable | fraction of the population working as labor | 0.35 | dimensionless |
| 5 | normal birth fraction | variable | multiplier fraction for birth rate | 0.03 | 1/Year |
| 6 | normal business demolition fraction | variable | fraction of businesses demolished per year | 0.025 | 1/Year |
| 7 | normal business construct fraction | variable | multiplier fraction of newly constructed each year | 0.07 | 1/Year |
| 8 | normal construction fraction | variable | multiplier fraction for construction of new units each year | 0.07 | 1/Year |
| 9 | normal death fraction | variable | multiplier fraction of population for number of deaths per year | 0.015 | 1/Year |
| 10 | normal demolition fraction | variable | multiplier fraction for demolished units each year | 0.02 | 1/Year |
| 11 | normal inmigration fraction | variable | multiplier fraction for population, total immigration each year | 0.1 | 1/Year |
| 12 | normal outmigration fraction | variable | multiplier fraction for population, total outmigration each year | 0.07 | 1/Year |
| 13 | Persons per House | variable | number of residing per house | 4 | Person/House |
| 14 | total land | variable | total available | 1000 | acre |

> **Note**: Use a final simulation time of 60 years, with a time step of 0.25.

### Problem 1
The SFD model has been given as follows. We need to mark the links and loops with polarities and types. Link polarities can either be + or -, and loop types can either be B or R, i.e., balancing or reinforcing. 

![Urban Dynamics SFD Model](https://sohamphanseiitb.github.io/th-ink-in-systems/assets/img/urban%20dynamics%20model.jpg)

<!-- Hey folks! To tie up everything we have seen so far, I will walk you through a simple and ready case. It is about constructing a system dynamics model of the population of a particular university campus. Incidentally, as you might have guessed, this is one of the simplest population models since we have strict rules with respect to the increase in the number of students. Hence accurate estimates can be obtained, and special statistical techniques are not required. The model with suitable (a lot :P) can be extended to construct models predicting a city or a nationwide population estimate.

Since you peeps should know the background, I was working to model the energy consumption trends on my university campus. Since energy consumption heavily depends on the number of users and usage per capita, my immediate task was to estimate the total population living on campus. The framework starts with obtaining basic data about the number of students, the student-to-faculty ratio, administration staff, and dependents living on campus, and estimating admission rates for students, hiring, and attrition rates for professors and other staff members on campus.

To give you an idea of how the student population on campus changes across the years, check this sketch below:

![Population Model](https://sohamphanseiitb.github.io/Think-in-Systems/assets/system-dynamics/population%20blog.jpg)

Obviously, the rate at which undergraduate students are admitted will be starkly different than graduate students.

Similarly, we can construct a model to estimate how the teaching faculty grows over time. To simplify stuff, the Student to Faculty Ratio can be assumed to be constant; however, it is better to assume it is adaptable since every university strives to attain the best possible ratio as mandated by national standards. The number distribution of undergraduate and graduate students on campus also affects the required amount of teaching staff. The Student to Faculty ratio in the case of graduate students is expected to be higher than undergraduates. In that case, two different ratio estimates can be calculated. However, it should be understood that there be a significant fraction of staff who will be teaching and advising at both levels. We can make assumptions about how the universities plan to implement policies to improve the ratio each year. The policies can be as follows:

- Case 1: If the ratio is higher than the mandate (low teaching staff strength)
  - Increase the hiring rate, vis a vis, and hire more people every year. 
  - Reduce attrition rate, vis a vis, provide incentives to people to improve retention period
    -  Provide schemes like subsidized medical insurance, interest-free loans, pension benefits, and provident fund schemes

- Case 2: If the ratio is lower than the mandate (high teaching staff strength)
  -  Decrease the hiring rate; in extreme cases, new hiring can be frozen
  -  Improve performance vigilance to keep under-performing staff in check and incentivize attrition

The administration staff, on the other hand, is trickier to model since it doesn't have well-defined ratios to be kept in check. A modest 3-5% growth can be assumed safely. If the university provides housing to teaching and other staff on campus and allows immediate family members to stay alone, a rough number of 2 dependents per working member of staff can be assumed to calculate the total number of staff dependents. 

With these population sub-models of students, teaching and non-academic staff, and dependents, a fair estimate of the total population on the university campus can be obtained. This further can be combined with other models to estimate the per capita energy consumption in each category and, ultimately, total energy usage at domestic levels for personal use. 

For commercial uses, like computing and use in research equipment, outdoor lighting, and common areas like gymnasiums, sports complexes, and auditoriums, energy usage has to be calculated with data since no modeling techniques can give accurate estimates. Constructing gymnasiums and new research labs on campus are discrete events by nature and cannot be predicted beforehand. In cases of infrastructural expansion, the total land area availability and the trend estimation timeline should also be considered.

All in all, if you see systems modeling can start with simple logic and building blocks which together can be assembled to produce useful results. Complex models can be built with simple models, and layers of statistical estimates can be grafted onto propagative models to create models with can accurately estimate real-world phenomena like business cycles, stock value predictions, or the global economic scenario. -->
