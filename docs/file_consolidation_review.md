
# Review of Member 1's Data Consolidation

**Reviewer:** Member 4 <br>
**Date:** 11/8/2025 <br>
**Branch Tested:** <br>
**File reviewed:** models/model.ipynb <br>



## Testing Steps
- Created a branch containing models/model.ipynb
- Verified data files were present 
- Ran code in the notebook
- Debugged Errors to get code working
- Verified consolidated output file was created
- Checked files to verify why some files only loaded 1 sheet

 **Note:** I focused on testing for reproducibility and consolidation. I did not test for data quality/cleaning. Member 1 or 2 should verify whether the data is clean.

 
## Results 

### What Worked
- Consolidated Output file was successfully created in the dedsignated location
- Each year (2014 - 2024) was correctly added and merged 
- Data appears complete for years with data files with 12 months of data 
- Fairly fast processing time: 45.6 secs (may be faster with better internet speed)
- Output has  rows and  columns

### Issues Encountered
**Incorrect file path**
- Got a FileNotFoundError
- The code had DATA PATH = "data" but files are in "/data/raw" folder.
- My fix: I changed file path to "../ML_12/data/raw" (this may not work for everyone however)

**Missing Dependency**
- Value Error: No objects to concatenate
- The issue missing openpyxl
- I have created a requirements.txt file and added openpyxl to it

**Incomplete 2025 data**
- Only 1 sheet was loaded for 2022-2025. The 2022-2024 files have only 1 sheet.
- Findings: 2022-2024 files correctly have only 1 sheet (annual data).
  However 2025 has 10 sheets but only 1 appears to have been loaded. 9 Months of data is missing.
  

## Suggestions

### Critical Fixes Needed
1. Update DATA PATH to correct file path. Files are in located in "data/raw" Use relative file path that works for everyone
2. Either load all 10 months for 2025 Or ***exclude 2025 alltoghether*** as it may skew analysis having only 10 months of data instead or 12 months of data like the other years.
3. Add openpyxl==3.1.2 to requirements.txt ***(I have completed this one)***
4. Add error handling for missing openpyxl to code: # Check for required Excel engine. Error handling if openpyxl is missing. 
try:
    import openpyxl
except ImportError:
    print("Missing dependency: openpyxl. Run `pip install -r requirements.txt` to install all required packages.")


### Importnt - Action Needed
**Data Cleaning** 

**Note: I did NOT check if data needs cleaning. This is critical!**

**Questions for Member 1 or Member 2:**
- Are there missing values? How should we handle them?
- Are there duplicate records?
- Are incident types consistent across years (same spelling/categories)?
- Are column names standardized across all files?
- Do we need to remove any invalid data (e.g., negative delays)?

**Recommendation:** 
- **Member 1:** Add data quality checks to your code (check for missing values, duplicate rows, date issues if not already included)
- **Member 2:** Verify data quality during EDA and document any issues found
_ **Member 1:** Please make these changes so that Member 2 can start EDA by Sunday with clean data.


## Review Status

###Approved with required changes [x]
The code logic works well! Once you fix the Issues flagged above, it is good to merge.

## Notes
Excellent processing performance. Adding error handling etc will make it production ready
**Next Steps:** After Member 1 updates, Member 2 should verify data quality during EDA.
