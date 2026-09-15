# Featurization: question1
#There were various frature that was relevent for finding bulk modulus:
#1 In composite feature we need to know the fraction of our materials, atomic size , electronegativity, and other elemental properties that we get from magpie.
#2 In structural feature we need to know density, volume , symmetry and packing fraction. Basicaaly global crystal structure.
#3 ChemEnv custom feature include local environment of material whic is also very releveant because while finding bulk properties we need to tae care of any local disstortion or nearby structures that influence things.



# question2:
#Since our dataset already have the information about Cu.Pt and Cu-Pt fraction so we may not need those in composite feature. Aslo properties such as Atomic mass and so which directly does not decide bulk modulus are irrelevnt.
#K_reuss and K_voigt are not need as feature are it can be obtained form k_vrh which is average of them.




# Question3
#The compositional feature which I used are Stoichiometry, ElementFraction, Magpie ElementProperty and ValenceOrbital.
#These features describe the Cu/Pt ratio, elemental-property statistics such as atomic size, electronegativity and atomic mass, and the fractions of electrons
#The structural feature were generated using DensityFeatures and GlobalSymmetryFeatures. 
#They include quantities related to density, volume per atom, packing efficiency, crystal system and space-group symmetry.
#I aslo used one custom feature that is ChemEnv which is ude to calculate mean, SD, min and max.
#The mean describes the dominant local coordination environment, while the other statistics capture variation and distortion between atomic sites.


#THis representation is choosen because to calculate bulk modulus we need crystal structure and chemical boding structure.
#Composite feature helps to distinguish between Pt,Cu, and Pt-Cu while structual feature help to get properties like density, packing fraction that are essential for bulk modulus.
#other features help to understand local structure , like neighbour arrangement of surrounding atoms and which structre resemble more to our structure.
#Since bulk modulus measn resistence to compression so that aslo depends on how loacl factor or structure influence it. 


# Question4:
#Two feature slection method that were used were:
# 1 Mutual-information method: Here each feature are evaluated independiently and the goal is to check which fetaure reduce the uncertainity from the target value.
#One of the disadvantage of this method is since it is evaluated independently we can sometimes miss the interaction bewteen two feature which might give better resuts.
#Moreover two correlated feature which give the same terget score might both get sellected.
#They are model indepindent.

# 2 Model based slection: Here the model such as random forest is trained to evaluate the feature relevence from the reduction in prediction error produced by feature splits across its decision trees.
#Feature with highest importance value are retained. Since it is model dependentso correlated feature divide importance bewteen one another. 

#MODnet: This feature slection method is very similar to Mutual information with one addition that it adds on an explict redundancy penality for same feature selected.
#It normalize mutual information to identify feature related to the target while also penalizing feature that contain information already represented by previously selected features.



# Question5: 
#If slection were performed on outer CV then there will be overfitting and data leakage, as model will also examine our target on the outer test data. SO to stop thiswe use inner CV as seperate container.


# Question6:
#Random forest:
#trees are trained independintly and final prediction take avergare of many trees
#usually reduce prediction variance and less sensitive to tunning.
#use random feature subset

#Gradient boosting:
#trees are trained sequientally and final prediction adds on the contribution of previous tree.
#reduces prediction bias and are more sensitive to tuning and overfitting
#each tree corrects error from previous one.

#There in no strictly better model between two but we we comapre through MAE GB+ model based sight outperform others.



# Question7
model	category	feature	mean_importance	selected_folds	total_ChemEnv_importance
0	RF + Mutual Information	Top overall	density	0.767351	5	0.035495
1	RF + Mutual Information	Top overall	packing fraction	0.075846	5	0.035495
2	RF + Mutual Information	Top overall	vpa	0.070842	5	0.035495
3	RF + Mutual Information	Top overall	ChemEnv_min_C:12	0.008161	3	0.035495
4	RF + Mutual Information	Top overall	ChemEnv_mean_AC:12	0.005706	3	0.035495
5	RF + Mutual Information	Top ChemEnv	ChemEnv_min_C:12	0.008161	3	0.035495
6	RF + Mutual Information	Top ChemEnv	ChemEnv_mean_AC:12	0.005706	3	0.035495
7	RF + Mutual Information	Top ChemEnv	ChemEnv_max_AC:12	0.004181	3	0.035495
8	RF + Mutual Information	Top ChemEnv	ChemEnv_mean_I:12	0.003948	3	0.035495
9	RF + Mutual Information	Top ChemEnv	ChemEnv_mean_C:12	0.003423	3	0.035495
10	RF + Model Based	Top overall	density	0.760846	5	0.097596
11	RF + Model Based	Top overall	packing fraction	0.060610	5	0.097596
12	RF + Model Based	Top overall	vpa	0.055503	5	0.097596
13	RF + Model Based	Top overall	ChemEnv_min_C:12	0.015158	5	0.097596
14	RF + Model Based	Top overall	ChemEnv_mean_AC:12	0.012284	5	0.097596
15	RF + Model Based	Top ChemEnv	ChemEnv_min_C:12	0.015158	5	0.097596
16	RF + Model Based	Top ChemEnv	ChemEnv_mean_AC:12	0.012284	5	0.097596
17	RF + Model Based	Top ChemEnv	ChemEnv_max_AC:12	0.007541	5	0.097596
18	RF + Model Based	Top ChemEnv	ChemEnv_mean_S:5	0.006522	5	0.097596
19	RF + Model Based	Top ChemEnv	ChemEnv_mean_C:12	0.006114	5	0.097596
20	GB + Mutual Information	Top overall	density	0.749648	5	0.079864
21	GB + Mutual Information	Top overall	packing fraction	0.078972	5	0.079864
22	GB + Mutual Information	Top overall	vpa	0.074510	5	0.079864
23	GB + Mutual Information	Top overall	ChemEnv_min_C:12	0.022950	3	0.079864
24	GB + Mutual Information	Top overall	ChemEnv_mean_AC:12	0.008383	3	0.079864
25	GB + Mutual Information	Top ChemEnv	ChemEnv_min_C:12	0.022950	3	0.079864
26	GB + Mutual Information	Top ChemEnv	ChemEnv_mean_AC:12	0.008383	3	0.079864
27	GB + Mutual Information	Top ChemEnv	ChemEnv_mean_S:5	0.004172	3	0.079864
28	GB + Mutual Information	Top ChemEnv	ChemEnv_mean_C:12	0.003629	3	0.079864
29	GB + Mutual Information	Top ChemEnv	ChemEnv_mean_MI:10	0.003394	3	0.079864
30	GB + Model Based	Top overall	density	0.736411	5	0.128862
31	GB + Model Based	Top overall	vpa	0.075699	5	0.128862
32	GB + Model Based	Top overall	packing fraction	0.049184	5	0.128862
33	GB + Model Based	Top overall	ChemEnv_min_C:12	0.035337	5	0.128862
34	GB + Model Based	Top overall	ChemEnv_mean_MI:10	0.011683	4	0.128862
35	GB + Model Based	Top ChemEnv	ChemEnv_min_C:12	0.035337	5	0.128862
36	GB + Model Based	Top ChemEnv	ChemEnv_mean_MI:10	0.011683	4	0.128862
37	GB + Model Based	Top ChemEnv	ChemEnv_mean_AC:12	0.011136	5	0.128862
38	GB + Model Based	Top ChemEnv	ChemEnv_mean_C:12	0.010994	5	0.128862
39	GB + Model Based	Top ChemEnv	ChemEnv_max_MI:10	0.010283	5	0.128862
