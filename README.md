
Issue: Taking a .csv file from a web scraper or any .csv file and using that for a Django fixture

**Step 1**
I'm a noob at web scraping so I used Open Web Scraper (a chrome extension).
I selected the names of the items so I am able to get the tag associated with that tag
after doing so I run the scraper and I am left with a downloadable .csv file

**Step 2**
Now that we have our .csv file the easiest way I was able to remove some useless information
was to import the file (File > Import > "path to your .csv") into google sheets. Delete the columns 
you dont need and add a column named pk or id depending on what you need, in my case pk. 
in the first row of your pk/id column type 1 in the row below the 1 type `=B2  +  1` this 
should return 2 and you will want to copy/paste this formula down the rest of the column. 

**Step 3** 
After your sheets file looks to your liking you make your way to File > Download > .csv
once you have downloaded your .csv open the file in any text editor and select all of the text
and copy. Navigate to https://csvjson.com/csv2json and paste your copied csv into the field on
the left and hit convert, if this data looks good for your purpose then hit copy.

**Step 4**
next you're gonna want to install jq im using ubuntu 18.04 so the command for me is 
`sudo apt-get install jq`. Once you jq installed navigate to your project folder and make a new .json file 
open up your new .json file and paste the data we copied. After pasting your data move back to your terminal and to convert this .json file to a Django fixture format you will want this command 
jq 'map({model: "**name of model** ", **pk/id**: .**pk/id**, fields:{ **new data name**: .**data name in your original json file**  }})' **filename.json** > **newfile.json**
everything above in bold can be changed to the data you have, and after inputting your own data you should be left with a second file containing your data formatted into a Django fixture.
