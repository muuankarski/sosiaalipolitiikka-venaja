# Ideoita..

Voisin puhua ensin hieman teoreettisemmin siitä, millaisten teorioiden puitteissa sosiaalipoliittisia järjestelmiä tutkitaan ja miten venäläinen "hyvinvointivaltio" näyttää niiden valossa tai suhteessa Eurooppaan/kehittyviin maihin.

Toiseksi voisin puhua ihan sosiaaliturvajärjestelmästä, sen neuvostoperinnöstä ja siihen tehdyistä nykyaikaistuksista.

Kolmantena teemana olisi sitten ihan köyhyys niin sosioekonomisena kuin paikkaan/alueeseen liittyvänä ilmiönä. Voidaan katsoa vaikka Karjalan tasavallan elinoloja väestötietojen ja aluedatan näkökulmasta.


```{rjohdanto, echo=FALSE, fig.width=12}
library(gdata)
url <- "http://www.ggdc.net/maddison/maddison-project/data/mpd_2013-01.xlsx"
dat <- read.xls(url, header = TRUE, skip = 1, stringsAsFactors = FALSE)
#
column.names <- as.character(dat[1, ])
column.names[1] <- "year"
df.mad <- dat[-1, ]
names(df.mad) <- column.names
library(reshape2)
df.mad.l <- melt(df.mad, id.vars = "year")
df.mad.l$value <- as.numeric(df.mad.l$value)
df.mad.l <- df.mad.l[!is.na(df.mad.l$value), ]
#
cntry.list <- c("Russia","F. USSR")
library(stringr)
df.mad.l$variable <- str_trim(df.mad.l$variable, side = "both")
df.mad.l2 <- df.mad.l[df.mad.l$variable %in% cntry.list, ]
#
library(ggplot2)
ggplot(data = df.mad.l2[df.mad.l2$year > 1945, ], 
       aes(x = year, y = value, group = variable)) + 
    geom_line() + geom_point() + 
    geom_text(data = df.mad.l2[df.mad.l2$year == 2010, ], 
              aes(x = year, y = value, label = variable), vjust=-2, hjust=1) +
    annotate("segment", x = 1991, xend = 1991, y = 0, yend = 10000, 
    colour = "blue") + 
    annotate("text", x = 1991, y = 11000, label = "Neuvostoliiton \n hajoaminen") +
    annotate("rect", xmin = 1985, xmax = 1991, ymin = 5, 
             ymax = 9000, alpha = 0.2, color="dim grey") + 
    annotate("text", x= 1987, y = 200, label = "Gorbatchov") +
    annotate("rect", xmin = 1991, xmax = 1999, ymin = 5, 
             ymax = 9000, alpha = 0.2, color="dim grey") + 
    annotate("text", x= 1995, y = 200, label = "Jeltsin") +
    annotate("rect", xmin = 1999, xmax = 2007, ymin = 5, 
             ymax = 9000, alpha = 0.2, color="dim grey") + 
    annotate("text", x= 2003, y = 200, label = "Putin 1") +
    annotate("rect", xmin = 2007, xmax = 2012, ymin = 5, 
             ymax = 9000, alpha = 0.2, color="dim grey") + 
    annotate("text", x= 2009, y = 200, label = "Medvedev") +
    annotate("rect", xmin = 2012, xmax = 2014, ymin = 5, 
             ymax = 9000, alpha = 0.2, color="dim grey") + 
    annotate("text", x= 2012, y = 200, label = "Putin")


```