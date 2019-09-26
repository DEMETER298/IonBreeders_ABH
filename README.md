# IonBreeders version 1.0
Genotyping and genomic selection plugins for the Ion Torrent NGS platform.


[IonBreedersの使い方 日本語版 ver.1.0 ](https://github.com/DEMETER298/IonBreeders_ABH/wiki)


# 1. Installation Instructions

## Download plugins
The ABH plugin of IonBreeders is provided as a zipped package containing files from the Latest Release project page on Github.  
The file name will be of the format IonBreeders_ABH.zip.

## Install
Automatic installation from the Torrent Browser Plugin  
Follow these steps for automatic installation of a plugin from the Torrent Browser:  
1.	In your Torrent Browser, click the gear menu (near the top right) and select Plugins

![1](https://user-images.githubusercontent.com/40309394/54818632-14aee380-4cdd-11e9-845c-7c7d8ac95a1f.png)
  
2.	In the Plugins tab, click the **`Install or Upgrade Plugin`** button: 

![2](https://user-images.githubusercontent.com/40309394/54819228-8fc4c980-4cde-11e9-92ba-1d4b64e70e64.png) 

3.	In the **`Install or Upgrade Plugin`** tab, select downloaded zip file, and click **`Upload and Install`**.  
 



# 2. ABH plugin manuals

### 2-1 Function

(1) Output of specified sample data: only the data of the target sample selected on this plugin setting screen are extracted from the samples at the corresponding sequencing run.

(2) Collation with genotypes of parents: the genotype of each sample is compared with those of its parents and is expressed as father-derived homozygous (A), maternal-derived homozygous (B), hetero (H), or missing (-).

(3) Collation with genotypes of the reference genome: the genotype of each sample is compared with a specified reference genome in VariantCaller and is expressed as reference-type homozygous (A), variant homozygous (B), hetero (H), and missing (-).

(4) Conversion of file format: The following three kinds of files are output.

1. Correspondence table of barcodes and sample names 

2. CSV file with markers as rows and samples as columns

3. CSV file with markers as columns and samples as rows

4. R/qtl package input file (only ABH output)


### 2-2 Input file
Prepare the genotype data of the parents as a CSV (comma Separated Values) file (save as .csv) in the following format. **The chromosome name and physical location must match those of the reference and HotSpot (save as .vcf) used in the VariantCaller plugin.**

![genotype_mother](https://user-images.githubusercontent.com/40309394/54862344-d406a700-4d7c-11e9-9f5a-72aaae15a94b.png) mother genotype (mother_input.csv) This file can be edited and saved in Excel as csv file.

![genotype_father](https://user-images.githubusercontent.com/40309394/54862345-d6690100-4d7c-11e9-9f32-83b076fd7dd9.png) father genotype (father_input.csv) This file can be edited and saved in Excel as csv file.

![hotspot_example](https://user-images.githubusercontent.com/40309394/54862343-d10bb680-4d7c-11e9-95ab-408985079718.png)
 HotSpot file for VariantCaller plugin (Hotspot.vcf) This file can be edited and saved in Excel as tab-delimited txt file.


Test data shown below:
![Github_parentalgenotype_hotspot](https://user-images.githubusercontent.com/40309394/65664271-f5ba5100-e073-11e9-990c-d37ff6cd4e1d.png)




### 2-3 Execution:

(1) Execute the VairantCaller plugin with the HotSpot specified on the corresponding run report.



(2) When the VariantCaller plugin is completed, record the serial number (arrow).


　　　　<img src="https://user-images.githubusercontent.com/40309394/65664999-7af23580-e075-11e9-8291-867d46cb7f4f.png" width="350">  
 

(3) Click the **`Select Plugins To Run`** button on the top of the Torrent Browser report screen.

　　　　<img src="https://user-images.githubusercontent.com/40309394/54862396-68710980-4d7d-11e9-8b1c-60a429933818.png" width="450">  


(4) From the list of plugins, click **IonBreeders_ABH**.

       <img src="https://user-images.githubusercontent.com/40309394/65665969-a70eb600-e077-11e9-9ea6-940e95875a13.png" width="500">  
       


(5) Set each item on the screen as follows:

![ABH_screen](https://user-images.githubusercontent.com/40309394/65666640-091beb00-e079-11e9-9008-fc4b911c7389.png)
**An error occurs if the number of genotyping sites is too large. (Acceptable parent genotype file size is up to about 2Mb)**  
**At that time, select target chromosomes and reduce analysis regions.**  
  
  
`Samples`: A list of barcode names and sample names of the samples analyzed in the run is displayed.

`Selected`: A list of the selected barcode and sample names is displayed. Select a line in the Samples column and click the `add sample` button to add a new sample.

`VariantCaller ID`: Enter the serial number of the VariantCaller plugin execution result confirmed in (2) above.

`No parent genotype available`: Select if you do not have parent genotype data. Reference-based genotype is output in its place.

`Select father genotype file`: Select the father genotype file.

`Select mother genotype file`: Select the mother's genotype file.

`Output file name prefix`: Enter the desired file name.  










(6) Output contents
When execution is completed, the following items are displayed on the screen.

* The output when parent data is input (ABH format) appears as shown below.

![7](https://user-images.githubusercontent.com/40309394/54862520-a8d18700-4d7f-11e9-877e-2e395f9d8e12.png)

`ABH (markers in rows/samples in columns)`: the CSV output file can be opened in Excel as shown below.
 
![image](https://user-images.githubusercontent.com/40309394/54862533-e9c99b80-4d7f-11e9-926e-8f196be97898.png)

`ABH (R/qtl)`: the CSV output file can be opened in Excel as shown below.

![image](https://user-images.githubusercontent.com/40309394/54862544-082f9700-4d80-11e9-9b20-6c7026f80093.png)

The letters are removed from sample name so that each sample is identified only by unique numbers. 




* The output when no parent data are input (reference-based format) appears as shown below:
 
![8](https://user-images.githubusercontent.com/40309394/54862569-36ad7200-4d80-11e9-9937-86d75bb0e417.png)

The ABH (markers in rows/samples in columns) output file can be opened in Excel as shown below.

![image](https://user-images.githubusercontent.com/40309394/54862581-580e5e00-4d80-11e9-9360-fbd3faac9610.png)

The genotype is expressed as reference-type homozygous (Absent), variant homozygous (Homozygous), hetero (Heterozygous), and missing (Nocall).

 If there are two variants at the same site, variant 1 represent Homozygous_1 and variant 2 represent Homozygous_2. Mixed_1_2 indicates that two types of variants were detected in the same position. 

NoCall_0 indicated that no reads were aligned at the site. 

NoCall_X indicate that despite aligning X reads at the site, no variant could be detected.
 



***

# Contact
Eri Ogiso-Tanaka, Ph.D. demeter@affrc.go.jp

Institute of Crop Science / National Agriculture and Food Research Organization
2-1-2, Kannondai, Tsukuba, Ibaraki 305-8518, Japan

# Version
Version 1.0

# Citing IonBreeders
Ogiso-Tanaka E, Yabe S and Tanaka T (2019) 

**IonBreeders: semi-automated bioinformatics plugins toward genomics-assisted breeding.**

# License
NARO NON-COMMERCIAL LICENSE AGREEMENT Version 1.0

This license is for 'Non-Commercial' use of software for IonBreeders.

1. Scientific use of IonBreeders is permitted free of charge.
2. Modification of IonBreeders is only permitted to the person of downloaded and his colleagues.
3. The National Agriculture and Food Research Organization (hereinafter referred to as NARO) does not guarantee that defects, errors or malfunction will not occur with respect to IonBreeders.
4. NARO shall not be responsible or liable for any damage or loss caused or be alleged to be caused, directly or indirectly, by the download and use of IonBreeders.
5. NARO shall not be obligated to correct or repair the program regardless of the extent, even if there are any defects of malfunctions in IonBreeders.
6. The copyright and all other rights of IonBreeders belong to NARO.
7. Selling, renting, re-use of license, or use for business purposes etc. of IonBreeders shall not be allowed. For commercial use, license of commercial use is required. Inquiries for such commercial license are directed to demeter@affrc.go.jp.
8. The IonBreeders may be changed, or the distribution maybe canceled without advance notification.
9. In case the result obtained using IonBreeders in used for publication in academic journals etc., please refer the publication of IonBreeders in the publication (in preparation).


Copyright (C) 2019 [National Agriculture and Food Research Organization](https://www.naro.affrc.go.jp/english/index.html). All rights reserved.
