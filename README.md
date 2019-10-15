# IonBreeders_ABH version 1.0
Genotyping plugin for the Ion Torrent NGS platform.


[IonBreeders_ABHの使い方 日本語版 ver.1.0 ](https://github.com/DEMETER298/IonBreeders_ABH/wiki)


# 1. Installation Instructions

## Download plugins
The ABH plugin of IonBreeders is provided as a zipped package containing files from the Latest Release project page on Github. The file name will be of the format IonBreeders_ABH.zip.
1. Click the "Clone or download" in the upper right and **`Download ZIP`** button
![install](https://user-images.githubusercontent.com/40309394/66794248-b7f66d00-ef3b-11e9-9fee-8f30137739be.png)
2. Unzip the downloaded IonBreeders_ABH-master.zip file in your PC


## Install
Automatic installation from the Torrent Browser Plugin  
Follow these steps for automatic installation of a plugin from the Torrent Browser:  
1.	In your Torrent Browser, click the gear menu (near the top right) and select Plugins

![1](https://user-images.githubusercontent.com/40309394/54818632-14aee380-4cdd-11e9-845c-7c7d8ac95a1f.png)
  
2.	In the Plugins tab, click the **`Install or Upgrade Plugin`** button: 

![2](https://user-images.githubusercontent.com/40309394/54819228-8fc4c980-4cde-11e9-92ba-1d4b64e70e64.png) 

3.	In the **`Install or Upgrade Plugin`** tab, select IonBreeders_ABH.zip file in  IonBreeders_ABH-master folder, and click **`Upload and Install`**.  
 



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

 #### Input format:  
Input file of mother genotype (mother_input.csv). This file can be edited and saved in Excel as csv file.  
![genotype_mother](https://user-images.githubusercontent.com/40309394/54862344-d406a700-4d7c-11e9-9f5a-72aaae15a94b.png)   

Input file of father genotype (father_input.csv) This file can be edited and saved in Excel as csv file.  
![genotype_father](https://user-images.githubusercontent.com/40309394/54862345-d6690100-4d7c-11e9-9f32-83b076fd7dd9.png)   
  
HotSpot file for VariantCaller plugin (Hotspot.vcf) This file can be edited and saved in Excel as tab-delimited txt file.  
![hotspot_example](https://user-images.githubusercontent.com/40309394/54862343-d10bb680-4d7c-11e9-95ab-408985079718.png)


 #### Example:  
![Github_parentalgenotype_hotspot](https://user-images.githubusercontent.com/40309394/65664271-f5ba5100-e073-11e9-990c-d37ff6cd4e1d.png)  
These files are the data used in the following paper:  

Targeted sequencing of polymorphic sites and construction of genetic linkage map using AmpliSeq technology.  
Eri Ogiso-Tanaka, Fumio Taguchi-Shiobara, Akito Kaga, Makita Hajika and Masao Ishimoto.  
Breeding Science (in submitted)  
  
  


### 2-3 Execution:

(1) Execute the VairantCaller plugin with the HotSpot specified on the corresponding run report.



(2) When the VariantCaller plugin is completed, record the serial number (arrow).


　　　　<img src="https://user-images.githubusercontent.com/40309394/65664999-7af23580-e075-11e9-8291-867d46cb7f4f.png" width="350">  
 

(3) Click the **`Select Plugins To Run`** button on the top of the Torrent Browser report screen.

　　　　<img src="https://user-images.githubusercontent.com/40309394/54862396-68710980-4d7d-11e9-8b1c-60a429933818.png" width="450">  


(4) From the list of plugins, click **IonBreeders_ABH**.

(5) Set each item on the screen as follows:

![ABH_screen](https://user-images.githubusercontent.com/40309394/65666640-091beb00-e079-11e9-9008-fc4b911c7389.png)
An error occurs if the number of genotyping sites is too large (acceptable parent genotype file size is up to about 2Mb) At that time, select target chromosomes and reduce analysis regions.  
  
    
**Items**  
`Samples`: A list of barcode names and sample names of the samples analyzed in the run is displayed.

`Selected`: A list of the selected barcode and sample names is displayed. Select a line in the Samples column and click the `add sample` button to add a new sample.

`VariantCaller ID`: Enter the serial number of the VariantCaller plugin execution result confirmed in (2) above.

`No parent genotype available`: Select if you do not have parent genotype data. Reference-based genotype is output in its place.

`Select father genotype file`: Select the father genotype file.

`Select mother genotype file`: Select the mother's genotype file.

`Output file name prefix`: Enter the desired file name.  
  
  
(6) Output contents  
When execution is completed, the following items are displayed on the screen.  
#### 6-1 The output when parental genotypes are input (ABH format) appears as shown below.

![ABHoutput_withParent](https://user-images.githubusercontent.com/40309394/65670039-8d716c80-e07f-11e9-98f1-6e9516a6d3c7.png)

`list of barcode/sample used:`: Correspondence table of barcode name and sample name.

`list of markers with region names:` Correspondence table of marker name and amplicon name (Only when the target regions of amplicons are specified (.bed file) in VariantCaller). If no amplicon target is specified, the amplicon name will be displayed as N/A.  

`ABH (markers in rows/samples in columns)`: the CSV output file can be opened in Excel as shown below.  
 
<img src="https://user-images.githubusercontent.com/40309394/65671363-11c4ef00-e082-11e9-81e8-bea799be892d.png" width="800">  

`ABH (marker in column/sample in row)`: the CSV output file can be opened in Excel as shown below.  

<img src="https://user-images.githubusercontent.com/40309394/65672687-67020000-e084-11e9-9f2c-c3b12583ac59.png" width="800">  
  
`ABH (R/qtl)`: the CSV output file for R/qtl format can be opened in Excel as shown below.
The letters are removed from sample name so that each sample is identified only by unique numbers. Output ABH-encoded genotype file only when parents genotype information is given.

<img src="https://user-images.githubusercontent.com/40309394/65671484-4d5fb900-e082-11e9-9b82-8caf8e2905c5.png" width="650">   



#### 6-2 The output when no parent data are input (reference-based format) appears as shown below:  
 
![output_abh_NoParent](https://user-images.githubusercontent.com/40309394/65672964-e5f73880-e084-11e9-9fb7-0a82e208c1ac.png)

`List of barcode/sample used`: Barcode and sample name correspondence table.

`The ABH (markers in rows/samples in columns)`:  output file can be opened in Excel.

`The ABH (markers in columns/samples in rows)`: output file can be opened in Excel as shown below.

![noParent_output](https://user-images.githubusercontent.com/40309394/65673657-2c996280-e086-11e9-9beb-b1a4245c6262.png)

The genotype is expressed as reference-type homozygous (Absent), variant homozygous (Homozygous), hetero (Heterozygous), and missing (NoCall).

If there are two marker names at the same variant, 2 markers integrated into 1 marker name as follows.
* Hotspot site (2 marker names, but variant is same)  
Chr01 3405219 Chr01_3405219_AT_AA  
Chr01 3405220 Chr01_3405220_T_A  

* ABH output (2 marker names are integrated 1 marker as following)  
Chr01 3405220	  Chr01_3405219_AT_AA_Chr01_3405220_T_A  


**Missing genotype**  
NoCall_0 indicated that no reads were aligned at the site. NoCall_X indicate that despite aligning X reads at the site, no variant could be detected.  
When the read depth required for variant detection is x10 in the parameter of VariantCaller. If the read depth is less than 10, variant is not detected and it becomes “No Call”. In addition, when variant detection is difficult (such as homopolymer sites), it may become “No Call” even if there is a sufficient read depth.
 
 
`ABH(marker in row/sample in column)`:output file can be opened in Excel as shown below.  
![noParent_ABH](https://user-images.githubusercontent.com/40309394/65673757-60748800-e086-11e9-9b77-948872104263.png)  

`ABH(R/qtl,IonBreeders)`:output file can be opened in Excel as shown below.  
<img src="https://user-images.githubusercontent.com/40309394/65673853-9154bd00-e086-11e9-8415-c5223f550a28.png" width="650">  






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
