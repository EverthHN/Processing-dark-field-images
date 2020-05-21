# Processing-dark-field-images
# A routine to run in ImageJ to measure phase thickness in EBTi-64
# An initial very first version. Threshold algorithm to be developed. Auto file import too. 
open("C:/Users/Everth/Documents/Builds/PREP-22/S1_01.jpg");
run("8-bit");
setAutoThreshold("Default dark");
//run("Threshold...");
//setThreshold(0, 120); %%Need to optimise this by using an appropiate algorith
setOption("BlackBackground", true);
run("Convert to Mask");
run("Close");
run("Watershed");
run("Analyze Particles...", "  circularity=0.60-1.00 show=Ellipses display exclude clear");
saveAs("Results", "C:/Users/Everth/Documents/Builds/PREP-22/Results.csv");
close();run("script:Macro.ijm.ijm");
