require(ggplot2)
## Loading required package: ggplot2
require(dplyr)
#png("plot3.png", width=number.add.width, height=number.add.height)
# Group total NEI emissions per year:
baltcitymary.emissions.byyear<-summarise(group_by(filter(NEI, fips == "24510"), year,type), Emissions=sum(Emissions))
# clrs <- c("red", "green", "blue", "yellow")
ggplot(baltcitymary.emissions.byyear, aes(x=factor(year), y=Emissions, fill=type,label = round(Emissions,2))) +
    geom_bar(stat="identity") +
    #geom_bar(position = 'dodge')+
    facet_grid(. ~ type) +
    xlab("year") +
    ylab(expression("total PM"[2.5]*" emission in tons")) +
    ggtitle(expression("PM"[2.5]*paste(" emissions in Baltimore ",
                                       "City by various source types", sep="")))+
    geom_label(aes(fill = type), colour = "white", fontface = "bold")
