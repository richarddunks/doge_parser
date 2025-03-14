# Summary
Doge is providing the receipts, so let's look at the results.

# Objective
To parse the data from the doge.gov website and see what the impact of these cuts are across the country. Interested in joining? [email us](mailto:dogeparser@gmail.com)

# Method
1. Scrape the contracts from [doge.gov/savings](https://doge.gov/savings) -> saved as [doge-2025-03-05.csv](data/doge-2025-03-05.csv) and [doge-2025-03-05.xlsx](data/doge-2025-03-05.xlsx)
2. Scrape the contents of the linked entry in FDPS
3. Fix the errors from differing fields
4. Publish to the web as [20250305_FPDSData_DOGE_CancelledContracts_.csv](data/20250305_FPDSData_DOGE_CancelledContracts_.csv) and [20250305_FPDSData_DOGE_CancelledContracts_.xlsx](data/20250305_FPDSData_DOGE_CancelledContracts_.xlsx)

# Key formulas for parsing data in Excel
## Extracting PIID from FPDS link download from [doge.gov/savings](https://doge.gov/savings)
```
=MID(D2,FIND("&PIID=",D2)+6,FIND("&modNumber=",D2)-(FIND("&PIID=",D2)+6))
```

## Parse the MAINBODY field
Copy the MAINBODY field into the last column (`AS2`) and then create a column for each type

| Column Name | Formula to Extract from `MAINBODY` | Description |
| --- | --- | --- |
| CORPORATE_ENTITY_NOT_TAX_EXEMPT | `=IF(ISERROR(FIND("Corporate Entity, Not Tax Exempt",$AS2)),0,1)` | Entity is not tax exempt |
| CORPORATE_ENTITY_TAX_EXEMPT | `=IF(ISERROR(FIND("Corporate Entity, Tax Exempt",$AS2)),0,1)` | Entity is tax exempt |
| ALASKAN_NATIVE_CORP_OWNED | `=IF(ISERROR(FIND("Alaskan Native Corporation Owned Firm",$AS2)),0,1)` | Listed as an Alaskan Native Corporation Owned Firm |
| AMERICAN_INDIAN_OWNED | `=IF(ISERROR(FIND("American Indian Owned",$AS2)),0,1)` | Listed as an American Indian Owned entity |
| TRIBALLY_OWNED_FIRM | `=IF(ISERROR(FIND("Tribally Owned Firm",$AS2)),0,1)` | Listed as a Tribally Owned entity |
| MINORITY_OWNED_BUSINESS | `=IF(ISERROR(FIND("Minority-Owned Business",$AS2)),0,1)` | Listed as a Minority-Owned entity |
| ASIAN_PACIFIC_AMERICAN_OWNED | `=IF(ISERROR(FIND("Asian-Pacific American Owned",$AS2)),0,1)` | Listed as an Asian-Pacific American Owed entity |
| BLACK_AMERICAN_OWNED_BUSINESS | `=IF(ISERROR(FIND("Black American Owned",$AS2)),0,1)` | Listed as Black American Owned entity|
| SERVICE_DISABLED_VETERAN_OWNED_BUSINESS | `=IF(ISERROR(FIND("Service-Disabled Veteran-Owned Business",$AS2)),0,1)` | Listed as a Service-Disabled Veteran-Owned Business |
| VETERAN_OWNED_BUSINESS | `=IF(ISERROR(FIND("Veteran-Owned Business",$AS2)),0,1)` | Listed as a Veteran-Owned Business |
| WOMAN_OWNED_BUSINESS | `=IF(ISERROR(FIND("Women-Owned Business",$AS2)),0,1)` | Listed as a Woman-Owned Business |
| WOMAN_OWNED_SMALL_BUSINESS | `=IF(ISERROR(FIND("Women-Owned Small Business",$AS2)),0,1)` | Listed as a Woman-Owned Small Business |
| CERT_SMALL_DISADVANTAGED_BUSINESS | `=IF(ISERROR(FIND("Self-Certified Small Disadvantaged Business",$AS2)),0,1)` | Listed as a Self-Certified Small Disadvantaged Business |
| FOR_PROFIT_ORG | `=IF(ISERROR(FIND("For Profit Organization",$AS2)),0,1)` | Listed as a For Profit Organization |
| LLC | `=IF(ISERROR(FIND("Limited Liability Corporation",$AS2)),0,1)` | Listed as a Limited Libability Corporation |
| COMMUNITY_DEVELOPMENT_CORP | `=IF(ISERROR(FIND("Community Development Corporation",$AS2)),0,1)` | Listed as a Community Development Corporation |
| CERT_SBA_HUBZONE | `=IF(ISERROR(FIND("SBA Certified HUBZone Firm",$AS2)),0,1)` | Listed as a SBA Certified HUBZone Firm |
| CERT_DOT_DISADVANTAGED_BUSINESS_ENTERPRISE | `=IF(ISERROR(FIND("DoT Certified Disadvantaged Business Enterprise",$AS2)),0,1)` | Listed as a DoT Certified Disadvantaged Business Enterprise |
| EDWOSB_JOINT_VENTURE | `=IF(ISERROR(FIND("Economically Disadvantaged Women-Owned Small Business (EDWOSB) Joint Venture",$AS2)),0,1)` | Listed as a Economically Disadvantaged Women-Owned Small Business (EDWOSB) Joint Venture |
| EDUCATIONAL_INSTITUTION | `=IF(ISERROR(FIND("Educational Institution",$AS2)),0,1)` | Listed as an Educational Institution |
| FEDERAL_AGENCY | `=IF(ISERROR(FIND("Federal Agency",$AS2)),0,1)` | Listed as a Federal Agency |
| FEDERALLY_FUNDED_RESEARCH_DEVELOPMENT_CORP | `=IF(ISERROR(FIND("Federally Funded Research and Development Corp",$AS2)),0,1)` | Listed as a Federally Funded Research and Development Corp |
| FOREIGN_OWNED | `=IF(ISERROR(FIND("Foreign Owned",$AS2)),0,1)` | Listed as a Foreign Owned entity |
| FOUNDATION | `=IF(ISERROR(FIND("Foundation",$AS2)),0,1)` | Listed as a Foundation |
| HISPANIC_AMERICAN_OWNED | `=IF(ISERROR(FIND("Hispanic American Owned",$AS2)),0,1)` | Listed as a Hispanic-American Owned entity |
| HISPANIC_SERVICING_INSTITUTION | `=IF(ISERROR(FIND("Hispanic Servicing Institution",$AS2)),0,1)` | Listed as a Hispanic Servicing Institution |
| HBCU | `=IF(ISERROR(FIND("Historically Black College or University (HBCU)",$AS2)),0,1)` | Listed as a Historically Black College or University (HBCU) |
| HOSPITAL | `=IF(ISERROR(FIND("Hospital",$AS2)),0,1)` | Listed as a Hospital |
| INDIAN_TRIBE | `=IF(ISERROR(FIND("Indian Tribe (Federally Recognized)",$AS2)),0,1)` | Listed as a Federally Recognized Indian Tribe |
| INTER_MUNICIPAL | `=IF(ISERROR(FIND("Inter-Municipal",$AS2)),0,1)` | Listed as a Inter-Municipal entity |
| INTERNATIONAL_ORG | `=IF(ISERROR(FIND("International Organization",$AS2)),0,1)` | Listed as an International Organization |
| GOODS_MANUFACTURER | `=IF(ISERROR(FIND("Manufacturer of Goods",$AS2)),0,1)` | Listed as a Manufacturer of Goods |
| MUNICIPALITY | `=IF(ISERROR(FIND("Municipality",$AS2)),0,1)` | Listed as a Municipality |
| MINORITY_INSTITUTIONS | `=IF(ISERROR(FIND("Minority Institutions",$AS2)),0,1)` | Listed as a Minority Institution |
| NATIVE_AMERICAN_OWNED | `=IF(ISERROR(FIND("Native American Owned",$AS2)),0,1)` | Listed as Native American Owned entity |
| NATIVE_HAWAIIAN_OWNED | `=IF(ISERROR(FIND("Native Hawaiian Organization Owned Firm",$AS2)),0,1)` | Listed as a Native Hawaiian Organization Owned Firm |
| NON_PROFIT_ORG | `=IF(ISERROR(FIND("Non Profit Organization",$AS2)),0,1)` | Listed as a Non Profit Organization |
| OTHER_GOV_ENTITIES | `=IF(ISERROR(FIND("Other Governmental Entities",$AS2)),0,1)` | Listed as an Other Governmental Entity |
| OTHER_NOT_FOR_PROFIT | `=IF(ISERROR(FIND("Other Not For Profit Organization",$AS2)),0,1)` | Listed as an Other Not for Profit Organization |
| PARTNERSHIP_LLP | `=IF(ISERROR(FIND("Partnership or Limited Liability Partnership",$AS2)),0,1)` | Listed as a Partnership or Limited Liability Partnership |
| PRIVATE_UNIVERSITY_COLLEGE | `=IF(ISERROR(FIND("Private University or College",$AS2)),0,1)` | Listed as a Private University or College |
| CERT_SBA_8A_JV | `=IF(ISERROR(FIND("SBA Certified 8(a) Joint Venture",$AS2)),0,1)` | Listed as an SBA Certified 8(a) Joint Venture |
| CERT_SBA_8A_PROGRAM_PARTICIPANT | `=IF(ISERROR(FIND("SBA Certified 8(a) Program Participant",$AS2)),0,1)` | Listed as an SBA Certified 8(a) Program Participant |
| CERT_SBA_EDWOSB | `=IF(ISERROR(FIND("SBA-Certified Economically Disadvantaged Women-Owned Small Business",$AS2)),0,1)` | Listed as an SBA-Certified Economically Disadvantaged Women-Owned Small Business |
| CERT_SBA_WOMEN_OWNED_SMALL_BUSINESS | `=IF(ISERROR(FIND("SBA-Certified Women-Owned Small Business",$AS2)),0,1)` | List as an SBA-Certified Women-Owned Small Business |
| SCHOOL_OF_FORESTRY | `=IF(ISERROR(FIND("School of Forestry",$AS2)),0,1)` | Listed as a School of Forestry |
| SELF-CERT_HUBZONE_JV | `=IF(ISERROR(FIND("Self-Certified HUBZone Joint Venture",$AS2)),0,1)` | Listed as a Self-Certified HUBZone Joint Venture |
| SELF_CERT_SMALL_DISADVANTAGED_BUSINESS | `=IF(ISERROR(FIND("Self-Certified Small Disadvantaged Business",$AS2)),0,1)` | Listed as a Self-Certified Small Disadvantaged Business |
| SERVICE_DISABLED_VETERAN_OWNED_BUSINESS_JV | `=IF(ISERROR(FIND("Service-Disabled Veteran-Owned Business Joint Venture",$AS2)),0,1)` | Listed as a Service-Disabled Veteran-Owned Business Joint Venture |
| SMALL_BUSINESS_JV | `=IF(ISERROR(FIND("Small Business Joint Venture",$AS2)),0,1)` | Listed as a Small Business Joint Venture |
| SOLE_PROPRIETORSHIP | `=IF(ISERROR(FIND("Sole Proprietorship",$AS2)),0,1)` | Listed as a Sole Proprietorship |
| STATE_CONTROLLED_INST_HIGHER_LEARNING | `=IF(ISERROR(FIND("State Controlled Institution of Higher Learning",$AS2)),0,1)` | Listed as a State Controlled Institution of Higher Learning |
| SUBCHAPTER_S_CORP | `=IF(ISERROR(FIND("Subchapter S Corporation",$AS2)),0,1)` | Listed as a Subchapter S Corporation |
| SUBCONTINENT_ASIAN_AMERICAN_OWNED | `=IF(ISERROR(FIND("Subcontinent Asian (Asian-Indian) American Owned",$AS2)),0,1)` | Listed as a Subcontinent Asian (Asian-Indian) American Owned entity |
| ABILITYONE_PROGRAM | `=IF(ISERROR(FIND("The AbilityOne Program",$AS2)),0,1)` | Listed as an AbilityOne Program participant |
| TRANSIT_AUTHORITY | `=IF(ISERROR(FIND("Transit Authority",$AS2)),0,1)` | Listed as a Transit Authority |
| US_FEDERAL_GOV | `=IF(ISERROR(FIND("U.S. Federal Government",$AS2)),0,1)` | Listed as a US Federal Government entity |
| US_LOCAL_GOV | `=IF(ISERROR(FIND("U.S. Local Government",$AS2)),0,1)` | Listed as a US Local Government entity |
| US_STATE_GOV | `=IF(ISERROR(FIND("U.S. State Government",$AS2)),0,1)` | Listed as a US State Government entity |
| VETERINARY_COLLEGE | `=IF(ISERROR(FIND("Veterinary College",$AS2)),0,1)` | Listed as a Veterinary College |
| WOMAN_OWNED_SMALL_BUSINESS_JV | `=IF(ISERROR(FIND("Women-Owned Small Business (WOSB) Joint Venture eligible under the WOSB Program",$AS2)),0,1)` | Listed as a Women-Owned Small Business (WOSB) Joint Venture eligible under the WOSB Program |

