---
title: API Reference

language_tabs:
  - JSON

toc_footers:
  - <a href='/provider_access/login'>Login Page</a>

includes:
  - errors

search: true
---

# Introduction

This page documents Pharmetika's Interface API.  This API is to be used to get information from a pharmacy management system into Pharmetka.  Validation is enabled on each endpoint.  If data does not pass validation the entry will be rejected and provide an explanation as to why.
Most Pharmetika APIs utilize a JSON body.  The example JSON body is shown as arguments to "json".  If the API is query-args-based, the arguments will be described under the "query" section.


# Authentication

> API calls can be made via basic HTTP Authentication.


A username and password will be provided upon request.  We recommend providing an email address along with the username so that the password can be easily reset.

`https://API_USERNAME:PASSWORD@[realm].pharmetika.com/api/endpoint`

<aside class="notice">
TLS v1.2 or v1.3 is required. If your pharmacy needs interface endpoints restricted to a particular whitelist of IPs please create a support ticket.
</aside>


# Data Validation

Upon submitting data Pharmetika's API will check each field to ensure it is properly formatted.  The API attempts to guide implementors by providing detailed feedback for each field it could not validate.  These errors will appear in the messages array of the response object.
> Example of failed response

```json
{
	"success": false,
	"messages": [
		{ 
			"message": "field_X is not in the proper format",
			"type": "error",
		},
		{ 
			"message": "field_Y is required",
			"type": "error",
		}

	]
}
```
### Common Data Types
Data Type | Description | Pattern
---------|------------|---------
Phone Number  | 10-digits, no dashes, etc.  Sometimes pharmacies will put 9999999999 to indicate the contact should not be called/faxed/etc. | <code>^(?:(\d)\1{9}&#124;1?(&#91;2-9&#93;((?!11)&#91;0-8&#93;\d)&#91;2-9&#93;((?!11)\d{2})\d{4})&#124;(\d)\2{9})$</code>
SSN  | 9-digits, no dashes | `\d{9}`
NPI  | 10-digits | `\d{10}`
NDC  | 11-digits (HIPAA NDC) | `\d{11}`
refills_authorized | Numeric or "PRN" | <code>^(PRN&#124;\d+)$</code>
timestamp | All dates and times are in UTC.  Please be sure to convert to UTC if the system is not natively set to UTC time. | `^[12][90]\d\d-?[10]\d-?[0123]\d\s?[012]\d:?[0-5]\d:?[0-5]\d(\.\d)?$`
date | date in "YYYYMMDD" or "YYYY-MM-DD" | `[12][90]\d\d-?[10]\d-?[0123]\d`

### Unlisted Fields

Implementors may include additional fields.  Sometimes this can be helpful if you are supporting similar APIs that require other data or you want to provide additional fields for debugging purposes.
Fields you think may provide the pharmacy with additional context are welcomed and this auxiliary data is saved as a JSON blob in Pharmetika.
For example, your system may record the lot numbers of dispensed medication.  Including a "LotNumber" field would allow the pharmacy to run a custom report from Pharmetika and query on that piece of data.

# Interface API Endpoints

## api login

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
POST /api/v1/login

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## post zrt lab results

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
GET /api/lab/:version/zrt/post_results

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## post zrt lab results

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
POST /api/lab/:version/zrt/post_results

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## interface test

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
POST /api/interface/:version/test

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## interface patient add

> Arguments

```json
{
   "json" : {
      "add_address" : 1,
      "patient" : {
         "DOB" : "1947-08-15 00:00:00.0000",
         "MRN" : 30851,
         "address_line_1" : null,
         "address_line_2" : "2730 DAVIS RD",
         "address_line_3" : null,
         "city" : "INDIANPOLIS",
         "country" : "",
         "date_updated" : "2017-12-04 13:39:18",
         "deceased" : 0,
         "drivers_license" : "8931-71-4964",
         "drivers_license_issuing_state" : "IN",
         "email" : "JUDYSALTER@COMCAST.NET",
         "first_name" : "JUDITH",
         "insurance_group" : "COS",
         "insurance_id" : 119,
         "insurance_policy_id" : "941462894-00",
         "insurance_relationship" : "1",
         "last_name" : "SALTER",
         "link_id" : 33656,
         "patient_id" : 34508,
         "patient_note" : "RESTORE - AUTOSHIP: USPS - FREE\n\nPAYMENT IN PMK\n\n12/4/17 FXD MDO FOR E1/E3/E3/PREG/PROG/TEST  REFILL. ADD TO A/S ONCE NEW RX IS REC'D KK//fax failed, manually fxd dv\n\n10-11-17 1st call lvmm that she has refills for a/s in Oct & Nov but need to make appt with her provider for more, put RX in Dee's pink folder- SRS\n\n10-11-17 SCANNED AND ENTERED E1 0.2/E2 0.2/E3 1.6/PREG 50MG/PROG 150MG/TEST 1.5MG CR INTO PT PROFILE.LP\n\n10/10/17FXD MDO FOR E1/E2/E3/PROG/PREG/TEST REFILL. ADD TO A/S ONCE NEW RX IS REC'D KK\n\n9/26/17 email rec'd:Change time please I thought I had enough, but was wrong. Do you send it as soon as possible please. Thanks, fill A/S today, sent message to pt/order was placed on 9/25. dv\n\n9-25-17 per pt email; Could you please send prescription as soon as possible.  I thought I had enough & I was wrong.  Thanks-\n changed A/S to 9-25-17 & send 3414740 E1 0.2/E2 0.2/E3 1.6/PREG 50MG/ P4 150MG/TEST 1.5MG/GM CREAM- fill & ship- SRS\n\n9/14/17 email rec'd Please send it 10/19.  Thanks, changed date to 10/19 & responded to pt dv\n\n7/21/17 PER PT'S EMAIL HOLD A/S UNTIL SEPT-- MOVE A/S OUT TO SEPT 19- EMAIL PT BACK WITH UPDATE A/S DATE-JS\n\n5/30/17: PER EMAIL FROM PT: Please don't send till July.  Thanks. UPDATED A/S DATE TO 7/3/17. JG\n\n4/7/17: PER EMAIL FROM PT: Please do not send order until May10, 2017.  Thanks UPDATED A/S DATE TO 5/10/17 IN PMK. JG\n\n4-6-17 PT CALLED TO UPDATE HER CC INFO.LP\n\n4-4-17 SCANNED E1 0.2/ E2 0.2/E3 1.6/ PREG 50MG/ PROG 150MG/ TEST 1.5MG CR  INTO PT PROFILE.LP\nMADE TICKET TO ENTER AND ADD TO A/S  ALSO SENT PT LINK TO UPDATE CC.LP\n\n4/4/17 SCANNED VOIDED E1/E2/E3/PREG/PROG/TEST/CRM. KR \n\n4/4/17 SCANNED NOT VALID E1 0.2/E2 0.2/E3 1.6/PREG 50MG/PROG 150MG/TEST 1.5MG CRM. CALLED MD TO REFAX. MD WILL BE FAXING OVER. KR \n\n4/4/17: FXD MDO FOR BI-EST/PREG/PROG/TEST REFILL. ADD TO A/S ONCE NEW RX IS REC'D. LVMM FOR PT TCB TO UPDATE PAYMENT INFO. ALSO SENT LINK VIA EMAIL. JG\n\n1/16/17: PER EMAIL FROM PT: Please do not send until 2/17/17.  Thank you. UPDATED A/S DATE TO 2/17/17. JG\n\n10/21/16 PER PT'S EMAIL HOLD A/S UNTIL 11/28/16- JS\n\n9/28/16 REC'D E10.2+ E2 0.2 + E3 1.6 + PREG 50 +PROG 150 + TEST 1.5 MG CREAM- \n- PER9/27 NOTE FILL AND SHIP AND ADD TO A/S - JS\n\n09/27/16 - A/S due.....faxed MD for RX....fill and send once approved...JT\n\n8/5/16 per pt fill e1+e2+e3+preg+prog+test cream-- start a/s- js\n\n6/10/16 per pt's voicemail send e1+e2+e3+ preg+ prog+ t. JS\n\n5/5/16: RVMM TO REFILL E1/E2/PREG/P4/TEST. RET'D CALL AND CONFIRMED REFILL REQ REC'D. ADDED EMAIL. JG\n\n5/5/16: 2ND CALL LVMM FOR PT TCB IF REFILL NEEDED. JG\n\n5/4/16-LM WITH AMY ON HER LINE TO VERIFY RX OF PATIENT-EZS \n\n5-3016 per dr marsh's office (amy) 40 grams is a 30 day supply as pt uses spoon jar and there is more waste and measuring variability. mmw\n\n5-3-16 LEFT PT VM TO CALL BACK IF SHE NEEDS A REFILL.LP\n\n5/2/16 scanned RX for Estrone/Estra/Estri/Preg/Prog/Test DV\n\n3/10/16 PT CALLED IN - ADDED ALL INFO\n- RUN INS AND CALL PT WITH OUTCOME\n- HONOR ONE TIME RESTORE PRICING IF INS DOES NOT COVER\n- FILL & SHIP ASAP AS PT IS OUT\n\n3/9/16: PT IS NOT NEW, SHE IS A RESTORE PT. RVMM FROM PT TCB FOR NEW RX. LVMM FOR PT TC US BACK. JG\n\n3/9/16 LM for pt to callback with info DV\n\n3/4/16 new RX DV",
         "pharmacy_system_patient_id" : 30851,
         "pharmacy_system_prescriber_id" : 1,
         "phone_primary" : "3178620544",
         "phone_secondary" : null,
         "phone_tertiary" : null,
         "postal_code" : "46239",
         "sex" : "F",
         "skip_patient_tests" : 1,
         "species" : "HUMAN",
         "ssn" : null,
         "state" : "IN"
      },
      "skip_patient_tests" : 1
   },
   "method" : "POST",
   "query" : {}
}

```	
> Result

```json
{
   "patient" : {
      "success" : true
   },
   "success" : true,
   "validation" : {
      "messages" : null,
      "valid" : 1
   }
}

```	


### HTTP Request
POST /api/interface/:version/patient

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## interface patient update

> Arguments

```json
{
   "json" : {
      "add_address" : 1,
      "patient" : {
         "DOB" : "1947-08-15 00:00:00.0000",
         "MRN" : 30851,
         "address_line_1" : null,
         "address_line_2" : "2730 DAVIS RD",
         "address_line_3" : null,
         "city" : "INDIANPOLIS",
         "country" : "",
         "date_updated" : "2017-12-04 13:39:18",
         "deceased" : 0,
         "drivers_license" : "8931-71-4964",
         "drivers_license_issuing_state" : "IN",
         "email" : "JUDYSALTER@COMCAST.NET",
         "first_name" : "JUDITH",
         "insurance_group" : "COS",
         "insurance_id" : 119,
         "insurance_policy_id" : "941462894-00",
         "insurance_relationship" : "1",
         "last_name" : "SALTER",
         "link_id" : 33656,
         "patient_id" : 34508,
         "patient_note" : "RESTORE - AUTOSHIP: USPS - FREE\n\nPAYMENT IN PMK\n\n12/4/17 FXD MDO FOR E1/E3/E3/PREG/PROG/TEST  REFILL. ADD TO A/S ONCE NEW RX IS REC'D KK//fax failed, manually fxd dv\n\n10-11-17 1st call lvmm that she has refills for a/s in Oct & Nov but need to make appt with her provider for more, put RX in Dee's pink folder- SRS\n\n10-11-17 SCANNED AND ENTERED E1 0.2/E2 0.2/E3 1.6/PREG 50MG/PROG 150MG/TEST 1.5MG CR INTO PT PROFILE.LP\n\n10/10/17FXD MDO FOR E1/E2/E3/PROG/PREG/TEST REFILL. ADD TO A/S ONCE NEW RX IS REC'D KK\n\n9/26/17 email rec'd:Change time please I thought I had enough, but was wrong. Do you send it as soon as possible please. Thanks, fill A/S today, sent message to pt/order was placed on 9/25. dv\n\n9-25-17 per pt email; Could you please send prescription as soon as possible.  I thought I had enough & I was wrong.  Thanks-\n changed A/S to 9-25-17 & send 3414740 E1 0.2/E2 0.2/E3 1.6/PREG 50MG/ P4 150MG/TEST 1.5MG/GM CREAM- fill & ship- SRS\n\n9/14/17 email rec'd Please send it 10/19.  Thanks, changed date to 10/19 & responded to pt dv\n\n7/21/17 PER PT'S EMAIL HOLD A/S UNTIL SEPT-- MOVE A/S OUT TO SEPT 19- EMAIL PT BACK WITH UPDATE A/S DATE-JS\n\n5/30/17: PER EMAIL FROM PT: Please don't send till July.  Thanks. UPDATED A/S DATE TO 7/3/17. JG\n\n4/7/17: PER EMAIL FROM PT: Please do not send order until May10, 2017.  Thanks UPDATED A/S DATE TO 5/10/17 IN PMK. JG\n\n4-6-17 PT CALLED TO UPDATE HER CC INFO.LP\n\n4-4-17 SCANNED E1 0.2/ E2 0.2/E3 1.6/ PREG 50MG/ PROG 150MG/ TEST 1.5MG CR  INTO PT PROFILE.LP\nMADE TICKET TO ENTER AND ADD TO A/S  ALSO SENT PT LINK TO UPDATE CC.LP\n\n4/4/17 SCANNED VOIDED E1/E2/E3/PREG/PROG/TEST/CRM. KR \n\n4/4/17 SCANNED NOT VALID E1 0.2/E2 0.2/E3 1.6/PREG 50MG/PROG 150MG/TEST 1.5MG CRM. CALLED MD TO REFAX. MD WILL BE FAXING OVER. KR \n\n4/4/17: FXD MDO FOR BI-EST/PREG/PROG/TEST REFILL. ADD TO A/S ONCE NEW RX IS REC'D. LVMM FOR PT TCB TO UPDATE PAYMENT INFO. ALSO SENT LINK VIA EMAIL. JG\n\n1/16/17: PER EMAIL FROM PT: Please do not send until 2/17/17.  Thank you. UPDATED A/S DATE TO 2/17/17. JG\n\n10/21/16 PER PT'S EMAIL HOLD A/S UNTIL 11/28/16- JS\n\n9/28/16 REC'D E10.2+ E2 0.2 + E3 1.6 + PREG 50 +PROG 150 + TEST 1.5 MG CREAM- \n- PER9/27 NOTE FILL AND SHIP AND ADD TO A/S - JS\n\n09/27/16 - A/S due.....faxed MD for RX....fill and send once approved...JT\n\n8/5/16 per pt fill e1+e2+e3+preg+prog+test cream-- start a/s- js\n\n6/10/16 per pt's voicemail send e1+e2+e3+ preg+ prog+ t. JS\n\n5/5/16: RVMM TO REFILL E1/E2/PREG/P4/TEST. RET'D CALL AND CONFIRMED REFILL REQ REC'D. ADDED EMAIL. JG\n\n5/5/16: 2ND CALL LVMM FOR PT TCB IF REFILL NEEDED. JG\n\n5/4/16-LM WITH AMY ON HER LINE TO VERIFY RX OF PATIENT-EZS \n\n5-3016 per dr marsh's office (amy) 40 grams is a 30 day supply as pt uses spoon jar and there is more waste and measuring variability. mmw\n\n5-3-16 LEFT PT VM TO CALL BACK IF SHE NEEDS A REFILL.LP\n\n5/2/16 scanned RX for Estrone/Estra/Estri/Preg/Prog/Test DV\n\n3/10/16 PT CALLED IN - ADDED ALL INFO\n- RUN INS AND CALL PT WITH OUTCOME\n- HONOR ONE TIME RESTORE PRICING IF INS DOES NOT COVER\n- FILL & SHIP ASAP AS PT IS OUT\n\n3/9/16: PT IS NOT NEW, SHE IS A RESTORE PT. RVMM FROM PT TCB FOR NEW RX. LVMM FOR PT TC US BACK. JG\n\n3/9/16 LM for pt to callback with info DV\n\n3/4/16 new RX DV",
         "pharmacy_system_patient_id" : 30851,
         "pharmacy_system_prescriber_id" : 1,
         "phone_primary" : "3178620544",
         "phone_secondary" : null,
         "phone_tertiary" : null,
         "postal_code" : "46239",
         "sex" : "F",
         "skip_patient_tests" : 1,
         "species" : "HUMAN",
         "ssn" : null,
         "state" : "IN"
      },
      "skip_patient_tests" : 1
   },
   "method" : "POST",
   "query" : {}
}

```	
> Result

```json
{
   "patient" : {
      "success" : true
   },
   "success" : true,
   "validation" : {
      "messages" : null,
      "valid" : 1
   }
}

```	


### HTTP Request
POST /api/interface/:version/patient

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## interface prescriber add

> Arguments

```json
{
   "json" : {
      "prescriber" : {
         "DEA_number" : "BS1515595",
         "NPI" : "1659374502",
         "address_line_1" : "5700 MONROE ST",
         "address_line_2" : null,
         "city" : "SYLVANIA",
         "credential" : "MD",
         "email" : null,
         "fax" : null,
         "id" : null,
         "label_name" : "SFERRA, MD",
         "last_name" : "SFERRA, JOSEPH",
         "pharmacy_system_prescriber_id" : 7008,
         "phone_primary" : "4198852525",
         "phone_secondary" : null,
         "postal_code" : "43560",
         "prescriber_group" : null,
         "state" : "OH"
      },
      "update_on_duplicate" : 1
   },
   "method" : "POST",
   "query" : {}
}

```	
> Result

```json
{
   "prescriber" : {
      "prescriber_id" : 99951370,
      "success" : true
   },
   "success" : true,
   "validation" : {
      "messages" : null,
      "valid" : 1
   }
}

```	


### HTTP Request
POST /api/interface/:version/prescriber

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## interface prescription add

> Arguments

```json
{
   "json" : {
      "prescription" : {
         "ADDRESS" : "8557236092 MAIL ORDER    ",
         "AMOUNT" : "1083.75",
         "AWP" : "1353.84",
         "BAL" : "1358.34",
         "BILLEDAMT" : "0.00",
         "CITY" : "8775656474 PA  ",
         "COPAYPAID" : "Y",
         "Cost" : "1085.90",
         "DATEF" : "Dec  1 2017 12:00:00:000AM",
         "DISCONTBY" : " ",
         "DISCOUNT" : "0.00",
         "FILLNO" : 1,
         "IncludeInMAR" : "N",
         "Is340B" : 0,
         "LMOD_TIME" : null,
         "LabelQty" : 0,
         "MAG_CODE" : "PEU       ",
         "MaxDailyDose" : "0.00",
         "ORDSTATUS" : " ",
         "OTHAMT" : "0.00",
         "OTHFEE" : "0.00",
         "PAYSTATUS" : " ",
         "PFEE" : "0.00",
         "PHONE_V" : "(800)922-1557       ",
         "PICKUPDATE" : null,
         "PICKUPTIME" : "",
         "PatTypeBinno" : "610014",
         "PatTypeInsName" : "UT                       ",
         "PrescribClinic" : 30,
         "REFREMIND" : " ",
         "RxReceivedBy" : "EMJ",
         "STATE" : "  ",
         "STAX" : "0.00",
         "SUBNO" : "E9FA3WA",
         "TagId" : 0,
         "TherapeuticClassID" : 1216,
         "TotBilledAmt" : "1358.34",
         "UnC" : "1358.34",
         "UsePAForAllRefs" : 0,
         "ZIP" : "     ",
         "_unit_price" : "1353.84",
         "billed_third_party" : " ",
         "claim_status" : "paid",
         "compound_indicator" : 0,
         "controlled" : 0,
         "copay" : "0.00",
         "date_created" : "2017-12-01 15:41:00",
         "date_discontinued" : null,
         "date_dispensed" : null,
         "date_entered" : "2017-12-01 00:00:00",
         "date_expiration" : "2018-12-01",
         "date_filled" : "2017-12-01 15:41:00",
         "date_patient_received" : null,
         "date_transaction" : "2017-12-01 15:41:00",
         "date_updated" : "2017-12-01 16:08:00",
         "date_written" : "2017-12-01",
         "days_supply" : "180",
         "diagnosis" : null,
         "discontinue_reason" : "",
         "discontinued_indicator" : 0,
         "dispensed_generic_indicator" : 1,
         "dispensed_indicator" : "1",
         "dispensed_ndc" : "55513071001",
         "dosage" : "60MG           ",
         "drug_class" : "0 ",
         "drug_description" : "PROLIA                             ",
         "drug_id" : "55513071001",
         "fill_number" : 0,
         "form" : "INJ            ",
         "generic_indicator" : 0,
         "medication_indication" : null,
         "ndc" : "55513071001",
         "pharmacy_system_patient_id" : 30387,
         "pharmacy_system_prescriber_id" : 4046,
         "pharmacy_system_transaction_id" : "3316950",
         "prescription_indicator" : 1,
         "prescription_status" : "B",
         "price" : "1083.75",
         "primary_third_party_adjudicated_amount" : "1083.75",
         "prn_indicator" : 0,
         "quantity_dispensed" : "1.000",
         "quantity_written" : "1.000",
         "refills_authorized" : 0,
         "refills_remaining" : 0,
         "rx_number" : "331695",
         "sig" : "INJECT 60MG SUBCUTANEOUSLY EVERY 6 MONTHS",
         "sig_code" : "PROLIA",
         "third_party_id_primary" : "PD5       ",
         "third_party_indicator" : 1,
         "transaction_id" : "3316950",
         "transaction_status" : "filled",
         "transaction_status_description" : "Billed",
         "unit" : "ML ",
         "void_indicator" : "0"
      }
   },
   "method" : "POST",
   "query" : {
      "{\n      \"prescription\" : {\n         \"ADDRESS\" : \"8557236092 MAIL ORDER    \",\n         \"AMOUNT\" : \"1083.75\",\n         \"AWP\" : \"1353.84\",\n         \"BAL\" : \"1358.34\",\n         \"BILLEDAMT\" : \"0.00\",\n         \"CITY\" : \"8775656474 PA  \",\n         \"COPAYPAID\" : \"Y\",\n         \"Cost\" : \"1085.90\",\n         \"DATEF\" : \"Dec  1 2017 12:00:00:000AM\",\n         \"DISCONTBY\" : \" \",\n         \"DISCOUNT\" : \"0.00\",\n         \"FILLNO\" : 1,\n         \"IncludeInMAR\" : \"N\",\n         \"Is340B\" : 0,\n         \"LMOD_TIME\" : null,\n         \"LabelQty\" : 0,\n         \"MAG_CODE\" : \"PEU       \",\n         \"MaxDailyDose\" : \"0.00\",\n         \"ORDSTATUS\" : \" \",\n         \"OTHAMT\" : \"0.00\",\n         \"OTHFEE\" : \"0.00\",\n         \"PAYSTATUS\" : \" \",\n         \"PFEE\" : \"0.00\",\n         \"PHONE_V\" : \"(800)922-1557       \",\n         \"PICKUPDATE\" : null,\n         \"PICKUPTIME\" : \"\",\n         \"PatTypeBinno\" : \"610014\",\n         \"PatTypeInsName\" : \"UT                       \",\n         \"PrescribClinic\" : 30,\n         \"REFREMIND\" : \" \",\n         \"RxReceivedBy\" : \"EMJ\",\n         \"STATE\" : \"  \",\n         \"STAX\" : \"0.00\",\n         \"SUBNO\" : \"E9FA3WA\",\n         \"TagId\" : 0,\n         \"TherapeuticClassID\" : 1216,\n         \"TotBilledAmt\" : \"1358.34\",\n         \"UnC\" : \"1358.34\",\n         \"UsePAForAllRefs\" : 0,\n         \"ZIP\" : \"     \",\n         \"_unit_price\" : \"1353.84\",\n         \"billed_third_party\" : \" \",\n         \"claim_status\" : \"paid\",\n         \"compound_indicator\" : 0,\n         \"controlled\" : 0,\n         \"copay\" : \"0.00\",\n         \"date_created\" : \"2017-12-01 15:41:00\",\n         \"date_discontinued\" : null,\n         \"date_dispensed\" : null,\n         \"date_entered\" : \"2017-12-01 00:00:00\",\n         \"date_expiration\" : \"2018-12-01\",\n         \"date_filled\" : \"2017-12-01 15:41:00\",\n         \"date_patient_received\" : null,\n         \"date_transaction\" : \"2017-12-01 15:41:00\",\n         \"date_updated\" : \"2017-12-01 16:08:00\",\n         \"date_written\" : \"2017-12-01\",\n         \"days_supply\" : \"180\",\n         \"diagnosis\" : null,\n         \"discontinue_reason\" : \"\",\n         \"discontinued_indicator\" : 0,\n         \"dispensed_generic_indicator\" : 1,\n         \"dispensed_indicator\" : \"1\",\n         \"dispensed_ndc\" : \"55513071001\",\n         \"dosage\" : \"60MG           \",\n         \"drug_class\" : \"0 \",\n         \"drug_description\" : \"PROLIA                             \",\n         \"drug_id\" : \"55513071001\",\n         \"fill_number\" : 0,\n         \"form\" : \"INJ            \",\n         \"generic_indicator\" : 0,\n         \"medication_indication\" : null,\n         \"ndc\" : \"55513071001\",\n         \"pharmacy_system_patient_id\" : 30387,\n         \"pharmacy_system_prescriber_id\" : 4046,\n         \"pharmacy_system_transaction_id\" : \"3316950\",\n         \"prescription_indicator\" : 1,\n         \"prescription_status\" : \"B\",\n         \"price\" : \"1083.75\",\n         \"primary_third_party_adjudicated_amount\" : \"1083.75\",\n         \"prn_indicator\" : 0,\n         \"quantity_dispensed\" : \"1.000\",\n         \"quantity_written\" : \"1.000\",\n         \"refills_authorized\" : 0,\n         \"refills_remaining\" : 0,\n         \"rx_number\" : \"331695\",\n         \"sig\" : \"INJECT 60MG SUBCUTANEOUSLY EVERY 6 MONTHS\",\n         \"sig_code\" : \"PROLIA\",\n         \"third_party_id_primary\" : \"PD5       \",\n         \"third_party_indicator\" : 1,\n         \"transaction_id\" : \"3316950\",\n         \"transaction_status\" : \"filled\",\n         \"transaction_status_description\" : \"Billed\",\n         \"unit\" : \"ML \",\n         \"void_indicator\" : \"0\"\n      }\n   } " : ""
   }
}

```	
> Result

```json
{
   "success" : false,
   "validation" : {
      "messages" : [
         {
            "message" : "dispense_as_written_indicator is required",
            "type" : "error"
         },
         {
            "message" : "prescription_status is not in the proper format.  Value sent: \"B\"",
            "type" : "error"
         }
      ],
      "valid" : 0
   }
}

```	


### HTTP Request
POST /api/interface/:version/prescription

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## interface transaction add

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
POST /api/interface/:version/prescription_transaction

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## interface prescription diagnosis add

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
POST /api/interface/:version/prescription_diagnosis/:rx_number

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## interface prior authorization add

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
POST /api/interface/:version/prior_authorization

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## account change password

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
POST /api/account/:version/change_password

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## account change email

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
POST /api/account/:version/change_email

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## create lab order

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
POST /api/provider/:version/lab_order

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## create otc order

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
POST /api/provider/:version/otc_order

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## provider rx activity details

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
GET /api/provider/:version/rx_activity_details

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## provider rx activity details

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
POST /api/provider/:version/rx_activity_details

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## provider get data image

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
GET /api/provider/:version/data_image

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## provider get data image

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
POST /api/provider/:version/data_image

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## provider get cf image

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
GET /api/provider/:version/cf_image

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## provider get cf image

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
POST /api/provider/:version/cf_image

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## provider mark patient recommendations viewed

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
GET /api/provider/:version/patient/:patientid/recommendations/mark_viewed

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## add provider rx template category

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
POST /api/provider/:version/rx_template/category

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## delete provider rx template category

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
DELETE /api/provider/:version/rx_template/category

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## sort provider rx template category

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
POST /api/provider/:version/rx_template/category/sort

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## add provider rx template med

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
POST /api/provider/:version/rx_template/med

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## delete provider rx template med

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
DELETE /api/provider/:version/rx_template/med

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## add provider rx template dose

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
POST /api/provider/:version/rx_template/dose

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## delete provider rx template dose

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
DELETE /api/provider/:version/rx_template/dose

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## external pusher

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
POST /api/external/:version/pusher

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## external tracking

> Arguments

```json
{
   "json" : {},
   "method" : "GET",
   "query" : {
      "id" : "740477200250"
   }
}

```	
> Result

```json
{
   "contents" : [
      {
         "address" : "695 A1A NORTH ",
         "carrier" : null,
         "city" : "PONTE VEDRA BEACH",
         "copay" : "51.00",
         "cost" : null,
         "date_filled" : "2017-11-07",
         "date_shipped" : "2017-11-10 00:00:00",
         "drug_description" : "BI-EST CREAM 3MG/GM",
         "id" : 64914,
         "name" : null,
         "patient_id" : 7660,
         "price" : "51.00",
         "quantity_dispensed" : 30,
         "rxn" : 3423143,
         "scan_id" : 3423145,
         "scan_original" : null,
         "service_type" : "90",
         "shipping_system_id" : "740477200250",
         "state" : null,
         "status" : null,
         "tracking_id" : "740477200250"
      },
      {
         "address" : "695 A1A NORTH ",
         "carrier" : null,
         "city" : "PONTE VEDRA BEACH",
         "copay" : "54.85",
         "cost" : null,
         "date_filled" : "2017-11-07",
         "date_shipped" : "2017-11-10 00:00:00",
         "drug_description" : "PREGNENOLONE E4M (DYE FREE)  CAPSULE 200 MG",
         "id" : 64914,
         "name" : null,
         "patient_id" : 7660,
         "price" : "54.85",
         "quantity_dispensed" : 30,
         "rxn" : 3423144,
         "scan_id" : 3423145,
         "scan_original" : null,
         "service_type" : "90",
         "shipping_system_id" : "740477200250",
         "state" : null,
         "status" : null,
         "tracking_id" : "740477200250"
      },
      {
         "address" : "695 A1A NORTH ",
         "carrier" : null,
         "city" : "PONTE VEDRA BEACH",
         "copay" : "55.11",
         "cost" : null,
         "date_filled" : "2017-11-07",
         "date_shipped" : "2017-11-10 00:00:00",
         "drug_description" : "PROGESTERONE E4M (DYE FREE) CAPSULE 200MG",
         "id" : 64914,
         "name" : null,
         "patient_id" : 7660,
         "price" : "55.11",
         "quantity_dispensed" : 30,
         "rxn" : 3423145,
         "scan_id" : 3423145,
         "scan_original" : null,
         "service_type" : "90",
         "shipping_system_id" : "740477200250",
         "state" : null,
         "status" : null,
         "tracking_id" : "740477200250"
      },
      {
         "address" : "695 A1A NORTH ",
         "carrier" : null,
         "city" : "PONTE VEDRA BEACH",
         "copay" : "48.69",
         "cost" : null,
         "date_filled" : "2017-11-07",
         "date_shipped" : "2017-11-10 00:00:00",
         "drug_description" : "TESTOSTERONE CREAM 1.25MG/GM",
         "id" : 64914,
         "name" : null,
         "patient_id" : 7660,
         "price" : "48.69",
         "quantity_dispensed" : 30,
         "rxn" : 3423146,
         "scan_id" : 3423145,
         "scan_original" : null,
         "service_type" : "90",
         "shipping_system_id" : "740477200250",
         "state" : null,
         "status" : null,
         "tracking_id" : "740477200250"
      }
   ],
   "destination" : {
      "address1" : "",
      "address2" : "",
      "city" : "PONTE VEDRA BEACH",
      "country" : "US",
      "postal_code" : "",
      "state" : "FL"
   },
   "human_url" : "https://www.fedex.com/apps/fedextrack/?action=track&locale=en_US&cntry_code=us&language=english&tracknumbers=740477200250",
   "service" : "FedEx Home Delivery",
   "status" : {
      "date" : "11/16/17",
      "delivered" : 1,
      "description" : "Delivered: 11/16/2017 3:10 pm Signed for by:Signature not required; Ponte Vedra Beach, FL; Left at front door.Signature Service not requested. 2017-11-16 15:10:47"
   },
   "weight" : ""
}

```	


### HTTP Request
GET /api/external/:version/tracking

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## external tracking

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
POST /api/external/:version/tracking

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## v1 api

> Arguments

```json
{
   "json" : {
      "note_text" : "TIMELESS HEALTH CLINIC ACCT",
      "npi" : 1134495997,
      "realm" : "PSOL"
   },
   "method" : "POST",
   "query" : {}
}

```	
> Result

```json
{
   "args" : {},
   "data" : {
      "success" : true
   },
   "errs" : [],
   "function" : "add_prescriber_note",
   "itime" : 1515138748.24688,
   "mtime" : 1515138748.24688,
   "stime" : 1515138748.47943,
   "success" : true
}

```	


### HTTP Request
POST /api/v1/:endpoint

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## provider access outstanding reauthorization requests all

> Arguments

```json
{
   "json" : {},
   "method" : "GET",
   "query" : {}
}

```	
> Result

```json
{
   "error" : "Not authorized"
}

```	


### HTTP Request
GET /api/pharmetika/provider_access/outstanding_reauthorization_requests

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## provider access patient list

> Arguments

```json
{
   "json" : {},
   "method" : "GET",
   "query" : {}
}

```	
> Result

```json
{
   "error" : "Not authorized"
}

```	


### HTTP Request
GET /api/pharmetika/provider_access/patient/list

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## provider access patient object

> Arguments

```json
{
   "json" : {},
   "method" : "GET",
   "query" : {}
}

```	
> Result

```json
{
   "error" : "Not authorized."
}

```	


### HTTP Request
GET /api/pharmetika/provider_access/patient/:patient_id/patient_object

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## provider access prescription history

> Arguments

```json
{
   "json" : {},
   "method" : "GET",
   "query" : {}
}

```	
> Result

```json
{
   "error" : "Not authorized."
}

```	


### HTTP Request
GET /api/pharmetika/provider_access/patient/:patient_id/prescription_history

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## provider access get medication adherence

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
GET /api/pharmetika/provider_access/patient/:patient_id/medication/:rxcui/adherence

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## provider access get medication adherence list

> Arguments

```json
{
   "json" : {
      "include_adherence_history" : "1"
   },
   "method" : "GET",
   "query" : {
      "include_adherence_history" : "1"
   }
}

```	
> Result

```json
{
   "error" : "Not authorized."
}

```	


### HTTP Request
GET /api/pharmetika/provider_access/patient/:patient_id/medications/list/adherence

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## provider access prescription history

> Arguments

```json
{
   "json" : {},
   "method" : "GET",
   "query" : {}
}

```	
> Result

```json
{
   "error" : "Not authorized."
}

```	


### HTTP Request
GET /api/pharmetika/provider_access/patient/:patient_id/prescription_history

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## provider access outstanding reauthorization requests

> Arguments

```json
{
   "json" : {},
   "method" : "GET",
   "query" : {}
}

```	
> Result

```json
{
   "error" : "Not authorized."
}

```	


### HTTP Request
GET /api/pharmetika/provider_access/patient/:patient_id/outstanding_reauthorization_requests

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## provider access prescription details

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
GET /api/pharmetika/provider_access/prescription/:rxn

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## provider access view refill

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
GET /api/pharmetika/provider_access/prescription/:rxn/refill/view

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## provider access view refill

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
POST /api/pharmetika/provider_access/prescription/:rxn/refill/view

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## provider access get medication adherence by rx number

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
GET /api/pharmetika/provider_access/prescription/:rx_number/adherence

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## reports family rxs

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
GET /api/reports/:version/family_rxs

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## reports family rxs

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
POST /api/reports/:version/family_rxs

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## reports new patients

> Arguments

```json
{
   "json" : {},
   "method" : "GET",
   "query" : {
      "end_date" : "2017-12-01",
      "start_date" : "2017-11-13"
   }
}

```	
> Result

```json

```	


### HTTP Request
GET /api/reports/:version/new_patients

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## reports new patients

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
POST /api/reports/:version/new_patients

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## reports new providers

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
GET /api/reports/:version/new_providers

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## reports new providers

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
POST /api/reports/:version/new_providers

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## reports autoship patients

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
GET /api/reports/:version/autoship_patients

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## reports autoship patients

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
POST /api/reports/:version/autoship_patients

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## reports rd faxes volume by day

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
GET /api/reports/:version/faxes_volume_by_day

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## reports rd faxes volume by day

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
POST /api/reports/:version/faxes_volume_by_day

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## reports patients that have dropped legacy

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
GET /api/reports/:version/patients_that_have_dropped

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## reports patients that have dropped legacy

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
POST /api/reports/:version/patients_that_have_dropped

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## reports autoship refill authorization required

> Arguments

```json
{
   "json" : {},
   "method" : "GET",
   "query" : {
      "end_date" : "2017-12-28",
      "start_date" : "2017-12-21"
   }
}

```	
> Result

```json

```	


### HTTP Request
GET /api/reports/:version/autoship_refill_authorization_required

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## reports autoship refill authorization required

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
POST /api/reports/:version/autoship_refill_authorization_required

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## lab queue report generation

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
POST /api/lab/:version/queue_report_generation

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## lab generate barcodes

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
GET /api/lab/:version/generate_barcodes

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## lab generate barcodes

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
POST /api/lab/:version/generate_barcodes

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## lab receipt

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
GET /api/lab/:version/receipt

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## lab receipt

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
POST /api/lab/:version/receipt

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## lab show records

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
GET /api/lab/:version/show_records

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## lab show records

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
POST /api/lab/:version/show_records

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## labcorp get reports

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
POST /api/lab/:version/labcorp/get_lab_reports

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## labcorp show report

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
POST /api/lab/:version/labcorp/show_lab_report

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## labcorp store results

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
POST /api/lab/:version/labcorp/store_lab_results

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## labcorp get lab order

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
POST /api/lab/:version/labcorp/get_lab_order

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## send refill

> Arguments

```json
{
   "json" : {},
   "method" : "GET",
   "query" : {}
}

```	
> Result

```json
{
   "messages" : [
      {
         "message" : "Successfully faxed to: 5745393581 for 3392669",
         "type" : "success"
      }
   ],
   "render_args" : {
      "RxN" : "3392669",
      "annotation" : null,
      "internal" : null,
      "secondFax" : null
   },
   "rxn" : "3392669"
}

```	


### HTTP Request
GET /api/pharmetika/:version/prescription/:rxn/refill/send

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## send refill

> Arguments

```json
{
   "json" : {},
   "method" : "POST",
   "query" : {
      "annotation" : "",
      "fax" : "true",
      "rxn" : "3391834"
   }
}

```	
> Result

```json
{
   "messages" : [
      {
         "message" : "Successfully faxed to: 9146588977 for 3391834",
         "type" : "success"
      }
   ],
   "render_args" : {
      "RxN" : "3391834",
      "annotation" : "",
      "internal" : null,
      "secondFax" : null
   },
   "rxn" : "3391834"
}

```	


### HTTP Request
POST /api/pharmetika/:version/prescription/:rxn/refill/send

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## sales get sales data

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
GET /api/sales/:version/get_sales_data

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## sales get sales data

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
POST /api/sales/:version/get_sales_data

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## search typeahead pharmetika

> Arguments

```json
{
   "json" : {},
   "method" : "GET",
   "query" : {
      "q" : "hutt"
   }
}

```	
> Result

```json

```	


### HTTP Request
GET /api/pharmetika/:version/search/typeahead

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## search typeahead pharmetika

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
POST /api/pharmetika/:version/search/typeahead

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## get recent patients of interest

> Arguments

```json
{
   "json" : {},
   "method" : "GET",
   "query" : {}
}

```	
> Result

```json

```	


### HTTP Request
GET /api/pharmetika/:version/event/patients_of_interest

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## event post notification to contact

> Arguments

```json
{
   "json" : {
      "event" : {
         "event_data" : {
            "comments" : [],
            "prescriber_id" : 4302,
            "rx_number" : "3401190",
            "status" : "attempting_to_contact_patient",
            "task_id" : 193668
         }
      }
   },
   "method" : "POST",
   "query" : {}
}

```	
> Result

```json
{
   "messages" : [
      {
         "message" : "Notification queued",
         "type" : "success"
      }
   ],
   "success" : 0
}

```	


### HTTP Request
POST /api/pharmetika/:version/event/:event_type/notify/:contact_id

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## event publish event

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
POST /api/pharmetika/:version/event/publish/:event_type

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## get action item score

> Arguments

```json
{
   "json" : {},
   "method" : "GET",
   "query" : {}
}

```	
> Result

```json
{
   "data" : {
      "team_action_item_score" : [
         {
            "date" : "2017-12-21",
            "points" : "20"
         },
         {
            "date" : "2017-12-22",
            "points" : "43"
         },
         {
            "date" : "2017-12-23",
            "points" : "47"
         },
         {
            "date" : "2017-12-24",
            "points" : "14"
         },
         {
            "date" : "2017-12-25",
            "points" : "30"
         },
         {
            "date" : "2017-12-26",
            "points" : "19"
         },
         {
            "date" : "2017-12-27",
            "points" : "30"
         },
         {
            "date" : "2017-12-28",
            "points" : "18"
         }
      ],
      "user_action_item_score" : [
         {
            "date" : "2017-12-21",
            "points" : "16"
         },
         {
            "date" : "2017-12-22",
            "points" : "29"
         },
         {
            "date" : "2017-12-23",
            "points" : "8"
         },
         {
            "date" : "2017-12-24",
            "points" : "4"
         },
         {
            "date" : "2017-12-25",
            "points" : "11"
         },
         {
            "date" : "2017-12-26",
            "points" : "14"
         },
         {
            "date" : "2017-12-27",
            "points" : "6"
         },
         {
            "date" : "2017-12-28",
            "points" : "9"
         }
      ]
   },
   "success" : true
}

```	


### HTTP Request
GET /api/pharmetika/:version/user/action_item_points

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## prescriber info

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
GET /api/pharmetika/:version/prescriber_info

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## prescriber info

> Arguments

```json
{
   "json" : {
      "DEANum" : "BJ9811325",
      "DoctorCode" : 1523,
      "NPI" : null,
      "_type" : "prescriber",
      "doctorFax" : 7346624481,
      "doctorName" : "JARRETT, HEATHER",
      "doctorPhone1" : 7346624474,
      "first_name" : "HEATHER",
      "label" : "[Prescriber] JARRETT, HEATHER",
      "labelName" : "JARRETT, HEATHER DVM",
      "last_name" : "JARRETT",
      "prescriber_id" : 1523,
      "realm" : "PSOL",
      "value" : "[Prescriber] JARRETT, HEATHER"
   },
   "method" : "POST",
   "query" : {}
}

```	
> Result

```json
{
   "DEA" : "FA4376382",
   "NPI" : 2757,
   "address_line_1" : "13201 Old Shore Place",
   "address_line_2" : null,
   "city" : "Salt Lake City",
   "contact_id" : 68230,
   "credential" : "DVM",
   "date_last_prescribed" : null,
   "date_updated" : "2017-11-13 20:01:21",
   "dids" : {},
   "email" : "bgrant1@mashable.com",
   "fax" : 2406266518,
   "first_name" : null,
   "general_notes" : null,
   "id" : 1523,
   "label_name" : "JARRETT, DVM",
   "last_name" : "Palmer, Lisa",
   "last_prescribed" : "2017-12-19",
   "name_full" : "Palmer, Lisa",
   "name_with_credential" : "Palmer, Lisa, DVM",
   "notes" : [],
   "patient_count" : 33,
   "pharmacy_id" : "1523",
   "phone_1" : 2406266518,
   "phone_2" : 2406266518,
   "phone_primary" : 2406266518,
   "phone_secondary" : 2406266518,
   "phone_sms" : null,
   "postal_code" : "20719",
   "prescriber_group" : null,
   "prescriber_id" : 1523,
   "rxs_0_30" : 5,
   "rxs_30_60" : 3,
   "rxs_60_90" : 3,
   "state" : "MD"
}

```	


### HTTP Request
POST /api/pharmetika/:version/prescriber_info

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## get contact call records

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
GET /api/pharmetika/:version/contact/:contact_id/call_records

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## get contact voicemail

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
GET /api/pharmetika/:version/contact/:contact_id/voicemail

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## get contact messages sms

> Arguments

```json
{
   "json" : {},
   "method" : "GET",
   "query" : {}
}

```	
> Result

```json
{
   "messages" : []
}

```	


### HTTP Request
GET /api/pharmetika/:version/contact/:contact_id/messages/sms

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## get contact log

> Arguments

```json
{
   "json" : {},
   "method" : "GET",
   "query" : {}
}

```	
> Result

```json
{
   "contacts" : [],
   "success" : true
}

```	


### HTTP Request
GET /api/pharmetika/:version/contact/:contact_id/contact_log

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## get contact log

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
POST /api/pharmetika/:version/contact/:contact_id/contact_log

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## contact add note

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
PUT /api/pharmetika/:version/contact/:contact_id/note

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## contact add note

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
POST /api/pharmetika/:version/contact/:contact_id/note

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## contact archive note

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
DELETE /api/pharmetika/:version/contact/:contact_id/note/:note_id

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## contact unarchive note

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
POST /api/pharmetika/:version/contact/:contact_id/note/:note_id

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## contact view rx notes

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
GET /api/pharmetika/:version/contact/:contact_id/notes/transactional/:rxn

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## contact view all notes

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
GET /api/pharmetika/:version/contact/:contact_id/notes/transactional

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## contact get action items

> Arguments

```json
{
   "json" : {},
   "method" : "GET",
   "query" : {}
}

```	
> Result

```json
{
   "action_items" : [
      {
         "completed_by" : null,
         "contact_id" : 1004,
         "data" : {
            "display_message" : "Ask about multi-vitamin"
         },
         "date_completed" : null,
         "date_created" : "2017-12-29 21:21:29",
         "date_expires" : "2018-06-27 00:00:00",
         "id" : 1036,
         "item" : "{\"display_message\": \"Ask about multi-vitamin\"}",
         "points" : 3,
         "ready_to_complete" : 1,
         "status" : "new",
         "type" : "ask_about_vitamins"
      },
      {
         "completed_by" : null,
         "contact_id" : 1004,
         "data" : {
            "display_message" : "Ask about Noctoplex"
         },
         "date_completed" : null,
         "date_created" : "2017-12-29 21:21:37",
         "date_expires" : "2018-06-27 00:00:00",
         "id" : 132106,
         "item" : "{\"display_message\": \"Ask about Noctoplex\"}",
         "points" : 4,
         "ready_to_complete" : 1,
         "status" : "new",
         "type" : "ask_about:Noctoplex"
      }
   ],
   "success" : true
}

```	


### HTTP Request
GET /api/pharmetika/:version/contact/:contact_id/action_items

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## contact add action items

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
POST /api/pharmetika/:version/contact/:contact_id/action_items

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## contact set action item status

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
PUT /api/pharmetika/:version/contact/:contact_id/action_items/:action_item_id

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## patient object

> Arguments

```json
{
   "json" : {},
   "method" : "GET",
   "query" : {}
}

```	
> Result

```json
{
   "error" : "Not authorized."
}

```	


### HTTP Request
GET /api/pharmetika/:version/patient/:patient_id/patient_object

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## add patient note

> Arguments

```json
{
   "json" : {
      "note_text" : "",
      "note_type" : "prescription",
      "rxn" : ""
   },
   "method" : "PUT",
   "query" : {}
}

```	
> Result

```json
{
   "messages" : [
      {
         "icon" : "glyphicon glyphicon-pencil",
         "message" : "Note Added!",
         "type" : "success"
      }
   ],
   "note_count" : 2,
   "note_id" : 86,
   "success" : true
}

```	


### HTTP Request
PUT /api/pharmetika/:version/patient/:patient_id/note

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## add patient note

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
POST /api/pharmetika/:version/patient/:patient_id/note

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## archive patient note

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
DELETE /api/pharmetika/:version/patient/:patient_id/note/:note_id

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## unarchive patient note

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
POST /api/pharmetika/:version/patient/:patient_id/note/:note_id

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## view rx patient notes

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
GET /api/pharmetika/:version/patient/:patient_id/notes/transactional/:rxn

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## view all patient notes

> Arguments

```json
{
   "json" : {},
   "method" : "GET",
   "query" : {}
}

```	
> Result

```json
{
   "args" : {
      "contact_id" : 480,
      "patient_id" : "21694",
      "prescriber_id" : null,
      "rxn" : null
   },
   "notes" : [
      {
         "attachment_id" : null,
         "contact_id" : 480,
         "created_by" : "rp-cs",
         "date_created" : "2018-01-02 18:41:16",
         "date_updated" : "2018-01-02 18:41:16",
         "id" : 84,
         "note_status" : 1,
         "note_text" : "",
         "note_type" : "prescription",
         "patient_id" : 21694,
         "rx_fill_num" : null,
         "rxn" : null,
         "updated_by" : null
      },
      {
         "attachment_id" : null,
         "contact_id" : 480,
         "created_by" : "rp-cs",
         "date_created" : "2018-01-05 07:59:39",
         "date_updated" : "2018-01-05 07:59:39",
         "id" : 86,
         "note_status" : 1,
         "note_text" : "",
         "note_type" : "prescription",
         "patient_id" : 21694,
         "rx_fill_num" : null,
         "rxn" : null,
         "updated_by" : null
      }
   ],
   "success" : true
}

```	


### HTTP Request
GET /api/pharmetika/:version/patient/:patient_id/notes/transactional

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## patient get document list

> Arguments

```json
{
   "json" : {},
   "method" : "GET",
   "query" : {}
}

```	
> Result

```json

```	


### HTTP Request
GET /api/pharmetika/:version/patient/:patient_id/documents

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## patient put document

> Arguments

```json
{
   "json" : {
      "category" : "transactional record",
      "data" : "data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAABsgAAAH0CAYAAACQIqi/AAAAAXNSR0IArs4c6QAAQABJREFUeAHsnQn8btW8/0vzPCtJ56SiQXWjidCJBlNIkuGiMsucOSS65msmc7gZk+GarjJUFCqkRHQVKilTg5Sm///zuZ1V66yz9jPueb/X6/X9rWGv/R3ea+39/J49rGeZZUgQgAAEIAABCEAAAhCAAAQgAAEIQAACEIAABCAAAQhAAAIQgAAEIAABCEAAAhCAAAQgAAEIQAACEIAABCAAAQhAAAIQgAAEIAABCEAAAhCAAAQgAAEIQAACEIAABCAAAQhAAAIQgAAEIAABCEAAAhCAAAQgAAEIQAACEIAABCAAAQhAAAIQgAAEIAABCEAAAhCAAAQgAAEIQAACEIAABCAAAQhAAAIQgAAEIAABCEAAAhCAAAQgAAEIQAACEIAABCAAAQhAAAIQgAAEIAABCEAAAhCAAAQgAAEIQAACEIAABCAAAQhAAAIQgAAEIAABCEAAAhCAAAQgAAEIQAACEIAABCAAAQhAAAIQgAAEIAABCEAAAhCAAAQgAAEIQAACEIAABCDQAgIryodDJGcsloOVu40EAQhAAAIQgAAEIAABCEAAAhCAAAQgAAEIQAACEIAABCAAgV4SeKOi+n+JuI0EAQhAAAIQgAAEIAABCEAAAhCAAAQgAAEIQAACEIAABCAAgd4RuLsiSm+OuX5F7yIlIAhAAAIQgAAEIAABCEAAAhCAAAQgAAEIQAACEIAABCAAgcETuJcI5G6OcYNs8FMDABCAAAQgAAEIQAACEIAABCAAAQhAAAIQgAAEIAABCECgfwR2V0hFN8fczhKL/RtzIoIABCAAAQhAAAIQgAAEIAABCEAAAhCAAAQgAAEIQAACgyVwP0U+6ubY+7V9xcHSIXAIQAACEIAABCAAAQhAAAIQgAAEIAABCEAAAhCAAAQgAIHeELiDInm1ZNTNsV9r+wq9iZhAIAABCEAAAhCAAAQgAAEIQAACEIAABCAAAQhAAAIQgAAEBktgeUX+Q8mom2Pets1gCRE4BCAAAQhAAAIQgAAEIAABCEAAAhCAAAQgAAEIQAACEIBAbwgsp0hulIy7ObawNxETCAQgAAEIQAACEIAABCAAAQhAAAIQgAAEIAABCEAAAhCAwGAJeLnEcTfGvH3BYAkROAQgAAEIQAACEIAABCAAAQhAAAIQgAAEIAABCEAAAhCAQK8InKpoxt0g27pXERMMBCAAAQhAAAIQgAAEIAABCEAAAhCAAAQgAAEIQAACEIDAYAkcoMjH3Rxba7B0CBwCEIAABCAAAQhAAAIQgAAEIAABCEAAAhCAAAQgAAEIQKBXBFZRNONujq3Yq4gJZikCyy/VQgMEIAABCEAAAhCAAAQgAAEIQAACEIAABCAAAQhAAAIQ6C+BZ4wJzTfHbhzTh80QgAAEIAABCEAAAhCAAAQgAAEIQAACEIAABCAAAQhAAAIQ6ASBZeXlqLfH1ulEFDgJAQhAAAIQgAAEIAABCEAAAhCAAAQgAAEIQAACEIAABCAAgQkJ3F/9im6QHTahDrpBAAIQgAAEIAABCEAAAhCAAAQgAAEIQAACEIAABCAAAQhAoDMEXiNPi26QLdeZKHAUAhCAAAQgAAEIQAACEIAABCAAAQhAAAIQgAAEIAABCEAAAhMS+JH65W6QfWDC/ekGAQhAAAIQgAAEIAABCEAAAhCAAAQgAAEIQAACEIAABCAAgc4Q2ECe5m6Oue0enYkCR0shcIdStKAEAhCAAAQgAAEIQAACEIAABCAAAQhAAAIQgAAEIAABCLSbwMoj3Lt8xDY29ZAAN8h6OKiEBAEIQAACEIAABCAAAQhAAAIQgAAEIAABCEAAAhCAwFIEDlyq5faGP99epAQBCEAAAhCAAAQgAAEIQAACEIAABCAAAQhAAAIQgAAEIACBfhA4RWHkllj8XD/CI4ppCPAG2TS06AsBCEAAAhCAAAQgAAEIQAACEIAABCAAAQhAAAIQgEBXCdy/wPEfFbTTDAEIQAACEIAABCAAAQhAAAIQgAAEIAABCEAAAhCAAAQgAIHOElggz3Nvj7ntjp2NCsdnJsAbZDOjY0cIQAACEIAABCAAAQhAAAIQgAAEIAABCEAAAhCAAAQ6QuCuI/y8dsQ2NvWUADfIejqwhAUBCEAAAhCAAAQgAAEIQAACEIAABCAAAQhAAAIQgMBtBPa4rbR0gRtkSzOhBQIQgAAEIAABCEAAAhCAAAQgAAEIQAACEIAABCAAAQhAoOMErpb/uSUWT+14XLg/IwHeIJsRHLtBAAIQgAAEIAABCEAAAhCAAAQgAAEIQAACEIAABCDQGQJrFHj6nYJ2mntOgBtkPR9gwoMABCAAAQhAAAIQgAAEIAABCEAAAhCAAAQgAAEIDJzAciPiP3PENjZBAAIQgAAEIAABCEAAAhCAAAQgAAEIQAACEIAABCAAAQhAoJMEtpLXueUV3bZ+JyPC6bkJ8AbZ3AhRAAEIQAACEIAABCAAAQhAAAIQgAAEIAABCEAAAhCAQIsJ3HeEb38ZsY1NPSbADbIeDy6hQQACEIAABCAAAQhAAAIQgAAEIAABCEAAAhCAAAQgsIzfICNBAAIQgAAEIAABCEAAAhCAAAQgAAEIQAACEIAABCAAAQhAYDAELlKkuSUWbxgMAQKFAAQgAAEIQAACEIAABCAAAQhAAAIQgAAEIAABCEAAAhAYFIHczTG3nTMoCgS7BAGWWFwCBxUIQAACEIAABCAAAQhAAAIQgAAEIAABCEAAAhCAAAQGQuDkgcRJmBkC3CDLQKEJAhCAAAQgAAEIQAACEIAABCAAAQhAAAIQgAAEIACB3hO4sPcREmAhAW6QFaJhAwQgAAEIQAACEIAABCAAAQhAAAIQgAAEIAABCEAAAj0mcHmPYyO0MQS4QTYGEJshAAEIQAACEIAABCAAAQhAAAIQgAAEIAABCEAAAhDoJYErehkVQU1EgBtkE2GiEwQgAAEIQAACEIAABCAAAQhAAAIQgAAEIAABCHSMgK9/cw28Y4NWs7s31WwPcy0iwMmhRYOBKxCAAAQgAAEIQAACEIAABCAAAQhAAAIQgAAEIDA3gS2l4Q2SixeLy24jQSAlcH3aQB0CEIAABCAAAQhAAAIQgAAEIAABCEAAAhCAAAQgAAEIdI3AdnL4Osn/S8Rt3kYaJoF0PoT6XsPEQdQQgAAEIAABCEAAAhCAAAQgAAEIQAACEIAABCAAAQj0icCJCibc/Ejzn2rbKn0KllgmJpDOhVDfb2INdOwdgeV7FxEBNUlgdRlfWeJ5tZ7k5sVl1/8muUXyT8lVi8s+CZEgAAEIQAACEIAABCAAAQhAAAIQgAAEIAABCJRBYDkpecAIRTtq27cl95f42iVpOATOVKg7Z8K9U6aNpoEQ4AZZvwfavzG3msQ3pdaW+CaV6/+QrCC5UeLkD45wM8t137jaVuIbWetLtpc4bSFZKPHNr60kCyTzphuk4BzJWZLfSv4i+Z5kWcmlkuCjiiQIQAACEIAABCAAAQhAAAIQgAAEIAABCEAAAnMRuI/2fozkM3NpYeeuESi6QeZr3SQIQKDDBFaS74skx0mulvgG1zTiG2enSHxzapr96uh7mXz6uuRxkoMk/vBaS+I7++tISBCAAAQgAAEIQAACEIAABCAAAQhAAAIQgAAEAoFRSyzG1zO3DjuQD4KAl1KMxz+UPzWI6AkyS8Bv6ZC6ScBvgvmgfpfkjt0MoRSv/ebbeZJzJVdI/DbcjyW+eeY2b/+z5HLJTZJrJSQIQAACEIAABCAAAQhAAAIQgAAEIAABCECgnwS2U1hnSPxTMKOSrx3uKPH1Q1L/CWyjEH0dOU2nqeG+aSP1YRDgBln3xvmucvkIyaHdc711HntpxyslF0oukfgG2y8lf5WcL/Hyj/7dNBIEIAABCEAAAhCAAAQgAAEIQAACEIAABCDQHQJbytVDJM+RrDHC7Ydq2zdGbGdTfwj4xQq/QJEmXwv2zwyRIACBFhPwb36dLAmvfpLXx8I3yz4keZrEv8PGjWVBIEEAAhCAAAQgAAEIQAACEIAABCAAAQhAoOUEVpB/r5cUXUv1A/K+mUYaBoGieTCM6IlyKQJc6F8KSSsbjpZXfmusy8m/b+b5dqPkKsnyEt+x94fUHST+XTH/ltqqklzyfu7bpvR2OfN9yQ8kjo8EAQhAAAIQgAAEIAABCEAAAhCAAAQgAAEItIuA3xz6mcRLLxYlX5f0zTJSvwn8XOFtnwmR+yQZKENoYuDbPcr+nbFXSOq4OXa97PxrMY4/Kv+nJPx2lz9EvPyg+/xBcp3kEolvdPm3vdzXSxWWuRyhb5hdLdlUsp7kd5K9JE725QkS+3UnideIXV3SdDpGDnxJcqoksGzaJ+xDAAIQgAAEIAABCEAAAhCAAAQgAAEIQGDoBLYWgO9IfC0xl45VIz9pkyPTr7YXKZz/zITk68xlXtvOmKCpjQS4QdbGUbnVJ4/NKZL7leSi11L9hcQ3tC6Q+AaOn5xwu5+QOEMSnpLIrcWqza1NfgPNJ7CNJXeUOI7dJb6h5w+/jSReR3aRxDcd3b/qdJwMfEpytuRPVRtDPwQgAAEIQAACEIAABCAAAQhAAAIQgAAEIDCSwAO01TfJitI+2nBS0Ubae0FgE0VxcSaSu6rtokw7TRCAQEMEXii7RWuiFrX7ZtfhkntLlpeQign4Rtkqkh0ku0gOlbxE8jHJmRK/vVbEedr2X0uX9a8jIUEAAhCAAAQgAAEIQAACEIAABCAAAQhAAALNEPiIzI66tueH7En9JeCf8MmNv2+OkiAAgZYQ8BtduQO1qG0/9S/67a6WhNRZN/wm37qSRZJnSz4pKRqHSdq9BOO+EhIEIAABCEAAAhCAAAQgAAEIQAACEIAABCBQP4HTZLLoOt6P6ncHizUTuCwz/gfW7APmIACBEQS8rGLRSTq0+3e4tpGwTOYIkBVuMncv5/hEyTskYVymyT+q/fwba4yhIJAgAAEIQAACEIAABCAAAQhAAAIQgAAEIFADgdVlY9Q1vPvU4AMmmiPwwcz4u40EAQi0hMDb5EfRSfoP2nb3lviJG0sS8JtmO0leIykav1y7b3a+SkKCAAQgAAEIQAACEIAABCBQF4EVZegQyRmL5WDlbiNBAAIQgAAEhkBgSwWZu04X2obAYKgxHpQZ+/8eKgzihkAbCXxGToWTcZqv1EaH8SlLYDO17ivxm2LpOObqF6jfuZKHSPgNOUEgQQACEIAABCAAAQhAAAKVEXijNKffS9xGggAEIAABCAyFwGMUaPpZGOq7DAXCAOP0ddcwziH/zQA5EDIEWkvAbxSFgzPOL22txzg2jsAd1OH+kldIrpbE45or/0N9TpXcQ8KPgwoCCQIQgAAEIAABCEAAAhAolUDue6fbSBCAAAQgAIEhEchdl3PbGUOCMMBY/66Y47H/6wAZEDIEWkvgKnkWH6Ch/JXWeoxj0xBYQZ13ljxY4qcTbpJcIwnjnOa3aNsnJf5tujUlJAhAAAIQgAAEIAABCEAAAvMS4AbZvATZHwIQgAAE+kBgCwWRXosLdVby6sMI52N4ezLul6jOil55VrRCoHYCRW8YHTXGE9aQHwOohZv9ZtkakodKvLyib4aFD+Gi/Gj12UFCggAEIAABCEAAAhCAAAQgMCsBlliclRz7QQACEIBA3wgUXYPbtm+BEs9tBPZWKR33B9y2lQIEINAYgWVlOT04Q32nMV7xBWcMoI5sPlx+/lYSxr0ov1h9Hi3xnCFBAAIQgAAEIAABCEAAAhCYhgAPWE5Di74QgAAEINBnAk9QcLnrb4f1OeiBx+abYemYP3DgTAgfAq0gsJm8SA/OUPe2USm3RIbfSCJ1k8Bd5PYHJWH8R+XvVb+FEhIEIAABCEAAAhCAAAQgAAEIQAACEIAABCAwOQEvrZe77nbm5Cro2TECuTF/dsdiwF0I9JJA2TfIfHJ/VC9JDSeoZRXqAZKTJbkP67jNPzC5o4QEAQhAAAIQgAAEIAABCEAAAhCAAAQgAAEITEbgJ+oWX2Nz+YLJdqVXRwn8VH7HY352R+PAbQj0isDmiiY+MEP5N2r3jZJRKbfEove/XMKPSo4i151tvoH6ZkmYF0W5l1/cujth4SkEIAABCEAAAhCAAAQgAAEIQAACEIAABBoj8HRZTq+zXae2tRvzCMNVE/i6DMRj7tXZSBCAQMMEHif78YEZyp+awC+vIR/6p7n1kvpDYA2F8iTJOZJ0rOP6t7R9oYQEAQhAAAIQgAAEIAABCEAAAhCAAAQgAAEI5AncXc3xNbVQ5nep8rz60LpfZsw37ENgxACBLhN4pJwPJ+A4P2LCoD5asP+lavfaqqT+EdhKIX1ZEs+XtPwFbV+tf6ETEQQgAAEIQAACEIAABCAAAQhAAAIQgAAE5iZQ9OLBrnNrRkFbCTxBjqXXUA9qq7P4BYGhEDhYgaYHpuu+oz1Juqs65fZ322MnUUCfzhJYKM8vkhSNv9t3kpAgAAEIQAACEIAABCAAAQhAAAIQgAAEIACBJQnkrqk9Z8ku1HpEwD9lk475/j2Kj1Ag0EkCj5fX6YHp+oIpojmxQMdNah/3O2ZTmKFrSwlsK7/Ol+Tmkds+IPFTMSQI1EnAc+4QyRmL5WDlzENBIEEAAhCAAAQgAAEIQAACEIAABCDQCgIXyov0etqLWuEZTlRFIB3vE6oyhF4IQGAyAnurW3pgur7xZLv/X6+dC3RYzyOm0EPXbhPYXe7n5lJou1O3w8P7jhF4Y2Y+uo0EAQhAAAIQgAAEIAABCEAAAhCAAATaQODrciJcNwv5c9vgGD5URiB9yeDPlVlCMQQgMBGB7dQrnIDjfPOJ9r6900UFeq68vQulARDwGzqvl8RzKS7zQ6MDmAQtCfGKzDy8qiW+4QYEIAABCEAAAhCAAAQgAAEIQAACEPiGEMTXzVw+ECy9JvDJzJiv1uuICQ4CLSewqvxLT8SuT3uDbN8CPda1o4Q0LAJ3U7i5eeW2d0tWGBYOom2AQO4Gmecfyyw2MBiYhAAEIAABCEAAAhCAAAQgAAEIQGApAuepJb1+ttNSvWjoE4EjMmO+W58CJBYIdJFAeiJ2fZY3fXJ6QlsXueDzfARW1+6nScIciPNT1c7v083Hl71HE/i+NsdzLpQPHb0bWyEAAQhAAAIQgAAEIAABCEAAAhCAQC0ErpGVcL0i5OvWYhkjTRG4V2bM92rKGexCAAK3Eggn4Dh/6Axw3qx9Yh1xeZcZ9LFL9wn4JthBknguhPLFal/Q/RCJoKUEDpdfYa6leUtdxi0IQAACEIAABCAAAQhAAAIQgAAEBkQgvV7hOg+U93sCrKXw0nH/SL9DJjoItJ/Ar+ViemA+fwa3V8roifXOoJJdekJgsxFzg5unPRnkloXheRWff+LyJi3zFXcgAAEIQAACEIAABCAAAQhAAAIQGB6B+FpFKA+PwrAiXk7hhrEO+S3DQkC0EGgfgY/KpXBAhvwhM7rpO95BR5r7JglpuATWV+inS9J54fq9h4uFyCsicAfpzc01t/2wIpuohQAEIAABCEAAAhCAAAQgAAEIQAACkxDwb6Sn1y3On2RH+nSewJ8yY8+bg50fVgLoMoG3Zw7KN8wYkH93Kj25h/rvZ9TJbv0h4KckXicJcyLOj+pPmETSEgLx/ErLq7XER9yAAAQgAAEIQAACEIAABCAAAQhAYHgEVlHI6bUKro0NYx68LzP2XKcaxtgv4yf6Se0jcH2JLv1Dun5XoG9TtbO0WQGcgTTfrDhfI3lqJl63P1PCB0IGDk2lE/j30jWiEAIQgAAEIAABCEAAAhCAAAQgAAEITEZgzUy3czNtNPWPwFmZkB6caaMJAhCoicA9ZcdrncZPLTxhDtu+ERbrisu/nUMvu/aLwNYF8+SD/QqTaBokEJ970vI5DfqFaQhAAAIQgAAEIAABCEAAAhCAAASGTeB+Cj+9VnHwsJEMJvp/y4z9OwcTPYFCoIUEniif0hPyJ+b0M9UX170MIwkCJuAPhAsl8fxw+QTJNhISBGYl4PmTzqu0zhyblS77QQACEIAABCAAAQhAAAIQgAAEIDAPgdwSi3ecRyH7dopAeo3qjE55j7MzE2CJxZnRVbrjxRVo32qEzneP2MamYRE4W+F6rvwqCftRqvvJieWTdqoQmJSAn8QalybpM04H2yEAAQhAAAIQgAAEIAABCEAAAhCAwLQEvKJXmrZMG6gPhsDOg4l04IFyg6ydE+D8jFsrZNqmafq1Ol9TsMMhal+2YBvNwyNwg0LeTXJkEvoi1S+RzLPcZ6KSKgSWILDyEjUqEIAABCAAAQhAAAIQgAAEIAABCEAAAhConsDPMiY2yLTRBAEI1EBgO9lIX+s8pQS7B2b0BjvPLEE/KvpH4NjFcyb+Tbyb1LZZ/0IloooJ7CX94XxTlL+xYh9QDwEIQAACEIAABCAAAQhAAAIQgAAEcgT8csJVknDNwi8arJTrSFsvCTxfUYWxD/mevYyUoCDQAQJexi4ciCH/RQl++43BoC+Xl2ACFT0ksKliulKSzpnj1Mabhz0c8IpCelhmDqVzyst4kiAAAQhAAAIQgAAEIAABCEAAAhCAQN0EdpHB9DrFHnU7gb3GCNw3M/5faMwbDENg4ARWV/zpCfkPJTF5aUZ3sLV/STZQ0z8CXlbxT5IwV0L+H2pbu3/hElEFBBZJZ5g3RfmZFdhFJQQgAAEIQAACEIAABCAAAQhAAAIQGEdgE3VIr1dsMW4ntveGwIqZ8b+0N9ERCAQ6SCA9Ift3ocpIuZtvwdY5ZRhAR28J+M3G70rCfAn5hWpbtbdRE1hZBLwsZ5gzRfkvyzKGHghAAAIQgAAEIAABCEAAAhCAAAQgMAUB/y56er1i4yn2p2v3CaTj77pXZCNBAAINEMgdkGW58R4pyum/We0LyzKCnl4S2FZRfVGSzp+/qm23XkZMUGURyP22YjqP/lmWMfRAAAIQgAAEIAABCEAAAhCAAAQgAIEpCGypvul1in2m2J+u3Sfw08wcuEf3wyICCHSTQHpCdr2slHtlONg7XUb4XamySPdXz/sUWpgzcf5v/Q2ZyOYkMOrt1XgOzWmG3SEAgQET8JN9u0qOXCwu87SfIJAgAAEIQAACEIAABCAAgbEEfD00vj7hsq+hkoZD4JEKNZ0DzxhO+EQKgXYRSA9G18tMRTc4bMdPTJAgMIrAatr4bElunr5q1I5sGyyBNQrmSzqHBguIwCEAgbkJfEEa0nPKJ+fWigIIQAACEIAABCAAAQhAYAgEcg/27j+EwInxNgJ3VCn9TnndbVspQAACtRLwcofpAVmmA5tn9Ad7J5VpCF29JnBEwTxyO79L1uuhnzo4v8URzjGj8qkVswMEIAABEThYUnRuOQhCEIAABCAwNQF/X3ymxE9Nu0yCAAQgAAEIDIFA+p2ClZKGMOpLxpjOAddJEIBAAwQulM30gCzTDb827OUUUxuh7t+aIkFgEgI7qVOYN3F+ntrXnkQBfQZDIJ4fReXBwCBQCECgVAJF5xS3XynxD26TIAABCEBgMgK5h+DcRoIABCAAAQj0nUD6veJJfQ+Y+JYicIpa0nnAw0JLYaIBAtUTOEEm0oOx7N8G88Gd2gj1P1cfIhZ6ROC+I+bSmj2Kk1DmIxDOL6Py+SywNwQgMEQCqyjoUecVb3vKEMEQMwQgAIEZCGyjfYrOqd5GggAEIAABCPSZQPoZ+Jg+B0tsWQKPV2s6D96e7UkjBCBQKYFXS3t6MK5UgcULMnaC3QUV2ENlfwlsqNAuk4T5E+fb9TdsIpuCQDwnisplPwgwhXt0hQAEOkpgHflddE6J23mruaMDjNsQgECtBI6RtfjcGZe9AgkJAhCAAAQg0GcC/1Rw8Wcfb1D3ebTzsXn1kXgOhHK+N60QgEBlBA6Q5nAAhtw/FFh2eo4UBv1p/suyjaGv9wT8u2O/laRzyfW9ex89AY4jkJsXadvy45SwHQIQgEBCYDnV/yVJzydp3b+jQ4IABCAAgdEE/qLN6fkzro/em60QgAAEIACBbhO4Se7Hn3tHdzscvJ+RQDwHQtkrl5AgAIEaCfhHIMMBGPJNK7B/h4ydYM+5b3iQIDANAX9gfFESz6NQ3ncaRfTtHYEwD0bl/MPRu2EnIAhUTuDusjDqvBK2eS153lKtfDgwAAEIdJzA7+R/OG+m+R86HhvuQwACEIAABMYR+Ik6xJ9/nx23A9t7SeDIZB54Tjyyl5ESFARaTGBd+RafkF3evyJ/P5OxFWy/qiKbqO03Ad94PVIS5lGcey1f0jAJxPOgqLzeMNEQNQQgMAeBSW+Q+bzjN+dJEIAABCBQTCBdWir+n40bZMXc2AIBCEAAAv0g8DWFEX/2ndiPsIhiSgJenj+eBy7/bUoddIcABOYksIL2Tw/Ex8yps2j31TO2YttF+9EOgXEEDleHeC6F8kvH7cj2XhK4pmA+hHnhfLVeRk5QEIBAlQS8xGJ8HhlVPqdKR9ANAQhAoOME/KDSqHOot/EwU8cHGfchAAEIQGAkgQ9ra/xZyPeHkbh6vTGeB6Hs6/UkCECgRgLh4Av5myq0nT4hEWw6375Cu6juP4FnKsR4PoXya/ofOhEmBM4smAthTjj3UzokCEAAAtMSiM8jo8r/kOItp1VOfwiMIOC35teS7Cbx762+WvJ2iVdo+C+JV2N4suTOEhIE2k5gKzk46hzqbdwga/so4h8EIAABCMxD4BXaOf4s/Os8yti30wSOSOaC58WDOx0RzmcJLJ9tpbEtBPxbGXtEzqwZlcsuetm7qwqUvlztLItXAIfmsQQ+oB5XSz6V9DxKdb+e/N6knWp/CZyv0HYaE961Y7azGQIQgECOwAlqPCC3IWnzW6ofkcT/XyVdqPaIgN8u9Pcd3xRdX7KtZBPJhpI7SbyKgre73y2SGyReXm5FyUUSb1tZ8l3JdhL3u0yyq2QLifffWDJNerQ6f0Vy0zQ70RcCNRGY5KKPjxESBCAAAQhAoK8E/pEE5oehSMMk8B6FfXQS+odUv0vSRhUCEKiQwPul23eng5xcoS2r9gWjYCvO/1KxXdQPg8DDCuYXP3I5jPF3lH5rMD635MrLDgcHkUIAAiUSeKd05c4pRW0blGgbVfUT8E0uPzjmG16PkhwoeYvk05JfSIrGvU3tz5WfvgFHgkCbCHgZ9HHHyc5tchhfIAABCEAAAiUT8P+W6WdhySZQ1yECZ2TmQ5UvsHQIDa5CoB4Cb5WZ+KT8q4rNenmY2F4o36x2LlpXDH8g6r30UJhXcc4X7WFMAD81H497rjwMEkQJAQiUTWB/KcydU4raPlq2A+irjIDf5jpE4i+nfiO9aEy72H664rmXhASBthD4thwZdyz5bUoSBCAAAQhAoK8EHq7A4s9C//9JGi6B3HWsFw8XB5FDoH4Cfio2Pim7XHX6rAykNl0/qGrD6B8MAS+BlZtjGw2GwHADXVQw9vF8GC4dIocABOYhsJl2js8lk5RXm8cg+9ZG4I0zjO0k49+mPn4ozjcCSRBokoD/F5/kuNipSSexDQEIQAACEKiYgFc5ij8PL6/YHurbTWCFZD54bvyh3S7jHQT6RWChwolPyi4vqDhEL1lzTcbuyRXbRf2wCDxP4aZz+3q1sdRQv+fB5plxT+dBvwkQHQQgUCWB9Hwyrp6uJ1+lb+iencAV2nXcWPZh+3mKk+VaZp8n7Dk/Af+e3iTH0mPmN4UGCEAAAhCAQGsJ3EeexZ+Hf2ytpzhWF4E3JHPC82OLuoxjp3oCXIyunnHXLFwih38i2SNx3PVVJNcl7VQhMAuBd2snP336xGjnlVR2+7OjNor9IuCboCQIQAACbSFwhBx5veRfbXEIP1pB4Fp58Q+Jl3S8ZbF42bltJF5y/JeSrSS+cecniv3/i/93djpHcpMk/rzzm2H3lzxNMurGgvVfJVkg4alUQSDVTsBLmU6SuIYwCSX6QAACEIBAVwksTBz/TVKnOjwCb1PIr0jCfqXqhyZtVCEAgYoIfEt6fWfa4gs4XkKo6uTlFIPNOH9V1YbRPygCvsj0V0k8x1zeb1AUhhWsLxKm4x3XTx8WDqKFAARKJhCfTyYtP7dkH1BXPoGyllj0b/l+WWJ9fkBnV4mf/PQDYL7JVUe6s4y8TzJufq5RhzPYgEBCwDd4x81Nb39Gsh9VCEAAAhCAQJ8I3E/BxJ+HX+pTcMQyM4Hjk3nhOeLvESQIQKAGAqfJRnxi9pPOdaTYZlyuwzY2hkPAHybx/ArldYaDYFCR+gJkGONcfuSgaBAsBCBQNoEvSmHu3DKuzQ9skNpLwA9X+M0Wv9H1M4kvUnxV8nGJf7vrLRLf6HyqZHfJzpLVJW3+wnpP+TduXq6qPiQI1Elg3JwM24+u0ylsQQACEIAABGomkP4kyEdqto+5dhK4l9wK/wuF3L9XR4IABGogcIJshAPPuV/hrCN9XUZiu6G8Yx3GsTEoAn4rMsyvkHv+kfpJIIxxLt+lnyETFQQgUBMB3yDJnVvGte1Wk3+YgUBMYBNV/ikpmp8fijtThkDFBMY9xBTP0/dU7AvqIQABCEAAAk0S8E2P+HPvWU06g+3WEPBDlX+UxHPDL7WQIACBGgh4CZj44PtcDTZt4t6J3eDDd2uyj5lhEXhpZr55qU9S/wiEc0ku37B/4RIRBCBQIwEvX5c7t4xr+0KNPmIKAjGBO6hymaRojm4fd6YMgQoJPEi6i+Zh2s45s8KBQDUEIAABCDROwKsTxJ99L27cIxxoCwFfp4znhsvrt8U5/IBAnwkcruDig89foutI/sIe243LbV6ypg422CifgJ/EuEASzzOXvawSqV8E0jGO6z7vkCAAAQjMQyA+p+TKN0h5rp3Pm3mos+88BLyUYm5Ous1PqZIgUAcB//h80TxM239eh0PYgAAEIAABCDRE4PmyG3/27dWQH5htHwFfD4/nhsvHtM9NPIJA/whsoZDSg883E+pIP5GR1LbrXsKIBIGyCawlhel8e3/ZRtDXOIF0jON6487hAAQg0HkC8TklV75UEeba/fYECQJNEdhShnPz0m13asop7A6KwOWKtmgOpu0XDooMwUIAAhCAwNAI+IZH/Nm36dAAEO9IAn6jMJ4fLvOw5UhkbITA/ARyywX5plkdqegHxM+rwzg2Bkng8Yo6/aDZapAk+ht0Or6hzm+t9HfMiQwCdRK4TsbCeWWa/Mw6ncQWBDIELlZbbs6+INOXJgiUTSA390a1lW0ffRCAAAQgAIG2EPimHIk/A+/fFsfwoxUEvKRiPD9cfmErPMMJCPSYwAqKLT3wfNOsrpTaDvXl63IAO4Mi4Lcj/SOXYZ45P2VQBPofbDy2cflx/Q+dCCEAgRoI5J7oi881Lr9Gkra5Xtcb+jVgwEQHCewqn3Pz8uQOxoLL3SKwmtzNzb1Rbd2KEG8hAAEIQAACkxNI3yDj+ufk7IbS8w0KNP4/6TdDCZw4IdAkgfT3Mupc4vAlCjw+6EN5zyaBYLvXBNbOzLmH9DriYQV3dmZ8fV7Ze1gYiBYCEKiIQO6JvvC/S8g3lu1QjvO63tCvKHTUdpzAygXz0m9FkiBQJYFHSHl8LpykXKU/6IYABCAAAQg0RcAPzF0mCZ+FXoKYh+iaGo322t0smiNhrjysve7i2TgCdxjXge2tIHBu4sXdk3qV1fcWKN+/oJ1mCMxL4Eop8I3ZOH0grlDuNIFfZrz3mJ+eaacJAhCAwLQE/jLBDteozz8z/dLPnkwXmiBQGYHrCzT7xhkJAlUS2DlRflZSpwoBCEAAAhAYKoFbhho4cY8kcJG2viPpcVBSpwoBCJRM4GPSF+5IOz+xZP3j1MW2Q/lf43ZiOwTmJHCJ9g/zzfmT5tTH7u0g4PNXPK4u/7gdruEFBCDQEwLpOSat76A4XyRJ23/ek/gJo5sERi1z182I8LorBP4hR+Pz4fuSerwtlLsSG35CAAIQgAAEpiHgF0m+K/HnnVfz4relBIGUJXAPtYb/i0K+dbYnjRCAQCkEniAt4WALeSmKJ1SyU8a+/SBBoEoCi6Q8zHfnvim7uoTUbQLfk/vxuLr8zW6HhPcQgEDLCBwhf9LzTFz3bx5uUtDHy2WQINAEgW1lNJ6ncbkJf7A5DAL+XZV4rrl8QKYt7TMMOkQJAQhAAAJDI7CbAo4/844bGgDinYrAS5P54t+vI3WQAEssdmPQ/CZNk4llNpqkP1zbJyv0L0bhr6jyo6M6xW4SyC0RW/dbsd0kh9cQgMCkBD48puM+2u7/rT6X6Xdopo0mCNRB4JEFRn5T0E4zBMogsH6i5DTVL03aqEIAAhCAAASGQuCvSaBpPdlMdeAETkni31P1FZI2qh0gwA2yDgySXMwtP7Z2za6/MWNv40wbTRAok8CrE2XHqs4rywmUDlWXk6/rZvxdM9NGEwQgAIFZCVwxZke/PeZ0wa3ZEn/XWaJGBQL1EXhMgamvFbTTDIEyCKQPBXxZSi8uQzE6IAABCEAAAh0ksEbi86eTOlUIxAR8vT7+HWs/EP7KuANlCECgXALxK74ub1eu+rHa7qIeqQ+5C91jFdEBAlMSOFr947l3+JT70709BPxQRjyWofzi9riIJxCAQE8IfEJxhHNMLneYXk7xuqSfnxLl/xtBINVKIPd/dpi3O9fqCcaGRsBv3Ia55vw+klG/hxf6Do0T8UIAAhCAwDAI+OWA8Fnn/LnDCJso5yCwvfaN54x/w44EAQhURCA+2FxO36ypyOwSan+kWuzHTktspQKBaghsKrV/kMRzb+9qTKG1YgJ+Gisex1DmrcCKwaMeAgMksKNiDueYXB6Q/Hem32PDRnII1ETgqbKTm6du880zEgSqIODf9vVv/Ia590+Vl11sKLQV5Yu7kUEAAhCAAAR6RcBvVseffVv1KjqCqYKAV0rym2Rh3vxK5ftWYQid1RHw0/ykbhDwevBx+re4UlP5s4md3G8JJV2oQmBuAr459sxEyyOSOtVuENi1wM0tC9pphgAEIDArgXPG7BguAv8802//TBtNEKiSwAsKlP9W7Sx3VwCH5rkJ+Oarf+M3pO+o4Is7JAhAAAIQgMBQCeyZBH55UqcKgZTAzWrYQ3Lh4g2+qfq+xWUyCECgZAJPl75wNzrkJZsYq+6O6vHrxX78Tjm/0yEIpFoI+DeqLpOEuf9Tle9di2WMlEngblIWxjDOuUFWJmV0QQACgcB5KsTnmri80eJO62f6+C0KHiJbDIiscgLryUI8N+Pycyq3joEhE3hgMvf2iWDE8zBXjrpShAAEIAABCPSGwLcVSfy55//TSBCYhIAfvIznzvKT7EQfCEBgOgJeDz4+0FxuIr1CRoMfL2/CAWwOlsAGivwiSZh/Pxksie4G/uRo/MI4Ol+huyHhOQQg0GICj5Rv8bkmLq8V+e3Pk3iby/59MhIE6iDwGhlJ51+ob1GHA9gYLIHzo7l3RUIhzMGiPOlOFQIQgAAEINALAvGD2f4MJEFgUgJeVjH+v+l7qvPQ5aT0Gu7HQDU8AFOYz90MaOINLj4gphg0upZK4M/S9rdI4z1V5mmeCEgHigsKfPSPwZMmJ+AL97tIvNY1CQIQKCbwjeJNy+wdbft4VA7F54cCOQQqJnDUCP3/O2IbmyAwL4FlIwXx/9hRM0UIQAACEIDAoAiEVSYcdPrwyKBAEOzUBH6gPb4Q7bVI5a2jOkUIQKAkAvGdaJf9VlndyevUHyO5ReJlOUgQqJOAl1WMj4Pfq75qnQ5gay4CXoc5Hr9QnkvpwHZ+csTw6wOLnXAhMAuB/9FO4VwT58+KlG1Y0CfqQhEClRC4l7TG8zIuP7cSiyiFwK0E9lTm5WQ95/wQ2gMkcbpalXg+puW4L2UIQAACEIBAHwj4emf8eXdpH4IihloJ+HeF4zl0aK3WMQaBgRC4RHHGB5qXO6w7rSyD10uCH76oRIJAnQQ+KGNh/jn3a8ykbhD4ltyMx87lf3TD9dZ4eXrCcEFrPMMRCLSTwEFyKz3vuP7MxN1cH34fMYFEtXQCJ0ljbu65zUtLkyBQFYGvSnE89zZPDKXb474ukyAAAQhAAAJ9I7CNAoo/777StwCJp3ICXuXns5J4HvmBOFLLCbDEYssHKHHvrUl9/6ReR9VvjvlGnZOfNrzu/0r8gUB9BL6YmHqn6vFvySSbqbaIQPzj78GtG0OBfCICP0p67ZjUqUIAAksS+Lyqfts4TY9OGp6X1F19VKaNJgiURWBNKdqrQNl5avf/2SQIVEVgjUjxlSpfHtVdPCupU4UABCAAAQj0nYBfBojTBXGFMgQmIHCz+pyR9IuX9k82UYUABGYh4IMqvgudnrxn0TnLPv7tJ/txruRusyhgHwjMSeBo7R8fC0+dUx+710PgX8m4eQzTfx7q8aS7VlaR676QFeb/DSpv1N1w8BwCtRD4tqyEYybk6cXg1TN93JcEgaoIvFqKw3xM80dWZRS9EBCBHSTxnMs9IPDgpE/c32USBCAAAQhAoG8EnqiA4s+7Jlbt6hvTIcazvoL2iyXxXOLB5iHOBGKujMCqyQHmg80XS+tOH5bBcKB/s27j2IOACOwmCXPQ+a8k8ZOwqpJaSCAes1A+toV+tt0lvxET+Dl/SNsdxj8INEzgANmPj5lQ3jjxK7TH+UpJH6oQKIPAslISz7O0XIYNdECgiMBh2hDPuZdmOi5M+sT9XSZBAAIQgAAE+kbAv/8af97xcx59G+H64jk4mUvH1GcaSxAYBgH/Xk98wr57A2H7QyL8qPPjGrCPSQiYwH9I4mPhOWBpNYGitzM8jqTpCOyq7vHcv0J1L9VFggAE8gQWqjk+ZkL52Un3ozL9fLyRIFA2gX2lMMzDNP9o2cbQB4GEwBdVj+fdgmS7q0X/t4X9MrvQBAEIQAACEOg0gePlfficc757p6PB+SYJeJUfL7cYzyd+i6zJEcF27wiclBxgTfwOmZ+mPmexHz9W7i9QJAjUTSBdHsY3j1et2wnsTUxgHfWM/zkI5adMrIGOMYF0yTh+KymmQxkCSxJYV9VwzonzY5fstsxmmX6fT/pQhUAZBP4uJfFcjMt3KcMAOiBQQMCrj8QXbLwEUFGK52VaLtqHdghAAAIQgEBXCZwux+PPu5W7Ggh+t4KAfwomnk++AUuCAARKIvAa6YkPsHeVpHcaNV6SKPZh+2l2pi8ESiTwCemK5+IzStSNqnIJ+OmreKxC+f7lmhmMtkMTnhervuJgoidQCExP4FrtEs47Ifdx46XuQnI5bAu59yNBoEwCd5WyML9yeZm20AWBlIBvwMbz7pNph6ge90vLUTeKEIAABCAAgV4QSD/rlutFVATRFIENZNi/GR/Pq3s35Qx2IdA3AndTQPHBdXZDAXpZIvvht3b86igJAk0Q2FlG4+PBZW4SNDES4216OdZ0rFz3m4Ck6Qn4Qv6NkpjpXtOrYQ8IDIbAexVpfLyE8loJgZ9l+iVdqEJgLgKj3h7jbeC50LLzBATSJcpH/e8QzpO5fAJTdIEABCAAAQh0ikD6edcp53G2lQTSB5tPa6WXOAWBDhJI14P3BdI7NBBH/ObOxxqwj0kImIBvEpwlif+ROdAbSK0j8DJ5FI9TKHvJVtJsBF6v3QJH51761scECQIQWJqAbzzEx0soL0q6vjnT785JH6oQmJXAttoxzL1c3sT/9LPGwn7dJHBeMgfvPiKMdKmpeM6O2I1NEIAABCAAgc4R8HKK8eecyyQIzEvAPzUSL23tebXPvErZHwIQuPXiZ/rFponXfg/SYIQPj6cxMBBokIA/XMJcdN7UTeMGEXTC9CnJOIUxa+L81QlgEzjptyUDx5DfY4L96AKBIRLwuSYcJ3GeLi92z0y/uw0RGDFXQiCee2n5yZVYRCkEbifg3x9L593tW5cuHZvpH/ZfujctEIAABCAAge4SWCjXw2ec8y90NxQ8bxmB9LfIvBIb18FaNki4000Cr5Xb8Yn7gAbCWDfy4ecqL9+AD5iEgAnkLnreFzStI3ChPIrPW6HcOkc75pAv7geWzr/aMf9xFwJ1ErhWxuLjJZRjH9I39d3nOXEHyhCYkcCjtV+Yc7mct8dmBMtuExNYqJ7x3DthzJ5PSfqHfS8bsx+bIQABCEAAAl0j4JWIwuec87d0LQD8bS2BNeRZPLdcfmxrvR2oY3wR6+bAr5C4vWlSr6PqG2Qhba8Cy3oFGuR1E/Dryk9PjL4uqVNtnsBmzbvQSw9ekUT1MNXXS9qoQgACtxL4TQGIDaN230RL0/ppA3UITEnA37mOH7HPftp2y4jtbIJAGQSelCj5dlJPq+enDYvrVxe00wwBCEAAAhDoKoFtEse/lNSpQmBWAtdox/R/sM+obe1ZFbIfBCBwKwFfaI7vPj+rITD+oh/8GLV+fUPuYXZABHzTOMzFkK86oPi7EGoYlzj/cxcc74CPvoAVc/1gB3zGRQg0QeBQGY2PlVB+SOLMn5J+X0y2U4XAtAQ+rh3CfMvl0+qjPwRmIXCVdorn33ZjlOyY9A/7suzUGHBshgAEIACBzhHwg3Thc8755p2LAIfbTCD38xhvb7PD+AaBLhDw21pXSsLJ+3KVm3iD61eRD0eqTIJAkwR8UyAcE85f1qQz2F6CQG4ZTI/RaUv0ojIrAb81Fs99l+M3YmbVy34Q6BuBtRRQeqy4/p0k0I8l/U5NtlOFwDQE/ERybt6FNq/EQIJAHQTCnAv5OJtF/7+NW5pxnF62QwACEIAABNpGIHw2hrxt/uFP9wncRyGE+RVyVlrq/rgSQYMEfDPMN8XCAXWFyk3cIHtk5IOfyiZBoEkCW8t4OCZC7iWNSM0TWF0uhDGJ83R5wOY97aYHuaeR3tPNUPAaApUTiM9BcTn+P+pweRFvu6RyrzDQVwIrJXMpnlcuf7OvgRNX6wgskEfx/PPDluOSz4vxPqF87Lgd2Q4BCEAAAhDoEIHcAyEdch9XO0TgPPka/p8KOdctWzCADEILBmEGF3wQvVxy4+J9XV+wuFxn5idiQzoqFMgh0BABv9GYpl3SBuqNEChawud/G/Gmf0ZvUEjPT8J6juprJm1UIQCBZZa5tADCwqjdX5LjtEpcoQyBKQh8ckxf//YYCQJ1EPj3xMjHk3qu6u+Yf8tsODfTRhMEIAABCECgqwTS3xv+alcDwe/WE3h4xsOnZ9poggAEJiTwIvXzl5Ygb5pwvzK7bRLZ92/g+ClZEgSaJPAsGQ/HhPP3N+kMtm8j4Isy8biE8oLbelCYl8CqGca8RTYvVfbvI4GDMseKz0mHRcHeOdMn2kwRAhMReKh6hc+7XM5DPBNhpFNJBL6RzMfdJ9R7RrKf5/ILJtyXbhCAAAQgAIEuEHi0nIz/VzuiC07jY2cJvCqZb55763Q2GhyHQMMEniz78Qn8dQ34c5fEhz0a8AGTEIgJbKBKfFy4HC+bFfelXB+Bj8hUOi6u81ZGuWPw3gxn5n+5jNHWfQKrZY6TcH4K0W2R6eM2EgQmJZCbQ2GeOX/zpIroB4GSCMTzz2X/JuMk6Xh1Svd95SQ70gcCEIAABCDQEQIfkJ/xZ128WlZHQsDNDhHILcH+mw75j6sQaBWB9ID6hbyr+0KolyD6oSR8kOzQKkI4M1QCYT6GfPuhgmhR3GfLlzAecd4iF3vhynoZzo/rRWQEAYFyCcTnobgcrORubnCDLNAhH0dgBXWI51Va5gvwOIJsL5uAl45K5+GkNh6W7Huz6ltNujP9IAABCEAAAh0g8Fv5GH9OpsutdyAEXOwYgV2TOef594yOxYC7EGgFgdwT0H6jq+50ugyGD5Jj6jaOPQhkCLxCbWFOOucp1wykmpvi8YjLNbsxCHN/UZQxY5f5B38QQ0+QUxD4rPqmx4nr8YM+50R9rld5IwkJApMQ+JQ65eZXaPMNNBIE6iTg37sI88+5z2+TpnTZKe/vNhIEIAABCECgDwT8XTn+jHSZBIE6CLxRRtK5t7AOw9iAQN8IXKCA4oNpwwYCPDjy4b0N2MckBFICO6khPi74ByclVH89HQ/X/1i/G4OwuJ2iTHnzFtkghp4gpyCwZ+Y48XFz0mIdfiP/mqSPf/uVBIFxBF6oDuk5OK4vGKeA7RCogMD3pTOeh0+YwgY3yKaARVcIQAACEOgcgbXlcfwZ+eHORYDDXSWQuznrubh8VwPCbwg0ReA9MhyfyP3mTN0pvhBwXd3GsQeBDIE7qC0+LviAyUCquSkdD9ePq9mHIZm7SsGmzIcUP7FCYBwBf+lIj5FQD/telvR5cthADoECArurPcyjXO4HeEgQaIJAOh83ncKJNdU33X+zKfanKwQgAAEIQKDNBPzQSPw599A2O4tvvSPg/6ni+efyJ3oXZQcC8oVkUncJXJ24fvekXkf105GRlVVePapThEATBG6R0QsSw9NcCEh2pTonAS8Hm0te4oxUDYHDMmp3zLTRBIGhErhJgf+rIPg1FrdfnmzfJKlThUBMYGtVfhA3JOUHq35W0kYVAnUQ8JPxabo4bRhRz93YfdSI/myCAAQgAAEIdInA/RJnz03qVCFQJYGLpPyQxMCTVD8oaaMKAQiMIODfyojvNE/zZWeE2qk2pa8jbzHV3nSGQDUE3iK18bFxVDVm0DoBgZ2TsQjjsuUE+9JlNgK5V/VvnE0Ve0GgtwTS36sM5yZ/IXE6UxLanH/djSQIZAj4QZCbJfF8icv7ZPahCQJ1EdhPhuL5+I0pDe+S7G9d/Ij8lBDpDgEIQAACrSXwK3kWf0621lEc6zUBf9eM56HL2/Y6YoKDQIkEdpOu9ABq4q3AGyI/nlhifKiCwKwE7qkd42PjK7MqYr+5CTw+GYswLk2cq+YOpkMKnprhfucO+Y+rEKiawDoyEM5Hcf6txYa/kGw/r2qH0N9JAsvK6+9I4jkUlw/vZFQ43ScC6YW/50wZ3ErqH89plx86pQ66QwACEIAABNpIIF12PV4hq43+4lN/CaRzMfzvxSpt/R1zIiuRQO4AamKZxRMVUzh4uRBQ4gCjamYC/hAJczLkMytjx7kIfCwzFh4TUrUEcr/Fd1y1JtEOgc4RCJ8Pae5APiyJ2/+3c9HhcB0EnpnMk3jONPHbwHXEjI1uEYjnpMtrTen+ruqf6jhmSh10hwAEIAABCLSRgJfAjj/j9m+jk/g0GAIbJPPRc/NkiR/II0EAAmMI/F3b4xP6YWP6V7H5I5EPZ1VhAJ0QmIFAfFy4TGqGwPkym47FVc24MjirX86wz/0WyeDAEDAEFhM4QXl6fnJ9VcmbMtvURILAbQSeqlJu/rjNS3XyZfY2VBQaIuAHJ+M56u+N06b1tEOsw+VXT6uE/hCAAAQgAIEWEnicfIo/4/wzNiQINEngATIez0n+72pyNLDdKQJ/SA6eDzbgvX9bIT6AWTqtgUHA5FIErkvm5YZL9aChDgLxuSGU/WYGqXoCuSeQ3li9WSz0iMCKiuUQyRmL5WDlbutL2kaBhPNSnD9M7S/PbPPv+5EgYAILJfGcictvdwcSBFpA4OPyIZ6b753Bp9wSi2+dQQ+7QAACEIAABNpGIF4mm9/sbtvoDNefVyn0+P83lxcNFweRQ2AyAu9Rt/jAaeKkvmfig5d+JEGgaQK+QBUfG/dt2qGB2o/HIJT3HSiLJsL+gowG7iFfoQlHsNkpAqvJ20dLwpyJ877dZI1jC+WTFXtu6TweABIY0jKbicG1kjBf4vylauf/YCZJWwjcnMzTBTM4tjDR4fn+xRn0sAsEIAABCECgbQS8sk34P+6ktjk3UH+2U9y+zv0CiX8zeqjpmwo8zM2QsxrQUGcDcU9E4MDMQVP3BZyVEx/uPZHndIJAtQTSpY+eV605tGcI+G2L8GEe5+tm+tJUDYHNM2NwaDWm0NoDAr4xlvu/Ij5+rwNCEQ8AAEAASURBVOhBnHEI56gSx+fy1ZLHZ9o3Uhtp2AT8BuVHJemccd0PJJAg0BYCm8qReJ5eOaNjyyZ6rJMbZDPCZDcIQAACEGgNgXQliUWt8Wy4juyo0G+ShP9ffqbyUFfw8Bv86YNOF6jN7SQIQCBDwG/FhJNHyNfK9KuyKb0I/oAqjaEbAhMSSP/hOW7C/ehWHoHc71b4POWLLaT6CPxVpsLng/NL6zONpY4QWF1+5t6YiudNKPftBtkTFXuILc73y7Sv35HxxM1qCPjt2x9L4nkSyq9Re90PqFUTJVr7QuDNCiTMT+dHzxhY+iCkdX1vRl3sBgEIDJuAf/LgMMmpkp9I/P38wZLlJSQI1E3gSBn0Z1qQe9btAPaWIpCuAuWxucdSvYbTcDeFGuZnyD+nNs6Zw5kDRDoFAX9ZDwdKyB82xf5ldf1d5McHylKKHgjMQcCvY4djwvnJc+hi19kIPFC7xWMQyrNpY69ZCeyVGYedZ1XGfr0isL2i8ZNo4dicJO/bEou+OZiL+/BMO2/IC8qA09MUe26u/I/ah/p064CnQ6tDz30/XDijx77xm857f26QIAABCExKYFV1fJYkPZeE+i+17Y6TKqMfBEoi8HTpCXPwYpX9QAipOQIby3QYj5D77XevcDLktLuCDzxCfvCQgRA7BEYRCAdJyN81qnNF246X3mD/pIpsoBYC0xDIfaGfZn/6zk/gKVIRzgsh//r8atEwJYHcsfC9KXXQvT8E/AbnQZJwTE6TH6z9vMRc39KFCijl8JZM2w59C5x4Jibgh7/SOeL6MyS8FT0xRjrWRCBdYeTyOe2mc/93c+pjdwhAYDgE/FZOeg7J1U8bDhIibQGBVeTDXyRhLr6oBT4N3YU3ROMRxuWxQ4eyOP4DMmz2hw0EILA0gXDyCPkflu5SeUv6RBAXCypHjoEJCPhJoHBcOGdeTgCtxC4fl66Yv8t+UotUP4FDZDIdi03qdwOLDRLw03dHS9J5MEn9zQ36XYfpt2W4nJpp44tIHaPRPhsPzswFHzc/lvhNHRIE2kbgs3IoPrcfPKeDsS6Xr5lTH7tDAAL9J+DPx09K0vPHqPq+/cdChC0hsFEyN1/bEr+G6oZ/Vyt3blg4VCCZuF+ZYbRmph9NEBg0gbMUfXoyqRvIExIf/MYCCQJNEzhRDsTHBq/N1zsi3034eyy89jypfgJe/is+Flx+U/1uYLEBAl7W5ihJOv6T1L3kjZe76HvaWwGmPG7JtD287yCIbykCR2TmgefKJyR9fJtyKQA0dJJAej6b93tZqs91EgQgAIEiAv7e4aXRcueOUW3nFymkHQIlE7iH9IW5+GeV71yyftRNR+A56h7GI+RnTqdiEL2/knC6QHXfXCRBAAKLCbxYeTiJhLzuH+3zD9cH287vtNg3Mgg0ScDLjcbzco8mnRmg7Zh9KPMB3txESG+S3ChXuGnc3HjUYflRMnK9JBx/k+ZXa5+71+FgS2wUPbWY8npSS/zFjXoI7C4z6Rxw/Y+SdepxASsQmJrAv2uPeN5+aGoNS+/w90Sn9ZMgAAEI5Aj4u0V8Dpq2vEdOKW0QKJlA/CC1y6RmCeTOE/s161Irra8lr66QxLxeovq8D0K1MlicgsAsBPbRTvEB4vJusyiaYx8/RRv7sO0cutgVAmUReIgUxfPSTwqR6iGwrMzE7EO5HutYyRHwm0RhHEK+V64jbZ0ncG9FEH/xC+M9Lv+n9tu+89HPFsDp2m0cn0NnU81eHSTwtIL5cLna1+tgPLg8HAJnKNT4XOaLKfOmWF8oz6uT/SEAgX4SOElhhfPELLnfiGD54n7OjTZFFX9P4gZZsyOTW8nD5441mnWrtda3k2c3SeLz6/Na6y2OQaBmAl53ND44XH56zT7YXOzDEQ3YxyQEUgKL1BDPy9ekHahXRiB3g+xTlVlD8aQEjlfH+Jj4yaQ70q8TBHwT9L2SeIwnLf9bJyKszsmXTcDt4OrMo7lFBHIPnvk48g3kLVvkJ65AICWwtRric/7PVPf/Y/Om30pBrNdlL6FGggAEIBATeJwq6bliljoP8MVUKZdNYIEU/lTimwxeTp6HqAWhweSb4ul54tgG/emC6U0zzPgpky6MHD7WQiA9oTSxfvO50UH6/lqixggERhPYSJvjY8PLkZLqIeCLiDF7l59Yj2msjCDgJ47SceHprBHAOrTJSyKmYztJ3Z/Xfgt86MnHwTheBw8d0gDif/yIecDy4QOYAB0P0Q8ixeexsm7oxjpDuYwbbx3HjfsQgEBEwP9LhvPDJPlTR/S/WNtWj3RThECZBPw73PEcXVCmcnRNReAuyViEcdl1Ki3D7PzuhN3fVGeVi2HOBaJOCIQTSZwnXSqvxgfo6ZVbwwAEJiMQHxNfnmwXepVAwE/+xexd3rsEvaiYj4DXpz5HEo/NcfOpZO8WEDgoGdN4fEeVWQ759sFbRcV0uYqUnX/bh9RfAq9UaOmYh/p9+xs2kfWEgN/o+rMkzNlrVC7rd0b9pH3QG/IN1EaCAAQgEAh8WIVwfhiVv179Vlgsfqi7qO8btY0EgSoIHCmlYd79Q2WvyEVqhoCvQ4SxiPNmvOmWVT+odHTC73ndCgFvIVANgS9KbXxCcXn5akwVan114kNhRzZAoEYCv5etcGz8oEa7QzeVewp/paFDaUn8D5Uf4ZgIeUtcw40ZCLwrM55hXIty3yRdewZbfd/lY2NYeuk9Uv8I+MGBwyRFxws3Avo35n2M6KhkDj+ixCAvTXT7WOHN4xIBowoCHSfgG/RFn6Fx+6Ikzu1Vv3bEvhsn/alCYF4CfjPxL5IwL18+r0L2n5mA//8O4xDnfmCNNBkBvzH2J0nM7x2T7UovCPSXwFMUWnxQuLxZzeFulfjgEx4JAk0TiJ9mu0XOMC/rGZFjZCY+J11Vj1msTEBgNfW5TBKPzwsn2I8u7SPg5RHjcRxXvln9Pda+kEFamsDD1TSK4V5L70JLxwn4wY0vSYrG/V4djw/3h0PAD4HF83jdEkM/MdFtO3crUT+qIACBbhN4tNyPzz+58oMKQnzfiH3PLdiHZgjMSsAr2sTzk5sJs5Kcfz8/eBiPRSjfcX7Vg9KwpqL9TcTyRpX5rj+oKUCwKQGfRMIJJeTPTjtVXPcXsWDbOetGVwwc9RMR+LR6xfNyi4n2otO8BL6ScD9uXoXsXyqBA5Lx8ZuWpG4RSMcwPs8VlR/VrRBr9zb3dmXMkvXwax+SSg2uKu1XSuIxjsvcAKgUP8pLJLB7Mo/9P1iZ6cdSFh8bLq9XpgF0QQACnSZwkrxPzxFx3asdFaU7a0PcNy3fo2hH2iEwA4EHap94ji2aQQe7lEPgQqmJxyKUY+3LqrKWZEvJbpL9JAdKniTx0vcPk3hM/bKGr4kP9caQWQR+f1T54xKuewoCaZgEcq+nnlYzipVlLxyUzv0kEQkCTRN4jByI5+UKTTs0EPsXJNyfO5C4uxLmpnLUbxPFx4bbSN0g4OUR47GbpHzvboTWqJcrjuHKUj+NDk+pxu80Zqy9nQSBrhA4W47GnwPLl+y4H3KK9bu8U8k2UAcBCHSXwFVyPT1HxPVxF639PTHun5a7SwbP20bgh8lca5t/Q/Fnw2QcwjHvN0rfLPl+wfbQb1zum0RfkzxfsqdkG4lvtvU1OTY/LHWmJLA5oa/BEhcEJiFwvTqFgyHkk+xXVh8flDdEPjyyLMXogcAcBDbTvuF4cM4bFHPAnGLXeG1vc/fTPqR2EXia3ImPjVPb5R7ejCDwnWTs4nFMy5eoL7//NwJmsumUEWx5Ei+B1dHqPiPG2McPDwt0dGAH6rYfkjxfEs79vllWdvq0FAb9Id+2bCPogwAEOklgB3kdzgu5/JkTROUbaLl9Q5vfMiNBoAwCYU45v7gMheiYmoCvG58kiceirvIZsnusxL89d1eJ/+fv0wP0vikWs3yA6uZNgsDgCLxXEccHg8t1L3P4g8iH9wxuBAi4jQTuG81JHxP+/R1StQS8DnJ6Lhr35GC1HqE9R2DnZJxuynWirXUENkrGLT3W4vq71ddvRZEmJ5B7UyIwXX5yNfRsKYGj5VcYzzT3m89+O5MEgS4ROF7Oei7fIjlX4ieIy07+jZb0eFlUthH0QQACnSRwlLxOzw+h7t88nvTis99KDful+ac6SQan20bgPskce13bHOypP35bzOIXKPxWl/9fSY/xJuvXyp8vSD4guadkS8kWki4m+/0JScxz/y4Ggs8QmJeAf/g0PhBc9gXQOtM7ZSz48M06DWMLAgUEfGPmvyX+IP6r5IESUrUEfHEmnAecX1+tObTPSMAX+38iicdqkqc8ZzTHbiUR+FgyZvH4xeU9S7I3NDW7jODLzcbuzoZV5LqfFI6Pkbh8SndDw/MBE0iXKPpGRSzeKL3x8eKyf/eDBAEIQCA9N8T1t02JJ943LvNdckqQdM8SOFKt8bx6abYXjfMS8DWGfSV+MN03t30drm03xeJ5UFT+lvz2jbO3Srz6hH/na6HE3yna/PD3avIv/imNa1T3/4skCAyKgC/cpAf3UTUTeGzkw//WbBtzECgicJo2hGPDZVK1BNaX+sDb+XHVmkP7HATW1b7xWP1TdZbjmwNoxbuuIP2+0R+PWa68UcV+9Fn9biP49jnuPseWvkmeHjP+vQMvU0eCQNcIeOmceD6/qqIAXpbYsc0DKrKFWghAoDsE1pGr8TkoLXv5xWnSgeqc6gh1X5QmQWAeAj/VzmE+Od9sHmXsexuBVVXyb10/WxJfd4tZT1v2yxZeIe0pkodL7iG5i8TXmXwDzjeBvGqRbW8uuZdkP8lzJb4xf6bkD5Jp7U7T/yLp93WuIyT2c1tJW+bUa+RLHIt95UFPQSANi8AfFW58ILhcZ/Jrs7H9les0ji0IFBCIP6i5QVYAqcTmF0lXfB54Yom6UVUuAd8M802xMF7/Utk3zUjtJOCHXsJY5fKrtd1fFEizE/AFmBxbt5G6RcBfoD8sKRpPtz+iWyHhLQRuI+DlQOPP7x+r7ocoqki+6JUeR8+owhA6IQCBThHYW96m54a4Pm0w/tyO94/LfnuDBIFZCfjzMZ5PLpPmI7Crdj9BknKdpe7r2AslVVw/XiC9vsF2iORdkm9I4v+fZvF33D5/ko0fSp4lWSRp4ga/H5qK/fRy2U34IbMkCDRD4HiZjQ8Cl6v6spSLcIPE/lq5TrRBoGYC8T/v58l2m1+JrhlNJeb+Q1rj85AvrJDaS8DLKvrGWBizX6jME0btGy8/KRfGKJd/m3ErbdD8Oz45xqUZQFHlBLyUSG4M47ZNK/cCAxCojkD6tquXua8qPU6K42PHZS+dRIIABIZN4N0KPz03hPqpM6JJ3/IJ+o6eUR+7QcAEtpaEueT8QjeSpiJwB/X2/x7+zhmznKTsJRaPkZxWsK//z6g7+UGjB0l2kfgh1M9ILpKEeOJlCkPbvPl/Sb/fNKsjeUWZ9Dvtq+swjA0ItIVA+gaXD2C/ilpXWk+G4pPGw+oyjB0IjCDwHG2L5+WiEX3ZND+Bx0pFeCrnfJX9zwep3QSukXscI+0dI98c87EUj1Eo+wvHayXc+BeEkpKX3At8Q/7rknSjpnoCD86MXxhH52dKfEyRINBVAn7C+iJJPK+3qDAYL28U23L59RXaQzUEINANAtfLzfTcEOqvmzGERxfoPGtGfewGARN4kyTMTed+m4Y0GYFl1W0vScxvkvJJ2ucxEj+0ZvF31aL9lte2tqQt5Yj/p9pB8n7JJyV/khT5Pmv756XzrpIqk5nfIIl99LVREgQGQcAnlnjyu+xXK+tKPnmeIQk+3K8uw9iBwAgCXo84zEnn/sAjVUfgV1IdeLtMaj8BLwEQxsx5nZ8b7afTvIevTMYnHqs3Nu9e7zzI3WC5tHdR9i+glRTS8ZL4+EjLT9Z2/69KgkCXCewu5+O5fUzFweyb2LPtt1VsE/UQgEC7CeSuO8XnpfvM6P4K2i/WE8pe7cI2SRCYhUB6g8P/65NGE/D/y0+ThGNwXH6x+r5Zspckd6w+o0CXl0NvezIL3+TzimlPkbxE8jHJOCaTbPd3zC0lVaXcQ047VmUMvRBoG4Gfy6H4QKz7aZsfR/bf0jY4+DNIAn4dPD4m/OFMqo4AN8iqY1uVZv9TFh8jLt+rKmPonYqALzCkYxPqX9C2FabSRudJCGynToFxyP88yY70aYzAZpkxC2MX8o0a8w7DECiPgP+n9VuQYV47XySpMm0j5bE9lz9dpUF0QwACrSewkzxMzwtxfdbl2n1h3TfDYl0u3yjJXXRXMwkCIwn45kY6nzYeuQcb/aJDyqyo/iT19c0jcx6Viva/06idOrDN5zrHv6fkZZJPSYpiHdX+Te13d0kV6XlSmtrevApD6IRA2wgcJYfSyb9KjU4+ObL/hhrtYgoCRQTW1Yb4mPhaUUfa5yawkjRcIgm8vewrqRsE/NRXGDfnvEXW/Lj5i8bfk3EJY3SD2rv+haJ5wnkPzD1wDvl1+a60toBAbnnxMG7Oj5Z4TEkQ6AOB9GbV92sIKvfQgN/WJEEAAsMl8EqFHn/WpuV5yHw5o/tmtS2cRyn7DpZA+rnpueqHTUhLE/BPY5wtSY/ntO7rafdYevfCllE31At36vgG39D33Hud5DJJyrCo/l71XU1SZvJ8/4wktXnnMo2gCwJtJJC7UFDnU7OvFZRw4P2sjYDwaZAEfh/Ny1MHSaCeoB8dcfZ54LB6zGKlBAK+IRbO3SFfWIJeVMxO4APaNYxFmr9odrXsOYaAv9CkvF13O6k9BPzwl99iyY1VaKtyyZL2kMCTIRH4SjLnH1dD8JslNn18faMGu5iAAATaS8AXyMNnbZpfMqfbue8ktvHEOfWy+zAJvF1hx3PUK16Rliawq5piTrnyQeozy+olOV1u22NpN3rb4gfJHyw5XVLEI24/WP3KTL7pdqkktuHyJmUaQRcE2kbAFwzSSV/nhbS7RPbPVXmWE2jbmOJP9wkcpxDCceFlG1btfkitjGCfiLN580WmlcOUdcpvWIRjJOSvz/aksQ4Co76k/KgOBwZuIxwDcX6/gTNpU/h3lDPx2KTlF2s7Twe3acTwpQwCa0pJPNevKUPpBDpWT+zaBy/pT4IABIZLID4XpeWXzonlIdo/1en6M+fUy+7DJOBrkvF8OmqYGAqjXllb/DtgMaO0/E5tn/WtpvuP0K1Ng0x+U+8tkpRzWj9RfbYokZCvgd6csctNshIho6p9BH6QTPo6lt8IFHZPbG8aNpBDoEEC6QfQig360mfTL1Bw8Qe7n5QhdYdA7tV7/xgtqV4CuYuR8XHl5a5I1RFYQ6pj3qF8RHUm0TwFAf8+YhiTXL7NFLroCoEuEXifnI3nvP/nqiOlN+bsgy84kiAAgeESiM9FaXnfObHkzjm24e/zJAhMQ8APS6Xz0w/0km4l4OX6Uz5x/bvavtYcsHIP4Ab9D5tDb192NZ+HSgKTonw/9SnrxZP1C+z5RRcSBHpJ4OWKKj24lq8pUtvx0+3Bvp/yJUGgaQL3lgNhTjp/UNMO9dT+eRHnW1T2hX5Sdwj4H+D4OHH5Zd1xvzeevj8zDmFcXtibKNsbiNdjD7zjnAvCzY/ZIQVj43H6lGTWp1ubjwwPIDCaQO7BibrekvR3u/hc6PL/jnaXrRCAQI8JjLro7fPDvNd/cjc1rNcPgZMgMA2BXdQ5/fziQelbCe6VYROz8ptf86b9pSDWGZfn1d2n/f0W32EjWJnbcSUG7Jth8ViE8oISbaAKAq0h4AMsTPKQH1Cjd1dG9ut6urHG8DDVQQJ7R3PSxwTzsppB9JI74Zzjm2X+AkXqFoH4AYcwln6jhlQPgXvKTOCey8t6eqyeaLppZdSFn25G1A+v36YwcseE2xb1I0SigEAhgddqSzz/31DYs5oNsW2Xr67GzFxafVF9W4mXhz5Jkvr8TbW9V/JwCTfTBYEEgRkJeJmu9PiK6zOqXWK3WF8of3uJHlQgMJ7A69QlzJ+Qj9+r/z3emuES+Hxa2+Z5ayzQyz1cE2wcGDqRL0HAb/SdIgmc0vwcbXvAEnvMXvGKNKl+1zefXSV7QqCdBJaTW9dJ4gn/3BpdfX5ke6ca7WIKAkUEfFE5Ph4+UdSR9pkJbJQwPnpmTezYJIE9knH0cfO8Jh0akO30PBWfs1zebEAsmgx11BJ+/v+KVC8B36BPl5YLx8a12ragXnewBoHaCawji2HOh9wXqOtMwW7I23KDzG/W+SFQv+EbfJskv0b9vyF5iMQPRZAgAIHJCeTOSfFxN7mm4p6xvlD+TXF3tkAgSyDMnZD/INtrOI0LFeqXJYFHmpd548oPq6T6Q53PXcEZkR6lbYFVLvdNsjIemi36zfMtR/jGJgh0ksA75XV8MPmpubrS22Uo2P5qXUaxA4ExBP6l7WFe/nFMXzZPT2DPiK85f2R6FezRAgJ+2usqSThWnN8kYTkKQag4+aZyzD0uczxVDD9Sf68R4+ClWkj1EVhFps6UxMdCKL9a7fzOZX1jgaXmCKQXmU5owJVw3IXcD2I2kfyW2NaSfSRfkgR/5s2fJl0+35AgAIHxBDZUl1HH3HgN43vk9H9t/G70gMBtBHIPHvrGwxCTb0jllpsMx5mvjfmztayU+9mGYOseZRnpuR4/iOAbuoFbmn9f23zdZt50XylIdbu+cF7F7A+BNhHwCS6d6HeryUE/jRds86P2NUHHzFgCV0bz0vOzjKcuxhodUIe9E767DSj2voX6kmQsfbwc1rcgWxbPJhnm4XPUuS8Kkuoh4As/8QMV8TgcXo8LWBGBdSW/l8T8Q/lJEILAQAjkljLz50XdKRx7cV6XD/5dSL/J/m7J3yWxD2WXt5R+EgQgMJrA5to86tgbvfdkW3P6PzrZrvSCwP8RuKf+pvNo44Gy8WdoyiLU/dCNb6CVmc6VsqA/znkLdDrKHpcDClia67ck95HMm+4nBfE4hbKPIRIEekHAN8PCxA55XXfr149s/0TlMu5s92JQCKJRAv8l6+FYcO4lAUnlEfi8VMV8/RYGqZsEip766mY03fA6PnbSMksV1zuGz5W5dAxC/Vf1ujJYa5sq8ssz43CT2ryNBIGhEPhPBRrOP85PbCjw2IdQrsKVDaTUF4N8Hv6K5DyJ31YLNuvI95A9EgQgUEyg6HtCOD6L95x8S9AV5zysNzk/et66jG48f1weWvJDH5+QpBxC/THaVvbNsV1H2PPDb6TpCfjll59Jwril+eHaNu/DtL7Rlup13W+YkSDQCwJfUhTxJD+hpqi2i+zeoDJL4NQEHjMjCTxfW+Pj4f4je7NxWgKnJ3zXnlYB/VtF4H3JePrYObBVHvbHmUdlWIdz1Tn9CbMzkTxxxHh4XEjVElhR6n8nCcdAyP+gtjtKSBAYCoFVFGiY/yHfoqHgg/04L8MV3/D2zbDPSWLd85a/KX1e8v9IyVslJ0mm0VnXQ6VyiwSBzhFo6gbZvp0jhcNNEkjP+T9t0pmabfuml6/JniVJObjulTLuLik7rSmFOXtu87U40uwE/NKJl1Us4nu2tm04u/r/23PHAv1cA5oTLLu3g8DRmQnut7uqTj4h+8uID94fSvxPFAkCTRPYXw7EHygs/1neiPiCZvyE7+/LU42mhghsLLvx8RLKZT9l1lB4rTHrp70C21y+Wms8HY4jh44ZE46B6ubCzlL96wz//1Ab/0tWxx3N7STwDrkVfy40ubxY7Ecoz0LNN7kfKfEN76CnjPwT0rePZNzT6X5466GSv0tG2f2jtpMgAIFiAqOOn+K9Jtuykrrl9PviOwkCkxBYT53SOfSkSXbsQR9/T/liJv7A40PaVtX/1K8usHuB2vn+JAhzJt8k882qWyRhPNN8+zlt3K1At7+jkSDQaQLPlPfpAbNVTRFdEtn2K58kCDRNwF/K4+Ph40071CP7KydsT+xRbEMO5QvJuPr48VIMpPIIvEGq4vNSXH5GeWbQNAWBj40YE4+PfzSZVA2BX0htfAy47GOEBIGhEfCbVemx0OS558qMP5OOyWbqeFhm/zS+SevXStenJX6YwUs5+YLRLOnftNMomw+fRSn7QGAgBEYdO/MiWEMKcvr9Vi0JApMQ8INV6RwawvzxW2G+DpPG7vrNkl0kVSXfmMnZddu8N22q8rmrel8ygrV5P1Uyzw3JuxTo30vtJAh0lkDuh52/VlM0r5CdcIL0iZoEgaYJ5Jaqadqnvth/kAIJx7vzF/UlsIHHcddkXMMYz/MP18CRLhF+emM58A35Ep2p1Ebgg7IUxiCXsxZ7+UOxu1SeluFu1nco3xwaIdB6Ar+Th/H558sNe3xF4o99G5X8JtfLJHEMs5Yduy8GPU9yZ0mZySurFPnlm4IkCEAgT6DouHH7vGlrKcjpn1cv+w+HwO8UajqH+h79IzIxBwbHaNs2FQLw/+q/LLD/5grtDln1qBuSHvdPzQnHDyCF+RPnvvlGgkBnCfxRnscT2uU60k4yEuz6CQ4SBNpAIMzJkLfBpz748BoFEZg6f3ofgiKG/yPgNcrjsXX50bAphYC/MKRsQ32LUiygZBYCnx8xLh6fl8+ilH1GEvihtoa579wXpp88cg82QqC/BHZTaPHx4HJVyyFNSvG7GZ/SfX2z6QDJf2f6pvEU1a/Rvv8jebzES2RZqk57yECRP75QT4IABJYmUHTMuH3e9EgpSPX74jsJApMQWF2d0vnztkl27Gif5eT3VzIxBwYnaFvVD7eOujnX9P8vHR3Widy+z4hx9/h/U7LmRJrynXw94npJmEsh3zHfnVYItJ/AsXIxTOSQ712D2/7B5WDvezXYwwQEJiEQ5mTI/Q8FaX4C35CKwNR5HRc05vcaDZMQ8Jsd8di6zFPVk5Ab3cdLZaVcQ903aEjNEThbpsNY5HJ/2SCVQ8APU/nz46+SwPoylf12JQkCQyTgi1jhWAi5v1M1nXzeC/6E3D75wstDJOMeLAj7pPk/te8nJX5b1Bc1m0qpX6H+vqYcwi4EWk7g5/IvHCdxfmMJfm+X0f2hEvSiYhgEvJJNPCdd3qanoXu1l4sy8Yb4/ZZR1TfHFo2wv622kaolsIPUh/HO5f/Q9jXmcGFhgf5XzqGTXSHQGIH9ZTk9UHwxourkC+RnSWy7DV/sqo4X/d0gcL7cjI+HeZ6o6EbE9XgZM3V5tXrMYqUmAun4uu4vr6TZCZyoXXNc3bbq7GrZswQCv5SOorFxu5+kI5VD4HSpCaz/pvLJkj0lJAgMlUDuB+6XbwGMD8uHcKyG/Clq84WXUJ80/4D28dLcq0jako6SI0X+s8xrW0YJP9pEYNSbovP6ma5M4mPz6HmVsv9gCPxCkabn86pvEjUB12/3pHGGut/6ruOmoB9oO7XAj2PUTqqHwKi5EObEPNfn/D/bdZKgy/kNkrKXvZZKEgSqJbCV1McTOZR9Mqsy+cvEhRLb85cnXq0VBFLjBH4kD8Ix4JynWuYfEh/bMVOXSf0icKDCScfYP/RLmo3AqLfHXjubSvYqkcC10pXO97ReorlBqtpJUacX13yzjASBIRO4m4JPzzU7twTIOzK+pb6Oqvtm2mYtiSXnxsYj4luU24E2CAycwMsVf+6Y/30JXHI3yNxGgsA4AmurQzovPzRupw5uv2cmzhD3Z2qKxw/vxA+6BfvOz63JB8zcTmBXFeMxyJXnuUnmFwtSnb5J9orbXaAEgW4QSCey636zrMrkE+ZfJLblC6kbSkgQaJrAJ+RAfDxwg2z+Ebl3wvT4+VWioWUE/NRdfNyE8gYt87Mr7pxcwNNceVK9+VEM83tUXvVDRs1TqM4Dn0/SZSy/qTbfNCNBYKgEfO7/syQ+77y9BTB84+hZkr8nvsV+5spefs03xbr0dHEuDrcdJSFBAAJLEvCyqEXHzJI9p68dnui+RfU63oaZ3lP2aBuBI+VQOi/9dk2f0i4KJo0x1F+sbXV9l3xZgR8+XhdJSPUT8ENVYS4U5fO8vf8Y6f9DYsPX+n1jmgSBzhA4Tp6mB4i/uFSd9pEBv7HzUck8d6ur9hP9wyHwVoUaHwsHDif0yiJ9TsL0sMosobhJAu9OxtnH0fubdKijtlfKcAznpAd2NKa+uR3GY1TOF4HZRt1PN54nidmeMpsq9oJArwj4olZ8XLjshw2bSveT4W9JUp9G1a9W/xdKNpF0MX1aTufi+73aV+xiQPgMgQoJFF2I/XUJNr8vHemxeFAJelHRfwJerjudO32KekEmvhDvA2oM1DdKgt00f1KNfmBqaQIPHzE2HqsfS/yw4qzJ34FvksTj7ge8Hj+rQvaDQN0EHiWD8QQO5aqfLvDrlsGWyyQINE3gtXIgzEnn3CCbf0TOTJj6xjipfwRyS2n6GFqhf6FWGtG7pD0+B8XlSg2jfGIC8ZgUlf1/FWk6An4TJeX5XbX5IhsJAkMmkLvQvEPNQHyx5J4S/z5YepyOqvvm0b9LHEPV3ytlotJ0gLQXxeq3ZUgQgMDtBPx787nj5Ve3d5m5dFlG96KZtbHjUAgsUKDpnHxbj4LPLXEX4vVDLXWldWUo2E1zH7vzvKFUVwx9t1P0dl8Yr/fOCaBoiV1/1yNBoPUE/CRfOBjivOoTKTfIWj81Budg+mHBkw7zT4Ebk/MLN0zmZ9pWDd9LxtqfJ49uq7Mt9Gu5DL/wmdy35T9aiH9il8KYjMr95ixpcgKbqet1kpjpBarP8wTj5NbpCYH2EvCbSfFx4fJbanTXy8U+IeND6lNa/5328dPqfiu6L8k3wdI4Q/3VfQmSOCBQIoFwfMR5GasUpd8trX/DEv1GVT8JHKOw4rnYt3lzRiY+x/jQGodzVdm6qcAP+7JHjb5gajQBr+TmMSmSh4zefezWzQt0z6t3rGE6QKAMArkD4/wyFI/QsZq2/VZi27xqOwIUm2oj4C+48bHw1Nos99NQbrm4fkZKVCaQe8r9BtBMTOAo9YzPP6H8uYk10LEOAmFcRuUfqcORnti4l+JIWfri1/Y9iY8wIDAPgQ9q5/j4uHgeZVPsu7X6npTYjv0YV75mCltd6Zq7WRk4nNuVIPATAjUS8HkgHCMh/04J9oOuOL9PCXpR0V8CvnETzxeXvVRnX9KTFUgan+uvrzFAf0beXOCHfTm2Rl8wNZ7AcuqSmzNx27wPHqT/wwbddx7vHj0g0CyBj8l8mLBx7ptYVaXNpTjY+ofKPqmSINAkgaNlPMxJ53U+cdNk3FXZ9tPDMc9fV2UIva0hEI93KK/eGu/a64iXngq80nyD9ro9SM/S8XH9gmT8qn7AqC/g/QUp5ekLanfqS4DEAYE5COyrfdPj4y5z6Jtk11FvSaW+uH6a5BDJwZJ4+09V72M6XUHFccZlX2wiQQACtxP4iorxMeLyW27fPHMp1el6ldesZnaUHVtD4HHyJJ03D26Nd/M5sjATm2O9fj61U+3tFR++IUkZx3X+t58KaS2d7zhmzDx+8yTPi1dK4nkQytwkm4cs+1ZOYP+Cifv8Ci2vId1XLrZ7tXIfQCQINEngEzIeTtrOeQV4vtF4XsLTb+iR+k3gMIUXH0Muv6DfIZcS3ZEZbmb3olK0o6RMAun8dv37krj9n2Ua7KmujRNmgR9fmHo64IQ1FYHc20pVrWrgC8uvkoRjcJL8SPWPj9X0Issfp4q2O529fG4Rn927EwaeQqAWAsfLSnq8fGZOy+tkdNrGlnPqZfd+E/iVwovnot90Wr4HIfv66U+S2EKca9cUnx/yPKHAh+DLQ2vyBTPTE0iv14UxC7mv7cyT/PMqx0mCvjhfOI9i9oVAlQT8hH88WUP5z1Uale74H6ftKraFegiMI/AldQhz3/ku43Zg+0gCv9PWmCc3HEfi6sXG3BIWngOkYgL+cuMbKvGxEsrmSWoXgTA2cf4tuRjXXSYVE7ibNqW8XOczt5gZW4ZDYE2FepYkPkY+UEH4flDxWYmd2Gau/DT1Xy3ji5c3i/ufmenTh6aNkjjjmI/tQ4DEAIESCXxauuJjxGW3zZN8sTXV6Xqffu9wHj7suzSB3ANZb1y6Wydbni6vc8fDY2uKxt9hv1zgQ/Dr7Jp8wczsBMJYFeXrza76tj1PVSmnf9PbelCAQMsI5Cas26p8+uDH0h/sVvVkZMsw406LCfw9mo+elyxtNt9ghWM75P6xd1L/CVypEMOYh3yz/oc9c4RPyPAyt71m1siOVRIIczrO3yWDcd1lX0glLU0gXl47ZubfPCJBAALLLPNaQYiPDf++ld+aKCv5TYuvSWIbo8pfUd97jTGePmjpH3/vY/IyiqNY9TFmYoLArAS8ckh6vHxwVmWL99sio9M2/BYrCQI5AseqMZ2Hffgf3Tct0rhc/6PEN66qTrZxjiTnQ9y2StWOoH9uAr7mGY9ZrjyvkbVG2Jj3t87m9Y39IZAl8Fa15g6Gd2d7l9N4WGTzheWoRAsEZiaQ3iAr42mJmZ3p+I5+wjg9n3Q8JNyfkEDuhs9rJtx3aN38BP81kvRYOV1tXrKC1D4C6Vi5/g5J2n5Q+1xv3KOiL2CsIND40OBASwg8V37E5xK/XVzGhbzlpef+kr8l+mNbadlLoU160Tl9Qv8U7dvXlHKK632NmbggMAuBT2in+Phw+TuzKIr2Kfo/gv+ZI0gUbyPgh3PTOXj8bVu7XfhuJjbHWsfNhhzXlLPrfiiO1A0C/lmH3BiGtkUlhHHXETbKfBCsBFdRAYFlllkwYsJWxedlkc0fVGUEvRCYgICfggkfACF3G2k2Avtpt8DR+a9mU8NeHSTgJ8XisXf5vA7GUYfLD8ywMi8/jU9qHwFfgEnntutvl/w62cZygQISpRVVvlGS8oNTBInioAn4gYn0+LjHnESs00stpXpH1R+k/tP+/5s+FOW3zvqacm/JB55+w4wEAQjcSuDDysKxEfJT5oRzz4xO62aJxTnB9nT31yquMPdC7jnU9bSzAgjxxPkLagjs7gW2Yz9cfnYNvmCiPAK5a6HpmE77v2HOu1Hzh5cTcsRoa5RAehCE+oKKvNpGeoMN52UcdBW5itqeE0iXh7m05/FWHd6RMhAf22+o2iD6W0Ugt3zTuq3ysHln/BTsFZL4OHG5L082Nk+4fA9yN389ZodL3i2Jx/KY8s13VqNvLJ6V8DGrR3U2IhyHQLkE/Pn4J0l8DnnPHCa8DJlX5oj1jSr7rWXfGJv1LYx06cE+3yD70giu/lwnQQACtxLwcorpeeeHc8IpujEwp1p27yGB3AV//y/a9eTrp/+SpMfWnysOzDxfmrGb+uH6Ryv2BfXVEFgktbnxDG2vKsmsVzQIOtP8TiXZQA0ESiHwDWlJJ6nrPytF+9JK/JsTsb31l+5CCwRqIeCndOO5+JNarPbXyE0Jz536GyqRZQjsnYy/j63DMv2G3PT8DKOT1HbHIUNpeewLMmPmuf1MiS9mx58hn1eddCuBNyuL2bj8EuBAAAK3EUg/D/zmxQq3bZ2s4Lc0F0mOkKTHW1H9repbxsMrfsgs/r9v3mXUpK61KT3Xx2zv2lqvcQwC9RP4gkzGx4fL894g2zej03pJEEgJPFUN6fx7RNqpg3V/v0jjukFtD6kwFi9/l9osqp+qvrM+bFNhCKiekEDRuIZ2L9ldRnqYlASdab5dGQbQAYEyCOwgJekEDfUy9Kc60icO/colCQJNEDhERsNcd/6mJpzokc2YpcssO9OjwZ0glLXUJ50D3HS+HZy/aPw9w+j5t3eh1EICfmozndeu+4KNt10fbf+AyqRlltlPEFJm/wMYCEDgNgL/oVJ8jFyl+jQPSvi700Ml/oyN9Ywqv0h9y34oMbbnN0f6mswujjUu+8FPEgQgcCuB7ymLjw+XfzsnnEMzOq2XBIGUwNlqiOff79IOHaz7sz6OKZTfX2EsTymwGWzHuX8XjWs+FQ5GDar9P2U8pmn5fSX6sP8IW57rJAi0gkB6EIT6PhV5F6/l/ryKbKAWAuMI+GQf5rpz3ngaR6x4uy+6xCxdJg2PwEUKOZ0HawwPQzbij2TY/FVtG2R709gWAk+QI+mcdn1XiW8Kx29QuOy2IaeFCj7Hiy/PQ54VxB4T8FtiN0rCceLyxnGHgvJ6aj9Q8iNJ2Hdc7t+C3VOykqTs5KWX4gcETinbQIv0jbpYeK8W+YkrEGiaQG5lonnPDa9SULlzXdOxYr9dBPzgWjpPDmuXizN5E183jePzQ3plJ3+HuUAS2xlV/oz68uZY2aPQjD5fkxg11muX6Jb/ly2y9Vht4ztjibBRNRuBb2m3okk6m8bRe/kLW7DHb3aMZsXW6gj8LJqHno87VGeq95oXKcJwTDv/au8jJsAcgReqMZ4HLm+Z6ziwtqLfsfJNFlK7Cbxc7qVz2vXVJP4iGd8gc7vbhpr8JfkKScqrjOXchsqUuPtFwBe0PieJjxEv11qUfEz5dxtOkMT7jCp72SVfUK7jsze+WfdW2exrGnWD7K59DZq4IDADgcu0T3p+OnMGPfEuX8/otA0SBGICJ6kSzz1f8PcDKV1OfgAjjimUX1pBUIcU2Ao20/xZFfiAyuYI+IHddIzjuv93LTM9Xcpi/XH5y2UaQhcEZiHgL1HxpIzLXhaq7ORlOGIbZetHHwTGEVhZHeI56DJPwIyjVrz9UwnPVxZ3ZUuPCfhHVtPj6i09jnfS0L6W4XKp2rr+xW3S+Lvc74zM2HmOh6fbTky2b9XlYOf0/RUJC3N6yJw62R0CfSLwTQUTf0Y+SPXc/57+XuYVNuK+48p+6Gs3id80qyvFD1i+qS6jDdg5SDaL+C9swB9MQqCtBH4vx9JjxUuwzZP+oJ1Tna6TIBAI+C3sdI704VpE+j9DiLHMh/F2ELtLMvyCrVy+cwBP3isCHx4zD8p+IOjhI+xt3yuyBNNJArmTn9veVUE06VsGFZhAJQRGEvByivGc90VQ0uwELtauMc9NZlfFnh0nkH6RPb/j8czr/tZSEB8bobzHvIrZvxYC/yoYv2D8+GR7n9+iCDHncr8NGeZ2yH3xnAQBCNx6Q/2RAvErSTg+fOErTv6/yd+5wvZJc7/lukiyoqTuFP/vN+9F8Lp9n8beY9W5aDzqvCE5jc/0hUATBHLHyX/P6UhO53fm1Mnu/SLwPwonnifXqt6Hc3McUyifXdLQrSY9/5lwCzaK8p+r/+ol2UdN+wh4ThSNvdt/UYHLDyiwuXsFtlAJgakI+Cn/ogNi2ak0je+8W2JrjfG70AMCpRJ4sLTF872KV9VLdbjFynx+iFm6HN6uaLHbuFYRgbdJbzofhnqOX14sfpPhcVpF7FFbPoF0Lrt+XWQmne/viLYNpeh5foMkZeU3tUkQgMAyy/h/zHB8eNmnz0q2kawpebEkbJsm94UtP/ndZPJbY8HnQ5t0pGLbfhM2xJnmq1ZsG/UQ6BKB9Phw/fNzBpDT6fMmCQKBwP9n7z7gpifqtY/Te5HeeR6QIiBdVAQFEUEBCyoqHpRi772+KCpHUVFsoHIsKAp2FLAeC7ajggULKgjSREAU6b34Xpfco/PMM8lmd5PdJPubz+d/p00mM99k997NJNn0GPHF+F1P89SAtF2ePr5Cw3zBjB+ZeNZcHKJhuIjGn9mfrbhWkSu/aN6Byk/qv8DL1cSiY8Dzd22A4EEq8+5ouz/XuI9TEgJTFfAJzKIXg3/0ss60lgqLt3XvOgunLAQqCJyuPPExuHuFdciSF1hbs2NLj5NmV2AVNT09HvyoqFlMT1OjUwtP7zmLGB1ss79M5vZffDW0P9THeX7WwXaOW+W3Jwb24PEr46qyfl8ENlFD4veIuzT9OMVlyfw4T9n4y7SefyuiDenzqkSo64faUKGG6rBv1M7Q3jBcuqFtUiwCXRQIr4t4OM57Q+47psv2+yoJAQsco4iPt5s1PV/R9eTzo3G7wrjPYQ1KRylDyB+G/n+d/k5bWFY2PFfrccHbIPH+LF9MTSk7Hrys7ptnrHcfhX8/9yDFrF5YraaT2iZQ9GLw1Y51puVVWLyt59ZZOGUhUEHgbOWJj8ENKqxDlrzAwxLLr+SzMXdGBPz+7hOA8evLJ9BnLaX/54IHj4XpzpGwvaoa9ls8fELUhP0zeaLFvR9dL9P+k3vfahqIQDWBLZXtDkX8/jHq+FNUTtvuVopPtvmuuL4mXzFdtN94YkJf9zrtGkUg9zrxnfajpqLHby07aoGs1yuBddWa9Jhr4g6XaaA9OtM2t/UnCndQOJZQbKVYU/EAxW6KRyquV6Quo0z7IkDS7AnsqyaXHS9Pnz0SWjyrAg8ueTHU/UEkftG9Y1bBafdUBPzj5/Hxx+POxtsNH0w8nzRecazdA4ETk2PiUk3P2kmkLyQG4T1n2o/E6sHhNbEmHFGwD32VW0graCTs2zBcOSzs+dBfzn+RtP/vmrYJCYFZF/DjE3+jCO8Low4foTLCo5HaZrqnKvQnxXmKXdpWuRrrs5nKKtp/vtqahAAC9wjkXidvGAPnvVo3V+YYRbJqjwT8fyc9PtbrSfvKzstenml36jDOtO9U92cY0uwKXKWmlx1Dbbtga3b3FC1vXKDohfDKmrccb+e3NZdNcQiUCfjq//j4O6UsM8sGCriDMfbcYOAaZOi7wO5qYHxMeLzPJ8/S/enHX6Xt9/Sn0oxMt1ogfW8L+3TJqNYeD/PD0Ce0ZyG5naHNYegv9CQEZl3AJw4uVITXxbDDP2jdHRRNPMZGxdaW/FsooW1Vfheltg1PuKDcSdjQbh6xOOGdweZaK+CLqcPrIh6+cIwax+WE8XEe2ThGVVi1ZQJ+zOatinBceHhMy+o4TnUG3cUTt7uu8XeqwhuOU2nW7Y3AdmpJ2XH1/t60lIYgMEDgM1pe9GKo84tafOXDFQPqxGIE6hQ4VIXdqfBxfrdiVk5mqqmNpPT9YtbuFGoEteOF5k4mPbTjbRqm+r9X5vR14Wn/lgKpOwK5fXhTpvppvvgRjJnsvZi1vlpxmyJu+/c1XefnxF5A0YiZEthYrT1VEb8uhhn3VdtdugN1VjrIfOL/lsx+vVLzSAggcI+AH/eWe7975ohA9yoo7wEjlsdq/RI4PDk+7uhX8xaZZAfZtbLbu2d+NGd8gW+oiNx7epjHeY3xjSmhAwLrlLwQ6nym75nJdjpAQxV7IOBHofg39cIb+zUa5/Eoo+/Y9MuQH7VDQsCdpGcrwuvMw9NmhKXod6teNyPt70szV1dD4uM3jB+RaWD6mMGTMnn6NstXmQaTMORxG33by7SnioD/3+2syHWghNfGoOGztf4yVTbWsjw7qT6hbX2+e9Tvbb6gLrQ1DO/SPN73hEBCQAIrKsJrIx7+14g6RZ+n3XFGmm2BeWp+fIx5/Ns9I/HjytM2NjF9vbbDo9F7dvDU1Bx3gJUdcz7vx4XxNWFTTLsFil4Idd7p9TERxNvhObftPib6Ujt3hsXHnTvL6CAbfe+mX14+O3pRrNkzAR8L8WvN46v1rI255tyQabfb7s5kUncEnqaqpsevp7fNNMF3TsV5z83k6dOsg5P2uu3v7VMDaQsCFQTcofUoRfzaH2b8PK27VYXttDnLh6L2f77NFR2zbu4EK9q3dJCNicvqvRHwnZa518lTRmzhiZny/jZiWazWL4G3Zo4NX+TftzSpu8huFNz8vuHRnloEXqtScu/rYd6htWyFQhBouUDZm3FdHVn+TbPwwvJw1ZabUL1+CKS/P/asfjRraq04WFuOX8ejfgmaWgPYcGMCb0mODR8nmzW2tXYUvLuqEb8ewvib2lE9ajGEwMkF+zL3+LM3Z/IOsanOZfVVuuHY9vAqBR3AnduNVHhEAXeIHKzI3VEUvy6Kxl+vdX2nRR/S29WI0M6P9KFBJW0I7UyHvPeVoLFopgR8J0H6+vD000dU8EWsaXk8jWFEzB6ttlbmuPCFan1NuY7i9HVR1/R6fUWkXSMLLKU1Bx1f80cunRUR6IjAoqpn0QvhpTW14fBkG/vVVC7FIFAm8E0tjI/tA8oys2ygwAcSzz5evTUQgQxZAX/Ijl9rHp/VE2g8fiB7iLR2pj8DXa5Ij18/kjeXDtPMNK/L6GP6oBqVtvWQPjaUNiGQCCym6QMV1ynS10CV6X20Xt86Ux4SWYz6GDUV0fpUdOLf+33L1teeCiIwGYGi80cvH2HzW2id3Puq55NmW+Adan56bOzRYxI//tAXo4zzGOfg9Z2MXVgWhpv22JKmjSaw44Djps9PEBhNjLV6KXBEwQuhrkcH7ZyUv0svFWlU2wTSq9E2aVsFO1YfP+oifKDycOmO1Z/qNiewroqOj40w3twWp1vy7gXtfdJ0q8XWRxDw+1g4XuOh74rMpftpZpzP4138PaFc2+J58zWRtvM5mueOAxICfRXwyalXKG5XpMf/oOnjtE6fP2d+PDL5scb7nIr2Nb+H1Oe9TtuGFci9To4ethDlP0aRlnXOCOWwSr8E1swcF7/pVxMLW7O8ljxMcaTiYoVfH7cprlVcqfA5mUsVFyr8//gUxfMVeyri8zNHaDp9baXTD1QeEgKxgC9yTo+TePrRcWbGEeijgL8Qxgd9PF7HXSJ+FFtc5igfnvroTpuaE3hwcsz1/ct8c5L/KdkfzMLr2D/ySkIgFgjHRjxcP87Qo3F/OYnbGcb7eidRj3bdQk3xnR5h/8VDd4Tlkk+Ax/k8vlMuY4fnLaG6v1mRtnN+h9tE1REoEnCnh7+nfEURf85Jj/+i6XdrveUUfU/PUwODwft73NilonaG9oYhj6Tq8Y6naUMLhNdFPPzF0KUsssgntU5chsfdaUaabYF3qvnpcXHQDJL4u+U43y+Lfmc5tt16Bl1pcrHAkloUHx/p+M1anvud7uISWYJABwW+rjqnB7+nj6+hLekJpboe3VhD1SiipwLPUrvi4/lTPW3npJqVnjD4xKQ2zHY6I3Cqahq/5jz+zM7UvnpFi+6W8wlWUvcEfFI8PW49XZRyj996VFHmjs73VaipiR+3SEKgLwKrqCE+zkd9hGJ4fbxXZYxz4qpLnn5MeWj3+7pU8SHrmn7eDW32MPe7lEMWT3YEeiNwq1oSvz7C+DAN3FyZb0/KuUPTPF5xGMX+5c191/IFLKTRBPxYyvD6LBruMFrRrNVTgSdWOGYe3tO20ywE/iWwnf4WvWGOS5T+k/viuAWyPgIDBH6q5fHxfP8B+VlcLuDb/GPPl5ZnZ+kMCvh3B+JjxOOf66GDTwym7fT0rJwk7dMu9T47P7M/3WlWltL970eg9CXlrhq8rC+Nox0zLeDHgz5ecbkifQ2PMu3Pme4wn5UUP3Lndz1utE/YFx0P8aOrekxA0xCoJPAu5cq9ViqtPJfpDZkyvjdMAeTtpcAJalV6bD2nly2dXKMekTFNjXedXHXYUgcEco+/TY8ZP4mOhEAvBXyiyLdLpge9p/cbs8V+VFFc7pljlsfqCJQJ+FE38fHm8RXLVmDZQIH4x9nt6Q51EgKxwF6aSF93nu5T8smxXBv9ODpS9wT8DPXc/txnQFPSdQZ1qA0orlWL45PgoZ0vaVUNqQwCwwn4sXi+MC8cz3UN3Zk8S+mRamyw8++t9TU9SA0L7UyHXAjT171Ou0YR2L/gtTLMe+NdmTL+Z5TKsE5vBDbKHBN+L+b9d/xdvHOBbfy/bpfxN0MJPRFYVe24SREfH+m4LzQlIdBbAZ8ESQ96T/sqyXGSr9r8gyKU/YlxCmNdBAYIpCc9feyRxhPw702E16+HK41XHGv3UMAfouJjJIzfq0dtTd9bQhu5eqqbO/k7BcfsoJM7Yb+HYV++HPi1GtoUhj/UPH+GI40v4LuNtp+LWbrzaHy50UrYVKtdqQjH8rDDq7Ru0ePnNxitSp1e67WR5f91uiXllX9h1M70mClfk6UIzJaALz5NXyOe3rciw2YF6/unOUi2o/crAABAAElEQVSzK/AzNT09rl40uxy1t/yBGd/U2x1pJAQscLwiPT7S6a2gQqCvAsuWvAD8TPZRkz9A3aEILyaPex4JgSYEvq1Cw7Hm4aub2MiMlfnJyNRX+3Fyb8YOgIrNjV93YfxRFdftQrZfqpKhXWH48S5UnDouJODfkgn7MB5euFDOhWf8JLPuwrm6NcdX5v4o067dutWM1tZ2F9Xsj5HveRrfsbW17XbF3NHrx/vGr+thx30n5eEFZfiO+llML1ajg+P3egxwVNTO0N4w7HGzaRoCIwncqbXC6yMMv1+xJH8/D+uEob9jkmZXYFs1PRwL8ZALteo9Jvwbf7FvbtwdaSQEil6T8THzNpgQ6LNA2rkQDv63jNFod4alH6DoIBsDlFULBXwnRzhmw/C+hblZUFXAd0gET79HkBDICYRjJB4ekcvYwXnuFI7bFcbXb7gtvjhld8VbFe9VfFrxMcVjFH6cLGk0gVdptbAP42GVD/lfzKw7Wi3as9bemTad0p7qdbYm26nmH1fcrYiPM4//STHOxWdanRQJuJPXj4RPnYeZ/ofW31xxeEE5ft+d1eS7QoJl1RPgXbTyZ9zQznTYxfZQZwSaFPD5ofR1cmPFDf4ms+5JFdclW/8E/D88PZY87f/HpPoF0p/Aydk/uP7NUmIHBXLHRjzvmg62iSojUFlgU+WMD/gw/rfKJeQzxneQucxl8tmYi8BYAo/T2uGYDcOxCmTlfwnEv094LCYIFAj8SvPD6y4MbynI27XZT8i0zV/um0qrqODnK4Jj0dAnhDnJPtxeKPoSbuMqF1S8OLNfunxXra/MvS3Tpg01jzS6gE8s3Kkoeu16/q6jF8+akcA6Gr9IUWY9aJnv6PN7w2sLyvHrfpaTLx4Ihlf0GCJ3AURod4+bTdMQGElga60VXh/xcM0BpflC6Th/GH/4gPVY3F+BpxccE3zHaW6f37/APLwePfT3TNJsC8THQ2783NnmofWzIODn7ucO/qeM0firkzL3GaMsVkWgSOA0LYiP3fcUZWR+ZQGfeIpN/QPmJARyAl/QzPhYCeO5vF2b97+Zth3aUCPmZ7YVLHPDbyg/jx+pvjNynZ3BtUopT83sn/lVVmxpnldm2vO+lta1S9XKPZI1HGdhSAfZ+Ht058zxG3yrDHfS+u4Yc3qdIrfOEf9aOtt/9ops+nwy5KdRO9NjYbaPAFqPwMIC/uyZvk48/aaFsy4w5/8VrLf8ArmYmBUBXzifO44OnBWAKbbzAQX28f54wRTrx6anK+AO6vhYyI37/A8JgV4LvFWtyx38N2j+qHd+3ZSU6UeYVEn+0hpO/IUvsFXWI8/sCeR+Q88nPkjjCeyh1eP3A9+lR0IgJ/AizYyPlTDe9fduP8owtCUerp5DGHPeoQXbirebG3/amNudldV9LOb8PM/Hb5U0T5nSMjaqsmIL8yyRaYvbtmoL69qlKq1W4BofNxcpD1dGj7dXj6zgHJvH4+nva7yhoCzumr9nH8Wdh38fb7e1em3v7/g4icdbXXEqh8CUBI7QduPXSRgvqk7R57CfFK3A/N4LnKEWhuMmHnb56Qxd2mk7FPjH++KzysNn1i7t1Xrqun2FY+P19WyKUhBol4A/rLjza13F/RTxG2I8XvURI0urDHdsraDwbzBcrIjLOVXTH1X4R+EvULjzLV5eZfxWrXOe4quKdyherjhA4cdEbqUIHWsaJc2AQO5xZD75RxpPIL2yyB2RJARyAo/VzNx7tx8X2OWUe2/5dgMN8iPtcn5V5/F+N3invKbEuOqVy7kft+5qB2Xut9gOH8xIjgECDyo5zsLr2RefkEYTcAeuf6smWA4z3CazyXcVlPWhTN5ZnbVvZHRtjxHeH7UzPa563GyahsDIAkWfXXcpKLHorl/+JxaA9Xz23mpf+l7raZ8/JE1OoOhndtJ9s9bkqsSWWiDguzjTYyCddicaCYFOC7gz7L4KfyG8TJEe5FWm3aF11lycoaE7qL6u+JnCHV7xbxZVKa+pPHeqLp9TvFvhOm6l8PN2Hb4qxScU7UHqtoA7Q9Nj6OhuN6k1tXdHdrC9rjW1oiJtFMh1HPjY8fwup+NU+fAaCMMn19ygtCM6bGeY4TNrrlPfits4sx+Drz8jVE3+3BDWC8NDqq7cony+2CHUPx76wibSeALf0uqxaW58vC3M7torq+kXVfBNzffUOunnfX8P+FJBWe/RfNJ/BOJHy/7tP7N7N5a7aMDH0uW9aykNQqA+AV+snL7n+g7fXDpfM9O8nibNnsA6anLuWPjs7FG0osV+Mkpuf6Tz/DQhn3sj9V/AN7Wk+z+e/oeWc2dh/4+DXrbQJ3QerPiGIj6oZ2387qT912j60jmXr2j4eoXvRPPV4L7CyVcB+846n0gitVdgL1UtPZZ9NyRpfIGXqYhg+7/jF0cJPRZYMzpWwjHjoV+fXU0rqeI+MRa356+avleNDfL/mIsV8TZGGf9ujXXqW1E2LjMdtlMoLevEDoK9ImPyyg62o21V3ijjmh4v7pQhjSZwlFZLPcumP678uc/wK2r+uQVlvV3zSQsKPEGTwfmuBRf1aqro7hZ3CqYdrL1qOI1BYAyB/bVueH8IQ79mVknK9N0nYXk89EXWpNkSWFLNvUkRHwdh3BfCkKYjsJw2e54i7Iui4SXK4w5OUn8F/JmnaP+H+b54ioRApwTWUG39uJxwEDMcz+IcWX5H4Y60AxU+EZL74q3ZpAkKpP/IfzLBbfd9U99TA8P7xsF9byztG0tgtehYCceMh12+s+mQTJteonl1JX9BLHq8V2z4CeX7b0U8Lx2/Q8vnKUgLCvgDvk/UpF5h2ncMDJv8WSCs76EvPupaiusfxpfuWiNaVt+1VZ9gWTb050fS8AK+2O96RZltvGzTgk34Aqo4XzzuDjjSwgKP1KzYye+rfUw+ZuJ2xuNFx1MfHWgTAsMI+P3gs4r49eLxZyeF+EKuNI+nN0jyMdlvAR8vfsJT7lh4WL+b3onW+e6wlxbsn3SfHaZ8/mxG6p/AfmpSur/jaZ9/JSHQGYF1VNMPK+KDmPFmPX4lb99ts4uCk0xCmFDy4zLTY3vvCW2775vxB6RbI99j+t5g2jeWgI+X9LXo6deNVep0V/adBGmbDqmxSoM6vf6uba0fbe9Ejaf1iadPjvIyeo/AcQPMRjnR+8WkzIs6hr1FUn8fQ37sEWk8gS9r9fj1WDTuO1NJwws8U6sUmcbz3618yxcUv1FJGV3+X1XQ3Npmu1M3Nvb/+z4mOsj6uFdp0yQE3BkWv0d4/GxF+Iy1eWZ5yK9FpBkSKOp8+cAMGXShqWX/D8Nr18MLFRt2oUHUcSiBeB/nxg8YqjQyIzBFgedo27mDuGvzrlA7rlT8QfGDufAt+KfMxec1dPhRNb5q6XTFtxS+OunXissULiO0+26Nu7ww3fTwLm3rBMUDFH39IqmmTTXZNbcf8a5vt/j1F4y3rK9YSuqhgL8Eh2MlHr6vo231Cdbc4z/qOrlddheD/dw57UcDxsl3hft/S+ybjsf5Z3286Et4MIs7H4exOjHZB9cOs3IL8p6a1N8e3B0x+o7xZ474EXTh+Coajr6l2V6zSgfkg0uIdtKyon3ytJL1WLTIIrsldn39nF30OcbHzUM4EBBAoFBgFS3Jvb8+UfPLXldbFZbIgj4KPFaNyh0n/9D8vv5f6fJ+9Hfhdxbss3Q/flT5lu1yY6n7vwXKPi+H/f7vzIwg0FYBP97Kb2DuCAoH7qSGP9E2z1D4MUPHKE5QuC7+PS//SGtaj9M0zx+kfKJxEv8M/Wa9usI/yO07jhzzFa9RvEThOroNaT3rnPZtqK9VjHpCTquSEoGDNJ3uo72TPEyOLrBz5Hu7xnkm+OiWs7Jm+nr09Ps72viHqt5pe75ZU1t8suD3mfLD9m7WMl9ckUv+Ehny5YaPzq00g/OeOMBpvzFMdk/K9u/ULTlGeZNc1Z+DcsfNJOvQt235c2TONDfvL31r/ATb88MSZ184UPYZ5bCSdR80wTZ0dVMHJH5LdbUhFeqde9163lsqrEuW0QT8Pd1PYHmk4lDFHop956b9e4GkbgjkLkry+ZVXKXKvq+93o1nUsiYBf6/JHQee5wsASe0V2EFVK9p36Xy/D/gcL6mbAr44N92n6fRG3WwatZ4lAZ+YuVGRHrzDTvvEmz/InKLwVf+D1veX0Sr/0NJyTtJ6bU2+UsJvDNsrfALt6YqPK76tSNsx6vRNKssnjX0i0x2FpOEFVtAqqf81wxfDGiUCj4iMffJpzZK8LELAAulr0tOndpTmTZn2+KKPOlL82sqZedtFyY9RzK0T5v2xaMUZmj9/gNHrx7TYK1O+53Uh7aRKhmMlDD/dhYq3tI7zVK+rMqbBNh0e2tJ2dKFaXypx3qakAUeVrLdhyXos+o+AOxHjY7nPvzkStzMe/8V/OBgbU8AXaviY8kVHsXHR+C3K9ziFv5+T2iuwqapWtA9z89dtb1OoWc0CW5QcG9vVvC2Ka0bANzUcrMi9ltN5P1O+5ynWVpC6JeDvhOn+jKef1a3mUNtZFFhUjb5SER+4Vcb9OMIDFO5oKEqDyvl40YrJ/LScE5LlXZr0P4dVFb7KzVdInKFI2zfstPfFwQo++AuhYvqT8qXOW1dcl2zVBOYp25mKyxUvq7YKuWZcIH1NevpjHTW5QfVO21PXHcBpuel02Z0Q8zL1StdfuqPmdVR7rQE+/mFwf24aJ3W5g+wdanh6vNBJMNrRcG+tNuzFaWWv7dFqMTtrPUNNTY/dMP0jLUtf177g7QMF69ym+VygJoSKyd95grWHy1Zcr4vZrk/aGre7i+1pU539/XmYO25j+zC+UpsaRF0WEviE5oR9VTZ8/kJrMqOvApuVHBMP7Wuje9wu//9/a8k+TV/3L1TeTXrs0aem+eaNdP/F03/tU2NpS38FHjvgQI4Pao/7EQZVr/zbu0LZVTp10jocq3L7lnwXn9/8fYfB6Yq0zVWnffX/ixW+W4c7doSQSb6rL/U8OpOPWeMJfFyrB2ePkxAYJBCOl3h4yqCVWrjcH/7jNoRxv8+Pm1ZTAaG83PC/K2wgt14875kVyuhjFt/R7ju0Y4t4/Ota5otcxk0+DuJyPe4LjrqQ0np7mjS8gD9HX6DIeZbNG35LrBEEBr13HhkyaujHql+myO2LkzSfx7YJYYj0QOWNLat89xui+FZl9UWLcVvj8bQTtlUVb2llfMHOwYpzFLHlOONcaNDSna1qbV9hP5+vPLyW2rsP66zZ7iqs6LXuc5ik7gr4IqSqHeI+BnzHsB+z6c/PpPYJlHVkh9cw+659+40aZQTCAVs29OMBR7ny3R9eysr1MpddlpbSwrSMY8pW6NEyd3D5OeqnKa5RpA5l0/4tOT/Wzle/PlGxg4IPk4sssp4ccm5+XAepXoGPq7hg7XESAoMEwvESD08YtFILl++uOsVtCON1VPUtBWWHbfgLx6D0NWUI+XND3x0xi+mranTOw/MuUtR1Z13uEb9f6AC4Ow1Sn990oN5trOJxGcvUNjfdxrZ0qU77D3A/Sst9Z9gNBfneqPmk4QV8Uis+nvvcQebvXXFb4/Fdh6ebyTV8kZG/u35HcaMiNqxj/P0qk9RegStVtbL9vEF7q07NahS4T8lx4PNjpH4IrKlmfFhR9ppPl/lCTq9Hao+Ab9JI91M8fa/2VJWaIFAssIYWxQduOu6TResUr15pyZcHbMPbLDuhlzuR9PpKW+5fJn+hfIziZMUoXxiu1nrvUfgDhzseZy3ZLz3GPe0rHkj1C7xTRQbvTesvnhJ7KBCOl3jo97uupeeownEbPP7rmhqRlptOV9nMLpn6peXM0gUVbusBJSZXalkdd46pmH+l3MVDPiHf9rS7KpgeJ49re6VbWL+HZhxT19w0d7qPvzP92vvhiP5PHn/zM1vCbom5H2Xb1+QTt7nXb5hX5/+SvhluoQb53EOwamp4p7Yxr294PWqP32uL9v39e9ROmlIs4Au7/TrNHQdPLV6NJR0W2Fh1P0RxnSK333PzfFfZzorlFKTpCbxNm87tnzBv1elVjS0jMJzAoOeE1nFXja/EDC+OomHZXWT+Xah0vcOHa2Yvc/sLlnviH644UVF0tWtqF0/7hO1Bilno0feV/9cr4vZ73CeySfUL+E4D38UYvH3ymYTAIIFwvMRDX1XWtfQVVThug8ffV0Mj5mXKjbdzRMVt+BEH8Xq5cd9tOyvp2WpozsDz7lI08Tim3Pba7u3fA0zrPYsX24yzn/wlMTWsOj1/nA2z7r8F/Jt531VUdXe+zf+9NiOjCNgv9u7zySx/d47bmo6/bBTAnq+zwwCz1HDQdNGJ9Xi9k3pu2tXm7aqKx98f433m8T6/d3R1n9Vdb989mu73MO1zl6R+C/jmjOcp7lCE/V516DvLdlTUcQ5bxZAqCGylPGX7Z5sKZZAFgdYI+M2n6IDetsZa3lSynbD91Qq2d+/Mui8oyDvLs91h9iCFP1T4zh2f1Au2VYbfUv5nKfr4uwpLql2nZjw+rXmkZgSWVrHxcbddM5uh1J4JxMdMGPcFAF1Lvvgg1D8MX1dDI07PlBvK93CYix3i9XLjs/IldBO5XV7g6s8uXt5Eypk3sZ06y0zr/Pc6C5+Rskb5wh/cZ4RoIs2seifZzarNQyZSo35vZE81LxzHHm7Z7+Yu8tmkvXHbPf7Cnre/avNy3/FTq7Lpn2tDeyjii1j82vZ32bK7kEKZykZqkcD6qkvYN0XD41pUX6pSv8BuJceAOz5IsyPgizkfp/izouj9YND8n2ndoxT+f+A7zXy+eQUFqR4BXyRp46L94PPSJAQ6JXCkalt0QLvDpa40TwUVbSfM9wnFXPIjBUOeMHx5LiPzFhBYU1N+hImvVPyDIthVGZ6s/L5zry/JjyVK232F5rnjjNSMgK8Wic3rfD9ppsaU2gaB3FWjH2pDxYasQ3zsh/GXDFlGmt0nfUJZRcN0nbLpMweU97WylXuyzP/nbitxmN9gO3P7MD7J1+CmRyradxSmdf7cSCXN7kqvzhgGU1/1GsaLhrMr10zLl1Oxgy46CPvCJ2XnN1ONmSjVdsHSw2Eu5ugi0AZJe+O2h/GHdrFhNdV5XZXz+QpGwcrDqxX+3HKYYlPF4opBKV4/N+7PVaR2CMxXNW5Q5PZTOs8nukn9EzhGTUr3dZjep3/NpUVDCPgu41MU4Xioc/hTleunCrxD8XrFkxS+MMo3Hvhc4bIKUl7AnY9F++ID+VWYi0C7BQ5X9YoO6rprXrSdeP7amY0+PFNHn0ggDSfgqyX8OMErFbH5oPH9ld9XcHQ1FXUC+2QfqTmB56vo+Njq+8mQ5iRnq+T4mAnjH+sgQah7PBy3g+zZyWsqLtvj/pA6TNpPmdMy0ulhyuta3uUHtN/eTabU2tMbNbnBMcv2nXRpnZ8+ZpmztLpPCKd+Yfp2LfPnrDCdG35ilrAm1FafYP/yAPd0Xxyh/G1+nU6IbujNPDBxvu/QJXRvBV9smB4/6fTzuteskWvsE417K85VpA6Dpp+qdZZWDJsGlbvTsAWSvxEBXxw0bIepLwIm9UPAn38OUuRer7dq/hr9aCatqEHA54rLLjbLHUN1zDtb2/2k4kOKbRWkewSu0iDn+3vNp2ORo6STAr4TK3dQe56/ONaZtlJhRdsK8/2hOU25f5g++U4aXWCeVn2hwldLBPtBwxcr7yhfTrTa1JIfu5G2yx+0/AgHUrMCB6v4YH9js5ui9B4J5D5ondjB9oVjPx76gpRRk/8fx2XlxofthF6uQpmj1rft6/mOVl8xmHP0vOcqmr6y/LLM9g/QvLamd6tiqZePIdJggUGvX792yzrQ7P6YwZshxxAC/nx4iSI9pqtM+3PkIxV+tAypmsA8ZYttfYdV35Nf1xcq4nbnxv+oPP7d3j4m/x+9n+KDilzby+ZdqnV818A46RytXLaNJ49TOOvWIrCqSvmLIreffqn5LyhY5vwrKUjdFnDn2A8Vuf3/V82f1+3mUfuGBHzBxYMVuZ9QyR1Ldc7zRW1bNNSurhWbO29j6xW71hDqi0AQeIVGit4wfHV13aloW/H8tPPidapEvNzjb667YjNcnr+UvUORGhdNf0R5/fjGtqdHq4K5Nqzd9or3pH5fivzP7kmbaEbzAtdEx014/R7b/GZr38ItmXa8c4ytDHqsxGkjlh2Mi4ZduyiiKsNJmf0TDM7XMn9hbzrlTggc3/RGxyj/W1o3GHl48xhlzdqqX0/sYsfHz2H4JGE8Px3nrvf6jhp/Drwi4+2THu74+l1mWbo/PH254uEK0mCBdZQlNky/6w0uoZs5NlG170jaHjvE4+54fayiy3co+n3Mdwf6xGXZ/9m43em4H6W4qaKOdKMKScuPpw+uYyOUMbLAylqz6P3Wj1ucr/AFTXcq4v0Wxv05hBOxQuho8jmooxVhf8bDv2j+sBf+dZSBatcg4P+1Pp/p73DxcdTU+GtrqHMfijgq4+15JAQ6K7CDal70xtHECSJ/aC7aXph/RqLpL59hWRjuk+Rhsh6B7VTMRYrgXDY8TvnWrWeztZfiq/BzdfcXNtJkBM7RZsI+8IlVEgJVBC5SpnDchOFHq6zYsjy3Zdrx4RHr6P93waJoOOqXyM8OKPtJI9a5zau9bECb/bloEulz2ki6Py+bxIZH2IY7Si9WxPX9nxHKmcVV/MSD2C0evzgC2aAkn9ch1SPwNhVztyLeDx7/iSLumNhQ01WvTP6M8vrzM6lYYFstis13Kc7auyV+Ykfc9irjP9M6b1UcppinaGPyeYLtFf6c4AuZqrSrLI9PbG6mqDOVbc/L/DMCpOkI+A7cPypy++j/ND/uRF+hIF9Yd9TPwCqWNCUB7zNfZBL2YTz096VVplQvNtsPgflqxmMUb1R8UeHvV/ExNu64z0+T7nmSwqGCOGsuDtHQ7+0kBDorcD/VvOgNwsuaSFeo0KJthvnzog37qvswPww9j9ScgDu+cifvgn88dEdZfFKhuVpVK3ljZYvr5/G7FDtWW51cNQnEr3PfdUhCoIqAP2Clr9+TqqzYsjx/yrTD76nDps21wk2K1CSefvuwhUb5B52U93b6lB6kxsR26fhLJtjY1xTUxf9T23aX9qMydX3sBK26uqknZ9ziY26ZqGE+0Rwvi8f/HOVjdDSB5bSaL57KdY79TvOL7kLw3WavUsT7o2j8g8rnz6CkhQV8Z1Hsdu+Fs/R6ju8Ujds/yrg/S/uqdXc2+q6aSSVva3WF3/Nfp3Bn8ij1L1rn8yov7gzRZG2paJth/la1bYmChhHw/v6LIuyHeHin5ufOQc0vyB/W9UXYpG4I7Kpqhv2WDv10BXe+kxBoUmBRFe7jbDWFP/9to/DnEj9F4GGKpyl8gduLFJ9SfFRxpuICxQsVJAQQ6KnANDrI3JmS/jNMp+Mr7d+dye95pOYFfELhDYp0/+SmP6l8D1D4H8600sHacK5uW06rQjO83Xg/HD7DDjR9OIEvK3t87Hj86OGKaEXuazLt+N6QNfMVWKlFOu1H0Iz7RTItM532ic0+JJ/oTtuWTi85wYb6C1i6/TD9ay1beoJ1GbSp3Mnd/QatNOPLc2Zh/3q4ReKzvKbvUMR5wjj/QxOsISfvpfwXK4JnPHTnb5XXvb+7uHPgooJy4jK/pzx0lAkhSr7wLjbaKVo2K6Pu3IoN6hj/s8o8QXGIwv9T5it84YvvvvD/bv8fWU/h5AsvHO6Y98Ui7hzy8GDFIQpffOqyfqH4h6KO+pWV8T5tw3dqNpXcsVe2fS9btqmNU26hwKDPYun/xrigHTRRtk+P0PI2fXaK6874PR37/p9btA99UdG432lwRgABBBBAYGQB/xP6uyL9R+UrLJv80PrDzDbTOqylPE5vUaTLPI80OYGVtSl/kUn3Q27anZc+cebOtUmmFbSxGxVpnZ4yyUqwrX8J+GqceD+8HBcEKgrkOsj8+1tdS2epwvFrwOPfGbIRf8iUkZbpE2LjJp8gS8uNp30FXdeTP+vEbcqNh5OIk2rrSwbU6ZBJVaTCdk7O1JWTUHm4xTXbJ5pzx1iYt3dmVXcYhOXpcLdMfmZVE9hc2XKPcfL3HD9ucdi0vlY4RpHuo9z0Vco3X0G65ztlbLT7jKL4tR87TGrc3/V9zE9qe7nt/EnbP1axi2ISj2Bap0J7lYU0QYGy/3M+ZtxBMij5+MkdX/G8Js9hDaofy4sF/DjieD/F45zbK3ZjCQIIIIDABAX+qG3F/6DC+IEN1iE9gR62GQ99K6vT5xTxfI97HmnyAj4h5s6OKlcW+hbkBypWUjSdDtEGcl/+Jn3Cs+l2dqV87/P4NfvwrlScek5d4JTk2PFxdOrUazV8BU7PtOPzQxTjR3XFr6HcuLdRV/qbCsptw/OuVCxX14amUI6vIr9YUdQ+z3+BYtLpddpgWZ1+OekKFWzPd4Wn9fQdBqSFBXxnxo8VqVc8fdDCq/1rzv1L1pvFu20KmIaava1y35Fx9XuaT56Pk3wXRK7jON7XYfzbynvfcTbWg3WXVxuCh4ez7DFP7b8w8Yht+jJ+jtp4ksIdGn5v9P+SSaattbFBlpOszyxvy5/DjhiwP4a54GuTAWV5v3t73i5p+gKrqwo/VRS9HvmMM/19RA0QQAABBOYEfqBh7h+Wn7nfZPJVZLnthnl3ablvpT8/k8/zSNMT8AfO/1L4asCwv4qGtyjPEQpfddtE8peuGxVh+75C0o83O1hBmo7Adtps2B8e7judarDVDgq8VXWOjx2Pf7aD7fhtph2eVyW9UplSg3T6NuWps9PqfirvzpLtvlzLupq+r4qnfvG0/0dNIx2ijcb1yI1Po17pNn2cpXX7SJqJ6X/9LpCPpdQqnn52idMTStblkUMlcAWLnlfg6ffOJxWsM8rs+2ilzyji/Vw07u81/q25SXcUaJNTT360X+wyzMnwqVe+oQpsqXJzd83HTl0cf4/atbNi2p0Tg+7W+1JD+5ViFxRYTZN+3y07lg9ccJVKU75ot+ziLm/PF4H7PZc0PYF9tOmyfe+LqUkIIIAAAgi0RuBo1ST3j8tXPDaZciddcvW4UpVI51/RZMUou7KAv/z4C4j3R7qPctOXKJ+vJKzrZM9hKuvqZNvXa9pXqpKmJ7CbNh3vf3eYkRCoInCaMsXHjscvrbJiy/LkvrT7vaks+aTphxRp+3PTTdzx5DJz2wrzNi6rfEuXVTn56N9qmUZaQxsNtkXDjaZRsWSbB2XqOcrJrKTYXk26w2XQ48v2G9BidzoWHQcDVmVxJOCTpu9U5Cxv0Hx/92gibaZCz1LktpvOu135tmmiEi0uc9XEZq8W13XSVfN3KR8Pz1V8WPEHRXrMtHn6E6rv/or1FG1KW6oyZW6Ht6myPayLj2t/VijbB1720DHa7kcav7rCNnyua4MxtsOqwwusqFXcCV20/6/SsnnDF8saCCCAAAIINCuwh4ov+ufV7JarnwzM1a/pulF+dYGllHUrxTBf6h6n/EtW38RCOX3iMD0u3Fl2yEI5mTFpAXeaxvtm/UlXgO11VuBrybETjqOuNSjUOx0WtWNdLbi5oO1pGbcq36JFBY0x3yeOL1ek24unxyh+4qt+e0Bb3K7HTrxWC24wts2Nv3/B7FOZ8u9CpHXzezxpkUV8AvYHitQnnd68Ala6Tpj+e4V1yXKPgE/Ifl8R7OKhHSfxGKctCrYf1yWM/155d1DMQnLHZWi3hzvOQqPHaOM8rXuY4nTFLYrYbtrj/t/6LMW9FW1O7nQsszq4zZXveN1y39Fz+8KPwa0j+VjMlR/Pu0h5/JpavY4NUkahgN/r36GI7dPxc7Tc+UgIIIAAAgi0TqDsx+v9/O4m01oq3I8cSf9xVplusl6UPZqAT7D6Kmk/Eq3KPnSeLyjWUQyTXqXMafnXaR4ftoZRbC7v85P9485TEgJVBHwyKH1te9pXiXYppXe2hjbtrUbEFwb4LqJBv0UV1g3DJk9K7aH6hO3khr5St+3JvkX+cZt8d9m0kz3jOuXGp13HkzN1XHPalZry9n2M+Y6J3P6K531Redz5XSXF68Xjv62yMnn+dSW6T7rFdmH8PM33hVyTTJtpY6cqQh3Khj9Uvl0VTVz4oGJbkVZWLWKDR7aiVt2ohI+LTRWPUfyfInasOl52h6uX+QKdmxSXKy5Q/EhxguLNiocpNlZ0La2gCpf5vLhrDepAfX2cnDTAPeyTujuqfD7L5yBC+UXDfyiPL5ZYTEGqT8Cefo8qcg/zX6s8k/5/XF8rKQkBBBBAYCYEPqVWhn9c8dAfkptOF2kD8TarjjddL8ofT8DPlHbnV9X9ebbyDuoo84evvTJl+svdUxWkdgi8XNWI97sfrUNCoIpAUQfZSlVWblGe+PjPjbtz5ksK3w2WW14073kTaOOZA+rkTr62pk1UsSK7dH4bTkYPOoHnOk875TodfPJ/VpM7qNNjKTf9pCGA/FuquTI8701DlDOrWf3orCK/v2jZNDt0/fmn6qNzT1Bed5QtqehbWl4NivfRPn1r4ITbs6y2t6XiFYrjFF9V+H/3dxX+TbzjFb5Y7fEKd+b7glS/DsJrwSeo2/A/UNVoNPm7ZXzcxeP/0+iWZ6vw9dVcXxAS+xaNv1f5muwgccfb/6tQl98rz/YK0ngC7hQ9TVG0v+P5W4y3KdZGAAEEEEBgMgIbaTPxP7B4fN+Gq+AP8fH2qo43XC2Kr0lgvsoZZh/7inqfLMqlwzUzPT5u17yVc5mZNzWBI7XleD/5JDAJgSoCZylTfOyE8RWrrNyiPH8saEdozyjDz02ofTtWqPvTladNJ9dclypXDgf3Nt1tHOpUNJzQbi/cTO5Yfkxh7v4u8Alpn4gu2k9hvk9Ubzskgz3D+unQHSakYgFfjJWahenztawtnw/9OegNCt+9EOpXNPRdQnXfXaEip5p8d0fc3vtPtTZsfFYE/Jtu8XEXj/viStJ4Amto9ZMVsWvZ+H3H29xQa99HuX9SoW7+bE1H2VC0i9j2bRVsw7HwSeVdbrhNkBsBBBBAAIHpCnxTmw//yNLhug1WzVdXpturMr14g3Wi6PoF/CH6XYoq+9Z5douq4A6zdxas23QHblQNRisKHJPsqw0rrkc2BPxFNfce0bWTaeldlLk2DTPPd5xNskPq0wX7Ia7zlcrjq4annfxFvcpJ51D3tpwwD24+cRDqlg6PCpmmOCyq3xSrNNFN+3X3UEW6b3LT31G+UT6bfqOk/CY/f2uznU6Hqfa5/eB5lyn82bFtycfT3opvK4rqHuafpTzbKPqQfHI0tMvDffrQKNrQegF/R4yPu3R8+da3oJ0VXFrVKut8TJ39Hd7vAdNIW2mjf1OkdUqn/X/4iQp35pMWFPC5uocrqtyZl7r25X/YgiJMIYAAAgj0XmBNtTD9pxam/aGhyRS2U3V4myrT5O35TbZ11sv2o2Oeoaiyrz+rfPMVP83kv0Hz/MgQUvsEPqAqxft3Wl+K2idDjQYJ/CI5dsJx1LWrO1dSO/weFeo/ztB3zk46uf5V63yk8k7jvdgnv986RD3dHn/Jb1tyh13u5M3Fmt+Gzryizt7XtA2ygfrcW2XerqjyWthf+UbpHHO1y8p3hwppYQG/Lxa5/UzL2vDaWbjWC87xiUPfLVbUjjD/V8rzJEWXP0v5hHpoj4ePUJAQaFrA5wri4y4df0jTFehZ+T5XNMznrt8q/zotMPAduWUXVKTHxeeV348OnNXk1829FC9SXKpIfapMH6z16GwUAgkBBBBAoLsCZR0XezTYrPup7Cr/bOM8L22wPhTdvEC4ijbep8OMb9Z8FdnCiAIf03rxvvSjqUgIVBH4gjLFx04YP6jKyi3Lc3BBW0Kbqgw3n2Kbdhyy/t9S/nkTqK//d/yXItepVGTqE+a+OKOtyR13Pnnjx/M5DlW0pTNvU9Ul5+rHU/mq8C50RKialZM7uXx3S67NuXnXKq870sZJuXLDvHHK7eO63j8nKoJPOnSHU5tf67l94hORrnfaltz0qcq3g2IxRZeS6xu3x9/7SAg0LZAed/Ex6PH/broCPSl/I7XjtYrUr2j6x8rbho6xlH9tzThyiHa4ff5e8gBF1x71ripXTv6f6c7ifRUnKO5SFO3bsvkXaL1tFSQEEEAAAQR6IeATT59TFP3ze0KDrTy3ZLu5+lyi/K4vqdsCvqp0mEcvXqn8m3a7yb2vfdpBtkHvW0wD6xI4UwXl3u9fXNcGJliO/z+dXtCeXBvjeU/Wer5Datrp8apAXK+q46dovecoHqXYXeG7BR6ucMfWTgrfDeHwF+nHKe6vmD8Xdsv9b99Q809UVK1DyMcJMKGNmYJl0fC+Y5Y/7dV9vG2pGObKeFu8SeEOm3HS8lq5yNV31JL+I7CKRi9XFHn5/0fuveM/JbR3zCcoH6zw+1VR+9L5fj9dQdGFxB1kXdhL/axj+rpJp/vZ6npa5U6upypuVaRuuenjlW81RduTO8pOUOTaMGje+VrvMwrfxfxExS6KLRS+0KErnWj+v+G6HqLwU19+qxjU7qLlv9O6r1asoSAhgAACCCDQOwFfDXyJIveP8GzN95ecJpK3m9tm2TxOvDexJ6ZTpj9Y/nnAMeDlPolAareAvzjEr9tl2l1datciga8lx044jt7ZojoOUxW/X+1R0KbQtjD0+9uzFG37kunOq1DHrg03U91J4wtspyIG7Xu/dt2J2ZXkx4g+UPF2xaC25ZZ73TqSO31y5XveG+rYQE/K2LTEyVbfUizVg7a6g893K/hEc9Fxkc6/S3mfr2jzydklkvY8RNMkBCYhcKw2kr5m4uk2v24m4ZPbxrKa+TbF3YrYqmjc/0e9TtfSeqrwMO+1Re1P51+tcn0xx48Ub1X4f7kvfvDFRL5D3bGcYn1F08ff4trGxgpfgPEOxUUK/89I6zzM9Be1vp/s4c8vJAQQQAABBHov4M6Kon+UZ2lZU50U+5VsN1cfOsj6dSi6k9RXIuX2tecd1q/m9rY16V0e83rbUhpWt8D3VWDu9e8vsF1OPjm4q+LTirR9H9I8nyz0l9i2Jv+vHecK07TNTU+/RPVt+qRDW/dVU/V6rQquut/8OvYJswMV+yt8hbVPCG2p2Etxb8WGim0VPu5DaLSx5I6HnRRHKq5UVG1Lmu+jWncxRV3Jj8tLtxGmD65rIx0v55ElRrby/wcfQ31Lft89QhGOhypDn5R9qqJtFyb59RfX3yeKSQhMQsCfr+JjLx135zrpHgG/bxytSI1y03cp35sUXewYU7UXSKtr6pWKXDvrnHd3yTb+qGVnKPwEBndkvUHxTIU/Rz1I4cfSup7rKLyffC5uublxX/BzH4XzHKo4QvFNxc2Kcet/7VxZz9Xw3goSAggggAACMylQ9mgl31beVHqLCq7yz/xc5fMXLlI/BPyFvmy/X6/la/ajqb1vxZeTfdm2EzW93wEdbuA5ybET3hP6dgKjq/+7/MXbX5bDfmnb0Cd21lWQmhH4nIqte5//TWU6fMX1LxTfUByn8OfMZyjcgbSJYtjXjNfZV+GTS19VjFvvH6uM9RV1p7VVYFHdDql7Yx0rz51en1cU+Xh+k99H2sLlzn4fx2UOuWWf1Dq+c6ANKX3EojvKSQhMSiD3+ojnPWJSFWnpdlZVvT6liE3Kxv2/ea2WtmWcavn7atn5rzKTviy7QwYfVByksEdTF8WraBICCCCAAALdEvDVtkVXnzymoab4JIhPhpZ90PAVOHs3tH2KnayATw5doSja35dome9I8kkyUjcEPqtqxvuziZOK3ZCglsMKnJ8cO+E4+uKwBZG/MYElVLKvbPXVw2H/THt4leqyh4LUrIDv8j5GMe397c8F7kz7uuIkxekKXy19oeIGRZ31u1jlNdnJ4JOMRfX9kJbNatpODS9yCfOfNoM4m6nNb65gE4w8vE7hDuNpJn+3i+vkdpAQmJSAP0PGx19ufE/l8XE6S2lTNdb/N3Me6bwLlO+1io0Us5D8eccd+YPOSaVOXZu+XW38sMLn1R6ioENMCCQEEEAAAQSKBN6tBUX/7OcXrTTmfN9C/l1Fut27Ne80xf0VpG4L+LEA71Ok+zhMu9OMjpVu7uOvJft1qW42g1pPQaCo08XHFKldAj6xf7QivGdPY3intv98BXepCmGC6ena1jT29yS3+V610cf4JFJRu/42iY23bBv+vHCyosgkzJ/1i+R8It8Xjn2/glUw+7TyTuqY1qYWSItpKtTDwy0WWMoEAs0KrKPi4+OvaPzUZqvRitL9WnTHT5FBbr4v1tigFbWfXiX8nruZYleFP3ceofig4jOK/1V8T3Gu4iLF1Qo7pt9p6r6AJ7evqsz7qer2HIUfzbi0goQAAggggAACFQX8bOkvKYr+4foKmyaSP4hspXjeXDxQw1UUpO4LDPqtOZ+YInVXwFfyx+8XG3W3KdR8wgLxcROPf2DC9WBz1QXupazPVMT7axLjb9M2fdKLNB0BX8Byh2IS+3oS27hRbXmrYhr/ry4rcVxKy2Yh+TP/IxRV9vXmswAyRBtt586y8xRV/J6hfH585SSTj+O4blzoOEl9tmWB4xXxMVg2/qiekblTzOdRhr0byh0p0+pU78MuCP+/11RjNlb44uB95sLv2W9XHKnwsXmBouyYHHXZRSrXv2vmi0p8xyB3iAmBhAACCNQp4A/ipNkS8D/4XyrcYZVLPkF2XW4B8xCYE/AVSs9WDOr88gf4M+fWYdBNgR+q2r7CLiSfiPHdnyQEBgn4C2AuHa6Zb8ktYF6rBFZUbfxj4rsotlf4AppbFH9W/F3hq2p/o1hV4XS9YmuFfzdsDcUeCp9IyCVfieuLdT6k+IHCnTOk6Qr4+4D330mK+063KiNt3Senvqjwbx/6OJ1WepU27Lrkki8o8m+o9Tn5pN0fKzTwH8qznuLWCnlnNcsSavjDFV8bAODvbDsr/jAgX12L/V4Rfw5cR9NX1lU45SBQQWBZ5bm5Qr44y1Ga+LziV4qiz6dx/raM+33A52zuozhW4SfzDJNuU2Z35Jyh6FK7h2ljW/P6c7P/x/kxw96Pmyj8GdkdlWsr/D9wRYXv/vL3a++raxR+P71E8TvFhYpzFf7sTUIAAQQQQACBBgTcCeYPSUXhf9gkBFIBfyHxXYBFx02Y784zOt9TvW5Ohy+SYd/6qjkSAlUEwjGTDg+osjJ5eiWw2FxrfIKA1H4Bn6jZUfFKxTcVPjlzhcInbv6iOF/h/w0/V3xd8T3FGYqTFZcr0td8ndMXq3x3Mj1W4Y7bNRRtSqupMkXt9RX8fU0+6Xeaoqjt8fxX9xWhwXb5QqXvKWLHdPxALV9K0XRaRhuIt71T0xukfAQyAitonu8Wjo/FYcfdmf8jxUcUfv0coHiMYhXF+orlFZNM/ozk/70PUDxf8VfFsG2K8z9d6/O5SwgkBBBAAAEEEECgTGAzLYw/RKXjvtqIhIAFllO8WJEeI+m0T6T55BCpPwI++RnvZ75o9WffNtkSd5DHx0087i//JAQQ6KeAO9ccviLad7/sq3ipwp8PrlLE7wVVx/1/6M0KnzQMna0abW3ynWxFbdultbUerWLuoHxnSXtTB3/3II0u4LtIUtN42sde0yn9/+6LLkkITEPAd7AP8/4Tv1aGGb9d2/mT4lsKd6a9TrG/wp9n3Znm/3lV04bK6Lvrd1McrPD5lg8ovqEYpk5leZ+jsoapk7KTEEAAAQQQQACB2Rbw1VFlH7A+quVdOBkx23uxmdb7C/Dmig8pyo4RL/OV5X6sDql/Aj9Tk+L9v3T/mkiLGhDYJDlu4mNoyQa2R5EIINAdAXeezVc8QfFCxXsUPkH4bsWrFJ7vzrCuvlf481D8npeO9+H/6Dpq49ED2hm3+xDlJdUj4O9lPqke+8bjvlPxgfVsKluK71KLtzc/m4uZCExOwP8/4mNyVse5m3NyxxxbQgABBBBAAIEeCvjKp7IPkpdr+dY9bDdNygv4MYoPV/xBUXZceNn7FT4RTuqvwCVqWjgO/JsT4feG+ttiWlaHQNnJuzrKpwwEEECgzQJnqHLhf2c6vFbLfBFSF9N9VenPKtI2FU0fq7z+nkGqX2BNFXmiImfvz2vzFU0k35kSb3PFJjZCmQgMIeD30/sp4uNyVsZ9R9t8BQkBBBBAAAEEEECgBoHlVMZ5irIPk6/Xcr7k1oDd0iLWVr2eqrhFUXYceNmbFTxSRQgzkD6mNobjwY/IIiFQReBtyhSOm3RYZX3yIIAAAl0WGPSEhpvUOF+Q1IXkRys/TnGJIn0/L5r+rfLOV5CaFzhMmyjaD76Qre6UdpD5jlASAm0QWF6VeIWi6PXQh/n+LvYaxTwFCQEEEEAAAQQQQKABAT+ywx0kZR8e/eV4N4Ufr0Hqh4CvBn6Romy/e5lP5vhRSHSMCWFGkh9vdb0iHBse7+ojr2Zkl7WmmTdGx004fjw8rjU1pCIIIIBAswInqPj4/S83fpLyuDOtjcm/F+YLonL1Lprn9/4d2tiYntfJnVSXKXL75bmav3KN7XfHbrydOsuusZoUNcMCa6jt71LEx2kXx/2bZy9R7K/YSEFCAAEEEEAAAQQQmKDAutrWoLvJzlQeTpRPcKfUvClfDby9osqJjxOUzyc73IFKmi0Bv8ZvVYQvlTdonNf9bB0Do7Y2HDPp8ImjFsh6CCCAQMcEVld90/fAsukfKP97FHsqtlNspZj0Zy9fBOUOle8q7lSU1TdedpHy3l+xqII0HYHVtNk3KOL9EsYv1fy67vRKf4PMHWYkBNoo4Md/HqC4QBFeC0VDP5a0aFmT82/Tdr+m+IBiR8W2io0VJAQQQAABBBBAAIEWCPgL+e6Ksg+Ev9DyZyuWUZC6IeD96sdPnK0o27de9jpFXV+mVRSpgwLpY3R+38E2UOXJC6Qnz+L3mi0nXx22iAACCExNwBcYxe+Bo4zfrjK+qvigwp/NdlP4Iqc6OiZWUDn7Kk5W/EkxbP18B9w2ClJ7BPxYxdx+9AVPPgE/bvJ3g7h8P6afhEBXBHwRgDvO7q3wRcHujNpZsY7iMYonK/xEneMV31Gco4iP9zrG/V5+kOKRCteHhAACCCCAAAIIINByAX9xfoWi7MPg+Vq+dcvbQfUWWeQJQrhY8VdF0f70CZgnKbgCWAikRXaSQXysXIoJAhUEHp8cN/ExxHtLBUCyIIBArwQeqNbE74N1j1+l8n+gOE7xfMXeik0V6ymWVvgErE8Eb6I4UPFKxY8V49TjRVp/AwWpnQJ+HNvfFLl9/IAxq+wLI0O5vuvGF8WQEOi7gJ++sqHCF3o9R/FGxf8qrlDcpgiviTC8RPP8vfpYxSMUWynoTBYCCQEEEEAAAQQQ6LKAH6t2piJ86MsN367lnPxs1172SZE3KfwBPrfPwryPajm/GSEE0gICPqEWjhEPf7XAUiYQyAscqdnxcRPG/T+EhAACCMyiwK5qdHgv7OrQjwF7nGLZWdyBHWzzI1Xn+DHZ8XHn7wajJt99E8q6S+N+2gAJAQQQQAABBBBAAAEEEJgJAV8huJvidEX4YpQOf6dl91OQpivgq9T8LPN0/4Tp67Ts24r/VqyiICGQE/DdhOGY8fCzuUwTnreGtuer8fdSPEuxr+J5ihcq/kvxMsXTFYcodlNsofAV9KTJCfhRnPFxE8ZfOrkqsCUEEECgdQL+HP0pRXhP7MLwT6rvmxWbKUjdE/BdL+cqcsea7yQc5fORO0hDeZdpfDEFCQEEEEAAAQQQQAABBBCYKQHflfT/FOHLUW74ei3nt8kmf1jso02eMmDfXKzlftwiCYFBAm9Thvj1/bFBKzS0/D4q991JXeJ6VR0/WWW4c43UnIBPnPmK8tw+8f8OEgIIIDDrAn58+QsUdyhy75Vtmfc01c/v6aRuC/hpAD9T5I6rn2v+sN/Xlo/KOl/jJAQQQAABBBBAAAEEEEBgZgU2UMt9ZWnuC1eY96CZ1Zlcw31Fsn8L4hZFcM8Nz9ZyP/ucKz2FQKok8GXlio+lSd8BtJ62/42kDnF9xhl/icr1Y4JI9Qq4E8y/SZLbN5xordea0hBAoPsCq6oJfmyh79Ly3WW/UviunNx76CTm/Vjb3kXBI9OF0KPk7wpnKXLH0AWa7zvNqqaVlTH8n6eDrKoa+RBAAAEEEEAAAQQQQKC3Av5tMj/aLPeFK8x7n5ZzIrreQ8BfdPdQ+DGJwblo+A7l2UExzJdfZSchsNCx9dQJmfhYPVhRdEzXOd+PGPIJSlI9AvbM7Z+v11M8pSCAAAK9F/CFTH5U9vaKvRTvUviCFXee5d5fx513icp9jmJ1Bam/Av7O5t+Ryx0v12v+ahWb7jsgnd/lfL7iOmRDAAEEEEAAAQQQQAABBHovsKlaeKMi96UrzPt/Ws4POY93KPgxKS8Z4Bx7b6O8XAU8nvmsru0TKeFYCsONJoCxlrYx6G7IUJ+6hn7vOkzhq6JJ4wn8Tqvn9svrxyuWtRFAAAEE5gT8f/JRCv/e5hcVvosn975bNO8vyv9+xQMUwz5eT6uQOizg3xwre2R1lU7SHVVGOLb+oXG+Z3T4gKDqCCCAAAIIIIAAAgggUK+AO7+erAhfmoqGj1ceOsqq26+vrK+t4Grv2xXPU6ynICEwjoDvqkpfw6uMU2CFdQ/NbDOtQ5PTN2n7B1eoJ1nyAr7zr2j/PDG/CnMRQAABBGoUcAeIH4HuC9d2Vmyt2FaxpsLLSAhY4L2Kov/Xgx6H7KdYnD23/is0JCGAAAIIIIAAAggggAACCCQC/hJ+iaLoi1eYf7Dy+DexSAsK2O9JCj+2JFgNGn5PefdTDPpSqywkBCoJuCM7Pe4qrThCJr8P+A6uOxXpNqcxfZnqcaCCq6KFMETyb04W7S9OzA4BSVYEEEAAAQQaFviIys/9z/bjE/0UgaLkR7yH9Xw3IgkBBBBAAAEEEEAAAQQQQCAj4BPLj1CEL1Blw98r34MVs3gy2o8yeaDCj8n5haLMKbfsjVpnbQUJgboFXqwC02Ou7m24PF+J/HNFuq1B06dpnXcp/kvxQsVLFc9WvF3xKcUvFYPKqLL8/iqHVE3gfcqWM7212urkQgABBBBAAIEJCfhpHkUX4/2mpA7+DbLwe3jPLcnHIgQQQAABBBBAAAEEEEAAAQmsrCj68pU7kfpJ5X+Gwo+E6VOH2UZqz+aKfRR+rMnpilz7q8w7T+s+RcHdd0IgNSZwvEpOj8e6N+bX+DDvDy9X/lF+L8WvP3ecpe2pOv0Vrev3MlK5wG1anDP9Y/lqLEUAAQQQQACBKQi4k+zbitz/7uMK6uMnXdw4t44vjCEhgAACCCCAAAIIIIAAAghUEPCdUp9W5L6Alc37otbZU+HfU3C0NfkuGMeKiqcqHqd4reJnirL2VV32d5VzoGKUzgGtRkJgaIETtUZ6fNbdaf3qzDbSbXr6HQq/h4ybXH93vv9ZkdvOoHnu5CblBXxFeZHf8/KrMBcBBBBAAAEEpizg7y9XK3L/w5+Qqds8zbt7Lv9JmeXMQgABBBBAAAEEEEAAAQQQKBFYWsuersh9Casyz3eYHa04SLGKYtKdZu6g8u/sbKjwnW6+K+W/Fe7AclyoqNKOQXnuUDnuoHiwwld3khCYtMAHtcH0OK3zrkW/htLy0+m7lOfQhhru94/XKW5WpNstm86dLGqoip0q9lUljjwGtlO7ksoigAACCMyYQNlFLul3LX8X+qrCn5X8mHgSAggggAACCCCAAAIIIIDACAJLaJ1dFB9QlJ2MrrrsyyrnlQr/HtEWCt9tMsrdLl5npbky9tbwMIUfMfIVxWWKqvUZJt+vVa7vlHuawne3LKsgITBtgdwjCfetsVI3qayy18ndWr5pjdsrJKWLKwAAKqpJREFUKsqPThy2096/z0ZaUKBsXy6YkykEEEAAAQQQaJvAeqpQ0f/y+GK9J0b5zmhbI6gPAggggAACCCCAAAIIINBVgfuo4i9SfE8x7B0dRV/mwvwbVOa3FF9S/I/iWIU75k5Q+ArIHyl8p0rIP86wqJw/zW3rDRr65PomCp/8X0xBQqCNAo9VpdLXgl8/dSR3Pqdlp9N1dsZVqfMaynRkhXqFer6zSqEzksePngwu6fD/ZsSAZiKAAAIIINB1gb3UgPT/uKc/EjXMd+B/cy7fHtF8RhFAAAEEEEAAAQQQQAABBGoS8LPw/fgO3w32ZsVpivBlzXeVhPE2Dd2p50csuvPrcMULFD7hvqNiRQUJga4J7KAKp6+x82pqRFpuOu0TL9NKG2rDRR3daT393uT3q1lPqUs8vc2s49B+BBBAAAEEOiRwjOoa/x8P437EvNO6it8p7lTsqSAhgAACCCCAAAIIIIAAAghMQGADbcOxi+IExfcV4QvbpId+JOK7FH7EyDMUfpyjT5JzolwIpN4I3EstuU0Rv77cQe2Os3HSy7VyXGZu3I85nWZaQhvPPWIyV9dblXetaVZ2ytt+lrafcwnzplw9No8AAggggAACQwj4M1D4H54O/V3H33/C/BOGKJesCCCAAAIIIIAAAggggAACNQv4B6U3UvgurTcqPqO4RBG+tI07/I7KOk7hu8E2Ufj3weJn8GuShECvBX6g1qWvo1+M0eKHZspLy/frri3pMapIWr+iaZ8wmrVO8vkDfPbXchICCCCAAAIIdEtgvqqb+7zzXs1fUvF+xU8UfloGCQEEEEAAAQQQQACBzgss2vkW0AAEFhTwMb2+wiert1f4bhTffeY7YpZX+Iudv/TdpLhOcbXiIsU/FOcobpkLDUgIzLSAf3PsmRmBazTv3Qq/ZtxhNl/hdIbir/8aW/DPcpo8SHH8grOzU74j06/JtiS/h/yyYmV+pHz+fTU/crXvye+nPg7KEp8vynRYhgACCCCAQHsFDlXVPpap3oGa9wmFv2f592K/piAhgAACCCCAAAIIIIAAAggggAACvRPI/Q5Z7oridN7HJfEyhe/uPERxmSLNk5v+qvK1Ma2tSuXqm5vnjve3KNyB1NfkDs9LFbn2h3nb9LXxtAsBBBBAAIEZEThP7Qz/18Pw9mhe7iKqGaGhmQgggAACCCCAAAIIIIAAAgggMAsCH1Ejw0mRpofLtBjUd0PlHjlZZvIareO7V/uWfqgGlbX76L41mPYggAACCCAwgwJFFwidKovXK3j0/AweFDQZAQQQQAABBBBAAAEEEEAAgVkSWE+NvVZR1iFSx7KdO4K65wgWx2qde3ekfWXVXFMLv68o298XazknzIRAQgABBBBAoAcC/i3mov/7Xfns1oPdQBMQQAABBBBAAAEEEEAAAQQQQGBaAr4LqslOskdNq2EjbndVrecrp4tOGBXNP0XrzFd0MfmRkT9XFLXN8y9RLKsgIYAAAggggEA/BHwH/Z8Vuf//dJD1Yx/TCgQQQAABBBBAAAEEEEAAAQQQGCDgEyS+e+ocRe4kyajzHjxgu21ePE+Ve53icsUw7T9X+XdT2LQLaV9Vskr7VupCY6gjAggggAACCAwlsLly5z4H+LMMCQEEEEAAAQQQQAABBBBAAAEEEJgpgdXU2icrPqm4U5E7aTJo3mVab0lFH5LvrnqLYlCbc8vfpPU2bCnC+qrXLyq06y/KM6+lbaBaCCCAAAIIIDC+QO7O+atV7FLjF00JCCCAAAIIIIAAAggggAACCCCAQDcF1lK13Vl2siLXAZTO+7XyPVqxnKJvySeJ3qtI21x12p1s2yuWVkwjraiN7qh4u6JqnX33HL85JgQSAggggAACPRbwZ5PcRVFv7HGbaRoCCCCAAAIIIIAAAggggAACCCAwlMBGyv00hR/FeKPCHS2+w+goxTaKrjxWUFUdOdngbEXVTqZcvku1/pGK+ynqMltdZa0xV6avBD9ecaoit/0q8z6mdddUkBBAAAEEEECg/wIPURNznw/8WYWEAAIIIIAAAggggEBnBeo68dZZACqOAAIIIIBAAwL+zY7/U/iRlOMkdzBeqXBZlyh+qfiDwo828tXcafL/9Y0U7pCcp9hpbriLhnX9z3+fynqxgoQAAggggAACsyPwKzV126S5P9b07oo7kvlMIoAAAggggAACCCCAAAIIIIAAAgjMuMAmav9FitxV112cd4DawmMVZ/ygpvkIIIAAAjMp8DC1+m5F+vnljTOpQaMRQAABBBBAAAEEEEAAAQQQQAABBCoJrKJcb1akJ5W6Mu272O5bqaVkQgABBBBAAIE+CuynRuU6yPxZxr/FSkIAAQQQQAABBBBAAAEEEEAAAQQQQKBQYAkt8e94fF/Rhc6xu1TPRytICCCAAAIIIDDbAl9S84s+u5ypZUvONg+tRwABBBBAAAEEEEAAAQQQQAABBBAYRmC+Mr9QcYriOkXRiadJzr9d9XiLwr+jRkIAAQQQQAABBCzwIIU/j5youGBuPP58spfmkRBAAAEEEEAAAQQQ6JTAop2qLZVFAAEEEECg3wLLqnm7KtZRrKZ4iuJ+irrSzSroLMXvFVcorlb8VnHb3PBWDUkIIIAAAggggEAq8CPN2GVu5hM1/FyS4Quafp7ib8l8JhFAAAEEEEAAAQQQQAABBBBAAAEEEBhJwBez7KB4leKjCt/hFV+xnRt3ni8q3qp4sGJtxeoKEgIIIIAAAgggMIrAs7WSP3Ocrlhe4ccqpp9BTtA8EgIIIIAAAggggAACCCCAAAIIIIAAAo0KrKTSV1FsMhcraricgoQAAggggAACCNQt8HEV6A6xMxS+eGcpxa8UaSfZPM0jIYAAAggggAACCCCAAAIIIIAAAggggAACCCCAAAIIINB5gW+pBe4MO08RfqrBj1RMO8jO17wlFSQEEEAAAQQQQAABBBBAAAEEEEAAAQQQQAABBBBAAAEEOivgDjE/5tmdYe+PWuH5H5ubH3eUPT/KwygCCCCAAAIIIIAAAggggAACCCBQi4AfZ3Oo4qy5OERDzyMhgAACCCCAAAIIINCEwBIq9CaFO8EuSzbg3zm9eW5Z3Em2fpKPSQQQQAABBBBAAAEEEEAAAQQQQGAsgaO0dnzyweOeR0IAAQQQQAABBBBAoAkBd5B9V+HPnUdkNvDQuWXxZ9RLNc93mJEQQAABBBBAAAEEEEAAAQQQQACBWgSuUinxyQePex4JAQQQQAABBBBAAIEmBDZQoeHz528LNvC/UZ6Qd5+CvMxGAAEEEEAAAQQQQAABBBBAAAEEhhagg2xoMlZAAAEEEEAAAQQQGENgOa17g8IdXy8uKGf5ueWhcywMly7Iz2wEEEAAAQQQQAABBKYusNjUa0AFEEAAAQSGEfAPpKcpNy/NwzQCCCCAAAIIIIAAAqMIbK2VVphb8REFBfg3yl6UWXZEZh6zEEAAAQQQQAABBBBAAAEEEEAAgaEFltIahyrOmotDNPQ8EgIIIIAAAggggAACTQisrULDHWFPHbCBq6O8YZ3FB6zDYgQQQAABBBBAAAEEEEAAAQQQQAABBBBAAAEEEEAAAQRaJfBI1SZ0dr13QM12ivKGdYoeyzigKBYjgAACCCCAAAIIIIAAAggggAACCCCAAAIIIIAAAgggMB2B7bTZ0NnlzrJBKeSNh0sOWonlCCCAAAIIIIAAAghMWoDfIJu0ONtDAAEEEEAAAQQQQAABBBBAoDsC60dVDb9FFs1aaHSzheYssshjM/OYhQACCCCAAAIIIIDAVAXoIJsqPxtHAAEEEEAAAQQQQAABBBBAoNUCW0e1uz0aLxo9Xwt+lSw8NplmEgEEEEAAAQQQQACBqQvQQTb1XUAFEEAAAQQQQAABBBBAAAEEEGitwN+imp0bjZeNvjFZuKaml03mMYkAAggggAACCCCAAAIIIIAAAggggAACCCCAAAIIIIBAKwVOU63C74ntU7GGi0frhHWfVnFdsiGAAAIIIIAAAggggAACCCCAAAIIIIAAAggggAACCCAwVYGTtPXQybXyEDV5T7Se179iiHXJigACCCCAAAIIIIAAAggggAACCCCAAAIIIIAAAggggMDUBM7TlkMH2QpD1GKbaL2w/hCrkxUBBBBAAAEEEEAAAQQQQAABBBBAAAEEEEAAAQQQQACB6QjcpM2GDq6lhqjCEtF6Yf35Q6xPVgQQQAABBBBAAAEEGhVYrNHSKRwBBBBAAAEEEEAAAQQQQAABBLoq4HMGy0WVvzMaHzTqvD9MMh2QTDOJAAIIIIAAAggggMDUBOggmxo9G0YAAQQQQAABBBBAAAEEEECg1QKLR7W7VeN3R9NVRo9PMj0omWYSAQQQQAABBBBAAAEEEEAAAQQQQAABBBBAAAEEEEAAgVYJbKjahMcj/nmEmq0Wre9y/j5CGayCAAIIIIAAAggggEAjAtxB1ggrhSKAAAIIIIAAAggggAACCCDQeYH4kYo/GKE112udf0TrucNs0WiaUQQQQAABBBBAAAEEpiZAB9nU6NkwAggggAACCCCAAAIIIIAAAq0W2DKq3RLReNXRO5TxS0nmfZJpJhFAAAEEEEAAAQQQmIoAHWRTYWejCCCAAAIIIIAAAggggAACCLReYP2ohldG48OMXpdk3jyZZhIBBBBAAAEEEEAAgakI0EE2FXY2igACCCCAAAIIIIAAAggggEDrBfyIxJC+F0aGHH4kye+7ykgIIIAAAggggAACCCCAAAIIIIAAAggggAACCCCAAAIItFLg/arVP+fi0BFr6Atzb4vKuUrjXKw7IiarIYAAAggggAACCNQnwIfS+iwpCQEEEEAAAQQQQAABBBBAAIE+CawZNebiaHzY0fgxi5yHGFaP/AgggAACCCCAAAKNCPDBtBFWCkUAAQQQQAABBBBAAAEEEECg8wK3Ry04LxofZvRuZT5S4aHTiort/jXGHwQQQAABBBBAAAEEpihAB9kU8dk0AggggAACCCCAAAIIIIAAAi0W2C2qmzu2Rk3rasVw/mEpjT931IJYDwEEEEAAAQQQQACBugTCB9S6yqMcBBBAAAEEEEAAAQQQQAABBBDoh8DKUTMuiMaHHb0kWcGdZCQEEEAAAQQQQAABBBBAAAEEEEAAAQQQQAABBBBAAAEEWiWwqGrzzyg8PWpaSSvGZd2o6WVHLYz1EEAAAQQQQAABBBCoQ4A7yOpQpAwEEEAAAQQQQAABBBBAAAEE+iWwRtSc2zTuDq5Rkx+xGKflNbFFPINxBBBAAAEEEEAAAQQmLUAH2aTF2R4CCCCAAAIIIIAAAggggAAC7Re4OariD6PxUUbPz6y0XGYesxBAAAEEEEAAAQQQmJgAHWQTo2ZDCCCAAAIIIIAAAggggAACCHRGYLWopuOeO7hLZf0yKs+jz0qmmUQAAQQQQAABBBBAYKIC437InWhl2RgCCCCAAAIIIIAAAggggAACCExEYJloK3+Mxkcd/XOy4qOSaSYRQAABBBBAAAEEEJioAB1kE+VmYwgggAACCCCAAAIIIIAAAgh0QuCOqJYXROOjjv42WfFeml42mcckAggggAACCCCAAAITE6CDbGLUbAgBBBBAAAEEEEAAAQQQQACBzgjsHdV05Wh81NGrMyuulJnHLAQQQAABBBBAAAEEJiJAB9lEmNkIAggggAACCCCAAAIIIIAAAp0S+E1U2+9E46OOfiOz4q6ZecxCAAEEEEAAAQQQQGAiAnSQTYSZjSCAAAIIIIAAAggggAACCCDQKYEDo9puE42POpp7nCK/QzaqJushgAACCCCAAAIIIIAAAggggAACCCCAAAIIIIAAAgjULrC/SvznXGxcQ+mLR+WFcn9ZQ7kUgQACCCCAAAIIIIAAAggggAACCCCAAAIIIIAAAggggEAtAl9VKaEj67G1lPif8kK5HpIQQAABBBBAAAEEEEAAAQQQQAABBBBAAAEEEEAAAQQQaIXAs1SL0JG1Sk01CuXFw9yjF2vaHMUggAACCCCAAAIIIIAAAggggAACCCCAAAIIIIAAAgggUF3gF8oaOrK2rL5aac6rojJD2euXrsFCBBBAAAEEEEAAAQQaElisoXIpFgEEEEAAAQQQQAABBBBAAAEEuitw+lzVz9fw4pqacUemnG0z85iFAAIIIIAAAggggEDjAnSQNU7MBhBAAAEEEEAAAQQQQAABBBDonMA+czVeWcPbaqq970pL0wPSGUwjgAACCCCAAAIIIDAJATrIJqHMNhBAAAEEEEAAAQQQQAABBBDolsBf56r7lxqrfWWmrK0z85iFAAIIIIAAAggggEDjAnSQNU7MBhBAAAEEEEAAAQQQQAABBBDolMASqu2dczU+W8O7aqr91Zly9s7MYxYCCCCAAAIIIIAAAggggAACCCCAAAIIIIAAAggggAACExVYQVu7W/FPhTu1FlXUkZ6tQlxmGnWUTRkIIIAAAggggAACCAwlwB1kQ3GRGQEEEEAAAQQQQAABBBBAAIHeC9ykFh4/18qXaOgOrTrS9XUUQhkIIIAAAggggAACCCCAAAIIIIAAAggggAACCCCAAAII1C1wXxUY7vI6p8bC94zKDeXX1flWYzUpCgEEEEAAAQQQQGAWBLiDbBb2Mm1EAAEEEEAAAQQQQAABBBBAoLrARcp6xlz2D1dfbWDO8LtmAzOSAQEEEEAAAQQQQACBpgXoIGtamPIRQAABBBBAAAEEEEAAAQQQ6JbAMqquw+mSewa1/L22oJSlC+YzGwEEEEAAAQQQQAABBBBAAAEEEEAAAQQQQAABBBBAAIGJCDxGWwmPQPxujVvcLCo3lO/hcjVug6IQQAABBBBAAAEEEEAAAQQQQAABBBBAAAEEEEAAAQQQGFpgSa3xEcXfFJsOvXbxCttoUdwxFsY3KV6FJQgggAACCCCAAAIIIIAAAggggAACCCCAAAIIIIAAAgg0L7CtNuHfC3MH1tNr3NwGc2WGjrEwnF/jNigKAQQQQAABBBBAAIFKAvwGWSUmMiGAAAIIIIAAAggggAACCCAwMwLrqqWLz7XWnVp1pbsLClqqYD6zEUAAAQQQQAABBBBAAAEEEEAAAQQQQAABBBBAAAEEEJiIgC+mPVJxnGKZGrd4H5UV7hqLhzvXuA2KQgABBBBAAAEEEEAAAQQQQAABBBBAAAEEEEAAAQQQQGBogSdojdCB5fG60poqKJQbD7evawOUgwACCCCAAAIIIIBAVQEesVhVinwIIIAAAggggAACCCCAAAIIIDCOwLIFKy9fMJ/ZCCCAAAIIIIAAAgg0JrBEYyVTMAIIIIAAAggggAACCCCAAAIIdFHgG6r0DxSXK75cYwOKLtLl3ESNyBSFAAIIIIAAAggggAACCCCAAAIIIIAAAggggAACCCAwvMDRWiU8AvGJw69euMZqUbmhfA8fWLgGCxBAAAEEEEAAAQQQaEig6OqthjZHsQgggAACCCCAAAIIIIAAAggg0HKBX8/V7zYNz62xrmsUlHWvgvnMRgABBBBAAAEEEECgMQE6yBqjpWAEEEAAAQQQQAABBBBAAAEEOilw4Vytf6LhxTW24MqCsq4tmM9sBBBAAAEEEEAAAQQQQAABBBBAAAEEEEAAAQQQQAABBCYi8GNtJTwC8ak1bnGzqNxQvof71rgNikIAAQQQQAABBBBAAAEEEEAAAQQQQAABBBBAAAEEEEBgaIH9tIY7rn6jWHHotYtXWEGL4o6xML5L8SosQQABBBBAAAEEEECgGQEesdiMK6UigAACCCCAAAIIIIAAAggg0FWBF81VfGsNV6+xEUW/QVbnNmqsLkUhgAACCCCAAAII9FmADrI+713ahgACCCCAAAIIIIAAAggggMDwAhfPrXKHhnX+PtjlBVX5R8F8ZiOAAAIIIIAAAggg0JgAHWSN0VIwAggggAACCCCAAAIIIIAAAp0UWGuu1rdreEuNLVizoKz1CuYzGwEEEEAAAQQQQACBxgToIGuMloIRQAABBBBAAAEEEEAAAQQQ6KTApnO1Xl7DJWpswV8KyiqaX5Cd2QgggAACCCCAAAIIjC9AB9n4hpSAAAIIIIAAAggggAACCCCAQF8EFlVDFp9rzK0a1nkH2WoFSJsVzGc2AggggAACCCCAAAIIIIAAAggggAACCCCAAAIIIIAAAo0LuIPsn1HUeQeZL9KNyw7jD2u8VWwAAQQQQAABBBBAAIFEgDvIEhAmEUAAAQQQQAABBBBAAAEEEJhhgfg8wU1yuLNGC3e+5dLGuZnMQwABBBBAAAEEEECgSYH4g2+T26FsBBBAAAEEEEAAAQQQQAABBBDolkB41GJdtb67oKCbC+YzGwEEEEAAAQQQQACBxgToIGuMloIRQAABBBBAAAEEEEAAAQQQ6JxAfDdX3ecM/EjFXKp7O7ltMA8BBBBAAAEEEEAAgQUE+BC6AAcTCCCAAAIIIIAAAggggAACCMy0wHVR66+Nxusazd0ttnldhVMOAggggAACCCCAAAJVBeggqypFPgQQQAABBBBAAAEEEEAAAQT6L7BN1MRlovG6RpfNFHReZh6zEEAAAQQQQAABBBBoVIAOskZ5KRwBBBBAAAEEEEAAAQQQQACBTglcGNX2mmi8rtFLMwVxB1kGhVkIIIAAAggggAACzQrQQdasL6UjgAACCCCAAAIIIIAAAggg0CWB+K6xuxqoeK7TbcUGtkORCCCAAAIIIIAAAgiUCtBBVsrDQgQQQAABBBBAAAEEEEAAAQRmSuABUWtzj0OMFo80ekFmrYsy85iFAAIIIIAAAggggECjAnSQNcpL4QgggAACCCCAAAIIIIAAAgh0SiB+xOINDdT8n5kyd87MYxYCCCCAAAIIIIAAAo0K0EHWKC+FI4AAAggggAACCCCAAAIIINApgZWi2i4ajdc1musgW6quwikHAQQQQAABBBBAAIGqAnSQVZUiHwIIIIAAAggggAACCCCAAAL9F9g0amITj1iM71ALm1ohjDBEAAEEEEAAAQQQQGBSAnSQTUqa7SCAAAIIIIAAAggggAACCCDQfoH4N8LuaKC622XKfJjmcX4iA8MsBBBAAAEEEEAAgeYE+ADanC0lI4AAAggggAACCCCAAAIIINA1gXtFFV4iGq9rNH6EYyjTj3LMPXoxLGeIAAIIIIAAAggggEDtAnSQ1U5KgQgggAACCCCAAAIIIIAAAgh0VmDNqOa5zqxo8UijRZ1uG45UGishgAACCCCAAAIIIDCiAB1kI8KxGgIIIIAAAggggAACCCCAAAI9FDgnatPK0Xhdo0XnITarawOUgwACCCCAAAIIIIBAFYGiD6ZV1iUPAggggAACCCCAAAIIIIAAAgj0S2C1qDlXR+N1jW5TUFATnXEFm2I2AggggAACCCCAAAL8CC7HAAIIIIAAAggggAACCCCAAAII/Efg0v+MLhJ3lkWzxxr9Y8HaOxfMZzYCCCCAAAIIIIAAAo0IcAdZI6wUigACCCCAAAIIIIAAAggggEAnBYp+I6yuxty3oKA9C+YzGwEEEEAAAQQQQACBRgToIGuElUIRQAABBBBAAAEEEEAAAQQQ6KTATUmt6z5v8I+k/DC5URhhiAACCCCAAAIIIIDAJATq/qA7iTqzDQQQQAABBBBAAAEEEEAAAQQQaEbghqTYfybT406uWlDAigXzmY0AAggggAACCCCAQCMCdJA1wkqhCCCAAAIIIIAAAggggAACCHRS4M6k1isk00wigAACCCCAAAIIINALATrIerEbaQQCCCCAAAIIIIAAAggggAACtQjcnpRyVzLd5OTiTRZO2QgggAACCCCAAAIIxAJ0kMUajCOAAAIIIIAAAggggAACCCAw2wLXJM0veiRikq2WyWVqKYVCEEAAAQQQQAABBBCoIEAHWQUksiCAAAIIIIAAAggggAACCCAwIwJph9h6E2z3hhPcFptCAAEEEEAAAQQQmHEBOshm/ACg+QgggAACCCCAAAIIIIAAAghEApdE4x79ezLd5OTqTRZO2QgggAACCCCAAAIIxAJ0kMUajCOAAAIIIIAAAggggAACCCAw2wJrJc1/dDLd5OT6TRZO2QgggAACCCCAAAIIxAJ0kMUajCOAAAIIIIAAAggggAACCCAw2wJ/VfOvigjOiMabHl2h6Q1QPgIIIIAAAggggAACQYAOsiDBEAEEEEAAAQQQQAABBBBAAAEE/imCayOGvaPxpkcn+XtnTbeF8hFAAAEEEEAAAQRaLkAHWct3ENVDAAEEEEAAAQQQQAABBBBAYIICi2pbq0Xb2yAab3r0lqY3QPkIIIAAAggggAACCAQBOsiCBEMEEEAAAQQQQAABBBBAAAEEEPAdZO9Q3Kjw4xa/rphUWnJSG2I7CCCAAAIIIIAAAgjQQcYxgAACCCCAAAIIIIAAAggggAACscAjNOHfA1tL8fJ4QcPjNzVcPsUjgAACCCCAAAIIIPBvATrI/k3BCAIIIIAAAggggAACCCCAAAIITFHg+ilum00jgAACCCCAAAIIzJgAHWQztsNpLgIIIIAAAggggAACCCCAAAIDBD4dLb8gGm969LqmN0D5CCCAAAIIIIAAAggggAACCCCAAAIIIIAAAggggAACCOQEvqCZ/i0yh3+LbHFFXSmUmxvuVddGKAcBBBBAAAEEEEAAgUEC3EE2SIjlCCCAAAIIIIAAAggggAACCMyWwJ+j5i6r8bui6SZH/9Rk4ZSNAAIIIIAAAggggEAsQAdZrME4AggggAACCCCAAAIIIIAAAghcGxH4vMGS0fQ4o8sNWHmpActZjAACCCCAAAIIIIBAbQJ0kNVGSUEIIIAAAggggAACCCCAAAII9EJgvaQVgzq2kuyFk4PuRLu4cE0WIIAAAggggAACCCBQswAdZDWDUhwCCCCAAAIIIIAAAggggAACHRe4Jqn/oI6tJHvh5OaFS+5ZcPuA5SxGAAEEEEAAAQQQQKA2ATrIaqOkIAQQQAABBBBAAAEEEEAAAQR6IbBC0or0jrJkceXJtOMtXbGujri0XKYRQAABBBBAAAEEEFhIgA6yhUiYgQACCCCAAAIIIIAAAggggMBMC9yQtH7ZZHrUya1HXZH1EEAAAQQQQAABBBCoW4AOsrpFKQ8BBBBAAAEEEEAAAQQQQACBbgukHWRb1dScVUrK+V3JMhYhgAACCCCAAAIIIFC7AB1ktZNSIAIIIIAAAggggAACCCCAAAKdFrg+qf0uyfSok/8sWfHmkmUsQgABBBBAAAEEEECgdgE6yGonpUAEEEAAAQQQQAABBBBAAAEEOi1wZlL7Q5LpUSd3KFnx9yXLWIQAAggggAACCCCAQO0CdJDVTkqBCCCAAAIIIIAAAggggAACCHRaIH3Eon+DrI7fIVu1ROXvJctYhAACCCCAAAIIIIBA7QJ0kNVOSoEIIIAAAggggAACCCCAAAIIdFrgvEztn5KZN+yse5escGHJMhYhgAACCCCAAAIIIIAAAggggAACCCCAAAIIIIAAAggg0LiAH7Po3wyLY9yLbOOy0vHXNN4iNoAAAggggAACCCCAQCQw7ofbqChGEUAAAQQQQAABBBBAAAEEEECgJwLfyLTjIZl5VWctPiDjnQOWsxgBBBBAAAEEEEAAAQQQQAABBBBAAAEEEEAAAQQQQACBRgU2UenpXV5/0bylRtzqVpny4vIPGbFcVkMAAQQQQAABBBBAYCQB7iAbiY2VEEAAAQQQQAABBBBAAAEEEOi1wAVq3fVJC9fV9KOTeVUndxuQ8br/394dq0YRRWEAZpMghhAQjC8gBIkhNvoEPkCKPIC9YGOdV4iQNm36lNYJpEkpFtYW+gqSIkX+KyxchhlnZ3DdMXwX/uTOzJ0zd772sLs9110mQIAAAQIECBAgQIAAAQIECBAgQIAAAQIECBAgsHSBD3lC/SmvMr9NXox48peWWnXtlyNquoUAAQIECBAgQIAAAQIECBAgQIAAAQIECBAgQIDAXxXYTLVvSd3IKvObZJYMGc0azeOdIcWsJUCAAAECBAgQIECAAAECBAgQIECAAAECBAgQILAsgZMUbjazyvFZsmiT7HVHjbpulhgECBAgQIAAAQIECBAgQIAAAQIECBAgQIAAAQIEVi9Qvk6xbmQ15+U3ybZ6ttm8p3n8ved+lwkQIECAAAECBAgQIECAAAECBAgQIECAAAECBAj8U4H3eVqzqdV2fJx1b5P9ZC0p4yhpW1ufe/d7pT8ECBAgQIAAAQIECBAgQIAAAQIECBAgQIAAAQIEJiLwKPv4kdRNrb75XdZ/WvCe9awzCBAgQIAAAQIECBAgQIAAAQIECBAgQIAAAQIECExKYDu76WuKjbl+Oqm3tBkCBAgQIECAAAECBAgQIECAAAECBAgQIECAAAEClcCTzD8nYxphXfdsVPVNCRAgQIAAAQIECBAgQIAAAQIECBAgQIAAAQIECExS4FV21dXwGnL+cJJvZ1MECBAgQIAAAQIECBAgQIAAAQIECBAgQIAAAQIEOgR2c/4iGdIUm6+97KjpNAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAIHJC5SvSSyfBvuazBtgf/r/M+ueJgYBAgQIECBAgAABAgQIECBAgAABAgQIECBAgACB/1pgLbs/SM6TtgbZr5z/mDxLDAIECBAgQIAAAQIrFZit9OkeToAAAQIECBAgQIAAAQIECDxEgcd5qTfJ82QvuU6uktIkMwgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIEDgoQrcA9Ykf548JTyhAAAAAElFTkSuQmCC",
      "description" : "signed on: 2017-12-19T12:33:40-05:00",
      "document_status" : "1",
      "encoding_type" : "",
      "mime" : "image/png",
      "patient_id" : "100",
      "title" : "Patient Signature"
   },
   "method" : "PUT",
   "query" : {
      "category" : "transactional record",
      "data" : "data:image/png;base64,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Oqm3tBkCBAgQIECAAAECBAgQIECAAAECBAgQIECAAAEClcCTzD8nYxphXfdsVPVNCRAgQIAAAQIECBAgQIAAAQIECBAgQIAAAQIECExS4FV21dXwGnL+cJJvZ1MECBAgQIAAAQIECBAgQIAAAQIECBAgQIAAAQIEOgR2c/4iGdIUm6+97KjpNAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAIHJC5SvSSyfBvuazBtgf/r/M+ueJgYBAgQIECBAgAABAgQIECBAgAABAgQIECBAgACB/1pgLbs/SM6TtgbZr5z/mDxLDAIECBAgQIAAAQIrFZit9OkeToAAAQIECBAgQIAAAQIECDxEgcd5qTfJ82QvuU6uktIkMwgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIEDgoQrcA9Ykf548JTyhAAAAAElFTkSuQmCC",
      "description" : "signed on: 2017-12-19T12:33:40-05:00",
      "document_status" : "1",
      "encoding_type" : "",
      "mime" : "image/png",
      "patient_id" : "100",
      "title" : "Patient Signature"
   }
}

```	
> Result

```json
{
   "args" : {},
   "data_id" : "30674",
   "messages" : [
      {
         "icon" : "fa fa-file",
         "message" : "Successfully added document!",
         "type" : "success"
      }
   ],
   "success" : 1
}

```	


### HTTP Request
PUT /api/pharmetika/:version/patient/:patient_id/document

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## patient put document

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
POST /api/pharmetika/:version/patient/:patient_id/document

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## patient get document

> Arguments

```json
{
   "json" : {},
   "method" : "GET",
   "query" : {}
}

```	
> Result

```json

```	


### HTTP Request
GET /api/pharmetika/:version/patient/:patient_id/document/:document_id

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## get patient addresses

> Arguments

```json
{
   "json" : {},
   "method" : "GET",
   "query" : {}
}

```	
> Result

```json

```	


### HTTP Request
GET /api/pharmetika/:version/patient/:patient_id/addresses

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## add patient addresses

> Arguments

```json
{
   "json" : {
      "address_type" : "alternate",
      "city" : "Port Saint Joe",
      "country" : "US",
      "line_1" : "Beverly Edwards",
      "line_2" : "Attn: RV Park",
      "line_3" : "1700 US 98",
      "patient_id" : "",
      "postal_code" : "32456",
      "state" : "FL"
   },
   "method" : "PUT",
   "query" : {
      "address_type" : "alternate",
      "city" : "Port Saint Joe",
      "country" : "US",
      "line_1" : "Beverly Edwards",
      "line_2" : "Attn: RV Park",
      "line_3" : "1700 US 98",
      "patient_id" : "",
      "postal_code" : "32456",
      "state" : "FL"
   }
}

```	
> Result

```json
{
   "address_added" : {
      "id" : "115500472",
      "rows" : 1,
      "success" : 1
   },
   "messages" : [
      {
         "message" : "Address added successfully",
         "type" : "success"
      }
   ]
}

```	


### HTTP Request
PUT /api/pharmetika/:version/patient/:patient_id/addresses

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## add patient addresses dates

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
PUT /api/pharmetika/:version/patient/:patient_id/addresses/:address_id/dates/:address_date_id

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## add patient addresses dates

> Arguments

```json
{
   "json" : {
      "address_date_id" : "794",
      "address_id" : "54415228",
      "start_date" : "2017-12-13",
      "stop_date" : "2017-12-29"
   },
   "method" : "POST",
   "query" : {
      "address_date_id" : "794",
      "address_id" : "54415228",
      "start_date" : "2017-12-13",
      "stop_date" : "2017-12-29"
   }
}

```	
> Result

```json
{
   "address_added" : {
      "id" : "794",
      "rows" : 1,
      "success" : 1
   },
   "messages" : [
      {
         "message" : "Address dates added successfully",
         "type" : "success"
      }
   ]
}

```	


### HTTP Request
POST /api/pharmetika/:version/patient/:patient_id/addresses/:address_id/dates/:address_date_id

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## remove patient addresses dates

> Arguments

```json
{
   "json" : {},
   "method" : "DELETE",
   "query" : {
      "address_date_id" : "782",
      "address_id" : "49849474"
   }
}

```	
> Result

```json
{
   "address_added" : {
      "id" : "782",
      "rows" : "0E0",
      "success" : 1
   },
   "messages" : [
      {
         "message" : "Address dates removed successfully",
         "type" : "success"
      }
   ]
}

```	


### HTTP Request
DELETE /api/pharmetika/:version/patient/:patient_id/addresses/:address_id/dates/:address_date_id

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## get patient messages

> Arguments

```json
{
   "json" : {},
   "method" : "GET",
   "query" : {}
}

```	
> Result

```json
{
   "messages" : []
}

```	


### HTTP Request
GET /api/pharmetika/:version/patient/:patient_id/messages

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## get patient messages

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
POST /api/pharmetika/:version/patient/:patient_id/messages

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## get patient action items

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
GET /api/pharmetika/:version/patient/:patient_id/action_items

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## get patient action items

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
POST /api/pharmetika/:version/patient/:patient_id/action_items

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## get patient contact log

> Arguments

```json
{
   "json" : {},
   "method" : "GET",
   "query" : {}
}

```	
> Result

```json
{
   "contacts" : [],
   "success" : true
}

```	


### HTTP Request
GET /api/pharmetika/:version/patient/:patient_id/contact_log

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## get patient contact log

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
POST /api/pharmetika/:version/patient/:patient_id/contact_log

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## get patient call records

> Arguments

```json
{
   "json" : {},
   "method" : "GET",
   "query" : {}
}

```	
> Result

```json
{
   "cdrs" : [],
   "success" : true
}

```	


### HTTP Request
GET /api/pharmetika/:version/patient/:patient_id/call_records

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## get patient profile keys

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
GET /api/pharmetika/:version/patient/:patient_id/profile

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## get patient profile key

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
GET /api/pharmetika/:version/patient/:patient_id/profile/:key

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## update patient profile keys

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
PUT /api/pharmetika/:version/patient/:patient_id/profile/:key

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## update patient profile keys

> Arguments

```json
{
   "json" : {
      "value" : "0"
   },
   "method" : "POST",
   "query" : {
      "value" : "0"
   }
}

```	
> Result

```json
{
   "args" : {},
   "messages" : [
      {
         "icon" : "glyphicon glyphicon-user",
         "message" : "Profile Updated!",
         "type" : "success"
      }
   ],
   "success" : true
}

```	


### HTTP Request
POST /api/pharmetika/:version/patient/:patient_id/profile/:key

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## patient prescription history

> Arguments

```json
{
   "json" : {},
   "method" : "GET",
   "query" : {}
}

```	
> Result

```json
{
   "error" : "Not authorized."
}

```	


### HTTP Request
GET /api/pharmetika/:version/patient/:patient_id/prescription_history

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## patient prescription history

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
POST /api/pharmetika/:version/patient/:patient_id/prescription_history

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## get patient tasks

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
GET /api/pharmetika/:version/patient/:patient_id/tasks

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## get patient tasks

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
POST /api/pharmetika/:version/patient/:patient_id/tasks

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## charts

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
GET patient/:patient_id/charts

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## charts

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
POST patient/:patient_id/charts

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## chart prescription count

> Arguments

```json
{
   "json" : {},
   "method" : "GET",
   "query" : {}
}

```	
> Result

```json

```	


### HTTP Request
GET /api/pharmetika/:version/charts/prescription_count/:days_ago

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## chart new patient count

> Arguments

```json
{
   "json" : {},
   "method" : "GET",
   "query" : {}
}

```	
> Result

```json

```	


### HTTP Request
GET /api/pharmetika/:version/charts/new_patient_count/:days_ago

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## chart prescription fill history yoy

> Arguments

```json
{
   "json" : {},
   "method" : "GET",
   "query" : {}
}

```	
> Result

```json

```	


### HTTP Request
GET /api/pharmetika/:version/charts/prescription_fill_history_yoy

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## view refill

> Arguments

```json
{
   "json" : {
      "annotation" : ""
   },
   "method" : "GET",
   "query" : {
      "annotation" : ""
   }
}

```	
> Result

```json

```	


### HTTP Request
GET /api/pharmetika/:version/prescription/:rxn/refill/view

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## view refill

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
POST /api/pharmetika/:version/prescription/:rxn/refill/view

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## send refill

> Arguments

```json
{
   "json" : {},
   "method" : "GET",
   "query" : {}
}

```	
> Result

```json
{
   "messages" : [
      {
         "message" : "Successfully faxed to: 5745393581 for 3392669",
         "type" : "success"
      }
   ],
   "render_args" : {
      "RxN" : "3392669",
      "annotation" : null,
      "internal" : null,
      "secondFax" : null
   },
   "rxn" : "3392669"
}

```	


### HTTP Request
GET /api/pharmetika/:version/prescription/:rxn/refill/send

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## send refill

> Arguments

```json
{
   "json" : {},
   "method" : "POST",
   "query" : {
      "annotation" : "",
      "fax" : "true",
      "rxn" : "3391834"
   }
}

```	
> Result

```json
{
   "messages" : [
      {
         "message" : "Successfully faxed to: 9146588977 for 3391834",
         "type" : "success"
      }
   ],
   "render_args" : {
      "RxN" : "3391834",
      "annotation" : "",
      "internal" : null,
      "secondFax" : null
   },
   "rxn" : "3391834"
}

```	


### HTTP Request
POST /api/pharmetika/:version/prescription/:rxn/refill/send

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## add to autoship

> Arguments

```json
{
   "json" : {
      "rxn" : 3414517
   },
   "method" : "PUT",
   "query" : {}
}

```	
> Result

```json
{
   "messages" : [
      {
         "html" : 1,
         "msg" : "3414517 was previously on autoship! Next fill date of: ",
         "type" : "warning"
      }
   ],
   "next_fill_date" : null,
   "success" : true
}

```	


### HTTP Request
PUT /api/pharmetika/:version/prescription/:rxn/autoship/add

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## add to autoship

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
POST /api/pharmetika/:version/prescription/:rxn/autoship/add

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## update autoship

> Arguments

```json
{
   "json" : {
      "_autoship_options_prior_auth_date_expiration" : "",
      "autoship_day_supply_start" : "2017-12-22",
      "program" : "day_supply",
      "resume_date" : "",
      "rxn" : "3410313"
   },
   "method" : "POST",
   "query" : {}
}

```	
> Result

```json
{
   "args" : {
      "options" : {}
   },
   "messages" : [
      {
         "msg" : " was updated!",
         "type" : "success"
      }
   ],
   "next_fill_date" : null,
   "success" : true
}

```	


### HTTP Request
POST /api/pharmetika/:version/prescription/:rxn/autoship/update

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## remove from autoship

> Arguments

```json
{
   "json" : {
      "rxn" : 3405035
   },
   "method" : "DELETE",
   "query" : {}
}

```	
> Result

```json
{
   "next_fill_date" : null,
   "rxn" : "3405035",
   "success" : true
}

```	


### HTTP Request
DELETE /api/pharmetika/:version/prescription/:rxn/autoship/remove

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## add autoship note

> Arguments

```json
{
   "json" : {
      "note_text" : "postpone PDX A/S also to 2/16/18",
      "note_type" : "patient-priority",
      "rxn" : "3412976"
   },
   "method" : "PUT",
   "query" : {}
}

```	
> Result

```json
{
   "messages" : [
      {
         "icon" : "glyphicon glyphicon-pencil",
         "message" : "Note Added!",
         "type" : "success"
      }
   ],
   "note_count" : 3,
   "note_id" : "0",
   "success" : true
}

```	


### HTTP Request
PUT /api/pharmetika/:version/prescription/:rxn/autoship/note

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## add autoship note

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
POST /api/pharmetika/:version/prescription/:rxn/autoship/note

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## archive autoship note

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
DELETE /api/pharmetika/:version/prescription/:rxn/autoship/note/:note_id

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## unarchive autoship note

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
POST /api/pharmetika/:version/prescription/:rxn/autoship/note/:note_id

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## view rx autoship notes

> Arguments

```json
{
   "json" : {},
   "method" : "GET",
   "query" : {
      "patient_id" : "66672"
   }
}

```	
> Result

```json
{
   "notes" : [
      {
         "author" : "user_dvo",
         "date_created" : "2017-12-06 14:33:00",
         "id" : 1620,
         "note_status" : 1,
         "note_text" : "pt wants 60 gm shipped every 90 days",
         "note_type" : "patient-priority",
         "patient_id" : 66672,
         "rxn" : 3424624
      }
   ],
   "success" : true
}

```	


### HTTP Request
GET /api/pharmetika/:version/prescription/:rxn/autoship/notes

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## view all autoship notes

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
GET /api/pharmetika/:version/prescription/:rxn/autoship/notes/all

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## autoship calendar

> Arguments

```json
{
   "json" : {},
   "method" : "GET",
   "query" : {
      "from" : "1512108000000",
      "to" : "1514786400000"
   }
}

```	
> Result

```json
{
   "result" : [
      {
         "class" : "event-important",
         "end" : 1513159201000,
         "id" : 3416856,
         "start" : 1513159200000,
         "title" : "Butler, Paul - 3416856",
         "url" : "javascript:open_patient_chart(59990)"
      },
      {
         "class" : "event-success",
         "end" : 1513072801000,
         "id" : 3417592,
         "start" : 1513072800000,
         "title" : "Fowler, Doris - 3417592",
         "url" : "javascript:open_patient_chart(14196)"
      },
      {
         "class" : "event-success",
         "end" : 1513418401000,
         "id" : 3417799,
         "start" : 1513418400000,
         "title" : "Ellis, Paul - 3417799",
         "url" : "javascript:open_patient_chart(70480)"
      },
      {
         "class" : "event-success",
         "end" : 1513418401000,
         "id" : 3417800,
         "start" : 1513418400000,
         "title" : "Ellis, Paul - 3417800",
         "url" : "javascript:open_patient_chart(70480)"
      },
      {
         "class" : "event-important",
         "end" : 1514714401000,
         "id" : 3417944,
         "start" : 1514714400000,
         "title" : "Matthews, Gloria - 3417944",
         "url" : "javascript:open_patient_chart(26228)"
      },
      {
         "class" : "event-success",
         "end" : 1514455201000,
         "id" : 3418801,
         "start" : 1514455200000,
         "title" : "Williams, Linda - 3418801",
         "url" : "javascript:open_patient_chart(11068)"
      },
      {
         "class" : "event-important",
         "end" : 1514196001000,
         "id" : 3420527,
         "start" : 1514196000000,
         "title" : "Hansen, Jennifer - 3420527",
         "url" : "javascript:open_patient_chart(7966)"
      },
      {
         "class" : "event-important",
         "end" : 1512468001000,
         "id" : 3420643,
         "start" : 1512468000000,
         "title" : "Rice, Jose - 3420643",
         "url" : "javascript:open_patient_chart(34190)"
      },
      {
         "class" : "event-important",
         "end" : 1514714401000,
         "id" : 3421401,
         "start" : 1514714400000,
         "title" : "Hansen, Jennifer - 3421401",
         "url" : "javascript:open_patient_chart(7966)"
      },
      {
         "class" : "event-important",
         "end" : 1513764001000,
         "id" : 3421570,
         "start" : 1513764000000,
         "title" : "Tucker, Larry - 3421570",
         "url" : "javascript:open_patient_chart(71226)"
      },
      {
         "class" : "event-important",
         "end" : 1514800801000,
         "id" : 3421906,
         "start" : 1514800800000,
         "title" : "Hunter, Matthew - 3421906",
         "url" : "javascript:open_patient_chart(11520)"
      },
      {
         "class" : "event-important",
         "end" : 1513936801000,
         "id" : 3422573,
         "start" : 1513936800000,
         "title" : "Perkins, Carlos - 3422573",
         "url" : "javascript:open_patient_chart(12022)"
      },
      {
         "class" : "event-important",
         "end" : 1513764001000,
         "id" : 3422908,
         "start" : 1513764000000,
         "title" : "Tucker, Larry - 3422908",
         "url" : "javascript:open_patient_chart(71226)"
      },
      {
         "class" : "event-success",
         "end" : 1514800801000,
         "id" : 3422918,
         "start" : 1514800800000,
         "title" : "Thompson, Brian - 3422918",
         "url" : "javascript:open_patient_chart(67202)"
      },
      {
         "class" : "event-success",
         "end" : 1513850401000,
         "id" : 3423618,
         "start" : 1513850400000,
         "title" : "Clark, Diana - 3423618",
         "url" : "javascript:open_patient_chart(70132)"
      },
      {
         "class" : "event-important",
         "end" : 1512640801000,
         "id" : 3423860,
         "start" : 1512640800000,
         "title" : "Tucker, Larry - 3423860",
         "url" : "javascript:open_patient_chart(71226)"
      },
      {
         "class" : "event-success",
         "end" : 1514800801000,
         "id" : 3424020,
         "start" : 1514800800000,
         "title" : "Pierce, Matthew - 3424020",
         "url" : "javascript:open_patient_chart(23966)"
      },
      {
         "class" : "event-success",
         "end" : 1514541601000,
         "id" : 3424290,
         "start" : 1514541600000,
         "title" : "Green, Jose - 3424290",
         "url" : "javascript:open_patient_chart(199140)"
      },
      {
         "class" : "event-important",
         "end" : 1513418401000,
         "id" : 3424807,
         "start" : 1513418400000,
         "title" : "Tucker, Larry - 3424807",
         "url" : "javascript:open_patient_chart(71226)"
      },
      {
         "class" : "event-important",
         "end" : 1514196001000,
         "id" : 3424932,
         "start" : 1514196000000,
         "title" : "Tucker, Larry - 3424932",
         "url" : "javascript:open_patient_chart(71226)"
      },
      {
         "class" : "event-important",
         "end" : 1513936801000,
         "id" : 3424992,
         "start" : 1513936800000,
         "title" : "Tucker, Larry - 3424992",
         "url" : "javascript:open_patient_chart(71226)"
      }
   ],
   "success" : true
}

```	


### HTTP Request
GET /api/pharmetika/:version/autoship/calendar

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## autoship calendar

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
POST /api/pharmetika/:version/autoship/calendar

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## prescriptionrxn

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
GET prescription/:rxn/autoship/prescription/:rxn

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## prescriptionrxn

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
POST prescription/:rxn/autoship/prescription/:rxn

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## prescription details

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
GET /api/pharmetika/:version/prescription/:rxn/details

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## prescription transactiontransaction id

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
GET /api/pharmetika/:version/prescription_transaction/:transaction_id

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## prescription transactiontransaction id

> Arguments

```json
{
   "json" : {},
   "method" : "POST",
   "query" : {}
}

```	
> Result

```json

```	


### HTTP Request
POST /api/pharmetika/:version/prescription_transaction/:transaction_id

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## insurance reimbusement form

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
GET /api/pharmetika/:version/prescription_transaction/insurance_reimbusement_form/:transaction_id

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## insurance reimbusement form

> Arguments

```json
{
   "json" : {},
   "method" : "POST",
   "query" : {}
}

```	
> Result

```json

```	


### HTTP Request
POST /api/pharmetika/:version/prescription_transaction/insurance_reimbusement_form/:transaction_id

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## get autoship report by date range

> Arguments

```json
{
   "json" : {},
   "method" : "GET",
   "query" : {
      "as_start_date" : "2017-12-08",
      "as_stop_date" : "2017-12-08"
   }
}

```	
> Result

```json
{
   "main" : {
      "main" : {}
   },
   "success" : true
}

```	


### HTTP Request
GET /api/pharmetika/:version/report/autoship/date_range

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## report autoship patients without fillable rxs

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
GET /api/pharmetika/:version/report/autoship_patients_without_fillable_rxs

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## report autoship patients without fillable rxs

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
GET /api/pharmetika/:version/report/autoship_patients_without_fillable_rxs

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## reports prescriber list

> Arguments

```json
{
   "json" : {},
   "method" : "GET",
   "query" : {}
}

```	
> Result

```json
{
   "result" : "Too large or binary"
}

```	


### HTTP Request
GET /api/pharmetika/:version/report/prescriber_list

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## reports prescriber list

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
POST /api/pharmetika/:version/report/prescriber_list

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## reports patient list

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
GET /api/pharmetika/:version/report/patient_list

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## reports patient list uim

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
GET /api/pharmetika/:version/report/patient_list_uim

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## reports faxes volume by day

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
GET /api/pharmetika/:version/report/faxes_volume_by_day

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## reports faxes volume by day

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
POST /api/pharmetika/:version/report/faxes_volume_by_day

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## reports autoship prescriptions without start date

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
GET /api/pharmetika/:version/report/autoship_prescriptions_without_start_date

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## reports payments transactions report

> Arguments

```json
{
   "json" : {},
   "method" : "GET",
   "query" : {
      "end_date" : "2017-11-30",
      "start_date" : "2017-11-01"
   }
}

```	
> Result

```json
{
   "report_datapoints" : {
      "fees_total" : 0,
      "fees_transactions" : [],
      "gross_paid_transaction_total" : 0,
      "net" : 0,
      "refund_fees_total" : 0,
      "refund_transaction_count" : null,
      "refunded_transaction_total" : 0,
      "transactions_by_date" : null,
      "transactions_summary" : {
         "date" : "Summary"
      }
   },
   "success" : true,
   "transactions" : [],
   "transactions_refunded" : []
}

```	


### HTTP Request
GET /api/pharmetika/:version/report/payments_transactions_report

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## reports payments transactions details report

> Arguments

```json
{
   "json" : {},
   "method" : "GET",
   "query" : {
      "end_date" : "2017-11-30",
      "start_date" : "2017-11-01"
   }
}

```	
> Result

```json

```	


### HTTP Request
GET /api/pharmetika/:version/report/payments_transactions_details_report

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## reports patients running out of medication

> Arguments

```json
{
   "json" : {},
   "method" : "GET",
   "query" : {}
}

```	
> Result

```json

```	


### HTTP Request
GET /api/pharmetika/:version/report/patients_running_out_of_medication

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## reports patients that have dropped

> Arguments

```json
{
   "json" : {},
   "method" : "GET",
   "query" : {}
}

```	
> Result

```json
{
   "result" : "Too large or binary"
}

```	


### HTTP Request
GET /api/pharmetika/:version/report/patients_that_have_dropped

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## reports new prescribers

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
GET /api/pharmetika/:version/report/new_prescribers

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## reports prescriber volume metrics

> Arguments

```json
{
   "json" : {},
   "method" : "GET",
   "query" : {}
}

```	
> Result

```json

```	


### HTTP Request
GET /api/pharmetika/:version/report/prescriber_volume_metrics

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## reports drugs coming due

> Arguments

```json
{
   "json" : {},
   "method" : "GET",
   "query" : {}
}

```	
> Result

```json

```	


### HTTP Request
GET /api/pharmetika/:version/report/drugs_coming_due

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## reports drugs coming due by prescriber

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
GET /api/pharmetika/:version/report/drugs_coming_due_by_prescriber

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## reports drugs dispensed by prescriber

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
GET /api/pharmetika/:version/report/drugs_dispensed_by_prescriber

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## reports prescriber patient list

> Arguments

```json
{
   "json" : {},
   "method" : "GET",
   "query" : {}
}

```	
> Result

```json
{
   "data" : [
      {
         "DOB" : "1995-05-11",
         "DoctorCode" : 3781,
         "DoctorGroup" : 3781,
         "EndDate" : "0000-00-00",
         "MI_name" : null,
         "SSN" : null,
         "StartDate" : "2014-12-15",
         "date_updated" : "2017-12-29 21:17:49",
         "drivers_license" : "617500567",
         "drivers_license_state" : "MO",
         "email" : "vstevensku@state.tx.us",
         "first_name" : "Mary",
         "last_name" : "Stevens",
         "patientID" : 4050,
         "patient_id" : 4050,
         "phone_cell" : null,
         "phone_home" : 4178903782,
         "phone_work" : 7191113284,
         "prescriber_id" : null,
         "sex" : "F"
      }
   ],
   "success" : true
}

```	


### HTTP Request
GET /api/pharmetika/:version/report/prescriber_patient_list/:prescriber_id

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## reports patient medication list

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
GET /api/pharmetika/:version/patient/:patient_id/medications_list

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## tasks get all

> Arguments

```json
{
   "json" : {},
   "method" : "GET",
   "query" : {}
}

```	
> Result

```json

```	


### HTTP Request
GET /api/pharmetika/:version/tasks/view_all

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## tasks get task report

> Arguments

```json
{
   "json" : {},
   "method" : "GET",
   "query" : {}
}

```	
> Result

```json

```	


### HTTP Request
GET /api/pharmetika/:version/tasks/tasks_report

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## tasks get all patient

> Arguments

```json
{
   "json" : {},
   "method" : "GET",
   "query" : {}
}

```	
> Result

```json

```	


### HTTP Request
GET /api/pharmetika/:version/tasks/view_all/patient/:patient_id

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## tasks get for prescriber

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
GET /api/pharmetika/:version/tasks/view_all/prescriber/:prescriber_id

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## tasks get by status

> Arguments

```json
{
   "json" : {},
   "method" : "GET",
   "query" : {}
}

```	
> Result

```json
{
   "success" : 1,
   "tasks" : [
      {
         "DOB" : "1977-04-19",
         "confirm_insurance_information" : null,
         "confirm_shipping_address" : null,
         "data_id" : 3401190,
         "date_due" : "2018-01-04 04:19:29",
         "date_scheduled" : "2018-01-03 04:19:29",
         "date_updated" : "2018-01-03 04:19:44",
         "first_name" : "Brian",
         "last_name" : "Carpenter",
         "patient_id" : 32790,
         "prescriber_id" : 4302,
         "prescriber_name_with_credential" : "Russell, Justin, NP",
         "schedule_pharmacist_review" : null,
         "send_prescriber_notification" : null,
         "task_id" : 206314,
         "task_priority" : null,
         "task_status" : "new"
      },
      {
         "DOB" : "1977-04-19",
         "confirm_insurance_information" : null,
         "confirm_shipping_address" : null,
         "data_id" : 3401190,
         "date_due" : "2018-01-04 04:21:03",
         "date_scheduled" : "2018-01-03 04:21:03",
         "date_updated" : "2018-01-03 04:21:03",
         "first_name" : "Brian",
         "last_name" : "Carpenter",
         "patient_id" : 32790,
         "prescriber_id" : 4302,
         "prescriber_name_with_credential" : "Russell, Justin, NP",
         "schedule_pharmacist_review" : null,
         "send_prescriber_notification" : null,
         "task_id" : 206316,
         "task_priority" : null,
         "task_status" : "new"
      },
      {
         "DOB" : "1977-04-19",
         "confirm_insurance_information" : null,
         "confirm_shipping_address" : null,
         "data_id" : 3401190,
         "date_due" : "2018-01-04 04:24:06",
         "date_scheduled" : "2018-01-03 04:24:06",
         "date_updated" : "2018-01-03 04:24:06",
         "first_name" : "Brian",
         "last_name" : "Carpenter",
         "patient_id" : 32790,
         "prescriber_id" : 4302,
         "prescriber_name_with_credential" : "Russell, Justin, NP",
         "schedule_pharmacist_review" : null,
         "send_prescriber_notification" : null,
         "task_id" : 206318,
         "task_priority" : null,
         "task_status" : "new"
      },
      {
         "DOB" : "1977-04-19",
         "confirm_insurance_information" : null,
         "confirm_shipping_address" : null,
         "data_id" : 3401190,
         "date_due" : "2018-01-04 04:37:34",
         "date_scheduled" : "2018-01-03 04:37:34",
         "date_updated" : "2018-01-03 04:37:33",
         "first_name" : "Brian",
         "last_name" : "Carpenter",
         "patient_id" : 32790,
         "prescriber_id" : 4302,
         "prescriber_name_with_credential" : "Russell, Justin, NP",
         "schedule_pharmacist_review" : null,
         "send_prescriber_notification" : null,
         "task_id" : 206320,
         "task_priority" : null,
         "task_status" : "new"
      },
      {
         "DOB" : "1977-04-19",
         "confirm_insurance_information" : null,
         "confirm_shipping_address" : null,
         "data_id" : 3401190,
         "date_due" : "2018-01-04 04:37:48",
         "date_scheduled" : "2018-01-03 04:37:48",
         "date_updated" : "2018-01-03 04:37:48",
         "first_name" : "Brian",
         "last_name" : "Carpenter",
         "patient_id" : 32790,
         "prescriber_id" : 4302,
         "prescriber_name_with_credential" : "Russell, Justin, NP",
         "schedule_pharmacist_review" : null,
         "send_prescriber_notification" : null,
         "task_id" : 206322,
         "task_priority" : null,
         "task_status" : "new"
      },
      {
         "DOB" : "1977-04-19",
         "confirm_insurance_information" : null,
         "confirm_shipping_address" : null,
         "data_id" : 3401190,
         "date_due" : "2018-01-04 04:38:03",
         "date_scheduled" : "2018-01-03 04:38:03",
         "date_updated" : "2018-01-03 18:33:30",
         "first_name" : "Brian",
         "last_name" : "Carpenter",
         "patient_id" : 32790,
         "prescriber_id" : 4302,
         "prescriber_name_with_credential" : "Russell, Justin, NP",
         "schedule_pharmacist_review" : null,
         "send_prescriber_notification" : null,
         "task_id" : 206324,
         "task_priority" : null,
         "task_status" : "new"
      },
      {
         "DOB" : "1977-04-19",
         "confirm_insurance_information" : null,
         "confirm_shipping_address" : null,
         "data_id" : 3401190,
         "date_due" : "2018-01-04 04:38:43",
         "date_scheduled" : "2018-01-03 04:38:43",
         "date_updated" : "2018-01-03 04:38:43",
         "first_name" : "Brian",
         "last_name" : "Carpenter",
         "patient_id" : 32790,
         "prescriber_id" : 4302,
         "prescriber_name_with_credential" : "Russell, Justin, NP",
         "schedule_pharmacist_review" : null,
         "send_prescriber_notification" : null,
         "task_id" : 206326,
         "task_priority" : null,
         "task_status" : "new"
      },
      {
         "DOB" : "1977-04-19",
         "confirm_insurance_information" : null,
         "confirm_shipping_address" : null,
         "data_id" : 3401190,
         "date_due" : "2018-01-04 04:39:01",
         "date_scheduled" : "2018-01-03 04:39:01",
         "date_updated" : "2018-01-03 04:39:01",
         "first_name" : "Brian",
         "last_name" : "Carpenter",
         "patient_id" : 32790,
         "prescriber_id" : 4302,
         "prescriber_name_with_credential" : "Russell, Justin, NP",
         "schedule_pharmacist_review" : null,
         "send_prescriber_notification" : null,
         "task_id" : 206328,
         "task_priority" : null,
         "task_status" : "new"
      },
      {
         "DOB" : "1977-04-19",
         "confirm_insurance_information" : null,
         "confirm_shipping_address" : null,
         "data_id" : 3401190,
         "date_due" : "2018-01-04 04:40:13",
         "date_scheduled" : "2018-01-03 04:40:13",
         "date_updated" : "2018-01-03 08:00:09",
         "first_name" : "Brian",
         "last_name" : "Carpenter",
         "patient_id" : 32790,
         "prescriber_id" : 4302,
         "prescriber_name_with_credential" : "Russell, Justin, NP",
         "schedule_pharmacist_review" : null,
         "send_prescriber_notification" : null,
         "task_id" : 206330,
         "task_priority" : null,
         "task_status" : "started"
      }
   ]
}

```	


### HTTP Request
GET /api/pharmetika/:version/tasks/view/:task_status

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## task state status report

> Arguments

```json
{
   "json" : {},
   "method" : "GET",
   "query" : {}
}

```	
> Result

```json
{
   "success" : 1,
   "tasks" : [
      {
         "DOB" : "1977-04-19",
         "confirm_insurance_information" : null,
         "confirm_shipping_address" : null,
         "data_id" : 3401190,
         "date_due" : "2018-01-04 04:19:29",
         "date_scheduled" : "2018-01-03 04:19:29",
         "date_updated" : "2018-01-03 04:19:44",
         "first_name" : "Brian",
         "last_name" : "Carpenter",
         "patient_id" : 32790,
         "prescriber_id" : 4302,
         "prescriber_name_with_credential" : "Russell, Justin, NP",
         "schedule_pharmacist_review" : null,
         "send_prescriber_notification" : null,
         "task_id" : 206314,
         "task_priority" : null,
         "task_status" : "new"
      },
      {
         "DOB" : "1977-04-19",
         "confirm_insurance_information" : null,
         "confirm_shipping_address" : null,
         "data_id" : 3401190,
         "date_due" : "2018-01-04 04:21:03",
         "date_scheduled" : "2018-01-03 04:21:03",
         "date_updated" : "2018-01-03 04:21:03",
         "first_name" : "Brian",
         "last_name" : "Carpenter",
         "patient_id" : 32790,
         "prescriber_id" : 4302,
         "prescriber_name_with_credential" : "Russell, Justin, NP",
         "schedule_pharmacist_review" : null,
         "send_prescriber_notification" : null,
         "task_id" : 206316,
         "task_priority" : null,
         "task_status" : "new"
      },
      {
         "DOB" : "1977-04-19",
         "confirm_insurance_information" : null,
         "confirm_shipping_address" : null,
         "data_id" : 3401190,
         "date_due" : "2018-01-04 04:24:06",
         "date_scheduled" : "2018-01-03 04:24:06",
         "date_updated" : "2018-01-03 04:24:06",
         "first_name" : "Brian",
         "last_name" : "Carpenter",
         "patient_id" : 32790,
         "prescriber_id" : 4302,
         "prescriber_name_with_credential" : "Russell, Justin, NP",
         "schedule_pharmacist_review" : null,
         "send_prescriber_notification" : null,
         "task_id" : 206318,
         "task_priority" : null,
         "task_status" : "new"
      },
      {
         "DOB" : "1977-04-19",
         "confirm_insurance_information" : null,
         "confirm_shipping_address" : null,
         "data_id" : 3401190,
         "date_due" : "2018-01-04 04:37:34",
         "date_scheduled" : "2018-01-03 04:37:34",
         "date_updated" : "2018-01-03 04:37:33",
         "first_name" : "Brian",
         "last_name" : "Carpenter",
         "patient_id" : 32790,
         "prescriber_id" : 4302,
         "prescriber_name_with_credential" : "Russell, Justin, NP",
         "schedule_pharmacist_review" : null,
         "send_prescriber_notification" : null,
         "task_id" : 206320,
         "task_priority" : null,
         "task_status" : "new"
      },
      {
         "DOB" : "1977-04-19",
         "confirm_insurance_information" : null,
         "confirm_shipping_address" : null,
         "data_id" : 3401190,
         "date_due" : "2018-01-04 04:37:48",
         "date_scheduled" : "2018-01-03 04:37:48",
         "date_updated" : "2018-01-03 04:37:48",
         "first_name" : "Brian",
         "last_name" : "Carpenter",
         "patient_id" : 32790,
         "prescriber_id" : 4302,
         "prescriber_name_with_credential" : "Russell, Justin, NP",
         "schedule_pharmacist_review" : null,
         "send_prescriber_notification" : null,
         "task_id" : 206322,
         "task_priority" : null,
         "task_status" : "new"
      },
      {
         "DOB" : "1977-04-19",
         "confirm_insurance_information" : null,
         "confirm_shipping_address" : null,
         "data_id" : 3401190,
         "date_due" : "2018-01-04 04:38:03",
         "date_scheduled" : "2018-01-03 04:38:03",
         "date_updated" : "2018-01-03 18:33:30",
         "first_name" : "Brian",
         "last_name" : "Carpenter",
         "patient_id" : 32790,
         "prescriber_id" : 4302,
         "prescriber_name_with_credential" : "Russell, Justin, NP",
         "schedule_pharmacist_review" : null,
         "send_prescriber_notification" : null,
         "task_id" : 206324,
         "task_priority" : null,
         "task_status" : "new"
      },
      {
         "DOB" : "1977-04-19",
         "confirm_insurance_information" : null,
         "confirm_shipping_address" : null,
         "data_id" : 3401190,
         "date_due" : "2018-01-04 04:38:43",
         "date_scheduled" : "2018-01-03 04:38:43",
         "date_updated" : "2018-01-03 04:38:43",
         "first_name" : "Brian",
         "last_name" : "Carpenter",
         "patient_id" : 32790,
         "prescriber_id" : 4302,
         "prescriber_name_with_credential" : "Russell, Justin, NP",
         "schedule_pharmacist_review" : null,
         "send_prescriber_notification" : null,
         "task_id" : 206326,
         "task_priority" : null,
         "task_status" : "new"
      },
      {
         "DOB" : "1977-04-19",
         "confirm_insurance_information" : null,
         "confirm_shipping_address" : null,
         "data_id" : 3401190,
         "date_due" : "2018-01-04 04:39:01",
         "date_scheduled" : "2018-01-03 04:39:01",
         "date_updated" : "2018-01-03 04:39:01",
         "first_name" : "Brian",
         "last_name" : "Carpenter",
         "patient_id" : 32790,
         "prescriber_id" : 4302,
         "prescriber_name_with_credential" : "Russell, Justin, NP",
         "schedule_pharmacist_review" : null,
         "send_prescriber_notification" : null,
         "task_id" : 206328,
         "task_priority" : null,
         "task_status" : "new"
      },
      {
         "DOB" : "1977-04-19",
         "confirm_insurance_information" : null,
         "confirm_shipping_address" : null,
         "data_id" : 3401190,
         "date_due" : "2018-01-04 04:40:13",
         "date_scheduled" : "2018-01-03 04:40:13",
         "date_updated" : "2018-01-03 08:00:09",
         "first_name" : "Brian",
         "last_name" : "Carpenter",
         "patient_id" : 32790,
         "prescriber_id" : 4302,
         "prescriber_name_with_credential" : "Russell, Justin, NP",
         "schedule_pharmacist_review" : null,
         "send_prescriber_notification" : null,
         "task_id" : 206330,
         "task_priority" : null,
         "task_status" : "started"
      }
   ]
}

```	


### HTTP Request
GET /api/pharmetika/:version/tasks/view/type/:task_type

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## tasks add

> Arguments

```json
{
   "json" : {
      "data_id" : "26374",
      "date_due" : "2017-12-05T19:30:00Z",
      "date_scheduled" : "2017-12-04T19:30:00Z",
      "task_data" : {
         "data_id" : "26374",
         "date_due" : "12/05/2017 1:30 PM",
         "date_scheduled" : "12/04/2017 1:30 PM",
         "patient_id" : "26374",
         "sub_title" : "ENTER AND ADD TO A/S FOR 12-13-17\r\nP",
         "task_note" : "ENTER AND ADD TO A/S FOR 12-13-17\r\nPROG 150MG SRCAP ",
         "task_type" : "other_patient_task",
         "title" : "BOLOS, DIANE "
      },
      "task_status" : "new",
      "task_type" : "other_patient_task"
   },
   "method" : "PUT",
   "query" : {}
}

```	
> Result

```json
{
   "messages" : {
      "message" : "Scheduled a new task",
      "type" : "success"
   },
   "task_id" : "206358"
}

```	


### HTTP Request
PUT /api/pharmetika/:version/tasks/add

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## tasks add

> Arguments

```json
{
   "json" : {
      "creator" : "incoming fax",
      "data_id" : "262680",
      "date_due" : "2017-12-04T23:48:29",
      "date_scheduled" : "2017-12-04T19:48:29",
      "task_data" : {
         "fax" : {
            "api_id" : 1100000009382162,
            "confirmed" : 0,
            "date_created" : "2017-12-04 13:42:08",
            "date_updated" : "2017-12-04 13:42:08",
            "duplicated" : null,
            "fax_sent" : "2017-12-04 13:42:08",
            "from_did" : 7344263979,
            "id" : 262680,
            "num_pages" : 1,
            "realm" : "psol",
            "task_created" : null,
            "to_did" : 7348218001
         },
         "page_data" : {
            "293376" : {
               "barcodes" : [
                  "293376"
               ],
               "date_created" : "2017-12-04 19:45:07",
               "date_updated" : "2017-12-04 19:45:07",
               "fax_sent" : "2017-12-04 13:42:08",
               "final_id" : null,
               "from_did" : 7344263979,
               "id" : 293376,
               "num_pages" : 1,
               "original_fax_id" : 262680,
               "page_num" : 1,
               "pdf_id" : 272050,
               "png_id" : 272054,
               "preview_id" : 272052
            }
         },
         "pages" : [
            293376
         ],
         "prescriber_id" : null,
         "title" : 7344263979
      },
      "task_originator" : "incoming fax",
      "task_type" : "incoming_fax"
   },
   "method" : "POST",
   "query" : {}
}

```	
> Result

```json
{
   "messages" : {
      "message" : "Scheduled a new task",
      "type" : "success"
   },
   "task_id" : "206360"
}

```	


### HTTP Request
POST /api/pharmetika/:version/tasks/add

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## task get

> Arguments

```json
{
   "json" : {},
   "method" : "GET",
   "query" : {}
}

```	
> Result

```json
{
   "patient" : {
      "DOB" : "1980-10-12",
      "MI_name" : null,
      "SSN" : null,
      "date_updated" : "2017-12-29 21:19:03",
      "drivers_license" : "807S881989",
      "drivers_license_state" : "CO",
      "email" : "cgreenen0@goo.ne.jp",
      "first_name" : "Joseph",
      "last_name" : "Greene",
      "patient_id" : 60388,
      "phone_cell" : null,
      "phone_home" : 3031492712,
      "phone_work" : 7184660889,
      "prescriber_id" : null,
      "sex" : "F",
      "sms_did" : null
   },
   "prescriber" : {
      "3408740" : {
         "DEA" : "FA4376382",
         "NPI" : 6992,
         "address_line_1" : "4617 Brentwood Parkway",
         "address_line_2" : null,
         "city" : "Rockford",
         "credential" : "DO",
         "date_last_prescribed" : null,
         "date_updated" : "2017-11-13 20:03:56",
         "email" : "krussell9t@i2i.jp",
         "fax" : 2025158094,
         "first_name" : null,
         "general_notes" : null,
         "id" : 5758,
         "label_name" : "GRAJCZYK, DO",
         "last_name" : "Rose, Juan",
         "name_full" : "Rose, Juan",
         "name_with_credential" : "Rose, Juan, DO",
         "pharmacy_id" : "5758",
         "phone_1" : 2025158094,
         "phone_2" : 2025158094,
         "phone_primary" : 2025158094,
         "phone_secondary" : 2025158094,
         "phone_sms" : null,
         "postal_code" : "20067",
         "prescriber_group" : null,
         "rxn" : 3408740,
         "state" : "DC"
      },
      "3408741" : {
         "DEA" : "FA4376382",
         "NPI" : 6992,
         "address_line_1" : "4617 Brentwood Parkway",
         "address_line_2" : null,
         "city" : "Rockford",
         "credential" : "DO",
         "date_last_prescribed" : null,
         "date_updated" : "2017-11-13 20:03:56",
         "email" : "krussell9t@i2i.jp",
         "fax" : 2025158094,
         "first_name" : null,
         "general_notes" : null,
         "id" : 5758,
         "label_name" : "GRAJCZYK, DO",
         "last_name" : "Rose, Juan",
         "name_full" : "Rose, Juan",
         "name_with_credential" : "Rose, Juan, DO",
         "pharmacy_id" : "5758",
         "phone_1" : 2025158094,
         "phone_2" : 2025158094,
         "phone_primary" : 2025158094,
         "phone_secondary" : 2025158094,
         "phone_sms" : null,
         "postal_code" : "20067",
         "prescriber_group" : null,
         "rxn" : 3408741,
         "state" : "DC"
      }
   },
   "prescriptions" : {
      "3408740" : {
         "controlled" : 0,
         "date_begin_day_supply_count" : "2017-02-03",
         "date_entered" : "2016-11-23",
         "date_stop" : "2017-08-22",
         "date_updated" : null,
         "date_updated_db" : "2017-02-03 16:52:21",
         "date_written" : "2016-08-22",
         "day_supply" : 30,
         "discontinue" : 0,
         "drug_class" : null,
         "drug_description" : "PROGESTERONE CREAM 200MG/GM",
         "drug_id" : "1116",
         "fillable" : 0,
         "filled" : 2,
         "first_filled" : "2016-11-23",
         "last_filled" : "2017-02-03",
         "max_fill_num" : null,
         "next_fill_due" : "2017-03-05",
         "patient_id" : 60388,
         "payor_id" : "3",
         "payor_type" : "R",
         "prescriber_id" : 5758,
         "price" : "32.00",
         "prn" : null,
         "quantity_written" : 30,
         "refills_authorized" : 3,
         "refills_remaining" : 2,
         "remaining_quantity" : "60.000",
         "rxn" : 3408740,
         "sig" : "Apply 0.1gm (2 clicks) topically to thin skinned area twice daily, then increase to 0.5gm (10 clicks) twice daily, rub in well and rotate sites (inner arm, inner thigh, behing knees)"
      },
      "3408741" : {
         "controlled" : 0,
         "date_begin_day_supply_count" : "2017-05-26",
         "date_entered" : "2016-11-23",
         "date_stop" : "2017-08-22",
         "date_updated" : null,
         "date_updated_db" : "2017-07-14 20:23:18",
         "date_written" : "2016-08-22",
         "day_supply" : 30,
         "discontinue" : 1,
         "drug_class" : null,
         "drug_description" : "BI-EST (50/50) CREAM 2MG/GM",
         "drug_id" : "1727",
         "fillable" : 0,
         "filled" : 4,
         "first_filled" : "2016-11-23",
         "last_filled" : "2017-05-26",
         "max_fill_num" : null,
         "next_fill_due" : "2017-06-25",
         "patient_id" : 60388,
         "payor_id" : "3",
         "payor_type" : "R",
         "prescriber_id" : 5758,
         "price" : "32.00",
         "prn" : null,
         "quantity_written" : 30,
         "refills_authorized" : 3,
         "refills_remaining" : 0,
         "remaining_quantity" : "0.000",
         "rxn" : 3408741,
         "sig" : "Apply 0.1gm (2 clicks) topically to thin skinned area twice daily, then increase to 0.5gm (10 clicks) twice daily, rub in well and rotate sites (inner arm, inner thigh, behing knees)"
      }
   },
   "task" : {
      "acknowledged" : "2017-05-26 13:06:32",
      "completed_by" : null,
      "data" : {
         "AccountSid" : "ACcab5932372bded0345ae8a0859c78c63",
         "ApiVersion" : "2010-04-01",
         "CallSid" : "CA87f7243a583ea9ca22be9cb5a6fad882",
         "CallStatus" : "in-progress",
         "Called" : "+17348871095",
         "CalledCity" : "ANN ARBOR",
         "CalledCountry" : "US",
         "CalledState" : "MI",
         "CalledZip" : "48108",
         "Caller" : "+17633544783",
         "CallerCity" : "MINNEAPOLIS",
         "CallerCountry" : "US",
         "CallerState" : "MN",
         "CallerZip" : "55124",
         "Digits" : "1",
         "Direction" : "inbound",
         "From" : "+17633544783",
         "FromCity" : "MINNEAPOLIS",
         "FromCountry" : "US",
         "FromState" : "MN",
         "FromZip" : "55124",
         "To" : "+17348871095",
         "ToCity" : "ANN ARBOR",
         "ToCountry" : "US",
         "ToState" : "MI",
         "ToZip" : "48108",
         "delivery_method" : "6",
         "delivery_method_description" : "FedEx Standard",
         "invalid_count" : "0",
         "msg" : "Gather End",
         "patient_id" : "60388",
         "payment_method" : "1",
         "rx_number" : [
            "3408740",
            "3408741"
         ],
         "rx_numbers_not_validated" : [],
         "rx_numbers_validated" : [
            "3408740",
            "3408741"
         ],
         "rxns" : [
            "",
            "3408741"
         ],
         "title" : "Margaret Turner"
      },
      "data_id" : null,
      "date_completed" : null,
      "date_due" : "2017-12-30 21:20:41",
      "date_entered" : "2017-05-26 04:15:50",
      "date_scheduled" : "2017-05-26 04:15:50",
      "date_updated" : "2017-12-29 21:20:41",
      "entered_by" : "user_jso",
      "events" : [],
      "id" : 134878,
      "past_due" : 1,
      "patient_id" : 60388,
      "prescriber_id" : null,
      "task_data" : null,
      "task_display_name" : "Patient Refill Request",
      "task_due_status" : "past_due",
      "task_priority" : null,
      "task_state_json" : null,
      "task_state_json_decrypted" : null,
      "task_status" : "new",
      "task_type" : "refill_request_from_patient",
      "time_since_scheduled" : -19368178,
      "time_until_due" : -471487,
      "updated_by" : null
   }
}

```	


### HTTP Request
GET /api/pharmetika/:version/tasks/task/:id

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## task update

> Arguments

```json
{
   "json" : {
      "acknowledge" : "1"
   },
   "method" : "POST",
   "query" : {
      "acknowledge" : "1"
   }
}

```	
> Result

```json
{
   "messages" : []
}

```	


### HTTP Request
POST /api/pharmetika/:version/tasks/task/:id

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## task update

> Arguments

```json
{
   "json" : {
      "acknowledged" : "2017-12-12 00:02:43",
      "completed_by" : null,
      "data" : {
         "contact_id" : 34972,
         "entity_type" : "patient",
         "patient_id" : 32790,
         "prescriber" : null,
         "sms_id" : "SM8ef77316dc17ff383f20321a51ac90d5",
         "sub_title" : "HUMIRA (adalimumab)",
         "title" : "Brian Carpenter"
      },
      "data_id" : 3401190,
      "date_completed" : null,
      "date_due" : "2017-12-30 21:17:34",
      "date_entered" : "2017-12-04 19:39:24",
      "date_scheduled" : "2017-12-13 19:05:45",
      "date_updated" : "2017-12-29 21:20:17",
      "entered_by" : "user_+16",
      "events" : [],
      "id" : 193666,
      "past_due" : 1,
      "patient_id" : 32790,
      "prescriber_id" : 4302,
      "task_data" : null,
      "task_display_name" : "Onboarding - Call New Patient",
      "task_due_status" : "past_due",
      "task_id" : 193666,
      "task_priority" : null,
      "task_state" : {
         "confirm_insurance_information" : true,
         "confirm_shipping_address" : true,
         "patient_authorizes_medication_billing_and_shipment" : true,
         "schedule_pharmacist_review" : true,
         "send_prescriber_notification" : true
      },
      "task_state_json" : null,
      "task_state_json_decrypted" : null,
      "task_status" : "complete",
      "task_type" : "prior_authorization_call_new_patient",
      "time_since_scheduled" : -1770186,
      "time_until_due" : -293477,
      "updated_by" : null
   },
   "method" : "PUT",
   "query" : {}
}

```	
> Result

```json
{
   "messages" : [
      {
         "message" : "Updated task status to Complete",
         "type" : "info"
      }
   ]
}

```	


### HTTP Request
PUT /api/pharmetika/:version/tasks/task/:id

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## task log task event

> Arguments

```json
{
   "json" : {
      "event_note" : "test event",
      "event_type" : "other"
   },
   "method" : "POST",
   "query" : {}
}

```	
> Result

```json
{
   "messages" : [
      {
         "message" : "Logged event",
         "type" : "success"
      }
   ],
   "success" : true
}

```	


### HTTP Request
POST /api/pharmetika/:version/tasks/task/:task_id/log_event

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## tasks get updated

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
GET /api/pharmetika/:version/tasks/pub_updated

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## patient tasks update

> Arguments

```json
{
   "json" : {},
   "method" : "POST",
   "query" : {}
}

```	
> Result

```json
{
   "messages" : [
      {
         "message" : "Updated 0 tasks to Complete",
         "type" : "info"
      }
   ]
}

```	


### HTTP Request
POST /api/pharmetika/:version/tasks/patient/:patient_id/type/:task_type

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## prescriber tasks update

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
POST /api/pharmetika/:version/tasks/prescriber/:prescriber_id/type/:task_type

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## tasks get updated

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
GET /api/pharmetika/:version/tasks/pub_updated

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## send email from args

> Arguments

```json
{
   "json" : {},
   "method" : "PUT",
   "query" : {
      "message" : "Pharmacy Solutions:  Your refill request has been received but will be delayed due to no available refills on your prescription(s).  We have reached out to your provider's office for a refill. As soon as we receive it, we will process and ship your prescription(s) out to you.  If you have any questions please contact us at 734-821-8000. Thank you!\r\n",
      "patient_id" : "24354",
      "recipients[]" : "PETERJHARRELL@CHARTER.NET",
      "subject" : "Pharmacy Solutions",
      "to_email" : "PETERJHARRELL@CHARTER.NET"
   }
}

```	
> Result

```json
{
   "messages" : [
      {
         "icon" : "glyphicon glyphicon-send",
         "message" : "Sent 1 email successfully",
         "type" : "success"
      }
   ],
   "sent_emails" : {
      "failed" : [],
      "success" : [
         "24354"
      ]
   },
   "success" : true
}

```	


### HTTP Request
PUT /api/pharmetika/:version/email/send

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## send templated email

> Arguments

```json
{
   "json" : {},
   "method" : "PUT",
   "query" : {
      "active_rx" : "active",
      "from" : "autoship@pharmacysolutions.online",
      "patient_id" : "8230",
      "recipients[]" : "8230",
      "reply_to" : "autoship@pharmacysolutions.online",
      "subject" : "Reminder",
      "template" : "dropped_patient"
   }
}

```	
> Result

```json
{
   "messages" : [
      {
         "icon" : "glyphicon glyphicon-send",
         "message" : "Sent 1 email successfully",
         "type" : "success"
      }
   ],
   "sent_emails" : {
      "failed" : [],
      "success" : [
         "8230"
      ]
   },
   "success" : true
}

```	


### HTTP Request
PUT /api/pharmetika/:version/email/template/:template

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## send templated email test

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
POST /api/pharmetika/:version/email/template/:template

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## get templated email

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
GET /api/pharmetika/:version/email/template/:template

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## email mark read

> Arguments

```json
{
   "json" : {},
   "method" : "POST",
   "query" : {
      "email_id" : "8482",
      "message_id" : "cio-62073-11"
   }
}

```	
> Result

```json
{
   "args" : {
      "email_id" : "8482",
      "message_id" : "cio-62073-11"
   },
   "success" : true
}

```	


### HTTP Request
POST /api/pharmetika/:version/email/read/:message_id

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## sms retrieve

> Arguments

```json
{
   "json" : {},
   "method" : "GET",
   "query" : {}
}

```	
> Result

```json
{
   "message" : {
      "message" : "",
      "message_bytes" : null,
      "message_hex" : null
   }
}

```	


### HTTP Request
GET /api/pharmetika/:version/sms/:sid

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## kazoo get voicemail

> Arguments

```json
{
   "json" : {},
   "method" : "GET",
   "query" : {}
}

```	
> Result

```json
{
   "audio_url" : "https://api.twilio.com/2010-04-01/Accounts/ACcab5932372bded0345ae8a0859c78c63/Recordings/REe1008c4d5eb8b38ac02227cd618ad6d8",
   "call_id" : "CA23aefeea84618d62fb38e7b530ba76aa",
   "contact_id" : 40086,
   "date_created" : "2017-11-15 12:14:28",
   "from_did" : 9792240241,
   "id" : 68158,
   "patient_id" : 15840,
   "to_did" : 7345489292,
   "transcription_text" : "Well.\n\n I did not need you to.\n\n Prescriptions to be just not thank.",
   "transcription_url" : "https://api.twilio.com/2010-04-01/Accounts/ACcab5932372bded0345ae8a0859c78c63/Recordings/REe1008c4d5eb8b38ac02227cd618ad6d8/Transcriptions/TR38905bbe1c9828c697cfffadbc246db0"
}

```	


### HTTP Request
GET /api/pharmetika/:version/voicemail/:id

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## get sent email

> Arguments

```json
{
   "json" : {},
   "method" : "GET",
   "query" : {}
}

```	
> Result

```json

```	


### HTTP Request
GET /api/pharmetika/:version/email/sent/:id

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## get received email

> Arguments

```json
{
   "json" : {},
   "method" : "GET",
   "query" : {}
}

```	
> Result

```json
{
   "email_data" : {}
}

```	


### HTTP Request
GET /api/pharmetika/:version/email/received/:id

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## get nppes registry data

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
GET /api/pharmetika/:version/prescriber/get_nppes_registry_data/:npi

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## get uncharged transactions

> Arguments

```json
{
   "json" : {},
   "method" : "GET",
   "query" : {
      "patient_id" : "59652"
   }
}

```	
> Result

```json
{
   "args" : {
      "charge_ids" : null,
      "patient_id" : "59652"
   },
   "success" : true,
   "transactions" : []
}

```	


### HTTP Request
GET /api/pharmetika/:version/payment/transaction/uncharged

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## payment add payment card

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
GET /api/pharmetika/:version/payment/method/add_payment_card/:patient_id

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## payment add payment card

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
PUT /api/pharmetika/:version/payment/method/add_payment_card/:patient_id

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## payment add payment card

> Arguments

```json
{
   "json" : {},
   "method" : "POST",
   "query" : {
      "stripeEmail" : "ORAND@COMCAST.NET",
      "stripeToken" : "tok_1BZ0XzLM7RaRgqcuDK1BAfzi",
      "stripeTokenType" : "card"
   }
}

```	
> Result

```json
{
   "messages" : [
      {
         "message" : "Failed! 400 response: Bad Request",
         "type" : "error"
      }
   ],
   "success" : false
}

```	


### HTTP Request
POST /api/pharmetika/:version/payment/method/add_payment_card/:patient_id

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## payment get sources

> Arguments

```json
{
   "json" : {},
   "method" : "GET",
   "query" : {}
}

```	
> Result

```json
{
   "customer_id" : null,
   "sources" : [],
   "success" : true
}

```	


### HTTP Request
GET /api/pharmetika/:version/payment/sources/:patient_id

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## payment send payment update link

> Arguments

```json
{
   "json" : {
      "method" : "sms"
   },
   "method" : "PUT",
   "query" : {
      "method" : "sms"
   }
}

```	
> Result

```json

```	


### HTTP Request
PUT /api/pharmetika/:version/payment/sources/request_link/:patient_id

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## payment post charge

> Arguments

```json
{
   "json" : {
      "amount" : "38.00",
      "charge_description" : "3425342 - DIHYDROERGOTAMINE MESYLATE (DHE) CAPSULE 1MG $30.00\n27741 - FEDEX GROUND $8.00\n",
      "charge_ids[]" : [
         "1613528",
         ""
      ],
      "customer_id" : "cus_9C6v5DgwHMI2F4",
      "items_manually_added" : "[{\"amount\":\"8.00\",\"rxn\":27741,\"description\":\"FEDEX GROUND\",\"manual\":1,\"price\":\"8.00\",\"quantity\":1,\"tax\":0,\"datefilled\":\"\"}]",
      "source_id" : "card_18tihcLM7RaRgqcu6qjxFXLK"
   },
   "method" : "PUT",
   "query" : {
      "amount" : "38.00",
      "charge_description" : "3425342 - DIHYDROERGOTAMINE MESYLATE (DHE) CAPSULE 1MG $30.00\n27741 - FEDEX GROUND $8.00\n",
      "charge_ids[]" : [
         "1613528",
         ""
      ],
      "customer_id" : "cus_9C6v5DgwHMI2F4",
      "items_manually_added" : "[{\"amount\":\"8.00\",\"rxn\":27741,\"description\":\"FEDEX GROUND\",\"manual\":1,\"price\":\"8.00\",\"quantity\":1,\"tax\":0,\"datefilled\":\"\"}]",
      "source_id" : "card_18tihcLM7RaRgqcu6qjxFXLK"
   }
}

```	
> Result

```json
{
   "messages" : [
      {
         "message" : "Failed! 400 response: Bad Request",
         "type" : "error"
      }
   ],
   "success" : false
}

```	


### HTTP Request
PUT /api/pharmetika/:version/payment/method/:source_id/post_charge/:amount

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## payment update source

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
POST /api/pharmetika/:version/payment/method/:source_id/update

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## payment remove source

> Arguments

```json
{
   "json" : {
      "customer_id" : "cus_9CshiTTzAM2Uox",
      "source_id" : "card_18uSvtLM7RaRgqcuvHzwhsB7"
   },
   "method" : "DELETE",
   "query" : {
      "customer_id" : "cus_9CshiTTzAM2Uox",
      "source_id" : "card_18uSvtLM7RaRgqcuvHzwhsB7"
   }
}

```	
> Result

```json
{
   "messages" : null,
   "success" : false,
   "updates" : {
      "source_id" : "0E0"
   }
}

```	


### HTTP Request
DELETE /api/pharmetika/:version/payment/method/:source_id

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## payment get charge transactions

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
GET /api/pharmetika/:version/payment/transactions/:patient_id

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## payment get receipts

> Arguments

```json
{
   "json" : {},
   "method" : "GET",
   "query" : {}
}

```	
> Result

```json
{
   "success" : true,
   "transactions" : {
      "success" : true,
      "transactions" : {
         "data" : []
      }
   },
   "transactions_alternate" : []
}

```	


### HTTP Request
GET /api/pharmetika/:version/payment/receipts/:patient_id

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## payment refund charge transaction

> Arguments

```json
{
   "json" : {
      "amount" : "54.89",
      "transaction_id" : "ch_1Baol8LM7RaRgqcuV5Kx3g7F"
   },
   "method" : "POST",
   "query" : {
      "amount" : "54.89",
      "transaction_id" : "ch_1Baol8LM7RaRgqcuV5Kx3g7F"
   }
}

```	
> Result

```json
{
   "messages" : [
      {
         "message" : "Failed! 404 response: Not Found",
         "type" : "error"
      }
   ],
   "success" : false
}

```	


### HTTP Request
POST /api/pharmetika/:version/payment/transaction/:transaction_api_id/refund/:amount

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## payment get receipt

> Arguments

```json
{
   "json" : {},
   "method" : "GET",
   "query" : {}
}

```	
> Result

```json

```	


### HTTP Request
GET /api/pharmetika/:version/payment/transaction/:transaction_api_id/receipt

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## payment get receipt alternate system

> Arguments

```json
{
   "json" : {},
   "method" : "GET",
   "query" : {}
}

```	
> Result

```json
{
   "args" : {
      "patient_id" : null,
      "transaction_api_id" : null,
      "transaction_id" : "33328"
   },
   "patient" : {
      "address" : null,
      "sms_did" : null
   },
   "transaction_details" : {
      "api_data" : {
         "amount_decimal" : "0.00",
         "amount_refunded_decimal" : 0
      },
      "success" : true,
      "transaction" : {}
   }
}

```	


### HTTP Request
GET /api/pharmetika/:version/payment/transaction_alternate/:transaction_id/receipt

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## payment create invoice

> Arguments

```json
{
   "json" : {
      "amount" : "45.00",
      "charge_description" : "3421578 - ESTRIOL VAGINAL CREAM 0.5MG/GM $45.00\n",
      "charge_ids" : "1608140",
      "customer_id" : "",
      "items_manually_added" : "[]",
      "source_id" : "payflow"
   },
   "method" : "PUT",
   "query" : {
      "amount" : "45.00",
      "charge_description" : "3421578 - ESTRIOL VAGINAL CREAM 0.5MG/GM $45.00\n",
      "charge_ids" : "1608140",
      "customer_id" : "",
      "items_manually_added" : "[]",
      "source_id" : "payflow"
   }
}

```	
> Result

```json
{
   "invoice_id" : "11352",
   "messages" : [
      {
         "icon" : "fa fa-credit-card-alt",
         "message" : "Ready to accept payment!  Invoice ID: 11352",
         "type" : "success"
      }
   ],
   "success" : true
}

```	


### HTTP Request
PUT /api/pharmetika/:version/payment/invoice/:patient_id

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## payment get invoices list

> Arguments

```json
{
   "json" : {
      "patient_id" : "100"
   },
   "method" : "GET",
   "query" : {
      "patient_id" : "100"
   }
}

```	
> Result

```json
{
   "invoices" : [
      {
         "data" : {
            "charge_ids" : [],
            "patient_id" : "100"
         },
         "date_created" : "2018-01-05 08:19:13",
         "id" : 11352,
         "invoice_status" : "pending",
         "patient_id" : 100,
         "transactions" : {}
      }
   ],
   "number_of_invoices" : 1,
   "patient_id" : "100",
   "success" : true
}

```	


### HTTP Request
GET /api/pharmetika/:version/payment/invoice/:patient_id

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## payment get invoice by id

> Arguments

```json
{
   "json" : {},
   "method" : "GET",
   "query" : {}
}

```	
> Result

```json
{
   "invoice" : {
      "data" : {
         "amount" : "215.04",
         "charge_description" : "3424414 - PROGESTERONE E4M (DYE-FREE) CAPSULE 50MG $98.93\n3424415 - BI-EST 0.75MG/TESTOSTERONE 0.75MG/GM CREAM  $116.11\n",
         "charge_ids" : [
            "1601942",
            "1601948"
         ],
         "charge_ids[]" : [
            "1601942",
            "1601948"
         ],
         "customer_id" : "",
         "items" : [
            {
               "amt" : "98.93",
               "autoship" : null,
               "charge_age" : "older",
               "charge_id" : 1601942,
               "copay" : "98.93",
               "created" : "2017-11-30 16:34:29",
               "date_filled" : "2017-11-30",
               "drug_description" : "PROGESTERONE E4M (DYE-FREE) CAPSULE 50MG",
               "manual" : 0,
               "patient_id" : 71564,
               "price" : "98.93",
               "pstatus" : null,
               "quantity_dispensed" : 90,
               "rxn" : 3424414,
               "third_party" : 0,
               "transaction_id" : 351670
            },
            {
               "amt" : "116.11",
               "autoship" : null,
               "charge_age" : "older",
               "charge_id" : 1601948,
               "copay" : "116.11",
               "created" : "2017-11-30 16:37:48",
               "date_filled" : "2017-11-30",
               "drug_description" : "BI-EST 0.75MG/TESTOSTERONE 0.75MG/GM CREAM ",
               "manual" : 0,
               "patient_id" : 71564,
               "price" : "116.11",
               "pstatus" : null,
               "quantity_dispensed" : 90,
               "rxn" : 3424415,
               "third_party" : 0,
               "transaction_id" : 351671
            }
         ],
         "items_manually_added" : [],
         "patient_id" : "71564",
         "source_id" : "payflow"
      },
      "date_created" : "2017-12-05 20:38:37",
      "id" : 10570,
      "invoice_status" : "pending",
      "patient_id" : 71564
   },
   "invoice_id" : "10570",
   "patient" : {
      "DOB" : "1991-05-24",
      "MI_name" : null,
      "SSN" : null,
      "address" : {
         "address_status" : 1,
         "address_type" : "shipping",
         "city" : "CHELSEA",
         "country" : null,
         "date_updated" : "2017-12-01 13:45:26",
         "dates" : [],
         "id" : 34046924,
         "line_1" : null,
         "line_2" : "338 ELM STREET",
         "line_3" : null,
         "patient_id" : 71564,
         "postal_code" : "48118",
         "primary_address" : 1,
         "state" : "MI"
      },
      "date_updated" : "2017-12-29 21:19:17",
      "drivers_license" : "760S364561",
      "drivers_license_state" : "FL",
      "email" : "dmooreh0@timesonline.co.uk",
      "first_name" : "Chris",
      "last_name" : "Moore",
      "patient_id" : 71564,
      "phone_cell" : null,
      "phone_home" : 4079967582,
      "phone_work" : 8644331800,
      "prescriber_id" : null,
      "sex" : "F",
      "sms_did" : null
   },
   "success" : true
}

```	


### HTTP Request
GET /api/pharmetika/:version/payment/invoice/id/:invoice_id

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## payment clear invoice by id

> Arguments

```json
{
   "json" : {},
   "method" : "DELETE",
   "query" : {}
}

```	
> Result

```json
{
   "messages" : [
      {
         "icon" : "fa fa-credit-card-alt",
         "message" : "Invoice cleared",
         "type" : "success"
      }
   ],
   "success" : true
}

```	


### HTTP Request
DELETE /api/pharmetika/:version/payment/invoice/id/:invoice_id

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## payment mark paid invoice by id

> Arguments

```json
{
   "json" : {},
   "method" : "POST",
   "query" : {
      "payment_alternative" : "check"
   }
}

```	
> Result

```json
{
   "messages" : [
      {
         "icon" : "fa fa-credit-card-alt",
         "message" : "Invoice marked \"paid\"",
         "type" : "success"
      }
   ],
   "success" : true
}

```	


### HTTP Request
POST /api/pharmetika/:version/payment/invoice/id/:invoice_id

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## push invoice to pos device

> Arguments

```json
{
   "json" : {},
   "method" : "POST",
   "query" : {}
}

```	
> Result

```json
{
   "messages" : [
      {
         "icon" : "fa fa-credit-card-alt",
         "message" : "Sent to POS",
         "type" : "success"
      }
   ],
   "pos_device_id" : "113",
   "success" : true
}

```	


### HTTP Request
POST /api/pharmetika/:version/payment/invoice/id/:invoice_id/pos_device/:pos_device_id

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## get payment signature pad

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
GET /api/pharmetika/:version/payment/signature_pad

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## download product list

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
GET /api/pharmetika/:version/util/product_list

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## upload skus

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
POST /api/pharmetika/:version/util/product_list

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## migration patient add remote

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
PUT /api/pharmetika/:version/remote_migration/:requesting_realm/patient/:requesting_realm_patient_id

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## migration patient add remote

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
POST /api/pharmetika/:version/remote_migration/:requesting_realm/patient/:requesting_realm_patient_id

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## migrationprescription

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
GET payment/migration/prescription

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## migrationprescription

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
POST payment/migration/prescription

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## migration transfer prescription

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
GET /api/pharmetika/:version/migration/prescription/transfer

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## migration transfer prescription

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
POST /api/pharmetika/:version/migration/prescription/transfer

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## migration read transfer log

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
GET /api/pharmetika/:version/migration/prescription/transfer/log

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## migration read transfer log

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
POST /api/pharmetika/:version/migration/prescription/transfer/log

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## migration view transfer prescription

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
GET /api/pharmetika/:version/migration/prescription/transfer/:RxN

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## migration view printable prescription

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
GET /api/pharmetika/:version/migration/prescription/printable

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## migration view printable prescription

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
POST /api/pharmetika/:version/migration/prescription/printable

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## kazoo originate call

> Arguments

```json
{
   "json" : {},
   "method" : "POST",
   "query" : {}
}

```	
> Result

```json
{
   "messages" : [
      {
         "icon" : "fa fa-phone",
         "message" : "Calling your phone and connecting to 4806957898",
         "type" : "success"
      }
   ]
}

```	


### HTTP Request
POST /api/pharmetika/:version/kazoo/call/:call_to

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## kazoo originate call

> Arguments

```json
{
   "json" : {},
   "method" : "GET",
   "query" : {}
}

```	
> Result

```json

```	


### HTTP Request
GET /api/pharmetika/:version/kazoo/call/:call_to

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## call recording

> Arguments

```json
{
   "json" : {},
   "method" : "GET",
   "query" : {}
}

```	
> Result

```json

```	


### HTTP Request
GET /api/pharmetika/:version/kazoo/call_record/:call_id/recording

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## kazoo queue pause

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
POST /api/pharmetika/:version/kazoo/queue/:queues/:extension/:pause

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## kazoo queue pause

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
GET /api/pharmetika/:version/kazoo/queue/:queues/:extension/:pause

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## view fax pdf

> Arguments

```json
{
   "json" : {},
   "method" : "GET",
   "query" : {}
}

```	
> Result

```json

```	


### HTTP Request
GET /api/pharmetika/:version/kazoo/fax/view/:id

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## fhir patient map existing

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
GET /api/pharmetika/:version/fhir/patient/:patient_id/map_existing

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## fhir practitioner map existing prescriber

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
GET /api/pharmetika/:version/fhir/practitioner/:prescriber_id/map_existing_prescriber

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## fax send document

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
PUT /api/pharmetika/:version/fax_document/:did

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## fax send document

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
POST /api/pharmetika/:version/fax_document/:did

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## fax send mass

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
PUT /api/pharmetika/:version/mass_fax_document

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## fax send mass

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
POST /api/pharmetika/:version/mass_fax_document

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## reauthorization request view

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
GET /api/pharmetika/v6/prescription/:rxn/reauthorization_request/view

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## reauthorization request view

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
POST /api/pharmetika/v6/prescription/:rxn/reauthorization_request/view

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## reauthorization request fax

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
GET /api/pharmetika/v6/prescription/:rxn/reauthorization_request/fax

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## reauthorization request fax

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
POST /api/pharmetika/v6/prescription/:rxn/reauthorization_request/fax

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## faxes incoming fax create task

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
PUT /api/pharmetika/v6/faxes/incoming/:fax_id/create_task

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## faxes view page

> Arguments

```json
{
   "json" : {},
   "method" : "GET",
   "query" : {}
}

```	
> Result

```json

```	


### HTTP Request
GET /api/pharmetika/v6/faxes/page/:page_id

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## faxes view all pages

> Arguments

```json
{
   "json" : {},
   "method" : "GET",
   "query" : {}
}

```	
> Result

```json
{
   "pdf" : {
      "pdf" : "%PDF-1.4\n%ÆÍÍµ\n1 0 obj << /Type /Catalog /PageLayout /SinglePage /PageMode /UseNone /Pages 2 0 R /ViewerPreferences << /NonFullScreenPageMode /UseNone >> >> endobj\n2 0 obj << /Type /Pages /Count 2 /Kids [ 5 0 R 15 0 R ] /Resources 3 0 R >> endobj\n3 0 obj << /ProcSet [ /PDF /Text /ImageB /ImageC /ImageI ] >> endobj\n4 0 obj << /Producer (PDF::API2 2.033 [freebsd]) >> endobj\n5 0 obj << /Type /Page /Contents [ 14 0 R ] /MediaBox [ 0 0 622.08 792 ] /Parent 2 0 R /Resources << /ProcSet [ /PDF /Text /ImageB /ImageC /ImageI ] /XObject << /CBA 6 0 R >> >> >> endobj\n6 0 obj << /Type /XObject /Subtype /Form /BBox [ 0 0 622.08 792 ] /Filter [ /FlateDecode ] /FormType 1 /Length 25 0 R /Name /CBA /Resources << /Font << /HelvCBB~1512430393 13 0 R >> /ProcSet [ /PDF /Text /ImageB /ImageC /ImageI ] /XObject << /CBA 9 0 R /CBD 7 0 R >> >> >> stream\nxÚM;\u000f?@\u0010?ÿÊ?Z »wÇC:\u001e\u0012c|\u0011®01?Â?H ÐÎßî!äân²ÍÌ|»Yt\u0018«\u0003?LóÖ`?Ä\u0011Ò\u0016ù r\u0000\u000fL\f¡ÐWÆ4t\u0007-\u0018oÔé?s?§6?Xã§Ó\u0010ZnªÇ+?ã\u000f»,?$¹??\r][? 2\u0014Ýà?YÖ·M\b\u0002Å¾d?h?Fgßaá\u0002û¡\u0014!K³D·!|©\u0002Á\u0001\u0011Ïq?ÞZ¤ë\t?<\u0015Ç]¹/\u000ee\u0016'?=\u000ek=}$Ç\u0017hX<´\nendstream endobj\n7 0 obj << /Type /XObject /Subtype /Form /BBox [ 0 0 101 24 ] /Filter [ /FlateDecode ] /FormType 1 /Length 8 0 R /Name /CBD /Resources << /Font << /HelvCBC~1512430393 << /Type /Font /Subtype /Type1 /BaseFont /Helvetica /Encoding << /Type /Encoding /BaseEncoding /WinAnsiEncoding /Differences [ 0 /.notdef /.notdef /.notdef /.notdef /.notdef /.notdef /.notdef /.notdef /.notdef /.notdef /.notdef /.notdef /.notdef /.notdef /.notdef /.notdef /.notdef /.notdef /.notdef /.notdef /.notdef /.notdef /.notdef /.notdef /.notdef /.notdef /.notdef /.notdef /.notdef /.notdef /.notdef /.notdef /space /exclam /quotedbl /numbersign /dollar /percent /ampersand /quotesingle /parenleft /parenright /asterisk /plus /comma /hyphen /period /slash /zero /one /two /three /four /five /six /seven /eight /nine /colon /semicolon /less /equal /greater /question /at /A /B /C /D /E /F /G /H /I /J /K /L /M /N /O /P /Q /R /S /T /U /V /W /X /Y /Z /bracketleft /backslash /bracketright /asciicircum /underscore /grave /a /b /c /d /e /f /g /h /i /j /k /l /m /n /o /p /q /r /s /t /u /v /w /x /y /z /braceleft /bar /braceright /asciitilde /bullet /Euro /bullet /quotesinglbase /florin /quotedblbase /ellipsis /dagger /daggerdbl /circumflex /perthousand /Scaron /guilsinglleft /OE /bullet /Zcaron /bullet /bullet /quoteleft /quoteright /quotedblleft /quotedblright /bullet /endash /emdash /tilde /trademark /scaron /guilsinglright /oe /bullet /zcaron /Ydieresis /space /exclamdown /cent /sterling /currency /yen /brokenbar /section /dieresis /copyright /ordfeminine /guillemotleft /logicalnot /hyphen /registered /macron /degree /plusminus /twosuperior /threesuperior /acute /mu /paragraph /periodcentered /cedilla /onesuperior /ordmasculine /guillemotright /onequarter /onehalf /threequarters /questiondown /Agrave /Aacute /Acircumflex /Atilde /Adieresis /Aring /AE /Ccedilla /Egrave /Eacute /Ecircumflex /Edieresis /Igrave /Iacute /Icircumflex /Idieresis /Eth /Ntilde /Ograve /Oacute /Ocircumflex /Otilde /Odieresis /multiply /Oslash /Ugrave /Uacute /Ucircumflex /Udieresis /Yacute /Thorn /germandbls /agrave /aacute /acircumflex /atilde /adieresis /aring /ae /ccedilla /egrave /eacute /ecircumflex /edieresis /igrave /iacute /icircumflex /idieresis /eth /ntilde /ograve /oacute /ocircumflex /otilde /odieresis /divide /oslash /ugrave /uacute /ucircumflex /udieresis /yacute /thorn /ydieresis ] >> /FirstChar 32 /LastChar 255 /Name /HelvCBC~1512430393 /Widths [ 278 278 355 556 556 889 667 191 333 333 389 584 278 333 278 278 556 556 556 556 556 556 556 556 556 556 278 278 584 584 584 556 1015 667 667 722 722 667 611 778 722 278 500 667 556 833 722 778 667 778 722 667 611 722 667 944 667 667 611 278 278 278 469 556 333 556 556 500 556 556 278 556 556 222 222 500 222 833 556 556 556 556 333 500 278 556 500 722 500 500 500 334 260 334 584 350 556 350 222 556 333 1000 556 556 333 1000 667 333 1000 350 611 350 350 222 222 333 333 350 556 1000 333 1000 500 333 944 350 500 667 278 333 556 556 556 556 260 556 333 737 370 556 584 333 737 333 400 584 333 333 333 556 537 278 333 333 365 556 834 834 834 611 667 667 667 667 667 667 1000 722 667 667 667 667 278 278 278 278 722 722 778 778 778 778 778 584 778 722 722 722 722 667 667 611 556 556 556 556 556 556 889 500 556 556 556 556 278 278 278 278 556 556 556 556 556 556 556 584 611 556 556 556 556 500 556 500 ] >> >> /ProcSet [ /PDF /Text /ImageB /ImageC /ImageI ] >> >> stream\nxÚ?=OÄ0\f?ÿ?GX?Äqâx½Ó\tÄ\bÝ\u0010\u001b\u001fËÝÂ\u0000\u001b¿ýÒ$\u0006Z\u0007©ªÔ¸y\u001bû±\u0013\u0007\u001cÌÏÇ;4ãá\u0016?à¹\u0018/àw\"ð\u0005¾|?Ë\u001b\tNð\b®Í?]¬óó¸TRWÒ¯¢?\u0010òì\nu\u001eûüükU?ñ?®kÕè\u001aì'¨\\®¼}\u000b8áæîõôyØ\u001f¾}ôHÁ\u0005\t 0½??3\\áuÉlº\u00078?å\u001a\u001c?\u0006°© «Æ&?àªR?\u0011T]°\tJ\u0016Pê??sZW]Â\u001f ?\bi¥è¿J?¼\u0015*? ¨»_W?²\u0006Î\u0006*b×ª1?\"Ù\nE\u000b¨\u001e<F\r\u0010mpQMÌö¥VáDC¨ä¶BùÑ?JºM?Í?bÝ&v\u0006?\u001b\u0014¡Øo?Ê#(Ömâl\u0002çÖ?yÝ?Y«?£]#µÍË°\\#Ô/?j,?\u0017VÍ6?w®Ý4î§¥.Õðø\n\nendstream endobj\n8 0 obj 313 endobj\n9 0 obj << /Type /XObject /Subtype /Form /BBox [ 0.0000 0.0000 622.0800 792.0000 ] /Filter [ /FlateDecode ] /FormType 1 /Length 12 0 R /Name /CBA /Resources << /ProcSet [ /PDF /Text /ImageB /ImageC /ImageI ] /XObject << /Im1 10 0 R >> >> >> stream\nxÚS(T\u0000\u0003 efd¤g`a` ` g`? Ì-PøP*9WAß3×PÁ%_!KA!P\u0001\u0000\bk\u000e`\nendstream endobj\n10 0 obj << /Type /XObject /Subtype /Image /BitsPerComponent 1 /ColorSpace /DeviceGray /DecodeParms << /Columns 1728 /K -1 /Rows 1100 >> /Filter /CCITTFaxDecode /Height 1100 /Length 11 0 R /Name /Im1 /Width 1728 >> stream\nù2\u0019\rY?.I²?¦u??3\u0005ÈA?\b²\u000526Ë8Ó C?\f\u00100¸P?\u0006¡p?\u0006\u0014)Ø¨RËÂ\u0005)Ø@è¼h»aHÆ\u0015\u0017\u0017m ¤cEãDí?\u000bÁ?I\u0017?!ÐA¹?\u0012?â\u001d\u0004\u001bJg??:\b73æy'\u001di?t79??¯ÂÐPµô¡h\"rZx\\.F?3\u0005Ð»B\u001eg?\u001b?¤°??\u0010C?½!Â\u000b\tZ?82)ÈªÚZa?\u0010^=\u0004 ?é\u0014\t?FbzFí,\u0012a?¼?\f m¥!<ÞØ¬%¨%\b/Òð?ý/HB\tÒI´°ÆÔVAB&Gèp?ø?è\"u/\u0004\b\u0010'©´ðZA\u0013?\u0017ë ¿Õ\u0004\u0018^\b\u0010 M¥£N\u0011n\u001cÅ4Za?ºé?\u0012!Ý\u001a??ùµ0°ûT?ô« ü+ù\u0007P+þAü/\u0011kcI¿JAäF\f\u0017ø0_ú\u000bÚÃ,r??~?\u0011\u0011\u0011\u0011\u0011\u0011\u0011\u0011\u0011\u0011\u0011\u0011Hcÿÿÿÿÿÿÿÿÿÿÿÿÿÿÿÿÿÿÿÿÿÿÿÿÿÿÿÿÿÿÿÿÿÿÿÿÿÿÿÿÿå²&\u0012\u0011|å²\u0012¬º0Ï?Á?\u0014þ~=Ke\u0006\\<R\u0010Â\f&\u0011ÏO´C?&~hÓ2w¯\u001cØMXpý\u0019ÞprÙN\b\u0011v¢\u0010d°?õoO7êç­?Ó¦þ[$V?Õ??y\u001eV\u0018KKý?)\nc?b\u0013\u0010¢?Æ\"\"\"4úxÿ?ÑZ6??k??s#?H/-@PÉ\u0002³E,Õ(¸-?Ë*®O?EÁl4?ò¹.c=?Ñq?ÈæG\u00030U9?ÈøÌ\u000bfb#²èö\"1\u0011\u0011ÿÿþ[&AèÞå²\fÏgób]\u001eÏ?$\u0002?e\u001aD¾YCF????ò4Î?ÁHy8\u0017µ´[°Å&\u0011xä/å¹l\u0013RÝ*5?¡??ÁO¢FP\n\u000eõ4\u0018@í\u0006?ppÓ´k\u000eèï§Ä\u001b(&æ«T²¸Ã9??\br=\u001c?G\u0019ÆlCaB\u0006\u0010eÂ î\u001döHz?7¾o?¯öÌ\u0004éþ?\u001fÏ\blS??h\u0010à¥Â\u001b\bn(?ÁB~?°ô½è\"ð9ü3[?çæNú?U4Ã}¶ßíÿùpDkïü·ñ\u000eF\u0005£?\u001b\bb>ÌÂ?\u0010¸C\u0001\u000eE\u0011 \u0017MB-á\u0013?íQvÂ.òpçÇòzNçx¿ÿ ?[{Â_üÏ?y?M\u001a\u0019?Fÿ÷ÿ?Õ:ÿÑ°=\u001aÚsXsðmì¯h»Í?û/Zº\b8?Û¡\rÐÂÅþ¿Ì\u0005ÿÿsàì?\bFÁ3?zQMÏÿ¹þÆºEÂ¯Ã\u0005?\n?Cÿ?mÅ´\b\u000bbíÐ·C[ýpD{¬Ø[³@ì?\f¸&¿ø^ým??÷9ÍÜ\"oõ~ÒÒxa ?¹?±E\u0015çn$a?$'?Þ¿Ë~\u0015}[r8vÛ4\u000eÉ`£\u0001óúê?káC\rÔó?2ÜÃ¬à?ÞÍÛû»mRº0¼çih\u0013ëTÛ\u0015¤Û\u0010©Ô0º³¼?DEûñýq°j?£Ï9s'?À]Òmï?ñÍðÝcà?ßÁ\u0006ÆÆÄlFÅqQQ±\u000býÄDDD|Gýzórô?F\u001cßC?¡º\u0004S?º/>·Ã\t±A\u0017?(¸I\u000b\u0002¸_Û$=?\u0019;4C/\f$?D|ì*??\u0005ÜDc°Â©p?\u0014Å#u?F\u0004?\fBëú|1?\u0012X0?\u0011ÿÁ?\u0011\u0011\u0011\u0011 ØKbÿ\u0011c\u0018b\u0016Â?Ê??T???õÞ#?¾#ÃýØ??\u0018?q\u0011\u0011{\u001e\u001f^Ç?<øñ\u0011?\u001c?0ocÃ\u001f¨ã\u0011?ñÅ\fDb#ÿÿ?Ñh4K\\Ì2CËVÃ$!\u001cå¥\bÐ2Le¡d2C^M??¢8\u000baÎf9?¨-?¹\u001e1\u0011Ù\u001f/?Äb\"\"#?ÐVS©m\n3\u0001LH;D9º?mòÚ+\u0004¿7C\u001c¶?\u001fA\u0013bO\u0011«±Á?Øqÿÿ-?Ì#?x\u0013ËX 2\u0000¬ý-5PÉ3xË0°2AÈìe?¥\u0017\fÚ#?¸et¬º.\u0010Á?\u0005°T11\u0019?¨d?ÀBìF\"2ÙZGÈú3Î\ns?\u0012:\f ÓM\u0013\u001c;»Ñ!ú\u0004\r»ñ§þY\u001b\u0010Ù\u001b\n|!e4\u0004oïÍ?ª.Ã=IÄ\u0011<Ïé.ÒÔ\"q??øZ\u000b,«.ÂØ[\u0004£?òÌ\f?\u001a\u000b¦!\u00060Ä&HÑcùtâ\"\"ÿ,Î¨óè÷ÞÇV(¸?}c\u0011\u0006??¦.$\u0018HÿùmQ?ËÄµÀòá?ËP£>\u0019!¹?¿,Ò?|2CAÞ#-\u0000y?É\rSy¼®2;±Ü?,#\u0000¶\u0018#Â)\u0011FI?Î¦N\u000ba¨^#â[¥??O\u0014\u0019\u001e%Íµ2E\u0011\u0010ÀÊ\u0001\u0012A\u001a\u001e\u0010%ùi?0@°E <$\b¹ %DH\u001e?^m\u0019åÄ(¥?\u00042¼\u0002à?\r?\t$\u0012\b\u0010$\u0010A\u0004\u0016L\u0011##iaÃ\u000b.\u0003¸ Ì?àEè\u001a\nÂ\u000bU\b\u0010\"??\b\u0016\b´í\u0007BÚP?£\u0004a\u0001?\u0014BAh ?\u0005P?P-Pb\u0014SË:ÜpRá#.\u0010?a\u0004ÚHï\t$¡\u0004\bÄÁ?\n @¡$?%æ0??ØÏ\t.ßA\u0005×h\"\u0010??x? Áó\u0006G4?,?h\u0011\u001e\u0003\b¶ð½B\u000bI ÉðD\u000f¨?Pw$\u0016\f?\b$ª\u0018I?!O²Y\u0004Lu\u0015¤???\u0006*?\u0014\u0011¡Á1I$\"!?®Y?Ñc?è\u0010nb4?R\b2\u0011L ?\u0004\u0011ÖI¤?IØòÎ??èÏ ?ÊÒ;Â@?ðjA\u0006\u001d:@QØai?\bÅ!Qu¤¡- ?!Ô¤R\b\u0013­ \u0018$b\f\u0010?ýRV\u0010A\u0004\u001bZ@?\ti\u0002.Íl$?J27­?\t?m\u0004\u000bÔ¤Ä ?J Ä\u0012CÁÐB\u0002\b$?¦0?\b*¢#Ib?gðA\u0010ó\f ?A\u0005N\b, ?ð@? J©7?\u0004Ä\u0010@?\u0010?°@?`!?¤\u0012\u0004\t\u0004R} Á±\u00040?\f??ÄÜEST\u0010D3H?\u000bè\u0018¡ÄEBA\u0004h4???â4PHJP%l|$\"#ÒªCõ\u001c¶uF\u0000ð'?±&l2\u0000à?rÕÓ#?I?ÆZE\u0004G\f?70?c,âY\u001c2A@?²\u0017\f×0æAY\u001cÎg\u0001l\u0016ã2?<\u0015\u000e\n%?*?Ùn¯7\u001e??²1?,4Ûn\u001dÚV\b¾Õg#ÓkÛ\u001fö+·³bÝÒþ·rÝ;°ª?u,?Am?Ó\u0014\b[iA\u0003ñ\u0013Ñé?? 7zzÐ0î?G?Ý>Ãêì;öÞ¶Ý?·~Þ®½·«kÛu¶«a¤\u0011?o\b%?bÓ\rá,ðÎÍ\u0019ñ\tMI´?\n'?=?\u001a ?\u0019þ\u0011Ø¸4v\u001aA\u0002F\u0018d\u0010Ð ÊËÔ ¤r.\u0019\u0001¶`zm#\t|Ö\b[¥ÇvÎû#?I?3\u0011â4?xcPÆ\b?\b ô%\u0001?ÙnS?\f?Y0£S&#Hæ`?g£Tj#T\b\u0013`?°ÒI*L$YÈ¸K\u0001 ?\u0012¢fG)\u0012%?ÄæL??6Ã&@\">\"\u0010M?\t\u0003T?\b$Ø?zUÓjn\bÃ????\r=­\u0010?q?#ÖÉvÙNÈY\u0004\u0012?° ?H$?@%J??âqp[\n\\Sæa?2qK?a.G\bË@?l¶\r?\u0010Y?Ó\bÂ\u0012A*\b  IRA$\u0015*AfN\u0019!°Ödc:³?ÈÈ³.d¸Ý\u0004Ø0Ñc?¦\f @ÙÚ\u0001?lÕ?\n\u0011}3\u0014 ê\u0013h ?±\u0002\t*\bÎ?\u0004\u0010A$?A ?I ?AF¿S©??é;L$?n¤ÎY\u0001 ?;Ã=??\u00126f0G EÔ?p?5?-¡$©\u0004\u0012\u0014\b$\u0012I$\u0010J\u0012T?v?[ô?.ª\b??Ò·´¶ÐÒ\f\u001a¶\b\u0010ËxA\u0004b\u0012\u0012?a\u0002A%¤ B?I H ?\u0005\t%IRHî¹\\­§Úü Dµa)C?íÓ·$=$\r\u0004ØF\u0010\b\u0016?\b¹ ¡1\b*]B%-$\u0012a\u0004\u0010A$?Ç ?\t$?$ É[6\u0014Îä²%??\u0014\bÏ??µÕ$\b\u0018i{n?·]\u0004N\u001f¤\u0010!Ð@?ª?\n\u0014%T?RJ\b¨ÂA $\u0012ÂJ?T\u0012P?HÞý?Éâ\u001b\u0004E?\\!0\u0019??!s·\u0004Ý$\u0010M?\u0017x*»Óé\u0003u¤\u0010I\u0004!$?\bK6 '¤6\b$\u0011ä\b, °Fp¡$???\u001d¿??¡?MB,\fÐ)qH?¾?%¨jè6ëI°??Çakô½\u0004\u001e???Q%?%3L ?I$%Y\u0016dø4?°?A(A(A9?\u0011??\u0005\b·ÿuH\"cí$¤¦\u0018!\u0004R\u001aq\u0004\\/\bBÂ\tßT¶*ï\fvNÍÇ\u0019ÈÀtð?H\u00112!$? @? öÌ\u0018`Õ Ã1\n@PA1)l,#:*\n´¿¤?´\u0010H'\b?Á\u0006\u0018Â?\u0001öG\u000eÚa'\u0004\u0017îýzO?ßEûâ\u0014JÕ?\u0010@??n%'%º?8AD,\u0010B?\u0010I\u0002-é\u0010³µþ?.aúI1\t Ü,9t!¶?3«\u0004\u0017µWøn«\u001fëá3?\u0004G\u001aA\u0019Ð?hT\u0011??ì??b \u001dÆ\u0010V\b*\u0004\t\u0004¬ Ä/¦IÒmR¨H&\u001db9¬\u001cù¶?P?\b\u0017_ê¿ÿâ!?H?\u0005\u0000?\b&!\u0003%%A\u0005`?l\u0010,ÔiPúJ×TºÃ!KzD\n\u000eÅ\u0003\bM=\u0005á¥éî?ÿòáDO?b/\u0012¤a\u0004\u0012BJ\t?b\t?  I)r.2H\u000bÜ\"ÇqZWh*I&Hz\f¾½á?\u001b¡c\u0017ßÉÜ0?l0?Íq¤?Hé\u0004?Øä\")\u0002-\n\u0018ÉØ[KFtÜ,#@¤X$!\u0007[i\u000eµ¯·®á?Üa?\u0004+I!\b$\u0011Üì I\u0002,Ü=(?t¢?Ká\u0013vEdF\u0012?{xkþÕ\u0016?\u0011\u0011'´I\u0004?\u000e?\t [a\u0004Ó\u0014Â\u0016ª?\u000bbw¿?´?ÛÛ¯ÁÒA$?mB\t \u000ba\u0004t?B!l¨a\u0005?\u0015¥±V\u0010M×·Õb?H$Þ?iC\u0010?k\u0006\r\u0005??\u001aM\u0006Â_ìRéB¤\u0015RH.ÂK\u00060¶80¤p\u0015¤øz½$?A% ?Qk$\u0003 EÂ°Ò\u0010bm?{Çèì?IB\b­`?­\u0004±Ï\u0006P?\f?ñ°¿êv\u0016Äo\u0004\tRJ¸\"U?\f\u001ai<&ÕZ¡\u0016\u0019AW\tlA`Ä\u0016ÃIüT2\u001d¹BÅ\u0005?\b?ë\u0007PÅXkÇÒ ?\u001a`?\u000bI\r¥ZÅþ?a*Õ7Zè/JÇ¤Ã\tQ?0½°??)Ç\u0006:A?`ízA?FâMU¤;\u001e»?°­.ékJ6?ÐVÁ\u0005`Â\n\u0018?\u001få´hRÙÐd Í\bà\u0011{J?~\u001b\b(?æ8}??3XûiB~\u001b\b(WØi\r?\u0016?m-.Åa.\u0018Y\f/j ????Ý\u0007$e?Fï\"ÀÓI?ô?ä\u001cøH0Û\u0017 ?²^é\u0006Û\u0004úL6Bòá\u0004Û\u0010^??àÇ\u0011\u001fÿå´P\r0¶£å¢\u0014ÿÿÿÿÿÿò×XQòØ+\u0019Ù?Ò?\u000fK<çxdïHó=?ÏÆò8ðj8!ÆG#?øÄ\b\u0018 \r8\"÷|J·\u0006<#xm\u001e¿Fö\u0003Á\u0011á~¸MÃ0þ?^þ?´?ÿà?_ÿÿÕ¿ÿ A×ÿÕoJþ×ö«a|.\u0018a&\u0018'M?Å¶?¡EÅ\fB'\u00101(~\u0018?\u0018Ð?ã?\"#\u0011\u0013®\"\"\".oäd7\u0011\u001fòÚÖ\"\u0011?a\u00172G-?çÂ?\u0019\u0011\u001c\n{\"\u0002?\u0010àB?\u0018T ?×-rA\u000e\u0004 ?pè?Ñ½?nhÜá6??~\u0011½£xg¤\bRÁ\u0010s§¦é±\fV\u000bZºü?¥äX?Å?»ýD\u0017ß~\u001a\u0016?Á?HA?_\f\u0015\u0004G¦;ÿá?jú_?\u00134?\t»1\u0014ý\u0018ºô\u0010Fàõ\u001a\u0018AÁ?W×Z7ÒY{\t%Ý\u0005\u0011\u001fiZQVrHÏ?QLS\u0014l!-\u000b\fPb ?\u0015\u0018???DD?È¦Pd<ðÏ\fä{??\t-rl??Æf!O\u001c\u000er\"\u0002?\b\b\u001d£X4k\u000fð0à?\u0004Ga\u0017a?^:(ð6Í\u001bØ?l[{Òn\u0011~Ñ½ ??)`?b'§%ýÿ§×OO?\n?Q??â°ÂUwA?û÷ßl?WT?\u0018?ö9½/ÿÿý+Ò\b·\u000fÊ#H1F\u0004Ë?\u001d®??ªt@ÝÕ\b??v¾­m],½ µmB?Þ°Á?+jÚM¥fê08¨¦)?6&])?\fNÝm?b?\u0014Ç\u0017>Ö?B\u0018???Ëd£¬ £\fö<3Ùøà§£Ì÷-p¡?\nQ??6\u0014Ò>Ï¾ ü\"ì?\b¼\u000f^\u00117\u000ew4T\"ú÷»\u0019ûè ßH&ø\"=Ð ãB?!Htw D{\tkWßêß«´¿[§?[ÿþ?~ý&DÇÓ­ÎEm+I´´?ìzAÃ\"\"··fë\nÁ?L[\u0015I7Ë]K1i\u0004a\u001e?§\fPbSÁ? ËP)?5?Ò¯V¬DDiábªÎJ©mÓË\\´$\u0012 ?(ØW¦?F\"\"\"#òÙW\u0012/÷)q¦t)l\u0003?\bú!æ??,àC?\u001b\bC\nl-?[?-qp?\u0002\u001cÏæ\u0002 íB6B.\u0006\u0011w\b¾hÞ\r\u001am\u001bú\u0004\rË\\+?ù\u000f@?õ¥?\b=\u0007?Ø?®¬\"\bûÜ/í[b?,õ¯l0?á?7Ë\\X\u0013üÀ\"NÍ?êÿÝpÄ/ÐLy¿ÿ<Õ6Þ\u001bµ°¶??wøHëÛKì+\f*Û¤P#\u001b\u0018b´\u0010aý$¶*ðÄ\u0011\u001f\fASÝ\b?¤?a(¤¢\"\"\",QÞ0I?\u0004?ª3\tpb\b1\u0004\f!\u0018?å²(éV[\u0004¦hTCf\u0019\u001cg?ã<f\u0019£:9lV\bNÌ\u0003?\u0007O?¿äíì?4K\u0003O?çïüC|-???KÿöõQo¾+Éõ?Å@ÆÄ'I¾\u000bÿ8\tùdë|½*º?K9sKé8[=Zas\b,.ÃHÂ[6}1±±;C®Å!±Ilã?x0@Ê\u001c\u0010?ß\u0011\u0015\u0011\u0011\u0011\u0012\u000e?Ë`ÐÂ\nÃ\u001d?B1ÿËe,Í#6|C8Í?r×3#6m?fÙ¸àSP!¶|Î\u0002^\u0010j?\u0004\u000fÿ\b\u001c?¿\b??\b??÷Ñ|ÿù¨á_¤ÿO¯\u0016ÿño­éþ½\u0016ïÿûÅê?ÿø'ÿït?ÿÿrÃkikk­õõú³°¬0?\f\u0015?\u0004\u0017OË](Â[\u001fìl`Å1?\u0010¢?ìBÃ#j\"\"4ñ\u0011\u0011ËéSrØ!?Ä*kÖ\u0018!\u0018?1ÿÿÿÿÿÿËg@V4\u0003Ì?¥® )\f\u00185\u0001\u0004¨\t$AÇ-U`¹?.h\u000e]\u001c\u0006\fÀ?a²ì-\u0003\u000f`Çu\u000ew\"8@Êr2¾\u0018yÇ8äs\"?\u001b$;4\u0019\u00106LìXB:vñ\u001e`â\u001dñ{ú}?aºì:(\u001e\u0012¿Nï½Þõ÷[ÏåÁF\u0010}ßsá?Ö?§õ~½ß?\u001d¿uäQÈÇ8÷µ?Ó??k_èG\\û{®?åª0þºM-p?ß|+`¿?a?\u0010ZMõû\u0004Ù\nèðl®$\u001f?tß×?6 ºAá?\u0014\u0018û|??8B>\u0019?\u0011\u001f?sÌ?ã?à«½sÁÒ?\u0011\u0011\u0011\u001d÷x?P??jt·#«ß\b\u0010dÌ1\u0012b\tývÏÁ\u000fù1Ðo\u0011½uûý8d\b\u001cã?9Ç)Ê\u001cã?å9C?g\u001dY\u000eK\u0011\u0011\u0011\u0011\u0011\u0011\u001a\"¥ð½z*hÚ.?éHù\u001f#²>G\u0002LDDDDGåª´?¢÷-P@ØÈ\u0018\u001c?rÇ8å\u000e{)Ê²?«\"l×LDDDDE×8ë\u000b\u0013?¨ZnEÑ´]\u0017Dt\\\u0012?+Ñ\u0017\"ä\\5ó0+Ñ?\u0003¡\u0011üµ\t? ?R0\u0018(\r\u0006ÃA°Ît\u0003\u001eòÍ¢;\u0015\nC\"á\u000e\u0006s??\u001a\n°ËÂ\r|\u0010;ùg\u0014\bTF3?]\u0017GÃÀ?@l(\u0006ä \u0010?Úfa??·??\b6¾Z\u0002?9°Ð`3??À?3\u0001?øei Ûª\t?\u0000ÙæÉ\u0001\u000e\u000e?HM\u001aë]\u0007Ä0?Úa?!C!C!\u0010CÑ?¡\u0013\u0010þ¡\u0004\u0018~ö¡9\f)@5\u0006B?x\f?!.\u0010?\u0005\u000eö?\f5\b=W·þZ\u0015\u0002Â\u0011jC?\"\u001b÷Oª\u000eò ëwÐOþ·à°ÿ×¥ª\u0004Ãÿÿþþ­ûí¸Vÿ½ïþ¼QàjïÿÉ\u0000a&\u001fõÿÿá\u0005ßöü\u0015'¿ßÿÈ\u0017G®õó?Ô?mé}ÿª\b/\u0007\u001f\u001f[ÚA\u0010Î9Çö¾«ßíþ¤&?êý°¨?Ò\u0012\r¿\fà.ý~?èèEÓ¯¶f\u000f¶\u0010U?\u00143ÀbAÈ\u0012\u001b;ÝûÝØa\u000eÂZeÔeÒ\u0006Å%ä0Ñv?µ^ÌÁ×é?\u000b!\u0001¢4\u0019q\u000e\u001bU « È\u0011kUû\u00198e,S\u0010­<2\u001b\u0007á¯\u000bÕ?\u0010ißþ®Ðao?\u0013M\u001d\u0003\u001e\u0012\u0012\u0018A\u0011÷ød3Ô0A?Xdà?\f>À²ø&?_?A2Á8â\u0018C\fB\t'ïã?\u0001\u0016º`ÉÑt\\0çQ\u0013:?pß]¯ª&b1\u0011\t$\u0019T\rØ>\u000bÓöapÃ\u00047ì\\/YØ?ÐP\u001b\u0005C Ó²êqÈÇ8à?øe\u0019)\fÓb,«R\t½~V\u0000Å\b???ä\u0017\u0015}QØðé±\u0013°\\|!³µTÇÿÿÿÿÿòÍ×ÿÿ?È·\u001fÿÿÿÿø\u0000?\b\nendstream endobj\n11 0 obj 5783 endobj\n12 0 obj 52 endobj\n13 0 obj << /Type /Font /Subtype /Type1 /BaseFont /Helvetica /Encoding << /Type /Encoding /BaseEncoding /WinAnsiEncoding /Differences [ 0 /.notdef /.notdef /.notdef /.notdef /.notdef /.notdef /.notdef /.notdef /.notdef /.notdef /.notdef /.notdef /.notdef /.notdef /.notdef /.notdef /.notdef /.notdef /.notdef /.notdef /.notdef /.notdef /.notdef /.notdef /.notdef /.notdef /.notdef /.notdef /.notdef /.notdef /.notdef /.notdef /space /exclam /quotedbl /numbersign /dollar /percent /ampersand /quotesingle /parenleft /parenright /asterisk /plus /comma /hyphen /period /slash /zero /one /two /three /four /five /six /seven /eight /nine /colon /semicolon /less /equal /greater /question /at /A /B /C /D /E /F /G /H /I /J /K /L /M /N /O /P /Q /R /S /T /U /V /W /X /Y /Z /bracketleft /backslash /bracketright /asciicircum /underscore /grave /a /b /c /d /e /f /g /h /i /j /k /l /m /n /o /p /q /r /s /t /u /v /w /x /y /z /braceleft /bar /braceright /asciitilde /bullet /Euro /bullet /quotesinglbase /florin /quotedblbase /ellipsis /dagger /daggerdbl /circumflex /perthousand /Scaron /guilsinglleft /OE /bullet /Zcaron /bullet /bullet /quoteleft /quoteright /quotedblleft /quotedblright /bullet /endash /emdash /tilde /trademark /scaron /guilsinglright /oe /bullet /zcaron /Ydieresis /space /exclamdown /cent /sterling /currency /yen /brokenbar /section /dieresis /copyright /ordfeminine /guillemotleft /logicalnot /hyphen /registered /macron /degree /plusminus /twosuperior /threesuperior /acute /mu /paragraph /periodcentered /cedilla /onesuperior /ordmasculine /guillemotright /onequarter /onehalf /threequarters /questiondown /Agrave /Aacute /Acircumflex /Atilde /Adieresis /Aring /AE /Ccedilla /Egrave /Eacute /Ecircumflex /Edieresis /Igrave /Iacute /Icircumflex /Idieresis /Eth /Ntilde /Ograve /Oacute /Ocircumflex /Otilde /Odieresis /multiply /Oslash /Ugrave /Uacute /Ucircumflex /Udieresis /Yacute /Thorn /germandbls /agrave /aacute /acircumflex /atilde /adieresis /aring /ae /ccedilla /egrave /eacute /ecircumflex /edieresis /igrave /iacute /icircumflex /idieresis /eth /ntilde /ograve /oacute /ocircumflex /otilde /odieresis /divide /oslash /ugrave /uacute /ucircumflex /udieresis /yacute /thorn /ydieresis ] >> /FirstChar 32 /LastChar 255 /Name /HelvCBB~1512430393 /Widths [ 278 278 355 556 556 889 667 191 333 333 389 584 278 333 278 278 556 556 556 556 556 556 556 556 556 556 278 278 584 584 584 556 1015 667 667 722 722 667 611 778 722 278 500 667 556 833 722 778 667 778 722 667 611 722 667 944 667 667 611 278 278 278 469 556 333 556 556 500 556 556 278 556 556 222 222 500 222 833 556 556 556 556 333 500 278 556 500 722 500 500 500 334 260 334 584 350 556 350 222 556 333 1000 556 556 333 1000 667 333 1000 350 611 350 350 222 222 333 333 350 556 1000 333 1000 500 333 944 350 500 667 278 333 556 556 556 556 260 556 333 737 370 556 584 333 737 333 400 584 333 333 333 556 537 278 333 333 365 556 834 834 834 611 667 667 667 667 667 667 1000 722 667 667 667 667 278 278 278 278 722 722 778 778 778 778 778 584 778 722 722 722 722 667 667 611 556 556 556 556 556 556 889 500 556 556 556 556 278 278 278 278 556 556 556 556 556 556 556 584 611 556 556 556 556 500 556 500 ] >> endobj\n14 0 obj << /Filter [ /FlateDecode ] /Length 30 >> stream\nx?S(T0T0\u0000B\b??« ïìä¨à?¯\u0010¨\u0000\u0000P0\u0005Ý\nendstream endobj\n15 0 obj << /Type /Page /Contents [ 24 0 R ] /MediaBox [ 0 0 622.08 792 ] /Parent 2 0 R /Resources << /ProcSet [ /PDF /Text /ImageB /ImageC /ImageI ] /XObject << /CBB 16 0 R >> >> >> endobj\n16 0 obj << /Type /XObject /Subtype /Form /BBox [ 0 0 622.08 792 ] /Filter [ /FlateDecode ] /FormType 1 /Length 26 0 R /Name /CBB /Resources << /Font << /HelvCBF~1512430394 23 0 R >> /ProcSet [ /PDF /Text /ImageB /ImageC /ImageI ] /XObject << /CBE 17 0 R /CBH 21 0 R >> >> >> stream\nxÚM;\u000bÂ0\u0014?ÿÊ\u0019uÐÞ?Ä¦v³µEÄW1? â ÖÅ\u001aÚA7»é?`.d9çûn\bjô§\u0006?Üô÷­B&\u0019?\u0016E?r?\u0010L\f¡ÐÜ]©æ\u0001?2>(ÿè®Ùã+#1èrj¡`u¾Ó$ÿò???$çÊ¹aJ/\u0011DÎb*?1Ê\u001b[Å\b)R¬%??}¹?õ?Å?\u001c¨c)b?n?±1´T?à??Ç¸À¬½r\u0016\n¯<\u001c÷?ëö¸»æ?ÓPóCf?\u001f)ð\u0003r{<Á\nendstream endobj\n17 0 obj << /Type /XObject /Subtype /Form /BBox [ 0.0000 0.0000 622.0800 792.0000 ] /Filter [ /FlateDecode ] /FormType 1 /Length 20 0 R /Name /CBE /Resources << /ProcSet [ /PDF /Text /ImageB /ImageC /ImageI ] /XObject << /Im2 18 0 R >> >> >> stream\nxÚS(T\u0000\u0003 efd¤g`a` ` g`? Ì-PøP*9WAß3×HÁ%_!KA!P\u0001\u0000\bv\u000ea\nendstream endobj\n18 0 obj << /Type /XObject /Subtype /Image /BitsPerComponent 1 /ColorSpace /DeviceGray /DecodeParms << /Columns 1728 /K -1 /Rows 1100 >> /Filter /CCITTFaxDecode /Height 1100 /Length 19 0 R /Name /Im2 /Width 1728 >> stream\nù2\u0019\rY?.I²?¦u??3\u0005ÈÀrvY\u0002Ù\u001be?ÀÈ\u0010á\u0003\u0004\f.\u0014 `¨_\u0004\f(S±P¥??\b\u0019Õ?\u000e?Æ?¶\u0014?aQxÑvÒ\nF2\u0004h»aBðh¼i\"ñÄ:\b73ÂS<C ?iLðA ?s>g?qÖ??Cs\u0010é\bzü-\u0005\u000b_J\u0016?' ?ø\\.F?3\u0005Ð»B\u001eg?\u001bT?\u0012ñÂ\bp?¤8Ah?\u001cpdS?U´´Ã\f ¼%A(%úE\u0002`????»K?þD?P6Ò?olV\u0012\u0004?\u0012?\u0017éxA~?¤&³ÿI&ÒÃ\u001bQA\u0004AB&Gèp?ø?éÿÁ\u0002\u0004\têm<\u0010DêA\u0013?\u0017ë ¿×ÿ\u0004\b\u0010&ÒÑ§\b·\u000ea ?Ai?\u0012ë¦\u0018H?tj#ðI?\u0012ùµ0°ûT?é*È?\nþAÔ\nÿ?b¼E­&ù\u0007Å ò#\u0006\u000bü\u0018/ðÂ\u0006\u000bÚÃ,r??~?\u0011\u0011\u0011\u0011\u0011\u0011\u0011\u0011\u0011\u0011\u0011\u0011Hcò¹Z*Hµ\u0014)4$èNÕ\u001174C\u0011\"\u0010?i¡%ªehDI´ÔNÇBK\u0014IÑi«BR?JàÑnB4B1\u0011+?Er\u0011nV¦HGe(²\r!\u0011??sT$ê\"YCRÏh®*?#-ÈDØ?\u0015á\u0013p¥2ä&BÈD·)C\u0012¸4$Þ´2Üº;\u001d\tn\r\u001dÍ\u001dÍ\fËT\"\"%¤?âY\u000bs²?íFwùÓ3Ï3Â?æ\u0000Ú\f?\u00030\u001bø\u0012ÈÀËÇ?¸Ö??ÆhDDDEò?£hJä©yÝ£²??ñ$Ðå?m|K@*ÅyÙ?2RC?¤M??ñ\u0012È\u001aÄ®h?ÊÒó²TV\u0011ß£²¤8?Dm\u000bñ*HD\t\\\rb?\u0012??Â\u0012!\u0019\u001a¯â\"?òn?¿???,Á5Çÿ×ïÿûÿÿÿÿ×¯ßÿÿÿÿÿÿÿÿÿÿÿÿÿÿÿÿ¯ÿÿÿ_¿ÿÿÿý~ÿÿÿÿÿûõþ¿ÿÿïÿÿ×û÷ÿû;Ñ}#hI·#\"Ô¦Bè²\u0019.â#?§_5';-Gf¹äK20!0DP)9?\u0006Hd?¤?lRpç@r\u00189V\u000ehÏ²A??~%qQ\u000eüB?#\f?Èa\t\fØ¤??°ç@å !£<d?5\u001a?\fM\u0001@)Ð3¦\b\u001fæ`Ga\u0003\b\u0018A?\u001f¿ÈRS4f??\u0019Ô6\u001a\u0019Ô3b?°a'S@al\u00100A?\u0006\b=ýÌ?\u0016\u000b?!8\u001aa\u0012?ý\u0012?Í\u001a'6?¢gh´?þ.#?à?K\r0?ùþ\u0011\u001f¼Ñ?GÁ?Ja¢Sh?\u001f¿?¢UtKPÑ7Â\rþ?\rú\b6n\u0015\r_×!\u0011ØR:¯?DztKPå½\u0002\u0007ý\u0004\u001bô\b\u001d\u0004\u001bA\u0006ÐMÿá\u0005è Ý7ôßí?v\"P?\u001f|Dz ¼ ?jÞÛü&þ¬_\u001b\u001fþ?©t?kr*ïâï!@?MzýÊ\u0011¢3DÍ ½&Ò¶EOÁ\u0014õ\u0017vE\u001a\"W×ÎÊ\u0012?êÚM?A\u0011ÿüØ\u0017\f?\u0014\u0010Å;ÿ\u0011\u0011_«VÙ\u0004#ÿ?\fød\u001dY\u0007?\u001aúÕ°d\u001fÿÿäà? '®EWÎÄ*ô??\u0006C\u001fý?\u00180`ÿò]k÷VDÄÿ_Vj¦±?±ÿÈhìtÊØßý+\"byÅÿVæ¡\u000b¢O_\u001dÿIÉAúÚ^pÒ´È<\u001fµÌ?®¢D!\b!ÿÒr\r\u001aÇoð?\u0015?¬?bFßÿÒM?]?m/l$Ã\t\u001f5\t¯ar\r\u000fra\t\u0014Cÿ«gT%ÍûVÒóÆ)0ÂGÏ\"\u000fíÿI¶\u0018.Ã\u0005`Ì\u000b?\u0004`Á&!1LBØñä­b$IôØÃ\tpÂ°`?sL°ÂL\u0018%\u0006\u0012`Á-?\u0005ÔÈB¿mWb\u0016Ä·?!.Ä Â\f ÂÃ!#ê?Âã$?Þ?? Åa?Ç?!hF\u0018?\u0018?\u0018 Åa??ä\u001a;Õ\u000býÕ6\f\u0013@ÉM\u001dHM\u0019 Ê?«È®\"øÄíÓ~é$Ø?\u000b\f'\u0006\tÜ0?\u0006\b\u0018'\u0006\u000bÜFý°?@??\"\"8?üìè[ö\u001aJâ\"\"&?DDGì?A?í??\u0016üÚ_??Ãö\u0018J?;´T?f¿\u0016DG\f?0?²Xgd:;2>$\b¯?`ü0`?MQ0ÄO\u001e]\tÚ«Î\u0006bA\fA%~4¿ÊDJ?\u0002A\fBJÇ5®\u0010?Dmk¹^\u0000?§\u000bM0?D~$U\b\u0001\u000eS?a²8?¢6?DE?\u001cDDGâ\"\"\"\"\"v$?ÂÌ?Gs_-Í\u0010?\"K\u00116H¾D?#\"Õ?\\?\tÚEò\b?dvT?!²¹¢\u0011ø?Ø¢\u0011Ä®H?é×Îæ?¢P?q$4\"D?È\u001a\u0011\u0012ÞÐ?Äw4FÑ(Y?ÑÜÑd-CöVÎRú?²¢?Ê6I\u00110?æ?âÊg$??pUð@?·.?­e|\u0014§g£â\u0012\u0002\u001a???ã.!&eÄ$2A?3aJ¶NÉ\u0000?\r?2àäá? Î¨~'i\u0006J\u0006u\u0014§\u0014??ÆR3c\u0013?Ï\u0019á\n³42\u0018A'G?æp9 \u0010?<ÉHÏ?@ødpÀ `ñ ?Ð@ý??\u0004\u001d±\f Í\u0016?&\u0011*Ge&}?\u0006t3Æ\\0|\u0017'\u0005ÐgØD\u0010\u0018³ùp^°D\u00181?`?ú?ø>%ðh?\u0006?Í¼?î'?\"Ñú&wR4Q4\u0006=ñ\u001e$Ü7?;a\u0011m?E°Þ&Ç!1û\u0012ÿá\u0011ûÙ\u0012tJö0½?\u000e?\u0006ÐAµ?\u001b?\u001bøOé\u0006ø\\ ß\\?C#;äTP m\u0013#Á\u0006à?\u0004ßH\u0010o?t\u0010oé¿ZnÇ¦÷úKêï\n/?\\?¬è?Â*ÑÕ\u0010%\tö\u0017\t½Ö?¦þ\u0017v?õ?ôwE¿A!v\r÷«÷\u0004¿zÏ\u0004\\xà\b?jH]?\u0017§§ü%_}\u0002à?~9Åñ[ ?_ßt!~y|A\u0019ãNí?\u0007Ù\u0004#ßý?Áï¯?G?¸þ?\u0005? ÿ_]Y\u0007\u0002øü?×«çjkø?Áyúïâ\n¿à¯õä?¤0®ëuè?G×?\u0006^¼kâeoÚò\u0010Jt\u000bû×È¢³Ëºä??r­}ÒÂ\"2>?.jZþHi.H;\t*\u0010ÒË\u0017?\u0007ÚÚü\u0015?Ú­\u0012;\u001fì*ÙA±\f)óÞÂV\u0012°­¯°ÂIØI°?|m{(3d?ó~èÔ­+[(:¦Òí\u0006ØKÌT0?9??\u0012a?\nÁ%?\u0004 Á&E\u001f\u0014F\u0002\u0011Á\u0003\u0014F\u0003±\b1\u000bùUPÂAa¨a?¡?àÁ\"?(\u0018I?\nÃ\t\u0014à?pv\f\u0012# V\f??#?h¼dÇ\u0014?Ïb\u0010b\u0010b\u0017&8?-Ä&%¼0¼0R8?\u0010`ºÙ¢\u0012?¥¸£`á?LPb\u0012ËqC&â?\u0013\u000eØ®?\u0014?Ïb(1\b\f\u0014*\u0006\b\u0018 `«\u0006\u000b\u0006L@!!?\u001bdìDDB6Á28?\u00100@Â|0X` Â¢\u0018G\u000e\f?¬'!?\f?'ÄDDEÆÄGûø???âGX???\f\u0019r¿­*­\u0017ïó°Txû;P\u0010ØCµ?Í½çd¯UHíd3|A ¨¥ª×ùÚ??Âù\"¦?\u0016YË6wßwi?\u001cDDGâ\"\"?ïõÿÿÿÿÿÿýÿýÿûÿÿÿëÿïßëÿÿÿÿÿ_¿×ÿÿ¿ÿÿåp4A?&\b?\u0005(d»$\u0019@RC82pC 9 0T\u0006\fÌñ?\u0019¨¾MÁ?\bf¢%Å)Ä a\tÌñ?\fÔy?i\u0001¼??3?`þ\b\u001f\f Â\f Â\rýý\u0019\u00163Xh3#P.T\f?\u0006\fÌ?2C(\f\u001a4\fÐ0H\u0005ÉÁ?\f\u0018úü\u0017\u0004B`v?x¢s\u000f44N?HáË;DÎÿýÙ \u000bÑ\f\u0014&\u0010uX'?Â\"@a\u0011l4G\u0011óÿÄ\"=z%¨h?î\u00107î7ºA¸Aµ\u000fA×ÿ?Dzp?È\r\u0013\u001d¢È}è?Þ\u000e?¡?H??!¢Èú\u000bÂ\b0Òo\u001fT?Zq|aõô\u000b´\u00107M«þ?oÒpÂu{\u000fÿ×Ó¤ò*ÕøÝ²\u0010\b?Óÿ¤½\u0004\u001bWaôþ66È£@ÇÿKÒo¶AÑýÿ6\u0005Ã êÈ9ÿ~Òõm+d.?ÿÜ2\bL?#ÿþÚM?\u0007ï¯ôP\bI?oÿþµl2\u0018?ûüØ\u0017\f?\u0014\u0010Çÿ×ÒÒl??õºú?¬§\u0019\u001b\u001e¿ô½[¦ÈÐ'ýÂ ?ý}é6EÏ÷_8ÖÒ4ÁÉx\u001d]ÿZM?sþ×êOTK²(ÿÿÙ\baXa/?\u0012l$\u0013\t&?Ø_ÿúYI½êÃ_8jØSÇ?\u0007í?öýÒIØa-?.\u0015?G\u000b8\u001d?A?b?¥bqÿ¯ÛUl&»\f+\f%Û\f$\u0018a&\u001a°ipÂÿþ?lBØ?ðÄ+Ã\b0A?\u001a ÂÿmÿTÛ\u0015±?!g\u0003?!1\t?\fV\u0018?w÷í¤­?\u0005@Á\tÐÄÑ?\f«B\"?ÿ{Ò°ÂÃ!^\u0018^\u0018@Á\u0003\b0?\u0018Uïí¤???¨ú¿m$?\u0011\u0011\u001141\u0011\u0011\u001fØ~Ã\u0004©¿ý·í??ÿØ5Ø0A$äµtv?yÀÌû\u000fØa$?ÎÒÎÍ?dp?cÃ\u0010?¿?ÿá\fB¦Éaëâ<®àE\u0014áát\"\"?\u0007P`?¾ÅÝñ\u0011\u0011\u001f?????ÿ\u001fÿÿ?Â?óµD$ÜÕ\u00121\u0016C\brléû+j\n6\u0016)u\u0012Ü4B!ùÙb\u0012M\t&??X?ñ'EÑä%)\bå~d¨S Êp?h»>Ì\nR3\u0002\u0014\u0019A?fÃ?\u0006he\u0000?i?fÃ?\u0006\bÂ~wD]\b??õ²´F±HªÌ?ÌÍ?Á\u000e¦pË?\u000f?\tÁð?8A\u0007½?\u001eá\u0003â\u0018Aµñ\u0013±#>f\u00048?\fá?\nP\u001cè\u000efg??¥C0\u0014?\fñ?\u0007!\f?\u0006\b\u0011?f\u0003\u0006`Á\u0018bK\u0017Ä=?;h?\u0006?x|MÎGïØ?ôNdgh?\u001fó\"µá\u0003\u001ap@Á\u0006\b>!Ä=â\u001f?\u001f\u0012vÂ\"ày)C??ß$C\b\u00106?\u0006ø@Ü ßÁ?¤\u001b4\\'I»øÊ{\u0013Íñ5(?ÃDÎêG@ätz²4_DÐù\u001a(\u0011 ñé¾«\r¸5ÓtßëôãÒ?uó 4#\b7Âm\u0004\u001b ý\u0007?\u001bÞ\u0017é7Ö-ý??\u001eENê÷üÌ_VüàWþ$4?f\u0017I4ö7WßÒý?I?÷äpvÙ\u0007B¿þ ¿ø?f\u0005ÿÚ\u0017ÇÌÅ\u0012êÙ\tªÞ¿³a×_²89ís\bîkþ ?\u0019\fÿä\u001c\u000fëÈJ·ñÍ\u0015ñC²\u0018§ÿâ\tÿâ\n<Gºäb¨ê\u0012úÿ?(ï¬°?©;2X×!?\u0012p[þB?wù\u0014gõá\u0010??îµµ×$\u001fØHÚì á¯óº?)/òbè§\u001dõÖ²Ê=¯\u0004uÙz/´?ÉÈ&?ó[?\u0012A?\u0013al$ªÃ\t\nÚ°Á/â6?ä?6ÔÑ\u0003ukk}?\u001bí¤­?°ÒÎÆ.\u0018Hæ\u0015?\u0012`Á&\f%R\u0014p?¨Ø?D\u0002\u0011Á\u0003\u0014S?±\b1\u000b_\r{I?\u0012\u0004\u001aW\u0006?\u0018J\u0018Xj?l\u0018H?Ö\u0018HÚ`Á,yn!!;Ø?\fBb\u0015Ëq\n[?\u0019\u000b\u0016\u0012T\u0018)\u0016\u00100?§æE*(Ø#\u0014Å1U\u0015-Å\u00060Ä\"0\u001c?\b\u0018??ãÃ\u0014!?Î«Ã\u0005\n?\u0006F \u0010àË\u0002??4\"R2v\"\"7ñ?áH®ØL\u0010a\\?\u0005?\b2\u0012á?î\f&?\u0018 dP?ñ\u0011\u0011\u001cq\u001f+J¾vj?Å?\u0011\u0011\u0011ÄÖ±\u0011\u0012??±\u0011\u0011ÿÔ(¦p¾#??ý?\u001dçj\u0002\u001b\bv²\u0019?;!~ªv²\u0019¤¡ð¡\u001cì?üíXCa\u000eÂ,xB\"\"?&Hò;5D\t\u001a%ûª\u0016A\u001c?,KuµöVü¡²?\u0005Ê?qø? B?Çùß¬·2_\u0012ßDW&?Ê?[Í\u000fËu\bDq*kçp??.???«\u0012X¾\"%?-\u000e&D«åy¢èi?¹?â\u0016RÙFå?l¶?\u0013·@\b?}\u0010ÿ\u001120?ù]B\u001fçz¡þ&@«-ý|È]\u0011´$Û\u0016$±\u0010µó´?!\u0012tuBN²Ü\u0011\bý?åJ¢??e®&FKâ,ª\u0015²R?\f©-\u0014-\u0013·_\u0011\u0011\u001c~vR?ú¯âVQÚ?]\toËø?¤\"&\u0011(EIdÝm|NÈBD!\u001b\u0013\b?/?ËP\u0016áhì-\büq\u001fÿÿ?ÊWñûÿ¿×ïõûÿònªf¶A?\u0010)\u0003\u0010¡?d6j:ù?i?á?ÌÍ`ä?\u0011 Á??\u0006H3@Á;@Í\u0001É\u0000¹80A?\u0017ýòn\\?B:??\u0010Ö\u0010\u0005'gÙ\r??²@\u0017²@7L ß ?ÙÇ?G\u0001?G¢\\Ñ/uÿÌ?ÌÖ\u0019Í\fÔ\u000b?\u0003\"`æfK²A??\r\u000e\fÌ\u0017(\u0006\r\u0000?\\\bÿØA\u0011\bÐDd\u0006?&?ú&???\b?Ð\"A @Ú\u0004\u001bÿþH\u0002ø v\b7ð?¶\u001ehÂ#àÂ#ðÑ)´JúÄ\"Uô\b\u0018h?º´?øM?{\u0005ÿÜB\"?Â# 4Lv?¡¯?I\u000fÐ t\b\u001bA\u0006ÐMÿõé6?pÇê?ÅÞE\u001a\"§_ý\u0002ð\u0003i]\u0007¦þ¬_\u001b\u001fý-Ò}¶Bë{ï¼â\u0004PðÈ:²\u000eýRô?I¸cú_?ì?4D¯þ½í¥?AÏÿëB0Á?\u0007ÿúúoÙ\u000b¯÷þÙ\u0007&AÏÿ­RÒl\u0002kõû\u0002\u00101?þ?¤ÚM?C\u0014ý?\u0003\u0000ÈaX?ïÿm[\"Ãßµõ?¢%Ì?ÚÿÿÒl\u0002kûGP?\fOëÿé²®\u0007õm/<i6§#\u000e½ÿêÙ\u0017/Ûýeë%Ù\u0014}¯ûé$Úa.\u0018+\f\u0012Îi?ö\u0018I?\t0ÂL\u0018.ÇýÒl¨aûVÒóÆ?\f$|ò ¾Öûöô¶+bw?+?Ø¦!1\b1\u000b\f?ÿþ¸k¶\u0015?\tg\u0003°`?\u0006\t0`?\u0006\tlo¿é+a?aP`ª?\u0006\u0011F\u0002\"F$;þÿé6ÅlL=?Ô1A?LPb°ÈwýûkM????±\u0011\u0011ÿþÚJØal,\u0018'pÂ\u0006\u00100?p`ºÛöÒJïþßÚÕ(DDM\u0018??{~Ã\t+çiG?\fÏ·í¤?cþ\u0019\u0010ý?>\"M?Ã;!×ýØ~Ã\b%|ìÉç4Ìü1¨1\u0004?oÁðÇ?BºI²Xgd\u001d|G?ð\u0017h?\u0014DDDGàÞj\u0006\u0012mÜ\\8â#ñ\u0011\u0011\u0011\u0011¿ÿ¯ÿÿÿýÿ&Ê¬?\f?dìè!\u001b3?p!\f9.£%#>eÂ??á?\u00044\u0004$\u0006\r\u0019öG\u0004!\f\u0011\u000erÃ/?¸;°D\u00171l\u00100D3×ùn/?H?²T?Ä*ÌÐÈaHÓ<fÃ?\u0001\b?ö!Ó\u0010Â\u0006\u0010|C?¬??¸?\b??ÄÓh?ßó £>Ì\u0005:?Ã6\bh\bH\f\u0019?ö\\9\bdpCC$6[?ð@öÂ\f\u0010:Ú? |?ð?QËCä?à?ì\u0010? ?ðNoÿ\u0010ö, Ð|C?1Ãî$óXD~ø?tJÆ??ô\u001bWéº\u000fô¾mê?ÿ??mÙ\u0019Ú'F\u001147?Í²T#C½\u0002\rðN?\r÷MøXNØôýý%õ®h/þ?|'A\u0006öøAº\rõ\u000bú~±ßÏ?<?×Þÿ?\u0007þø?|\u000bÿ§ZU»\u001e??½/[ð·ÿÄ\u0016\u0019\fSÿñ\u0005þò\u0018#ÿ·Ï\u0005\u0017d.¿ÿ²8?×Ä#Àcÿ@9 ?Ö¿#\u0015÷K&\f½WÿÐ??C\u0014ÿüAð_ÚòbÒ0»[­`½×É\u0006ßþ¾A\u0006¥\u0000?¯ò §¿?.^«ô?$\u0019?Hû\u000fÚN¶¶P\r%ml%þéYbò0»V×äÊ;i-\u0012\u000eÿ?\u0012\u000ba&\u0018JÂ\\0?\u0006\u0012a??\u0012)Á\bà?0)\u0018\t\u0014\u0018?þ×É\u0006lÒ>Ã÷V?ke\u0007[\r.Òa?¾(à#\u0010??ÅrÇ\u0010¤Ç\u0010?ìW?!\" ðÁ\u0006\u0017ûIm[\tZðÂÃ\tXVÂE8!\u001c\u0011?\nS°VDt\u0018¯?á\",C\b\u0018A?Xaa?\u0018T\f?PT\u000243©\u0003\u0004'F?â?\u00021LS\u0015Ë\u001cB?8¦'\u001eÅxb\u0014LðÅ\u0006\u0017ç±\u0011\u0011\u001c\\DD|DË??\u0015ì\u0010a\u0006\u0012á??\b0?0NÌ<0Âh\u0019\u0014!j>:ÿû\u0011\u0011\u0011\u001cq\u0011\u0012Æ\bDDô¤?ÖC3ÿýùÙ+ó°\u0010¯ùÙ*.½$?Ö?3ú¨L!þ?çj\u0002\u001b\b¸??ÿØL!þ\"\"#ü²\n¯äØ\u0011\u001aÿ\u0011;UYeT_\u001c~YV×ÎÝY\u0006?²t$ë+Ñ\u001dÖ¸Ð?,EI\u0010hq\u0012l.¹XF?*\u0011ß¢ÝB\u0011\u001c·©2?\nØÞ#?(Ú\nÜÊÚr?\u001a?n\u0004?~y\b?D#Äí\b?T?û(Ù(£jÿ#hDíU\u0012ÜB\u001c²?£½\u0017È?8??Zø¡\u0015Å\u0016[?Cñ\u0012¤?«D¡cñ\u0011ý?éKô?ËF?~[?!×ò?\u0016á\u0016[?§âvèL?¬·ô$Øºø?Å\u0010â'e«ã?E´?;äM?,~#?Ð¾v,±ù­\tn]\u0012Ü±\u000eY\u0014?Øº*×±ÄGÑnH²Üµ|q^vë,¢æJ£Y¾È?%?\u0011ÜÖW$\u0010äx?\u0005'd¹?\u0019 )A?\u0014?\u0010è\u000eH\f\u0015\u0001?6}§üKqd$±\t:Ì?Lè\n\fÌè\u0019Ð°@ïÁ\u0003ì Á\u0006\u0013\b?ïÿårSeL?A?2Ã\"\u0006]?H!+!ô êÈ<Éñ2\tÔNJ?\u0012Á\u0010\rB#÷^\u0011\u001f¼Ñ¢th?Ú&v?CÿôdXgPØhgP`¨\u0018 Bl\u0017M<\u0011\u0005éa?\u0006\b\u0018A?\u001eÿ?%WDµ\r\u0013vaA\u0006ÿ@?~m\u0004Ý6­ÿüìÕe\u0000c\u0004\r1Dx\u001fá\u0011ðy¡¢^\u0018D¨Â%6?C×ô\u0012è ÝXì\u0015ý7õbÝ?\f6¿??E\u0011éÂ#\f4Lv?!Ñ¢ô\b7è Ú\b7\b\u001d'ÿÎá$Þ?jÜ??ûø»²\u0014Á\u000e\u001fÇ!®J??\u0015A\u0002ô\u0010n?ÞÇÒ\u000fôØ·c\fñIum&Ã ?ÿþl\u000b?AÕÄÿ?Æ?/A\u0006ÕàÎ?ú\u0004S¿\u0017vD\u0003!tÿõÓ¤ä4\u0019\fÿü 90\u0015;­>ÎÉUzM¥l?X!ûÇò\u001aÍvAu\u00041;ÿßëbA?þ¾²õDA?3Ç?¥?¤+þ?aÄç\u0017ÿ?@Ã$Á?ÿò?Ód ým/8tÞxÜ?'í~ÊDkÕµl??Ç«¯Yt+¢C\u0014??ÿ¿??d!¥¶¬4?l$Ã\tZ¶\u0017a?äYqýk¦ÉC£ëV×Î:lR%Ì?kÿúM°Â\\a?S`?S\u0010? ÅlLó\u000b\u001f^þ?T\u001dØ?)ÞÚ^Ã\nØHùQ.KØ_µÛIm?Ã!Þ\u0018^\u0018@Â\u0006\u0010`?0±ýþÚ¤Û\f%BÁ?°Á,àv\f¸¬S\u001b\u0015??³ÉRrQ)\u0018?¡4b\"\u0011J_íÿJÛ\u0015lL;b\u0015ìB\f Â\f,2\u0011ÿo¶)Sb#ÿöÕ&Á? `?:\r?#£C\u0006F\u0010µ\u0006Ý_\f?a?\u0012Mçio6\u0019¤­}¿´ªÄDDG\u0011\u001fÙ\u0010ü0gÅVÉa ëñû\u000fØa$?ï\fxb\u0012Wã»8åARYö\u000fÃ\u0006\b%l??Ù\u0007¥?l3r»?z#\u0002ÓB\"\"#ðÇ?!$ß°Nï??Ì\u0003Fk\u0007«ÄDGø??ÿÿÿÿÿÿ,?l?ÆbB\u0010gü¯Ä@³1\bb\u001a??3Æ`B­?\bPÉ\u0006pÍ?*\u0019;$\u0003#?\\0\b\u001füÉHÏ?\"\t©|\f?\u0018>\u000b?\u0006¸@ðû\u0010ü\u0011\u0010pé?|Â#àÿ?ò%?j\"0Sª5\u0011HÍ?Hd6y?\bU²vC\nF?ó6\bP\u0018#\u000f¨?ß\u0012x\u001a#ÀÑ/|MÎ&÷ò)þ?QÜ\u0010t\b\u001bþd\nfl¸SQ?3\u0000??à?blñ? !\u0003ø`?ð@Þ!?\u000fÆ\b\u0018{$E\u0002\u0006Ð ß\u0004\u001b?\rü+ô\u0010~\u0016-ÿâ\u001eÄá?EpÂ#°ø?\u000e&ÇìMïÂ#ðÕ?¢?!ïAúZnØ.?ßê¾?ð¯üd¨\u001dHÐÑ3´Y\u000f?p@Ã?\u0006\u001fÁ\u0007ô\b\u001bx\\&ÿ¾?Bì??¿?\tÿåÁ\u000f¢ù\u001c*ÿ ÝÂÒo~!\u0007§úÿ~?_]ü?\u0018Ù\u0007Géþ!ñ\u0004?Gþ?Ò\u0016àÇï¿¢qýk?\u000fïüA`Áÿkò\u001coÿ#\u0011ÿþ`\u0013d\u0010?ûüWûÄ#à_õä?gQ\u0017^¾L£Úð¥ëÿß\u0010°Èbÿ?ÿä>?ºXEF?.nÚVºä?öÒ\\m?¿õÈA)\f/®¿$/ïYa\u000b×ö\u0012[(0MO\u001f¦?¥jÚ^Ã\t\u0011?X0?\u0006\t¿?\u0017DAýu­\u0012\u001f¶½?\u001d¥ðÂG0°Á Ã\t0a-?¢?Ø¢0\u0010?\bÅ!8ö!\u0006!wí%É\u0006lÔñ·ÃXkkkÛa%°¡?\u0012ù1Ä$&\u001eÅ1\b1\tQ7\u0015.\u0002\f??\u000bÁ???!\u0006\u0011B\f\u0015Xa&\u0018$Ã\tpÁ(3\u0002°`¬\u0019\u001d\u0011Å#\u0001\bà?B\"\u0001\u0018 Ä/Ã\n\u0015\u0003!j\"?\u000482Ì1\u0011\u0012M?±\u0011\u0011ÿ,q\bà?vÅ1\t?äÇ\u0010¤Ç\u0010??ìD/\f)\u001bØ ÂüDDEÇÿøaV\u0018 `?\u0005á?Ã\u0004\f\u0010Å l?ø?þªv°\u0019¿ÄDDG\u001cD|;$?;P\u0010ØOÿ¯~ë C_;%?;Q?1\u0002¬?oB\"#wÿ??|j¿Ó\u0004\u0018!ï???ÿÿÿÿÿÿÿýÿÿÿÿë÷ÿÿÿòluü®!\u000eM?×Ç\u001f§EZ;\u0016EÑ\r\u001d©¢Ü?þ\b\u0010?&?D?GiÐñe3¨d\"ùÚD]\t\u0002Gj\u0011ÜÖ$Þkâ\"K\u0011Õ\bÑ(L£e¿;[B6#ó°Ð?Á¬??¾\"M¹P?!|ËØüL??ñþd\b?Ô\"ë-ÉWÎæ?!\u0013è·\u0014EIcò??ìº\u0011\u0011%?øÚ\u0013$´97\u0006F´p???áN¡Ê@æ?xÉ\fÖ\u0011Ì?Y\u0018\f\u0013?¬\u001c«\u0019\u0012\u00074d»$\u00198`\u0013?\b?\u0010\f\u00100@ßÿ?\u0014\"Ý-dD?uGÙÒ)ßd0QÁºa\u0007î\u0011\u001e\u0007F?\u0011.\f\"S\r\u0013£DÎÿþ&2:#\u0011\u001c)\u001e420)HDP9Äm?ì?Ê\u0001\n\u0019±\r\u0001Èa??\\?\u0005Á;Mz\b?~\u0011\u001a\u001a&;DÎÿ\b\u00107º\b\u001bA\u0003i\u0007I×ÿ?Î?£:\u0006?Á\u0003\u001fÁ\u0007¶\u0010a\u0006?°\u001a#Àþ¼B%W\b aÓÓÿ\tõIÅñ±wÿ?\u0017\b?@í\u0013£ý\u0012 y¡¢ga\u00128h²\u001a,?ÿ ½\u0004\u001bVáë{??m²\u0010\b?ÓÿÎÐ?Ë¡\b?\\ @ÃE»H7ú\t¾?\r°Ó{zÿKÐM¥d4Èpúïj.l\u000b?AÕÅ?üE\u0005è Ú·ôýµcm?\foÿþÒlC!?÷ý×'\u0004$Á5ÿ?\r$½&ÒvBUõ\u001fd\u0011!\u000eGÿýÒl?ý×ùz¢?dH·ÿ?ý6¶\u0019\fSïþl\u000b?C\nÈcÿëÿ¶EÏ×¯8tÞ\u000eAáýâ¢\u001aô³j?\u0006\u001emÿÂ ?ÿþ?T\u001bö¬0¿??\t\u001f5\t¯\f/ñÇ½±I²,<_©z¢ È¡ÿÿäëI»\tl0¬\u0018 ³aÃ\u0014Å1LVÄã¿çiH¯üÚI°~Ö\u001a^pÕµ<nD\u001dm?÷üRI°ÅlNðÅ{\b0A?\u0018J\u0018_ñ\u001fú\u0015Ê?û\nØ^?\t0a&Õ?\u0017a?ÿíêØ\"¬*\f,\u0019\u0017@D?H2¢$Ð?×ü\u0011O§Zm?¶0Ä,àv!\u0006!1LBØ??ÛûJ±\u0011\u0011\u0011ÄFÿ?\u0014¦ÉÐýé6\u001a¢?\u0019\u000eðÂðÂ\f\u0010`?á?þ\u001f¶\u0012I¿þ8 Cí¤?d\t? B\"\"hb\"'T??\u001f?\f$­?ÖvAçio6\u0019?a¶?Ø???<1\t&ï@?þv´?ö\u0018$?yÚYç?3\u0007Á?«¦?D~!d%?NKYØn»\\DDD?¡*\u0017ÃØ1\u0004?~.Ó(?áR\u0005?üÈQ\u0011´a\u0019ä4D\b\"\u000e\"\"#?T?â\"&?Dò\u0012lP±ùR*Ð??;ó³¢T?A\u0002\u0013±E¯\u0012M\tSGf¨G-ÉQ+_\u0011\u001cD?£4ü®°?ÂÄ~#?U$D\u001f³±?®\r\u0015µ?ÉQ\u001d\u0014ì?2­\u001f\"??\u0019\r?\fã<\u0010«dì\u001c3Æ`\u0010?0D\u001añ2H?L#Ë2RflÀCQ?3`?`ä?Á? Á\u0010@?$ôØ ü |XDX\u000f~\"$Ê&c\"Lñ?\u0010è\u0014??Â\u000fbÂ\f ø?\u000e'Æ÷\u0013{ð?Mì?í\u0013Cþd\nflÀ?¶y?\nP\u0014ê\u001c?Ï3\u0001\n¶`!9?\fó6\bB\u0019;(\f[dpÀ \u0004]DÞù\u0014í\u0012£DÐê\b\u001b?\r¯\u0004\u001fÐA¾\u0013Óü }?\u0018@Á\u0003¨?Â\u0006ü_?E?ø?Á¢^\u001f?Á\u0006øZ\b7M\\ Ý7ÕMú?ø??ÄÓa\u0012ðÑ:>E÷\u0013Íï\"¾?¡ðAÐ@ßíô?W\f~éÿ\u000bêý\u001e\nÿÆ\b7Á6?\u0006è7Â\rÂ\rêÂuÒo??Wç?\u000eÈpôý¿?Áÿø?|\u000bÿÛê·Ç¦÷Þ?ý???ÿ?N\u0019\fO¯üHC\u001fù\u000f§ý??È?þ¯\\à_²89ðQÿÈ \u001c\u001f¾éy!~ëË\bjºÿ¸??AÏ§ýâ\u0013ÿÄ\u0012ý×&.??úÕú$i-?\u001c4·ÿPX0w}ÿ!Æû¯\"?þ«?\fÙ©öý­¥kÃöÒ[VÁ-Ü?U\u001a?õëYe>þ\t?ªøi+i6\u0012µá? ÂPÁX0R?\u0010?\bÅ\u0011??S\u0010·öµ\b?µ%ßu­ù\rûi+e\u0006Ø_?6\u000f\u0014Å1\\\u0011\u001c\u0012Xâ??vÄ/\f$Dx`?þÒO@í#çö\u0012????\u0016í?\u0012#5?\u0012`Á\u0005òà)\u0015á?\u0018 Â¬0°`?¢\u0018¤\r?²?\u0011\u0011ÿ\u0006\t\u001cÁY\u0017\u0013\"ºcâ¢??{\u0014S??Á\u0018¤'\u001eÅ1_?£ª\u0011\u0011\u001cq\u0011\u001f\u001fòÜR\u0013=?A?L.Lp¥ÀA??\u000bÁ?a82\u0014a\u0014'Äòuü23ª!?\f?¹ ?\u0011\u0011)\u0019;\u0011\u0011\u001f³µ?çjÐ)?\u0014í`3????ãøAú\u0015\u0015ÿõSµ Ìú®\nHØÎÉOÎÔ\u00046\u0011q\u0011\u0011\u001fÿÕ3?Rñþ\"\"\"?Çÿÿÿÿýÿÿý~ë÷ëÿïÿÿÿýÿ¯ßÿÿÿ_¿×«å? d\u000fäÙm\u0014#\u0019\u001d?\f??Ñ\u001cÈèÈ?öT³\u0019äa\u0017F\bØdY?c6?\"?\"\"\"#òÊ³?Dv]\u0011ÑpÉ\r\"æ^.?åÐ?????s\"ÔCG????äa?È?\bG\u0005°Ó#æ\u0011\u001d\b??]B\u0011\u0011\u001bÈ\u001e\u0006\u001c??9!ÈÇ3?\n\u001c?\u00149à¤\u00149M\t_)?%ÿÿÿÿÿÿÿÿûÿúýþ¿ÿÿÿòÈ\u0004¿?b\u0011RL£g?RÕÊRÄ??qã?¢ùZY7\u0012GsCñÍ\u0011ß¡%?r¾¨?!|YMÄ\u0014nµ\u0011$×Å?±2?Éµxü«G~?qø?YJWÎÆ?n!\u0019Mbv6¹)X?ãÙCsº?Z\u0013®8?ÅV&AKçcHNè±ø?éÐ?¥?(_%Ñß @?qø??%rhNè¿b'x?,??ÐâW&½?\bÍ\u0010%¡\u0011,kù©\u0016å(wØ?Ù?Ë!ZùØº\u001cWÑ\t^?íQ~?HhrÐ\u0011?\u001cWgah·B ÑRYf\u0015§çDUP???\u0012t$\t\u0016õ£*ÖYJ?ñ\u0011\u001c_?·\u0012FZ/â\"RÑÜÖY\u0016Òñ\u001c_å¸*+?_ÄJåkäÜÑcòn!\u0010Ðå??UWÄH\u0012;(X)k\u0011Ë6Ñ\u001d?\u0017?Z\u0014,·-E¸Y\u001f?Æ{'\u0019Á?\u0019À§??ç²ñ?g\u0011Ã?\b/<?\"R\u001c®S\u0013¢?Ñ\u00143èM??O\u001d3y\u000e1\u001f? =\u001f\u001e\u0011±£ÛF¶@Ñþ==\u00120÷âÄ²$C?Ò`?/\u0018\b\b\u00110F³ã\bÖ~ã÷?rA\r$ØD#­]\u0004\u0010!ßÎØ®¾IQt9SE¸?\u001f@?ÓA\u000bÓa\u0010?\u0013}|<{m Ï\u001bZâ\u000eG?\u0019à\u0014×6\u0017ø?\"w?îh?_?%?³Cm>$îö\u0019\u001cöKè Ä/?\u0018ìù'Â\u0010m¤tÿåQ2ï?\\ÁC1pÂ¼(?Þ\bÝÃxl¿?Hø|\u0014\u0011­ßN^ ?ó8\"éë¿â'c\u0017è(O?\f¿?¦??Ta\u0014z]±?Çð?ÛV\u0018I°?¨½\u000b\u0014|(cøðh\u0011å?ZÁ??b\u0015<\u001cc¿¹]X¨\u0013\u0014?\u0010??\u0018?\u0018?\fimKr¢?é??b©???¶<8???????ÿ?\u0006\b\u0018\"?B\"\"\"#÷\u0011\u0011\u001f­÷¯??ÅS?æy\u0018Îg2ñÌð§AJ\u0002\u0018\u0014À¦2ñMæãòÑ\u0001LF\u0019?µ×ÿ\u0004_\u0006Á³å\u001f\u001a>=çÀô\u0011\u001fÿ£¼ÿá\u0006öðY.'Ü2Çëÿ&àÙPGR%Ä5?&\u0003?Fq\r?ÏKÑßÿûò<pÆÄñ?\u0007à¿Mÿ2+20\u001843X9&DL\u001cÌÉvH2prs?\u0004AÈ\u0006\b\u0018@Õuë¥·ÿÿ\u001c22\u0011¸\u0011í?4?`«[ÿÁF\b\u001aa\u0007øAì¡à?¶\u0018D|\u001a'á¢s¿ý>ÄlG?Ê?z)?LBðÉæ?þ\u0011\b~\b?pÓ\b?Ûú&w?t\b\u001b@´\u0010:\b7ýmúMá?\u000er¸¡\u0006??q\u0011\u001cb?þ(?]\u0002\u0006\u001a&î?¤ßÂl[X%\u001fÓØ|q???á?LQ\u0004ÿú\tt\u0010o{\u001fé¿\u0017v\fY\u0012¿¾\u0018éè\u0019ö«ézM¥l?×º¿ç\u0011ä]\u001bíud\u001d\u001fñ\u0011\u0011î?«i6\u0019\fSÿú\u0011\u0011?\u0006I?ÿÿþ´?#@?ÿîu\u0010\u000bÿÿÿVÈ¹zºù?Yz¢ È£í¯ÿM?\f?}¥à?I°?ór ý°¿ÿý.×?\n\u00180?p8a?L?Ô\u0019±[\u001fÿÿI¶+bw±\u000bV!\u0006!\u0006!5l?÷ßm%l\u0018,\u0018X0[\u0004G@Á\u0011\u0003%Ì?¡\u001fþß¶´Ø???£\u0011\u0011\u001fþÚ}¤?ýÿ`ÚÃ\u0006\b$?%¨º; ó³#Î\u0006nY\u0016\u001fÃ\u001e\u0018?¯\u001f\u000bß\u0005ø7?\u0004?{??ås0F¾\"\"\"6W\u0005\u0006ºý\u0015ÀÀÁ.G`ÚFJ¢ÿ+?\u0019Á³·F?\u0016Läk³$°È\u000529\u0011Ñp¦ §\u0019\u0012b?\u001ew<Û8ç#?A\u0002=\u001e\u0019\"/\u0011ÈÀ?ãl¸C\u0011s/2,\u0006çz³º?¸à7\u0004Ls?\u0019£°?;Hæb.g\u0006~1\u0018\t\"a\u0016\u000bó\u001c?Æ?áÄ\u001e?Aá\u0007¶n?\u000fypÿþd¡\u0017\fù+\u001d1)8eÈ]ðAZC\fÄaü»rì9ð0ß+\u001f6Aæ¿Ë·£{ékú\tw¿±\u001c?\u0006\u0012.#\u0013¨¥?N??l®´6ð?ÿ\u0015µOÃ\u001e ¿â\u000bF\u001fÿl?g!??8H\u0010á\u001dÕ¤?G\u000bÿóe?lýóR¥?DF|<}X#\u0017¿úÁ\u0013Ñ¢Ãa\u0013xé??i3]?­¤\b¾°Ò.=Br$\u000e<?øý?**5÷e@?`7A\u0005Y§\u0014Ä _á\u0002\u0010?\u0010«\fB?ûA `?\bØñ\u0011\u0011Ýù6!\u0012?\"HöGGÅ$ÌÂ\u0011¶xÍ?(\u0007\"\n?Ö*?,{a\u0002U\b-!?z\u0006GÔDDq\u0012\r±]2\n3æ\\!­?fÃ??\u0010ÁÍ\u0019ö\\9PÁ\u0010ô&CbÁ\u0003Ô\u0010=Á\u0006\u0010>ì?J\u0004\n?A=%¤?\u001aa?ÄA?a? ö\u0010a\u0006\u0010|C? ??¹øD¦\u001f\u0013Q¢g~Ä°8@?6\u0010ZA\u0005¤\"#ú?½ìMF?Ð4Z\u001f#??'??\rúA»?ô\u001bòÝBH\u0010TÅi%¥ñ?\u001bà êß\b7Mý{ÓÕ(·â ?X\\BJ¿MúÕØôôÿA-R»Ï\u0005wð?Bô£ÿôf »!ô÷Ûùpß?#0/é\u0002\t$\b¿¥_ß?Xd1OÿÄ\u0017ýH8 ?£\\?zI?þAÀ¤?ÿõò1nëÉ\u0017'ªú\u0004\t\"?ÃiB¯ê²bÒ0»«_?C_}Ñ\r¸_???\u0010øØt?~ëÉ\fÙÑö\u001f´­+[@ÝÛ\t+aXa/a$\b\u0007?\u001bT?ü0?ØV\u0018XkÃ\u0005?\u0012?\nÁ?E8f1\b?\u0004?LBñH\u0010%Øi%þ(à#\u0014Ä&+?8?,qLLö!H#Ã\t\u0011^\u0018@Á}\"êì\u001aI%ù7\t\u0011\u001e\u0018 a\u0003\u000bÃ\u0005?\u0004\f\u0016H\bL\u0011?\u001a¡\u0011\u001fB\u0015`ÅU\u0011\u0011\u0011\u001cq\u0011\u0016?\u001fA.)/ÿ^ô\u0015$©;%ÈëÎÉ ¦ðSµÍÐ-*¯ñÞ?$!>\u0012ÒHJæbqãÿü\u0014\u0010è$?\u0013¹äËGæèâ<DDGJI6D²\u001a<?Ñäs8fó\u0019vo.fóq±äs83?g£÷½%I#<Ï83\u0001K?l?C\u0019\fiªiá\u001a\u0003á??fýÑ¡Ù½\u001aÚ5ÓÿZQø£Û4?+??>¿Ò\u001e??ÐMÓtÝh\u0011ÿ¤?\u001d.?\u0017qñ_õ?G\u001f?_ÿÿßûÒ¿?8%Ñ?0þsþ¼?þ|<Uºµµ½&ãþ?OÍ? ?ÂÓ?]?­0¬0?\t?\u0013????b\u0013\u001a¼ßþ?«ËõtDj\u0018Xb\u0010`Á\u0006a\u0006%[(Æm?\"\u0004µ5!xm¥fí!ÄDDDçÿÄt??\b4Ä#aÐ]\bÊëKA\u001d\b???üïDv]\u000eU¢¹bQø?4$ÜIb)\u001aÑ?J>þv\u0004?ì©\u000ed(??$?íÐ Epy<hgÈÄ\u000bÄì-\t\u0002Gx?±\u000b;?v|\u0014í)\b?Þ¨ÔÒ'?¬æc.Í?ó??\u000eBF\u0019?p! ?\u0005.EÂ?\u0003\u0004\f a\u00168müÊ\u0010?¡\u0011ÊÞ\u0012a ?ê?ãÈò6?\bK£\u0006m\u001eG?Ä}\u0018?äPFÙ@Í?lB|ÜlS\u0019?\\SyÌÀ?à@?îÎ\u0019\u001d?4\u0007áÂ.\u0003\bÐ\u001eCöÒ\bÝ?aÏl\u001d?ú5´lhº!?DuÙJÊ7\u0018Rà#4Ng£\u0002\u001c#??ùÁMç3b???o7??\n\b\u0011;»?1&?F?Ý¶nG°Ã?ls[?\u001eèøðèØý?\u001b ?'\b8?ÿ?âß?b\u0012]h_\u0015¶\u0019\u0016È¶¾\b\u0010?ãØF?ÄÒ\bÖ\u001c=µF·èøÝ\u001f?ÔøÒ\u0017×?Ó?múI&ñºêý_Å¿_dxwö|/ØÙ\u001c/é5ù©ô?ãI?\u0017Ä?£µ\t× ÚT7è\u0011|[ø¼oïÃ#¾üB¼¸_?_?\u0005ûýÿ_×4?·Ùóôc¦~æÂ?\u0004G??­¤\u0013²ö`F(ØBá5ø?\u0004?ø ¸\"÷«uó\u000eq×ÿæ?ÿ?\u0015\u0015?ºÏ?£®l_¥ki^^J×ÂeßMÅ1^\u0010qLQ\u001c?~\u0012nø@? Ä,0ÈéÁ?\f\u00100F??ùÛ£±d'c\u0012¿Ú\nBCoêËÉZ¸Ò??XCó\u000fcö<\u00141A\r?\fPL1_\u0010?2>\u0019<A0Ä Á?M4Ð0ègpFµ?hDq\u0011aø?hEDDZù2BVP?¡+?,­þ]t?5û\u001aTñA?\r4\u0018?ÉÇpa?dðe\r?±\b?áhDDq\u0015\u0011Ìy\u0012\u000e\u0018ñ±ø?º\u001c[?ÒÎK?HDDDD5B\"'Ö'öû%0??\u0017\u0011\u0011\u001f?ä?]¸&)?6:i\"?pH\u0012·q\u0011\u0011\u0011øâ\"\"\"\"\"\"#ó!4v.?Â.¿??å?\u0017Ë@ªR(?âH©!ù\\?.\"&J×Ì?!Äï\u0015ñ24J?)HìI\u000büD?/æE¨rÝM|NÅ\u0011d,XüKp$?ÎÌ??Hîhrokâ$±\u000e%u\u000fã?\u0017É°Ú2?A?\u0012\u0014?\u0019ÇH§|#6{.fó?¼ô^.f#l¢(\u0014¹\u0013?`RälS?åò¸\u0012 Ä DE\u0002???Ù Ê\u0003?\u0019±IÁ\b`¹@`¨\u0005ÕUrÑ\\?@âS»ÓØf/Ñ­?£c?\u0018:6\u0007Ì?Ìè\rÐ3¨\u0010? ?\u0006¶\u00104\u001a#?Ñ,\u000fÿ&ä!M\u001b\u001c/Úá/é>Èì^?ÎÖV\u0017\u0004DÀi¢^\u001bú%7?4N\u0013;E¡ ?\u000fÿ+?¡Fv<WWÄ\u0016ç\u0004ü\u00189³üîÿ¡\b?G§\b@Í¤Mè\u0010?º\b7é\u0006ÐA´(/ü|Úæ=4?k<R\b»¶¶\bÑm ?\u0015l\u0014\u000bÐA±ï\u0015úoë\u0017?\u0016\fòÑ\\?hT?b0XØ´\u0016\u0018?\u0013b\u0010b\u0016\f-þd4?ô\u0010m&Ù\u0012¿«ø½²\u000eL?\u0011ÿ\u0011\u0010g \u0010??W?a\b??\u000fóµ4$4?ö?l?£ÿù°0\f?\u0015yÿÄpÅÐïóµ\bG!¯IÒl?d5ÿý\u001d\u0002\u00100?ùd(Ea\b?q'XßûeÑt@ÅÇW_ÙzÈ?\"µñ\u001f?&ºý,D?¾ûKÏ5mO7\"\u000fð¾[?FJ\u0017ÎÄÿé6T\u001aö\u0015?\u0017á?L\u0018 ¡?a?ì??Ä\u000fÎÓ¡ÿ5-[$&+>?Ã\u0010³`?Bb\u0013\u0010??lIñ\"Kâ@?X_¶ÊÅM?\u000b\u0010ÈX?\u000bÁ?\u0006\u00100@Á0??ùoÈ?!;3_\u0013Z\u0016ïÇJÉ?\u0011\u0011\u0013F\"\"#ø?,Có°4@·[\f$?ùnd?íÑÞ/?°ÛÃ\f$­ÙÚYç?3\u0011\u001f±ì?ÁSdµp½?Á?$?ñ\u0011\u001fåw\u000620\";(ÏÄDÿÿÿ-\u0016?Ù7\r£ã2Ät?ó3Íæbÿ@?õF¨è?ÇFm?Îg\u000f#³¦u\u0019±?\u0010ÆHLØ?ã???\u001a\f Â\u0004GiØ/òo\u001a?ÌEÂ\u0018\u0014?7\u0017?Æó\u0002\u0002\u0006cPÃ\u0004\b¼\u001bð\u0001Ù?\bØÑñÍoqFÏ¢ñ¸:5Ä6ú7_â?Lù?Ãwpß>MWð?¤Ý\u0006ñ±n/?o×âÙ\u001c*Z_É¸+&B?8üx!Ð)\u0006z\u0004Gÿ#??ì>FëÿOù\f/\u0012¾p!\u0002?I3æÿùS3fÅ)ÙæxB@S¨rv}?\bT\u0019p¤æH3?`\u001c?3C'\u0005ÓL\u0010`¯WÞ?û\u0019¥6}ÝkV×KgÄ_J\u0011¿\bß53\rØØ¬&?\u0014\u000b·¯»\b\u001fdp\\\u00100@ü Ý\u0007ì_¢<\u000e??í\u0012ðßI¿ÍÐÒÂá\u0019æ-´?aBlPAÆÄ$+/±LS\u0015Öá?eÂ\u0006\bC@Î?B7¿âl\u000fb_´KÚ'GÄÞ\u001cO0ß?Ný\u0002\rðM?\u0010mub\u0014\"9°eý\u0005?\b\u0018A²û@Á\u0006?F(D{ÄDDý?\u001b\u001fÆ\b\u001bà? ?i\u0006øA¸A¿?þ{¬Cø?#???\"><\u0016\u0018ñ\u0011_OÒÓxôûý\u0005úº ?¿eì?¼DDGýô\u0012\u0017d%Zºÿ0\té?\u0014|\u0014.\"\"#ýø­ÁÿÚñ\u000bïà?ÿÿ ºI8?ÿò\u0014KýÈÄ\u0013Óÿ×?\u0016??î®??\u0017î¼#¢ªÿÝ,\"\u001e}©.û]W¢\u001bÞÒ\\ Øi{û^Ðv?óûJ\u0018I?\u0015?\u0017<??\f\u0012#0¬??×Ã\u0004à°`?\u0006\\H®*!1±\b?\fÆ!!0ö(0¿òc?HLðÄ&!\u0006¹n\u0014·\b2\u0015á? \u0006\n\u0015\u0010Â\u0011\u0005ÿÃ\u0004ÂÁ?5??1ÏX??HÉØ??ûüDDG\u001d_þ§kA?ÿ;%~v¬!°?¿ÿ?\b¸??å ª5#8?ç|þ97N\u0004^\t\u0004\u0013h\u0011!&Â?Â\u0014G#èÞc9?Û$\u0019ò&56l?ÏÐFyN?\t³£ y?Æc7?\u0019?Î?OL0í°\u0001?|\fS\u0007?·üÊ£>e\bÔ?óHÎ8?3?`?iÛ`f\u001bþ\u0011±·ÏÔ\"?ïöôô0D{G;þ\u0011 0\u0001¦#iÃP\"\u001e\u0011÷ÛHÆÃ\r÷Ò¿ÿÕ¸i?þüE¼¨Ð\"=\u0004GÜÂI\u0004ùÀªßÿù?¬ýuz__ðÁ?¤­¯ÿdw×um?¥ùñUæ\u0002l2ïý?\u0010C;I?ÌeÔSi6\u0010ö='T\b?4é´í?\u0017§Ê?\u0012·[=¯;Õ\u001fË­'Éä?m\u0018?èÞGÊ?Â\r?F?*\u0019¦Ø?g\tÒºÍÉ¦\"!¦\u0018Kù?¢Å ?ñ\u000fAV·kðq¶\f\u0010?¾;\u001b\u0018ø?\u0010ú\r\u00067f?\\\u0011 Å1\b0?A?_Á?!\u0004Øçµné½\u0007\r±5£aBD¢?D}¢:ó\u0002?0`?\u001cDDDDD?MÅqÛ\u0014Æ\f Á\u0006Q7\u0004GP?DDDDDGü!\u0011\u0011\u0011\u0011\u0011\u0011\u001f¸ÿúýÿÿûÿÿÿýÿÿòÌ­ÿ@?B(\u001fòÊ·?Dñ?4Èyâ'Ï?F|Cz?f3?\u0001\u0011`0@??òÊJ @Á\u0002.Â\u0004bÕ\u001eÃÂ>\u0006 ?î??èøÙ\\Ð@Ý}\u001b\u001a>4\u0010 ?é!I!A|\u0011úÅÐñ¿þù\u001cî´µn½/ÿçèd}øb\u0017Ù¸1ZL2î??Õ¿[Ë°?\f\u0012(çÓ£G.?\r´\u0012?jïé°?\b\u0011uN\f0a\u001c?üíZ-Ö?o_¦ãHt\u0012?Å?â!¡\u0011\u0011\u0011`Â_\u0011ØØ¦)??\b??!lP1âc\u0006!r¨²m4w4d\u0016°Á\u0014!\u0011\u0011\u0011<?DxâK\u0010?:ÄGâv1\u0015???é?Â~)ÞZ\u0016×Êä?$a\u0011`?æq\u001a¢\u001b(\u000eHfÅ'\u0004:?\u0010Ã\u0005@`&??Äª¯?\u0011\u0011Ca¡@?!?\u0006â??\u001aØA?\f&\u0011\u0016\u0003¯ó!$M?Püp\\\u0011\t`ì\"^\u001fN\u0011)??4N?J\u0013;DÐúß\u00112.3?¤n$E\\a?eÙ÷ÜB#×¢Z\u0006?z\u0004\rþoÒ\u0004U´\u0010m&ÒÿòlH?Å3HÌ?ã6`\u001cû4\bf\u0010¢4\nl\u0010Î\"\u0018 Ø?Ò?Òoê?\\ ?kv=ôßÐ¸¼1`Ç¿ËryD\\\u0010Ã3?Å!2\u0018r@CÑ?0Í\u0001àÔ\u0011\u0004ÀßÑ8\f\"v\u001e?ÆC½\u0017Í¿ÄX¦ßº\u000bÒ\r¤Û\"W£k§|nÃ!Ò\u0010tkø}·`?8sÃA2­\u0004O\u001fÑ/^6ÞCn\u0007A\u0003zMùáô-þÂ\f?ë}ZM²\u000e?:ÿ?\u0003\u0001Â°}þÅ\u001d&Ý\u0002\rô¥\t½=oI¶\u001fðÅ+Øcì¡Á\u0011ý?P<ØT\u001a\u001fê´?l?ÿNC\n@?_ù^ÓXaâÛ\u001aA\u0002\u0016ù?ä?Ìí÷c6\t?DÏ²\u0013¸?á?ò®\b·a\u0017ÿÿé6E\u0004ýÕ~^¨?2&uþ,×8\t\u001b?Fä¿oCÛü\u0017Èb¿\u0006C¼ÖÑ§É\u0016n¿??¿ÒÉAö·¾pÕ¼üä»~×î°?Ê¨A\u0011ô\u0017¥ä½±ÚÍ9\ræqúë3g¯s6ÿâ#\u001fÇ¯Õ² ß!«\nÃ\t.Ã\u0004?0I\u0006°ÂÛ\u001f¶?® æêI&ÔÜPÒ?÷l%~¦øjÃ\u0004?1?\u00040\u000eh\u000eÅ1æ\u0003?ÿ¤Û\u0015?\u0018b\u0013?\u000e\u0018¦!\u0006)?Ù\u0007\u001fÛ\u0014¶¨0I'V6*¨ \u0013pÄ&3\u0000åÃ\fB\u0006!&\u0018_&9NTLá\u0011\u001f?\u000b}µI¶\u0016\u0019\u000b\u0010Â[\u0006\bÖ\u0010\u0018\"\u0006(ÏÕÌÁ#\fBI?\u0006\b0Tó?\u0014Ü§Ä¥&þê?5\"\u001c\"\"&?DD\u0011\u0011\u0011\u0011\u0011\u0011ø¶»a$¬G÷-ÇEÉ}?øa??Ì?Vvdó??Õq&ÉÐüî\u0010cÙ\u0013\u0002I²ZÎÈ8Gv?èGì­¬ðb\u0015CÊRq\u0018!\u001c·0¾'f`ÆD\b?e.Ä??/?¡\u0011\u001c~%¹*2­;,BDÐÿ&hG-\tKæ´%u$h?Ô#*ÖW\r\tÛ¯²?\n?ÑK©D???[Iâv\u0015æ??C?üDï\u0010?íe-\u001d/4@?*Bvt;*^T?¼DI·??D?j\u0014?3ÌàC r\\ó$!;JBv§?£\bÜn>*¨ílÌã?)Ùæp! )Ô9;>eÂ\u0015lÀBs$\u0019æ`\u001cIÌ&\b\u001aØA?\u0007âW\u001d\u0015Á\u0011?(g\u0002YÌêG?|!>lS\fÀ?\u0002°Ó?pÛ\bÐMüÔ?L\u0010>Â\u0006\u00100@ú\b8?ç×\u0016]x\"-?ÄÞÂ#÷êT324\u0014¡\u001bÈæxÆó??æC?Å.f\u00048\u0014?J?@?ÌÑ\u001d\u001f\u000f\u0006°Â7Å\u001b\u0018y­£}½?î?\u000fñ;\u0013\\Mñ7°?{D¦ø?aÈ¾\u001e;#;\u0013\u000bÐ o?m\u0004\rùn®?\u0019?ØK9?\b?Â-Ø\"pî%C\bÖ\u001bwvÞ?\u001e|hße'º\t±H\"\u0017F.?7Å ºâ»\u0017â0?{\u0004\u001d\u0004\u001bA\u0006ú\rÂ\rú\tÇÐFÓõ?ÿ£Û4?)\u001d¤\r?m\u001ehi±mú¯\u0017ò9 ?Hj½Â\b3Ç.\u0012³¨^\\ÿÎ?#ï ýtÞ==:úý\rô\u0012¿2\u0014U«a\u0005\u0010Dv-?\b·VG\u000bÕùÀ?8?î)~\u0010\\#N§î¬ø¸G?¿7\u0004Í\u001fé¿\t\u000b²%~êß£`???õ~(ø(ñ;\u0018?÷\b Â?³æªê~_V¡\u0017yûÁ\u001cý/Â\u000b\tE1[?ìPM?µ\b?=?Yx6üè?R+\u000bü?\u000f²\u0018>³E?¯â\u0010ÿ\u0004¾U£!Ñ\u0006?/ÐZDðJ\u001aWdê)?\t±à¨'\r\u0002lV©d{\\ç\u0010?[ÄCBÛ?u\nÒø?ÿ\u0010X0ÿ\u001cãwþF ??\u0011\u0014¨¾ê?å\u0014Ä Ä'Æx\u0004-\b?4,7JØi6\u0016?Î«\ft!?Kÿ?\u0016??ïºù!~ëÂªòº¢J+JÓ?\"Áø¹×cPÆ?\\A?A?!\u0011\u0011\u0011÷ªÑ.Ô?ZûD7ðÒ[(6\u001aø¢\u0013\u0002b??@Å8¸???¿???\u001d¤|þ\u0018J\u0018J\u0018Xjøa???¬\u0018$\u0019\u0016\u0017????ú?\t\u001bÂÁ?°f\u0005b¸¨¦6(§\u0007#?1A\tÇ±A?^dT?¹bû,q\n'xb\u0013\u0010?å¸Rà\u0010d,C\u0005àÈE\u000b$\bK??º:¯j\u0018*Á???$\u0011?x??HÉØ??øñ\u0011\u0011\u001a\u001fÿÿª¬?oüì?ï;V\u0010Ø_ÿ]Ô!þâ\"#üÿÿÿÿÿÿÿÿÿ?d#\u0019:1?äù g³q¿ùe*#æ|\u0011á?Ç£ìè\u0010Ã=\u0017\u0001\u0018iÚá\u001aÃÓÿ?k\f#Øa\u001aÃ\bÖ\u001a=½;\bß·m\u001a?÷­ o?#ÿút?!¡Hx\">?ô¸D{b\u0016\u001bØ¬}&ÿ÷ÿêßuíì÷ãg¹°?ÿðÉ`f&\u0019\u001d?_?)«IÿoºÂ?í\"\u001fé7ýÑí?\u001e\r?Ð e:Õû¿\fnºïY¤±ÇýlhRÍÃôÅ;\u000fÝ?Ù\u0014{\u0014x(b\u0015?ö(Ø¦Åb\u0011Áuì\u0018ðí`Á\b??ýDDDDDDDGý÷¯ÿ-\u0006H?\f£<E>lS\u0002?\u0019ìÀ?\u0004/\u001a_É¸.i??N\u0014Üf?ÆO\u001a\nP\u001cÞb3?EãL\u0019É¦\bÐ\u001a£Øb?|?l\u000f?ÜØÛKù&CFlêgÌÍ??Â9?Î\u0011ÌæCÉÆs9?Í?ÜgÝ?'l§®Á\u0017¸FàÈÏo§PÃð?WAºH`Æ\fEúzØ¯çjB?\u0019>z\u0004\r0@?ì#@h\u0011x EáF?îÑì?Ñ¬?Ññøaº\u0005»\u000fA7Ó~\u001bí?o Í\u001fK\u0006K\t?ûÙñGàÑñªEÚ?\u0007P´?A\u0006ÐA±\rúMþ!¿Õ¿mkÐ\"=Ó{\u0006>Ç³Úc6\u0016??\u0015a??=Â=Ùñ-­«iÇndvG,Ròåÿ¶D\u0005wßÎ\u00044\u000bûî`q®N\u0017oß\u0006H?\u0011»Ý\u00027Â7ô\u00100Ëé\u0003\u000e|q±@´G8Dsµÿk¤\u0018T,?ñBÄ/cgê­¥¨Fë>-W\tFÿ)ì0ýsTFz\u000bÝ*þ(\u0011ò?\u001cDDqÅ?þ\u0019>éi:Lð?ßá?'Z)?c§b?7\u001b\u0010§]½ö6\u001aYûûö8{\f,(¤BFí¯èçéD$\bâA+\r Þ¡\u0015ÈDD£¼DGã\ff÷\fB6\b\u0018?P\u001f\f{@Å\u0003\u0014\"\"\"?ìÅa ?KQa\u0010?*6**Ø×\u0011\u0011\u0011\u0011\u0011\u0011\u0011\u001fá?A?Sâ\u0010`?DDDFþ\"\"5ònLþYEÌ?¢!è\"Þ34O\u0013?Æq?\u0019Ã.FÙ\u001cd3»?Ö\fî??\u0019\u0007\u0010Ù\f!!?\u0014\u0014ê\bt\u0004*Ã\u0006lù ×H?£¤i?dtGÈù 0PfÌÃ#?¶}?\u0007$3Â\u001b3lã0\u001c }øAöÄ§oÔÈ¬ÍA°ÌÍ@¹V26\u000bê ?[\u0004\u0018@Á\u0006\u0010}~W1\u0014?ó(?\u0019?ç¢?3\u00073\u0010\b¦b?fÃ?\u000f\fàcø?8~\u0017\b?7ù;màþÏ?á?ü\u0012Á\u0003TK\u001f¸Dx\u001ehÑ/\f\"Th?\u001a%Gÿ?-?}?\u0006|Ó\b\u001dßpÂ?\f-¢Ü>NÛ.Þ?ù\u0006ê¡\u0007ô]\"-ÿA+ÿ\bmñ_Ä\"=\u001e\u0011\u0019\u0001¢c´\b\u001bý\u0002\u0006ü ?h Ú\t¸Oÿ¢c?¢ÝÒH¸z??(?á\u0013ö?D7Ózé>üWù\u0010\tüTÃ¿ÿät÷\b\u0012Z\u0004\f4­&¿I¿§\u0017±??ú\b6\u0011\u0007?>?}%×A´´[³`?Ä-¿^EþÇ/?Ë\"Ãÿ???7\"QúW??Û?F~ñíæ\bpÿþÉÅHîÒ¿Â\u000bdo_êåßùaØÉ\u0000÷rðÑ0?9!¶??[0Õ¼ ãb°AÆ?ëéÒl2\bG×^ÍpÈaY\fOþÆõ\u0010ëbô?\u000b)ðÇ_«oö\u0012³\f?$?dQìlz\u0018EÏ±LJ\u001ca?pÆ¡?x0U@ÁÒô?I°d\u001e÷õ(\u000eL\u0007ÿßAK°ó\u001aA?\u001deí\u0005?h¾·ú[\u0010¸¦!K\u001e?qpË?\f\u0010³????¸0?G\u0006?ÿúäL'ïý2z\"0??÷ù\\w\u0015¼^<ifÜt?é7?,¡ø???7z¸Oÿþ?%\u0007ëkç?ùø9.ß×Ì?®a)Æ?\u0017¬\u0010ÆÁ?L~ÆP\u0018L>\u0018Dt\"#ÿý&Ê?ýí¥ö?a$\u001e?°Á~!B??¨¨I1P?1\b?¨Æ\"\"#ýÿI¸av\fØ?R?\u000eÅ\u0006)?b­Ã\n?ª(¡B\u0011\u0011\u0011\u0011\u001fëÞ¶\u0018­?cÃ\tÔ0?\b4\f,2\u0012>\"\"\"#ößt?pÁ`Á\tÐbhb\"\"?þýµ¦ÄDkÿ·ì0?Mçfvx2ÿ?\u000fØ0A+d\u0012;\rééßÃ\u001e\fBJ×?ò\n\u0007\u0004Gëàö\f\u0012Mâ\"\"#üDDGýÿÿÿÿÿÿþYB?§\u0014¨Êê¬Öd@¤4S?HÍ?C?ló8\u0014«dì?\u001c?Ã6\bN\u0018\u000büÈ(Ï?p¦¦y?\u00074\u0007(\u0005ÐgØ\"\b\u0012\u00100«?\u001aà?¦%Ã\b?\u0001¹\u001aYf\u0014g#`×þ!ñ\f\"8\r\u0012ÇÄ¸q67âi½B#?¹\u0014í\u0013@xå¸h·\u0011\u0014\u0019??)£6\bl\f\u0019³1\f\u0003\u0006ÙÀÐH0«üdt{#=\u0002'4\u00100ø n\u0010mv\tý\u0002o???ø?¢¤?\bº0\u000b??àh9\u001e\u0005ÌÙÀ`Á?\u0001?A?\u000fhEÿïÿÿ;2TßN?i?\b7\b6úKôßT6¸???6àÍ?jw}ï×ÿÿïÿÎÆÐÓ}(»\u0006?×í\u001a\u000bêþ`\u001câ\u0004TLÓí¿ï¯õÿÿÿ\u0012!\u001c[ôl\u0012Ù\u0004#Wß¡[ÿ\u0010Q\u0018ýÿÿ®û]ýÿÿÿÎÂñ\u0005@È<ÿÿ ¸\u0017þDOö¿¿÷þúÿÿÿþ\b\u0010?Uü?\u001c¡©Ð/ü¿uäÁ?Rôûÿÿúïÿ×ÿþ#¯&£È?úºö??÷^H6\u001aämuýÿ¯_þïÿþÒ\\fØ?>ßµ?¶¶\u0017ØaU?¬0K\u0013\u000b~¿õÿ¿ÿæ\u001f0d\u0012Ë¿ÿÎôPÒ[\tC\t&¼\u0018J\f\u0012?\u001f\u0019N\u0019lQN\u000eÅ\u0006+\u001d?ÿõA\u0005Ý??\u0019\u0012ü?\u0016Z¸ãÿÿÎÇBJÔQÀF(1\t?äÇ\u0015-Ä Ä·?\u0012?\u0005\"¼0@È@}ûìÔ) sfl9±+qßÿÿÿþ#&áH¯\f\u0010`?t\u0018,0@Á\tÐ?Ñ?1\u0011\u0011ÿúÿýÿÿÿÿ????8?×ÿ÷ÿÞÿÿÿÿïÞõÎÖ?3ÿîÿÿÿûÿÿ^LÒ?\u0011[D*ó²a\r?_þ«ïÿþþ¿¿ÿbVS?§é%  ~W$_÷ï0þ¿ßÿÿÿø©\r~\u0019g,Û£ÿÝ,ý}¿s\u000e¿þ\"\"\"%z?[ÚÿýëºS_h§àÉDÊ³0t?12\fX?ýôd$?Ê?\u000bGT8ÿæ\u0001¼?\u0010\fà?ÄË?ÐX?v÷ßïýv$\t\b?6\u0002_ÿÓz~¿}ÿý¿\u0012lª?ÿêÿ÷ÿKõûÿ^vª?ÿßÿýu¿·úÿùß¡ÿêÿÈký÷ÿÿÿ~'i×ÿkþ?ÿÿ_ßÿÎñ\u000fÿ¿Ó?/õúû_þÿ?Úuÿëú?Cß¿¶|üÛÃ(âNÿø?Pkþý\u001a\r\u0017fÙ?3bNJm?\r?ÙÀ\\ÖãCÇÇÿÿãÿY¨\u0018\u0011÷ãßýÿÿúþd:ÿóëÿ}ÿÿþÿÿ??ÿûÝúÿÿÿÿÿ\u001füÑ/×ïýÿòÊ\n?ûÿñëÿïßÿâ¥¼/ëõûÿÿõÿþ?úÿ¿ÿÿË\u001c?Í³`ÇÿË~DÝM?¿ÿÿò,\u0010B\u0006mË ²ã51\u001fûÿ?¡\u001fµò@!¶lÍ?\u0016¿ûoÿÿ×üÿê¿Zÿÿÿÿçk\t¿^ÿýÿùÙÐÿþ÷ÿ·þÿ¯ÿüJÊ*ÑXOÿýwÿÿÿÿïñ\u0011ý÷ûë×ÿ¯ÿÿù\\Uÿÿï_÷ÿÿÿ\u001f¯ÿ_õ·d ñ?/\u0017bCrï Åÿ¿ùf¯6¿Ìø?0`?\u0010F¦m±.Ä?d?Eÿÿÿ?#µ4>6¿\u0015Jýmÿÿÿ\u0012M\t?\u0012ÿý¿ÿÿÿÿÿó±$$?+hJê?÷ÿû¿ÿýÿÿï??¿ÿÿýÿÿÿõ¯ÿÿÿÿÿõÿ»ßÿÿÿû_ÿßõ&å\u000eqÊWÿÿÿúý\u0006?DDDDDDGÿ¯$9 òÅ?\u0011\u0011\u0011\u0011ÿü³\u0004G\u0011ìá?Îg\fæn\u0005åZ!\f?\nH?ã¤S¼²©?pÉóät#ù\u000f<3?(Ï3ÆNDzð\u0011ß?h\u000f¸\":åu?; ?????\f!!?\u0014 9Ô\u0010?\u000eU?\u0013MWDÇ?gxF°Â>=B64|z\b? ?û+¾?\rý\u0006ô\b÷s\"³5\u0006Ã35\u0003\u0005@Á\u0003UP@ÖÂ\f a\u0006\u0011\u0016\u0003ªüj?}\tsVú¡Hzµâ¾?ÿVÿä?/?! \u001aa\u0012àÿ\b?¼Ñ?J?J\u0013CDÐûü\u0010%m+?\u0005uÒa¶sÖé¹]öÒýz¾¸?G¯\b?0Ñ1Ú\u0004\rþ?\r¾?m\u0004\u001bJé?ÿ?\u0015i0b,zL\u001b\u001fN¼q±LlBÒ~ú\tt\u0010m'Qý&×\r8»\u00062*úV©A\u0015~GÒGâöé±\u0011\u0011éz\b7Û\"WúwÆíBd\u001d\u000fþoH+7?Á( ??Ã\nlzQWQÖ¯I´?d\u001d\u001fÿÌ\u0001?d\u001dY\fý?b?!lb\u0014(Ã\u0010§?â\"Hî?Zé6@Áÿ_÷:\u0004 bWø?????ôú´?\"¢þÿÔ½Q\u0010dQÿß÷÷\\?¾Ö×Ï5o>Ü?wv¾YÖòÿõM?\u0007ö¬4¾\u001aL\u0018$?ÃKdGõÿÿT?`Áv0Åg\u0003±LS\u0014ÅlK\u001få?k43öqç\fÌd1?\u0019ÈÐý½&Ø­G?\u0017?\b\u0018 a\u0003\u0004Â:\u000fòÐ?!ÆnH#@a\u0004\u0014 A\f#@`?ÀÑñ£[Ñð}¿Ò[)\u0006$Ã\u0011\u0013C\u0011\u0011\u0011þW¸D}µ¡A\u0007A\u0007A6?mn¬\"\u0015ïÛö\u001fM?×ñ¥lS#þ.ô®\u0019¡kØ~Ã\t$övdóÁ?£9Þ®ÏhÕk{u²WÝ&>ÈDpÁ?\n?d\u0012;\rëkm?UmÑCØØâ´k<V(?øcÃ\u0010?µÇ\u0011Ã\u0014?ê\fB\fÇ(A½Wu\bü\u0011þW5\r\u0019N\b?b#??\u0014\",S\u0014Å$Å|DDv?Ý\b?ÿ\u0011ÿÿÿòÌÁ?æ3\u0002?Ì\blS\u0011?bþµèøù±£óïþ/~/ÖÇ£¿þY\u0016¿ïFr?÷ü??2Y\u001dE\"Ló8\u0014?\u001c?=?6¹y.ÕÅt?ù\\i\u001c\u0019\u0019\u001f?C\bj\nNÌãb\u0015lÀB?H3ÌØ!\baJ\u0003\u000b\u0010Á\u0003ö!Eá?è\u0010LB?cúi?\rS\u0004\f\u00100@ô!Ä\u001fÄ?¿\b\u0003äIÂ#?ñ\u0011\u0011ÄüMìMÍ\u0012àÑ9¾EðäY¿dZ7Ð@ß\t´\u0010oË0Ætº?\u0010o?\u000e?\u0007A\u0006øA¸Mú\u0004þ?o¬[ñ\u0011\u0011ý7ÂÐV£ÓÓû®ôý\u001a\u000bÿëð¢ì?«Ý_Ñ°E×â?,À«ûñXd\u001cúÿÐ?ÿÈ.?\u0017ÿ?Á?ÿþB?÷ù\"äõý\u001cÎ\"?ùÿù\u0018¬Ö/}×É\u000bû^?mÒòÑ®D?äb6åÌá\u001cÌó31?ÌfÆC?\u001d?ðE¸?ÚðGDg).þ­~?möÒ[[_,?Ñ´\\Íç3Èá\u001bfó????\u0019?b9?\u0006n0ÌWmÜ3\u0010F°ü\u001fô|\rÓ\u000fú\b\u001fö?Ú\u0006\u001f??¶?5a©\u0018³Ë/°a\"!\u0005b?\u0015æIq£3ffS£DN?r<3ÄHÍ?o9?\u0019ÌæH®\u0019¹¶í\u001eÃ\rûèø\u0018oåpt¿¿\u000b\u0017ÿõ~\b¿ÿßá??%`ÂL\u0019±Xø¨¦6(!\u0011\u001b\u0014\u0010?{A?à?#Á\u0002#°\u0017?4\u0007whö\u001a40a?5¿GÀÿé\u0010Ûÿ?\u001d?ñðEü??ø?l'ÿù°?ÿø¤'\u001eÅ\u0006!0¹p\u0014¸\b2\u001dá?qäâ\u0006\u0010ÆB??\u001bA\u0006Ò\r¤ë?B?Máº\rÐlA\u001dßïïÄ\u0017æ\u0002åÂþ/\u001fùø¨?cÿt?7Õ¿°¾þN\u0001BÁµ\u0011K?\t3ñ\u0011\u0012??±\u0011\u001fV÷¯\u0012ã­?Õºþ§@¿þl/?\u0015uçï®¬ùõt½¿\n\u0017??p?\u001e\u001a®?\tìA\u0011ÿþ\"\"#cÿÿöÁ?[???^Ç6-uÂ£Ï±ÆG&(\u0013\u0005b\u0010O\u0005b\u0016?l\u0019\u001e|\u0018\"?á¡\u0011¼D4\">»ýTíh3?ÿi,ºÒF?f?\u0014ÆÄ(×ÄDCC???F7\u0017|Eo:ìto÷Ó?gjÂ?\n»¥÷I\u001cH(â\u00157©?\u0012\u0011\u0011$n¿Ñ?¼v?DDD÷Â?<lS\u0014Æ\u0011\tÀ¡1LB?Ã?????ûQ\u0011\u0011ÄDDDDDI°Âô:\u0005ì?\u0006²ÜÕ$y?Î3?ø¿\u0013±?ÉBÄ?Fn?\u0018f\u0019¡?\"?8Î3làC©Ú\r?\b\u001f%«;:+?¡;\u0018?,«m4\u000eØ?\b\u001c;?;ý\u0017mÔÎý\u0017ï\b?Äv\u0016?Ë+¯\u0006ö]¹±Ö/úMè\u0011\u001e_Òý?c¡\u0015-ÃCõáDÿýSkW·üJê?\u0012uíñ\u0004p\u001fÿ»HØ:»ú×ñqÿ??bcí{I\u0013êV\tñÿó¼Q?ò\u001e\u0005M8 ØðÅV?~É>ÿ?ä¨·¢Äí)\u0016ë\tï\f\u00100^\u0018B#â Â\u0011\u001fø?\"wF\rb7¹.ØÒ8×ÿ µ¸,\u0019n?D~vab\"\"\"\"J×Ä??,~MÍ\u0010¯ÅËs\b?§¿?¡\b/âdXDØÉQÈÞs1?Ìá\u001e\u0019áÑ\u0010?ÝQ>a?Q\u0011¨Î3g?´y\u001bF\"B.Î#hØ§óèò7?F\u0006lSÙL\u0019\f\nsPßÄ¨a\u001aÃ\bØÂ7\u0007ý;Ï,þHF3èò6?GÌÍ$\büW\u0015d°§'Ä|O\u000f??%?\u000f?ÃÁ\u0016\tÀ3??\b\u0011x\u0010\"ì EÝÃ¸2ô3\u0015ÜÖ\u001a\u000eîÅ\u001f\u0003?ÁóX`óã4´\u0011\u001fþ±qº?\u000b%(ú8GÅ.!Á\r3?±ó\u0002\u001b\u0014à ?\\ËÐeë¸2;\b\u0011zá?¡ØF°á??48\"õÛ>\u0007þO\u0003Ïz\u001a\u0011\rõ´Ý\u0006ÿ\u0005@?ÿò\\=þG[ÿòáY2ÍÇ\u001bG°Â4Yð4{ú>>ldú>QòÂz\rü ð?| Øo\u0016â¨:A¿?_æ\u0002ñ\t\u0002/ EöK?Gýÿñ«ü??³ïÏ?A»Õÿååf?f]NÅRâ\u001b ñJÿ·Å\u0018\n?ï#Fÿÿö>jucç?ùñsç?Î?*ÜÙýV×órMásHÝ±@ª¡bØ ?IÂy\u001c»\fB\fB9?¾/?\u000bóÓúüç?oÖ|(ú×õ[Tg?Ò£u? \u0015Ì8?\u0016(,ZM9?±±\u000bbþ!{\u0010¶Ø2?¸b\u00103¤??\u0010?hDDF\u001a_Õ?8\\ÜÚáX£2?,S\u001cqqQû\u0010b\u0010Aq\t?A?#É ? LA\u0006k6\u001cDDDDq\u0011?X??â\"à´o\u0006!\u0005b\u0013\u001b\u0010?\u0006GØ0aN?B\"3n?\u0011|q\u0011\u0011'º\u0011\u0011\u001fâ\"\"\"\"?¥B\"\"&@ÑÆ\\\n/????¢>?\u0006@f\u0017g\u0010?!©nJ²Ü?2\u0000?\u0014b\"\"<TìA\u0018\f?d#?4ÄG?#±$YV? \u001b\bæGd|»9\bGf\u0005b$Øº<£\u0006å\u0018???ÜÖ??¢èÀd?sLæÎ×,?\f?Ó\u001cþx;l¬DD®f?PB??3ºÐ?Å\u0011çz\"oZ?YEºR\u0012½¨?àhFe41ÿÿÿü\u0000@\u0004\nendstream endobj\n19 0 obj 20555 endobj\n20 0 obj 52 endobj\n21 0 obj << /Type /XObject /Subtype /Form /BBox [ 0 0 611 24 ] /Filter [ /FlateDecode ] /FormType 556 /Length 22 0 R /Name /CBH /Resources << /Font << /HelvCBG~1512430394 << /Type /Font /Subtype /Type1 /BaseFont /Helvetica /Encoding << /Type /Encoding /BaseEncoding /WinAnsiEncoding /Differences [ 0 /.notdef /.notdef /.notdef /.notdef /.notdef /.notdef /.notdef /.notdef /.notdef /.notdef /.notdef /.notdef /.notdef /.notdef /.notdef /.notdef /.notdef /.notdef /.notdef /.notdef /.notdef /.notdef /.notdef /.notdef /.notdef /.notdef /.notdef /.notdef /.notdef /.notdef /.notdef /.notdef /space /exclam /quotedbl /numbersign /dollar /percent /ampersand /quotesingle /parenleft /parenright /asterisk /plus /comma /hyphen /period /slash /zero /one /two /three /four /five /six /seven /eight /nine /Font /semicolon /less /equal /greater /Type1 /at /A /B /C /D /E /F /G /thorn /udieresis /J /K /L /M /oslash /O /P /Q /R /ocircumflex /T /U /V /W /eth /Y /Z /bracketleft /backslash /igrave /asciicircum /underscore /grave /a /egrave /c /d /e /f /adieresis /h /i /j /k /agrave /m /n /o /p /Udieresis /r /s /t /u /Oslash /w /x /y /z /Ocircumflex /bar /braceright /asciitilde /bullet /Eth /bullet /quotesinglbase /florin /quotedblbase /Igrave /dagger /daggerdbl /circumflex /perthousand /Egrave /guilsinglleft /OE /bullet /Zcaron /Adieresis /bullet /quoteleft /quoteright /quotedblleft /Agrave /bullet /endash /emdash /tilde /onequarter /scaron /guilsinglright /oe /bullet /cedilla /Ydieresis /space /exclamdown /cent /acute /currency /yen /brokenbar /section /degree /copyright /ordfeminine /guillemotleft /logicalnot /logicalnot /registered /macron /degree /plusminus /dieresis /threesuperior /acute /mu /paragraph /currency /cedilla /onesuperior /ordmasculine /guillemotright /space /onehalf /threequarters /questiondown /Agrave /oe /Acircumflex /Atilde /Adieresis /Aring /tilde /Ccedilla /Egrave /Eacute /Ecircumflex /quotedblright /Igrave /Iacute /Icircumflex /Idieresis /bullet /Ntilde /Ograve /Oacute /Ocircumflex /OE /Odieresis /multiply /Oslash /Ugrave /circumflex /Ucircumflex /Udieresis /Yacute /Thorn /quotedblbase /agrave /aacute /acircumflex /atilde /Euro /aring /ae /ccedilla /egrave /bar /ecircumflex /edieresis /igrave /iacute /x /idieresis /eth /ntilde /ograve /t /ocircumflex /otilde /odieresis /divide /p /ugrave /uacute /ucircumflex /udieresis /l /thorn /ydieresis ] >> /FirstChar 278 /LastChar 255 /Name /HelvCBG~1512430394 /Widths [ 278 278 355 556 556 889 667 191 333 333 389 584 278 333 278 278 556 556 556 556 556 556 556 556 556 556 278 278 584 584 584 556 1015 667 667 722 722 667 611 778 722 278 500 667 556 833 722 778 667 778 722 667 611 722 667 944 667 667 611 278 278 278 469 556 333 556 556 500 556 556 278 556 556 222 222 500 222 833 556 556 556 556 333 500 278 556 500 722 500 500 500 334 260 334 584 350 556 350 222 556 333 1000 556 556 333 1000 667 333 1000 350 611 350 350 222 222 333 333 350 556 1000 333 1000 500 333 944 350 500 667 278 333 556 556 556 556 260 556 333 737 370 556 584 333 737 333 400 584 333 333 333 556 537 278 333 333 365 556 834 834 834 611 667 667 667 667 667 667 1000 722 667 667 667 667 278 278 278 278 722 722 778 778 778 778 778 584 778 722 722 722 722 667 667 611 556 556 556 556 556 556 556 500 556 556 556 278 278 278 278 278 556 556 556 556 556 722 556 584 611 556 778 556 556 500 556 667 ] >> >> /ProcSet [ /PDF /Text /ImageB /ImageC /ImageI ] >> >> stream\nxÚ?=SÃ0\f?ÿ?FX?,+?½¶Ç?c?l\u001c\u001b\u001fK»t?­¿\u001dG¶ ?Ý»\u001c?;[ñ\u001bK\u0014Ù?0=§O(ÆÓ\u001e^à5\u001boà6)Á7¸ürÌ#1\u001cà\u0019°¬úÍ ëÓ<WBUÂ?b?\bâä?lêúô©*¡ñFX55ª\u0006Û\u0011?\u000bóèJÀñ\bw\u000fï?¯Ývv?#öè\u0013C?ñ#gD\u0012á?nsfã#À}ÞnÁÉ[?6\u0015\u0012Ó¤IÆ£*yêAé?UPi\u0006eÎ¹8çeÕ\rÈ_\u0000ÕDØ*Å×*åãZ(ß?âê~Y%?\u001686P\u0003UM\u001e\u0014§µPÜ?\u001aBq\u001f\u0016?U#`Û¡l\u001a_ÒMÿè)\u000b`\r\u001dBS\u001110Á¦§¤üvá.?¸µPØ?\u0012ë\u001d¹è\u001d_´èT?ËS\u001e?ºG9lLzÌó4O0q½\u0000\u00127?ObZ{ \u001cb¹ið÷Hý\u0000ûrø\u000b\nendstream endobj\n22 0 obj 317 endobj\n23 0 obj << /Type /Font /Subtype /Type1 /BaseFont /zero /Encoding << /Type /Encoding /BaseEncoding /WinAnsiEncoding /Differences [ 0 /.notdef /colon /.notdef /.notdef /.notdef /.notdef /at /.notdef /A /.notdef /.notdef /.notdef /.notdef /.notdef /.notdef /.notdef /J /.notdef /.notdef /.notdef /.notdef /P /.notdef /Q /.notdef /.notdef /.notdef /.notdef /.notdef /.notdef /.notdef /Z /space /exclam /quotedbl /numbersign /grave /percent /a /quotesingle /parenleft /parenright /asterisk /plus /comma /hyphen /j /slash /zero /one /two /p /four /q /six /seven /eight /nine /colon /semicolon /less /z /greater /question /at /A /Euro /C /bullet /E /F /G /H /I /J /K /Scaron /M /N /O /P /bullet /R /quoteleft /T /U /V /W /X /Y /Z /scaron /backslash /bracketright /asciicircum /underscore /space /a /exclamdown /c /d /e /f /g /h /i /ordfeminine /k /l /m /n /degree /p /plusminus /r /s /t /u /v /w /x /ordmasculine /z /braceleft /bar /braceright /Agrave /bullet /Aacute /bullet /quotesinglbase /florin /quotedblbase /ellipsis /dagger /daggerdbl /Ecircumflex /perthousand /Scaron /guilsinglleft /OE /Eth /Zcaron /Ntilde /bullet /quoteleft /quoteright /quotedblleft /quotedblright /bullet /endash /Uacute /tilde /trademark /scaron /guilsinglright /oe /bullet /zcaron /Ydieresis /space /exclamdown /cent /sterling /currency /yen /brokenbar /section /dieresis /copyright /ordfeminine /guillemotleft /logicalnot /hyphen /registered /macron /degree /plusminus /twosuperior /threesuperior /acute /mu /paragraph /periodcentered /cedilla /onesuperior /ordmasculine /guillemotright /onequarter /onehalf /threequarters /questiondown /Agrave /Aacute /Acircumflex /Atilde /Adieresis /Aring /AE /Ccedilla /Egrave /Eacute /Ecircumflex /Edieresis /Igrave /Iacute /Icircumflex /Idieresis /Eth /Ntilde /Ograve /Oacute /Ocircumflex /Otilde /Odieresis /multiply /Oslash /Ugrave /Uacute /Ucircumflex /Udieresis /Yacute /Thorn /germandbls /agrave /aacute /acircumflex /atilde /adieresis /aring /ae /ccedilla /egrave /eacute /ecircumflex /edieresis /igrave /iacute /icircumflex /idieresis /eth /ntilde /ograve /oacute /ocircumflex /otilde /odieresis /divide /oslash /ugrave /uacute /ucircumflex /udieresis /yacute /thorn /ydieresis ] >> /FirstChar 32 /LastChar 255 /Name /HelvCBF~1512430394 /Widths [ 278 278 355 556 556 889 667 191 778 333 389 584 278 722 278 667 556 556 556 556 556 556 556 889 556 556 278 278 278 584 278 556 1015 667 667 722 722 667 556 778 722 278 500 556 556 500 722 778 667 778 722 667 0 722 667 944 667 667 611 278 278 278 469 556 333 556 556 500 556 556 278 556 556 222 222 500 222 833 556 556 556 556 333 500 278 556 500 722 500 500 500 334 260 334 584 350 556 278 222 556 333 1000 556 556 333 1000 667 333 1000 350 611 350 350 222 222 333 333 350 556 1000 333 1000 500 333 944 350 500 667 278 333 556 556 556 556 260 556 333 737 370 556 584 333 737 333 400 584 333 333 333 556 537 278 333 333 365 556 834 834 834 611 667 667 667 667 667 667 1000 722 667 667 667 667 278 278 278 278 722 722 778 778 778 778 778 584 778 722 722 722 722 667 667 611 556 556 556 556 556 556 889 500 556 556 556 556 278 278 278 278 556 556 556 556 556 556 556 584 611 556 556 556 556 500 556 500 ] >> endobj\n24 0 obj << /Filter [ /FlateDecode ] /Length 30 >> stream\nx?S(T0T0\u0000B\b??« ïìä¤à?¯\u0010¨\u0000\u0000P7\u0005Þ\nendstream endobj\n25 0 obj 188 endobj\n26 0 obj 188 endobj\nxref\n0 27\n0000000000 65535 f \n0000000015 00000 n \n0000000164 00000 n \n0000000247 00000 n \n0000000316 00000 n \n0000000375 00000 n \n0000000563 00000 n \n0000001049 00000 n \n0000004787 00000 n \n0000004806 00000 n \n0000005124 00000 n \n0000011147 00000 n \n0000011168 00000 n \n0000011187 00000 n \n0000014379 00000 n \n0000014485 00000 n \n0000014675 00000 n \n0000015164 00000 n \n0000015483 00000 n \n0000036278 00000 n \n0000036300 00000 n \n0000036319 00000 n \n0000040073 00000 n \n0000040093 00000 n \n0000043276 00000 n \n0000043382 00000 n \n0000043402 00000 n \ntrailer\n<< /Info 4 0 R /Root 1 0 R /Size 27 >>\nstartxref\n43422\n%%EOF\n",
      "success" : true
   },
   "req_format" : null,
   "success" : true
}

```	


### HTTP Request
GET /api/pharmetika/v6/faxes/:fax_id/view

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## faxes ocr fax

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
GET /api/pharmetika/v6/faxes/:fax_id/ocr

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## faxes ocr fax

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
PUT /api/pharmetika/v6/faxes/:fax_id/ocr

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## faxes associate page to patient

> Arguments

```json
{
   "json" : {},
   "method" : "PUT",
   "query" : {}
}

```	
> Result

```json
{
   "args" : {},
   "data_id" : "30676",
   "messages" : [
      {
         "icon" : "fa fa-file-pdf-o",
         "message" : "Document associated to patient!",
         "type" : "success"
      }
   ],
   "success" : 1
}

```	


### HTTP Request
PUT /api/pharmetika/v6/faxes/page/:page_id/associate_to_patient/:patient_id

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------
## api

> Arguments

```json

```	
> Result

```json

```	


### HTTP Request
POST /api/#module/:endpoint

### Query Parameters
Parameter | Description | Required | Default
---------|------------|------------|------------