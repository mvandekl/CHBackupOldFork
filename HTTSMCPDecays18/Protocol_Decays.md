# Creating datacard

with cutbased cats:

    MorphingSMCPDecays18 --output_folder="19_cp" --postfix="-2D" --ttbar_fit=false --doDecays=true --input_folder_tt="Imperial/CP/201902_Feb/19_cp/" --do_jetfakes=true --no_shape_systs=true

with ML based cats:

    MorphingSMCPDecays18 --output_folder="15_cp" --postfix="-2D" --ttbar_fit=false --doDecays=true --do_mva=true --input_folder_tt="Imperial/CP/201902_Feb/19_cp/" --do_jetfakes=true 

option --no_shape_systs=true can be used as well

# Building the workspaces:

    combineTool.py -M T2W -P CombineHarvester.CombinePdfs.CPMixtureDecays:CPMixtureDecays -i output/201902_Feb/19_cp_new/cmb/* -o ws.root --parallel 8

# Run maximum liklihood scan

    combineTool.py -m 125 -M MultiDimFit --setParameters muV=1,alpha=0,muggH=1,mutautau=1 --setParameterRanges alpha=-90,90 --points 20 --redefineSignalPOIs alpha  -d output/201902_Feb/19_cp_new/cmb/125/ws.root --algo grid -t -1 --there -n .alpha --alignEdges 1

# Plot scan

1D scans can be plotted using scripts/plot1DScan.py script.
To plot alpha:

    python scripts/plot1DScan.py --main=output/201902_Feb/19_cp_new/cmb/125/higgsCoine.alpha.MultiDimFit.mH125.root --POI=alpha --output=alpha --no-numbers --no-box --x_title="#alpha (#circ)" --y-max=0.7