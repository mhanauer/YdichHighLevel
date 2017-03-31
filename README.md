# YdichHighLevel
# Example for Jags-Ymet-XmetSsubj-MrobustHier.R 
#------------------------------------------------------------------------------- 
# Optional generic preliminaries:
graphics.off() # This closes all of R's graphics windows.
rm(list=ls())  # Careful! This clears all of R's memory!
#------------------------------------------------------------------------------- 
# Load data file and specity column names of x (predictor) and y (predicted):

myData = read.csv( file="HierLinRegressYDicotDataExtend.csv" )
xName = "X" ; x2Name = "X2"; x3Name = "X3"; yName = "Y" ; sName="Subj"
fileNameRoot = "HierLinRegressData-Jags-" 

graphFileType = "eps" 
#------------------------------------------------------------------------------- 
# Load the relevant model into R's working memory:
source("Jags-Ydich-XmetSsubj-Dicot-MrobustHierExtend.R")
#------------------------------------------------------------------------------- 
# Generate the MCMC chain:
#startTime = proc.time()
mcmcCoda = genMCMC( data=myData , xName=xName ,x2Name = x2Name,x3Name = x3Name, yName=yName , sName=sName ,
                    numSavedSteps=20000 , thinSteps=15 , saveName=fileNameRoot )

#------------------------------------------------------------------------------- 
# Get summary statistics of chain:
summaryInfo = smryMCMC( mcmcCoda , saveName=fileNameRoot )
show(summaryInfo)

