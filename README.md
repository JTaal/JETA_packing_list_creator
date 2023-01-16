# JETA_packing_list_creator
Python application using PySimpleGUI to create packing lists from [Open Source Point of Sale](https://github.com/opensourcepos/opensourcepos) order info
 
# How to use

Below is a list of all the steps which make up the general use case of this program. This is meant as a guidance not a definitive method of using the program. In the troubleshoot section, the layout and inner workings of the program are explained. Using this information, you could troubleshoot the current method or develop a different one.
## 1.1	Make an order in OSPOS
Navigate to the sales section in the main menu to start making an order. Then add the customer you’d like to send a shipment to, on the top right. Then start adding all the items into the shopping cart and give the correct amount and price. If there is an item with multiple different prices, then take them from the virtual locations so that you’ll be able to adjust the prices individually (because the same item is added in as a separate item).

![Figure 1  The main menu in OSPOS](https://user-images.githubusercontent.com/71385957/212723686-56cb5d9e-e621-474e-94df-09b49978cab4.PNG)
<sub> Figure 1. The main menu in OSPOS </sub>

![Figure 2  The sales section with in OSPOS](https://user-images.githubusercontent.com/71385957/212723815-07d26662-6735-45c3-b1bd-6da02cb4667b.PNG)
<sub> Figure 2. The sales section with in OSPOS with nothing filled in yet </sub>

![Figure 3  Adding in a customer name which can be selected](https://user-images.githubusercontent.com/71385957/212723834-bc5e195b-c52f-424f-97bc-df256c830de5.jpg)
<sub> Figure 3. Adding in a customer name which can be selected </sub>

![Figure 4  Adding an item to the shopping cart](https://user-images.githubusercontent.com/71385957/212723851-f2b73a2a-ba79-4d44-82d3-7bbd7a7ae36e.png)
<sub> Figure 4. Adding an item to the shopping cart </sub>

![Figure 5  Finishing the order by entering the register mode invoice](https://user-images.githubusercontent.com/71385957/212723864-bc88e391-0393-45ff-998a-d5b09abaf898.png)
<sub> Figure 5. Finishing the order by entering the register mode: invoice. </sub>
 
![FIEF8B~1](https://user-images.githubusercontent.com/71385957/212723877-dd0ceea1-17ad-469d-b4bb-d66aeab9363c.PNG)

<sub> Figure 6. Finalising the order by adding the PO number in the comments and the invoice number. To generate the invoice and log the transaction press the invoice button. </sub>

## 1.2	Copy detailed description from OSPOS
To get the order information you’ll have to navigate to the reports section in OSPOS. Within this section you’ll see on the top right side of image X that detailed reports section. There you can enter the transactions log which will contain all the orders. You’ll have to adjust the date range to contain the order you made. Figure x shows the date range being changed to “All time”. Navigate to the order you’d like to create a packing list from and press the + icon on the left side of the row. Copy the contents of the order (with or without headers).
 
![Figure 7  Reports tab within OSPOS and the Detailed reports section with at the top the transactions tab](https://user-images.githubusercontent.com/71385957/212723888-d68ecaf4-4f83-4f3d-a742-380a1fe605f4.png)
<sub> Figure 7. Reports tab within OSPOS and the Detailed reports section with at the top the transactions tab </sub>

![FIA9CD~1](https://user-images.githubusercontent.com/71385957/212723907-748d3e74-1d56-45a9-bbec-5ec92f9242c7.PNG)
<sub> Figure 8. Within the detailed transactions report adjusting the Date Range to "All time" to reveal all the transactions ever performed </sub>

![FIGURE~1](https://user-images.githubusercontent.com/71385957/212723914-6faff870-d944-439b-b4d1-1de4834ae208.JPG)
<sub> Figure 9. All the transactions that have been logged with their respective contents. To access the order description you'll have to press the + icon on the left side of the individual rows </sub>

![Figure 10  The opened order that was made and all its contents being copied](https://user-images.githubusercontent.com/71385957/212723929-9c1fd6bd-63ad-41cf-9771-50ae22d9abd9.PNG)
<sub> Figure 10. The opened order that was made and all its contents being copied. This can be done both with and without headers just make sure that the order file headers are changed properly. Otherwise, you'll be able to find the dictionary with all the hard coded headers in the troubleshoot section. </sub>
 

## 1.3	Insert the detailed description into the order file
Simply paste the information copied from the detailed transaction report over to the order file then save(!) and close the file. If you leave the file open, you’ll run into a permission error of python trying to access the file but not being allowed to by windows.


![image](https://user-images.githubusercontent.com/71385957/212724841-8fed5242-8734-4cde-b93a-0aa612d5f1a9.png)

<sub> Figure 11. The order content being saved into the order file below the headers. Be sure to check the correct location of the information being pasted and their respective headers. The headers can't be changed since these are hardcoded into the program. Refer to the troubleshooting section to find the dictionary with the headers. </sub>

## 1.4	Open JETA_Packing_list_creator
Navigate to the JETA_Packing_list_creator folder which you downloaded. Then find the JETA_Packing_list_creator.exe and simply open it. The file should open albeit with a warning telling you the customer list is empty.  
 
## 1.5	Fill in all the necessary additional information and designated the correct pathways

You’ll have to point the program to the correct files located within the required files folder nested in the JETA_Packing_list_creator folder. If you’ve selected the correct documents, then you’ll need to save the pathways by pressing save. After that, exit the program by pressing X at the top right and open the .exe again. This time there should be no prompt and you’ll see a list of all the customer names if you open the list in the customer section. Once that is done, you’re setup to start creating packing lists.
 
## 1.6	Create the packing list
Now simply add all the additional information needed to complete a packing list and press the submit button. If everything is alright, you’ll receive a prompt stating that the packing list has been created. If not consult the troubleshooting section within this documentation.
 
## 1.7	Check the packing list for mistakes
As a final control always check the document for any mistakes. If there is something wrong with the items list, then locate which part of the packing list contains the mistakes. Using the figure below you can figure out where the mistake originated from, and you’ll be able to perform the needed corrective actions. 
 
![Troubleshoot picture white background smaller](https://user-images.githubusercontent.com/71385957/212729401-4e0f796a-2eba-473c-8916-1aa571c7eef1.png)

# Troubleshoot

## Required files:
##### 1.	Packing list log.xlsx

The packing list log is a simple excel sheet which records all the packing lists created. This document could be used to keep a complete record by forcing the users to link their pathway to the same file or individuals could retain the link to their own copies of the packing list log. The program will still function even if the pathway is left blank. Very few problems should arise from this file and if they do you can simply purge the entire file if necessary.

```python
if values["log file location"] == "" and isfile(base_dir / "1. Packing list log.xlsx"):
   values["log file location"] = base_dir / "1. Packing list log.xlsx"    
try:
   excel_path = values["log file location"]
   df = pd.read_excel(excel_path)
   log_data["date"] = current_time
   log_data["Save location"] = values["output folder location"] #Double save location index addition
   df = pd.concat([df, pd.DataFrame(log_data, index=[0])], ignore_index=True)
   df.to_excel(excel_path, index=False)
except Exception as exception:
   sg.popup_auto_close("Couldn't open log file!\n\n" + str(exception), keep_on_top=True)
```

##### 2.	Order file.xlsx

The barcode format used is EAN13 and requires an integer number of 12 characters casted as a string. Due to data casting, the barcode number absolutely can NOT contain any special characters. The only numbers allowed are.
•	A 12-character integer or 12-character float.
o	012345678912 & 012345678912.0000
The barcode is checked and cast according to the code below. A float is bottom rounded to an integer and then converted to a string.

```python
if (type(record["Barcode"]) == str or type(record["Barcode"]) == float) and record["Barcode"] != "":
    record["Barcode"] = str(int(float(record["Barcode"])))
```

The order file is read into python per row and the values are paired to the headers in a dictionary (key:value).
The header is therefor case sensitive (because keys are hashed for faster lookup times) and as of version 3.3.8 are the same as the output of OSPOS detailed reports. When setting up OSPOS the attributes should be named according to the keys shown in the code below.

```python
#Here a list of the headers/keys used to read in the required values.

 row["cols"] = [ record["Barcode"],
     record["REF"], 
     record["Name"], 
     record["Description"], 
     record["Category"], 
     record["LOT"], 
     record["Expiration_date"], 
     int(str(record["Qty"]).split("[")[0]), 
     int(str(record["Qty"]).split("[")[0]), 
     "0"
       ]
```

Due to a client requiring us to add their own classification system in terms of an “item code” to the packing list whenever we want to send something to them the following code is executed, to add the “item code”:

```python
#Exception made for Turku while generating the items list
 
if customername.lower() == "client_name":
 	row_list = row["cols"]
 	row_list.insert(1, record["Item_code"])
```

##### 3.	JETA Packing list customer info.xlsx

This file is named “3. JETA Packing list customer info.xlsx” and located inside the required files folder.
For the program to function properly it requires the user to assign the pathway to the customer information. This file needs to contain the headers in the table shown below and especially “DISPLAY_NAME”. If there is a problem with the file, the program will default to empty strings and prompt the user to correct the problem and restart. Without the customer information you’re not able to create a packing list.
 
Troubleshoot:
 1.	If you made changes to this document (especially the headers), it could be that it can’t be imported properly. Check whether the document you’re currently referencing to, contains the same headers as shown above. (These keys have to be exactly the same)
 2.	If changing the document didn’t fix your problem and you still can’t start the program. Then you should clear all the saved pathway settings (Code below or run CLEAR_PATHWAY_SETTINGS.PY) to allow the program to default back to empty strings rather than opening something malicious. 
Another option could be to simply delete the file "user_settings.json" in the same folder as the executable.

```python
import os
import PySimpleGUI as sg

def user_settings(filename = "user_settings.json", path = os.path.dirname(os.path.realpath(__file__)), clear = False):    
    sg.user_settings_filename(filename, path=path)
    if clear == True:
        clear_dict = {"Clear History log": "-path_log-", "Clear History order": "-path_order-", "Clear History customer": "-path_customer-", "Clear History output":                       "-path_output-", "Clear History mother": "-path_mother-"}
        for key in clear_dict:
            sg.user_settings_set_entry(clear_dict[key], [])
        print("Clearing setting files executed!")
    return

user_settings(clear=True)
```

Note:
After the key “DISPLAY_NAME” all headers will be placed from left to right in line 1 till 4 within the packing list on the top left. Otherwise as can be seen in the mother packing list, the keys are not specified in lines but rather the Keys shown below.

##### 4.	Mother-packing-list.docx 

The mother packing list is the template that is later rendered into a usable packing list. All the items/information that will be rendered is designated with a key inside of a dictionary. These keys can NOT be changed and will break the script when done so. Anything that does not look like {{EXAMPLE}} or {example} can be changed or modified without too much trouble. Be careful though changes made to the mother packing list will influence all subsequent packing lists made. Therefor please make sure to create a copy of the original which has been tested to produce good looking packing lists. 
##### PACKING LIST
The information used to render parts of the packing list are taken from different sources. The sources are further highlighted in the figure below and should be your first reference when troubleshooting unexpected output.

```jinja
To: {{NAME}}	        Date:	       {{DATE}}
    {{ADDRESS}}	     Invoice:	    {{INVOICE_NR}}
    {{POSTAL_CODE}}	 PO:	         {{PO}}
    {{TAX_NR}}	      Description:	{{DESCRIPTION}}

            {{SHIPPING_WARNING}}

{%tc for col in col_labels %}	{{col}}	{%tc endfor %}
         {%tr for item in tbl_contents %}
{%tc for col in item.cols %}	{{col}}	{%tc endfor %}
                {%tr endfor %}
```

## Additional script/folder:
##### 1.	Output folder
##### 2.	CLEAR_PATHWAY_SETTINGS.py

Probably the most common error will be the permission error. This error occurs whenever the script tries to access a file which is already open. This will likely happen when checking the latest packing list and making adjustment while the document is open. The program will automatically restart for you however, your previous input in the “Input Elements” tab will unfortunately be lost. If there are no documents open when this occurs, please check your permissions regarding the files you’re using. 
 
A proposed fix might be to run the .exe in administrative mode. You do this by right clicking the .exe and then “Properties”. Check the box next to “Run this program as an administrator in the Compatibility tab.

## 2.3	Recompile code
So, this is a tricky one. If you were to make changes to the code and want to recompile the code using pyinstaller you’ll have to make changes to the code inside of the barcode library. Because your local version will probably still work, however any other computer will fail to render barcodes due to a font error occurring. The fix can be found here:

https://stackoverflow.com/questions/71448645/after-turning-a-python-file-into-a-exe-file-the-barcode-module-stops-working 

###### Otherwise here is the text in case this thread disappears:
> The solution is quite strange and it is mentioned in IO Error:Cannot open image while generating barcode after freezing using py2exe but what you need to change has changed a tad bit so felt I could make this thread to help any beginners not knowing how to fix this.
> The solution is to change this line of code:

```python
self.font_path = os.path.join(PATH, "fonts", "DejaVuSansMono.ttf")
```

> In the file writer.py in C:\Users\TERMINTATOR\AppData\Local\Programs\Python\Python310\Lib\site-packages\barcode .
To this:

```python
self.font_path = 'arial.ttf' 
```
