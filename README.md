# Processing-dark-field-images
# A script to run in ImageJ to measure plate thickness of alpha phase on Ti-64 samples
input = getDirectory("Input directory");
output = getDirectory("Output directory");
 
Dialog.create("File type");
Dialog.addString("File suffix: ", ".jpg", 5);
Dialog.show();
suffix = Dialog.getString();
 
processFolder(input);
 
function processFolder(input) {
    list = getFileList(input);
    for (i = 0; i < list.length; i++) {
        if(File.isDirectory(list[i]))
            processFolder("" + input + list[i]);
        if(endsWith(list[i], suffix))
            processFile(input, output, list[i]);
    }
}
 
function processFile(input, output, filename) {
open(input + filename); // Auto Import Threshold - Segmentation Method.
run("8-bit");
run("Auto Threshold", "method=Otsu white");
run("Invert");
run("Watershed");
run("Analyze Particles...", "  circularity=0.15-1.00 display exclude clear");
run("Summarize");
saveAs("Jpeg", output + filename);
saveAs("Results"); //Tobe optimised
run("Close All");

}
