# Exploratory-Data-Analysis
Repository for the solution of project week 1

```R

# Code for the first graph solution

powerDT <- data.table::fread(input = "household_power_consumption.txt", na.strings="?")
powerDT[, Global_active_power := lapply(.SD, as.numeric), .SDcols = c("Global_active_power")]
powerDT[, Date := lapply(.SD, as.Date, "%d/%m/%Y"), .SDcols = c("Date")]
powerDT <- powerDT[(Date >= "2007-02-01") & (Date <= "2007-02-02")]
png("plot1.png", width=480, height=480)
hist(powerDT[, Global_active_power], main="Global Active Power", xlab="Global Active Power (kilowatts)", ylab="Frequency", col="Red")
dev.off()

```
![](https://github.com/ironfact/Exploratory-Data-Analysis/blob/main/plot1.png?raw=true)
```R



# Code for the second graph solution

powerDT[, dateTime := as.POSIXct(paste(Date, Time), format = "%d/%m/%Y %H:%M:%S")]
powerDT <- powerDT[(dateTime >= "2007-02-01") & (dateTime < "2007-02-03")]
png("plot2.png", width=480, height=480)
plot(x = powerDT[, dateTime], y = powerDT[, Global_active_power], type="l", xlab="", ylab="Global Active Power (kilowatts)")
dev.off()

```
![](https://github.com/ironfact/Exploratory-Data-Analysis/blob/main/plot2.png?raw=true)
```R

# Code for the third graph solution

powerDT <- powerDT[(dateTime >= "2007-02-01") & (dateTime < "2007-02-03")]
png("plot3.png", width=480, height=480)
plot(powerDT[, dateTime], powerDT[, Sub_metering_1], type="l", xlab="", ylab="Energy sub metering")
lines(powerDT[, dateTime], powerDT[, Sub_metering_2],col="red")
lines(powerDT[, dateTime], powerDT[, Sub_metering_3],col="blue")
legend("topright", col=c("black","red","blue"), c("Sub_metering_1  ","Sub_metering_2  ", "Sub_metering_3  "),lty=c(1,1), lwd=c(1,1))
dev.off()

```
![](https://github.com/ironfact/Exploratory-Data-Analysis/blob/main/plot3.png?raw=true)
```R

# Code for the fourth graph solution

powerDT <- powerDT[(dateTime >= "2007-02-01") & (dateTime < "2007-02-03")]
png("plot4.png", width=480, height=480)
par(mfrow=c(2,2))
# Plot 1
plot(powerDT[, dateTime], powerDT[, Global_active_power], type="l", xlab="", ylab="Global Active Power")
# Plot 2
plot(powerDT[, dateTime],powerDT[, Voltage], type="l", xlab="datetime", ylab="Voltage")
# Plot 3
plot(powerDT[, dateTime], powerDT[, Sub_metering_1], type="l", xlab="", ylab="Energy sub metering")
lines(powerDT[, dateTime], powerDT[, Sub_metering_2], col="red")
lines(powerDT[, dateTime], powerDT[, Sub_metering_3],col="blue")
legend("topright", col=c("black","red","blue"), c("Sub_metering_1  ","Sub_metering_2  ", "Sub_metering_3  "), lty=c(1,1), bty="n", cex=.5) 
# Plot 4
plot(powerDT[, dateTime], powerDT[,Global_reactive_power], type="l", xlab="datetime", ylab="Global_reactive_power")
dev.off()

```
![](https://github.com/ironfact/Exploratory-Data-Analysis/blob/main/plot4.png?raw=true)
```R
