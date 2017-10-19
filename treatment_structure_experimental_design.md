## Experimental design and analysis of data

***

**Youngjun Na**  
Department of Animal Science and Technology, Konkuk University  
Email: ruminoreticulum@gmail.com  
  
1/19/2017 Seoul National University  

*** 

###Index  

*** 

1.	Treatment structure and experimental design
2.	Analysis of data using SAS ®

***

### 0. Basic concepts

*** 

- Experimental unit  
-	Sampling unit  
-	Variation  
-	ANOVA  
-	Interaction  

*** 

### 1. Treatment structure and experimental design

***

#### 1.1. Treatment structure

***

**Types of treatments – Unstructured vs. Structured**  
- Unstructured (unrelated) treatment: no natural order or relationship is established among the set of treatments (e.g. Beauchemin and McGinn, 2006)  
- structured (related) treatment: 1) Grouping 2) Gradient structure  
1)	Grouping (factorial) structure: two or more groups of related treatments (e.g. Hammond et al., 2016; Zhou et al., 2016; Figure 1).  
2)	Gradient structure: Incremental differences are present (e.g. Campos et al., 2014; Xue et al., 2011)

***

#### 1.2. Experimental design

***

General design structures – CRD, RCBD, and LSD (Figure 2)  

- Completely Randomized Designs (CRD): the simplest design structure possible because treatments are assigned to experimental units completely at random. Use of this design is appropriate when experimental units are relatively homogeneous (uniform).   ANOVA table for CRD is given in Table 1.  

- Randomized Completely Block Designs (RCBD): experimental units are arranged in homogeneous groups (block) on the basis of a single source of extraneous variability; that is, there is one restriction on the randomization. The extraneous source of variability may be a management factor such as time or location (e.g. different farms or buildings) or an animal factor such as body weight, parity, DIM, litter, breed, or gender. ANOVA table for RCBD is given in Table 2.  

- Latin Square Designs (LSD): two restrictions on the randomization. This double blocking makes it possible to remove two independent, extraneous sources of variability from the experimental error. Often in animal nutrition experiments, columns refer to individual animals and rows refer to time periods (Figure 3). ANOVA table for LSD is given in Table 3. For making a balanced LSD, please refer to paper of (Kim and Stein, 2009).  

* The principle objective of blocking is to reduce experimental error. By putting experimental units that are as similar as possible together in the same group (block) and by assigning all treatments into each block separately and independently, variation among blocks can be measured and removed from experimental error.  

***

###2. Analysis of data using SAS ®

***

SAS PROC GLM vs. MIXED

UPPER CASE = SAS CODES; lower case = your dataset

***

#### 2.0. DATASET

***

> DATA dsname;  
> INPUT  
> trt animal period response  
> ;CARDS;  
> 1 1 1 200   
> 2 1 2 210   
> 3 2 3 207   
> ;  

***

#### 2.1. CRD  

***

> PROC MIXED DATA=dsname;  
> CLASS trt;  
> MODEL response=trt;  
> LSMEANS trt/PDIFF;  
> RUN;  

***

#### 2.2. RCBD

***

> PROC MIXED DATA=dsname METHOD=REML;  
> CLASS trt block;  
> MODEL response=trt/DDFM=SATTERTH;  
> RANDOM block;  
> LSMEANS trt/PDIFF;  
> RUN;  

***

#### 2.3. LSD

***

> PROC MIXED DATA=dsname METHOD=REML;  
> CLASS trt animal period;  
> MODEL response=trt/DDFM=SATTERTH;  
> RANDOM animal period;  
> LSMEANS trt/PDIFF;  
> RUN;  

***

#### 2.4. Unstructured

***

> LSMEANS trt/PDIFF;  

***

#### 2.5. Factorial arrangement (grouping structure)  

***

- If experiment is conducted for 2 x 2 factorial arrangement

> MODEL response=A B A*B;  

***

#### 2.6. Orthogonal polynomial contrast (gradient structure; Figure 4)

***

- If experiment is conducted for 3 equally-spaced level  

> CONTRAST ‘LINEAR’ trt -1 0 1;  
> CONTRAST ‘QUADRATIC’ trt 1 -2 1;  

***

#### 2.7. Coefficients estimation for Orthogonal polynomial contrast (equally or unequally-spaced level)

***

> PROC IML;  
> X={0 20 30 40 100};  
> XP=ORPOL(X,3);  
> PRINT XP;  
> RUN;  

***

#### 2.8. Pearson’s correlation coefficient

***

> PROC CORR DATA = dsname;  
> RUN;  

***

#### 2.9. Regression

***

> PROC REG DATA = dsname ALL;  
> MODEL response=trt;  
> RUN;  

***

#### 2.10. Mixed model regression

***

- Mixed model regression is used for integrating quantitative findings from multiple studies (St-Pierre, 2001).  

***

#### 2.11. Repeated Measures analysis

***

- Repeated measures analysis is used for examine and compare response trends over time (Littell et al., 1998).  
- e.g. Sari et al., (2015); Cardozo et al. (2004)  


***

### REFERENCES

***

1. Beauchemin, K.A., McGinn, S.M., 2006. Methane emissions from beef cattle: Effects of fumaric acid, essential oil, and canola oil. J. Anim. Sci. 84, 1489–1496.  
2. Campos, A.F., Pereira, O.G., Ribeiro, K.G., Santos, S.A., Valadares Filho, S. de C., 2014. Impact of replacing soybean meal in beef cattle diets with inactive dry yeast, a sugarcane by-product of ethanol distilleries and sugar mills. Anim. Feed Sci. Technol. 190, 38–46. doi:10.1016/j.anifeedsci.2014.01.003
3. Cardozo, P.W., Calsamiglia, S., Ferret, A., Kamel, C., 2004. Effects of natural plant extracts on ruminal protein degradation and fermentation profiles in continuous culture. J. Anim. Sci. 82, 3230–3236.  
4. Hammond, K.J., Jones, A.K., Humphries, D.J., Crompton, L.A., Reynolds, C.K., 2016. Effects of diet forage source and neutral detergent fiber content on milk production of dairy cattle and methane emissions determined using GreenFeed and respiration chamber techniques. J. Dairy Sci. 99, 7904–7917. doi:10.3168/jds.2015-10759  
5. Kim, B.G., Stein, H.H., 2009. A spreadsheet program for making a balanced Latin square design. Rev. Colomb. Cienc. Pecu. 22, 591–596.  
6. Littell, R.C., Henry, P.R., Ammerman, C.B., 1998. Statistical analysis of repeated measures data using SAS procedures. J. Anim. Sci. 76, 1216–1231.  
7. Sari, M., Ferret, A., Calsamiglia, S., 2015. Effect of pH on in vitro microbial fermentation and nutrient flow in diets containing barley straw or non-forage fiber sources. Anim. Feed Sci. Technol. 200, 17–24. doi:10.1016/j.anifeedsci.2014.11.011  
8. St-Pierre, N.R., 2001. Invited Review: Integrating Quantitative Findings from Multiple Studies Using Mixed Model Methodology1. J. Dairy Sci. 84, 741–755. doi:10.3168/jds.S0022-0302(01)74530-4  
9. Xue, F., Zhou, Z., Ren, L., Meng, Q., 2011. Influence of rumen-protected lysine supplementation on growth performance and plasma amino acid concentrations in growing cattle offered the maize stalk silage/maize grain-based diet. Anim. Feed Sci. Technol. 169, 61–67. doi:10.1016/j.anifeedsci.2011.05.011  
10. Zhou, X., Beltranena, E., Zijlstra, R.T., 2016. Effect of feeding wheat- or barley-based diets with low or and high nutrient density on nutrient digestibility and growth performance in weaned pigs. Anim. Feed Sci. Technol. 218, 93–99. doi:10.1016/j.anifeedsci.2016.05.011
