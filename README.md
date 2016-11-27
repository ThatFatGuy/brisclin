# brisclin
Summary of the analysis of isolates obtained from Brisbane (for re-analysis if required)

>**Data is included in the compressed file, blisclin.txt - contains all the summary data, and was used for the total analysis of transformed data. brisclin1.txt - contains the resistances to individual antibiotics.**

>These can be loaded directly into R in their current form.

>I have been diligent to not include ANY data in this 'public' forum - This is why i have not done a direct markdown output from R showing the results within, or included any of the data here (can never be too safe).

```R
library(ggplot2)
library(data.table)

bris_clin_all <- data.table::fread("~/path/to/file/brisclin.txt")
view(bris_clin)

overal_plot <- ggplot(bris_clin_all, aes(x=groupA, y=MIC_all, fill_factor(ab)))+
geom_boxplot(fill=('white'))+
geom_dotplot(binaxis = 'y', stackdir = 'center', dotsize = 0.8, stackratio = 0.4)+
labs(x="Isolate location", y="Minimum Inhibitory Concentration")+
theme_bw()
overal_plot

```

>**This will (hopefully) give an output the same as brisclin_all_resis.eps (attached in the compressed file).**

>To get the breakdown of individual resistances you can repeat the above with some slight changes on the other dataset

```R
library(ggplot2)
library(data.table)

bris_clin <- data.table::fread("~/path/to/file/brisclin1.txt")
view(bris_clin)

tobr_plot <- ggplot(bris_clin, aes(x=groupZ, y=MIC_data$`MIC tobr`, fill_factor(groupZ)))+
geom_boxplot(fill=('white'))+
geom_dotplot(binaxis = 'y', stackkdir = 'center', dotsize = 0.8, stackratio = 0.4)+
labs(x="Isolate location", y="Minimum Inhibitory Concentration (Tobramycin mg.L-1)")+
theme_bw()
overal_plot

```

>Apologies for the weird y axis formatting in the above code - it is because i added a space into the header of the brisclin1.txt file, so the axis has to be defined in a slightly different way (to get around this, simply remove the space and replace with _ or something similar).

>**To examine the statistics of the data - i was simply using an ANOVA.**

```R
cipro_resist <- aov(bris_clin$`MIC cipro` ~ bris_clin$groupZ)
summary(cipro_resist)
TukeyHSD(cipro_resist)

```

> This can be repeated for all the antibiotics and then on the combined data in bris_clin_all.

****Any issues, don't hesitate to contact me - sam.taylor-wardell@otago.ac.nz****
