# Processing-dark-field-images
# A routine to run in ImageJ to measure phase thickness in EBTi-64
# An initial very first version. Auto file import to be developed. 
open("C:/.../S1.jpg");
run("8-bit");
run("Auto Threshold", "method=Otsu white");
run("Invert");
run("Watershed");
run("Analyze Particles...", "  circularity=0.15-1.00 display exclude clear");
saveAs("Results", "C:/.../Results.csv");
