# heart-beat cycle start

```json
[
	//comment:***new
	{
		"api_type": "RS>all_local_DB_C",
		"cycle":"nnnnnnnnnn",
		"time": "yyyy-mm-dd,HH:MM:SS"
	},
	{
		"api_type": "DB_C>all_RS",
		"cycle": "nnnnnnnnnn",
		"T_hash_this_cycle_local_RS": "nnnnnnnnnn",
		"total-T_hash": "nnnnnnnnnnnn",
		"query_this_cycle": "nnnnnn",
		"fault_query_this_cycle": "nnnnnn",
		"DB_C-hash": "hhhhhhhh.hhhhhhhh.hhhhhhhh.hhhhhhhh.hhhhhhhh.hhhhhhhh.hhhhhhhh.hhhhhhhh"
	},
	//end of new

	
	{	
		"api_type": "DB_C>all_local_PS(DB_T)",
		"prv_hash_for_each_PS": "hhhhhhhh",//use of previous hash?
		"cycle": "nnnnnnnnnn",
		"time": "yyyy-mm-dd,HH:MM:SS"
	},
	
	{
		"api_type": "PS(DB_T)>all_DB_C",
		"cycle": "nnnnnnnnnn",
		"RS_PS_ID": "RSid_PSid",
		"add T_hash": [
			"hhhhhhhh.hhhhhhhh.hhhhhhhh.hhhhhhhh.hhhhhhhh.hhhhhhhh.hhhhhhhh.hhhhhhhh",
			"hhhhhhhh.hhhhhhhh.hhhhhhhh.hhhhhhhh.hhhhhhhh.hhhhhhhh.hhhhhhhh.hhhhhhhh"
		],
		"T_hash_this_cycle_local_PS" : "nnnnnnnnnn",//need this?
		"total-T_hash": "nnnnnnnnnn",
		"PS(DB_T)-hash": "hhhhhhhh"
	},

	{
		"api_type": "PS>all_local_TS",
		"pre_hash_for_each_TS": "hhhhhhhh",
		"cycle": "nnnnnnnnnn",
		"time": "yyyy-mm-dd,HH:MM:SS"
	},
	{
		"api_type": "TS>PS",
		"cycle": "nnnnnnnnnn",
		"T_hash": "hhhhhhhh.hhhhhhhh.hhhhhhhh.hhhhhhhh.hhhhhhhh.hhhhhhhh.hhhhhhhh.hhhhhhhh"
	},
	//comment:***new
	{
		"api_type":"TC>TS",
		"transaction_json":"json_for_transaction_info"
	},
	{
		"api_type":"TS>TC",
		"upload_success": true //true for success, false for fail
	}
	
	//end of new
	
	//***********Query
	
	
	{
		"api_type": "DB_C>QS",
		"valid": true, // valid of DB_C?
		"cycle": "nnnnnnnnnn",
		"time": "yyyy-mm-dd,HH:MM:SS"
		//when to give feedback of query? if DB_C>QS then QS>DB_C, need another DB_C>QS? , how to know time of upload?
	},
	{
		"api_type": "QS>DB_C",
		"RS_QS_ID": "RSid_QSid",
		"?hash": "hhhhhhhh.hhhhhhhh.hhhhhhhh.hhhhhhhh.hhhhhhhh.hhhhhhhh.hhhhhhhh.hhhhhhhh"//"Q_hash"?
	},
	
	//comment:**new
	{
		"api_type": "QC>QS",
		"Q_hash": "hhhhhhhh.hhhhhhhh.hhhhhhhh.hhhhhhhh.hhhhhhhh.hhhhhhhh.hhhhhhhh.hhhhhhhh"
	},
	{
		"api_type": "QS>QC",
		"Q_hash_valid":true,
		"time_of_upload": "yyyy-mm-dd,HH:MM:SS"
	},
	
	//end of new
	
	
	{
		"api_type": "RS>all_dashboard",
		"cycle": "nnnnnnnnnn",
		"time": "yyyy-mm-dd,HH:MM:SS",
		"RS_info": [
			{ "name": "nnnnnn" },
			{ "geo_Long": "nn.nn" },
			{ "geo_lad": "nn.nn" }
		],
		"T_hash_this_cycle_local_RS": "nnnnnnnnnn",//Know from RS_PS ID?
		"total-T_hash": "nnnnnnnnnnnn",//can be calculated?
		"DB_T-hash": "hhhhhhhh.hhhhhhhh.hhhhhhhh.hhhhhhhh.hhhhhhhh.hhhhhhhh.hhhhhhhh.hhhhhhhh",
		"query_this_cycle": "nnnnnn",
		"fault_query_this_cycle": "nnnnnn",
		"DB_C-hash": "hhhhhhhh.hhhhhhhh.hhhhhhhh.hhhhhhhh.hhhhhhhh.hhhhhhhh.hhhhhhhh.hhhhhhhh"
	}
]
```

# TS upload t_hash

```json
{
    "api_type": "TS>PS",
    "cycle": "nnnnnnnnnn",
    "T_hash": "hhhhhhhh.hhhhhhhh.hhhhhhhh.hhhhhhhh.hhhhhhhh.hhhhhhhh.hhhhhhhh.hhhhhhhh"
    }

{
    "api_type": "next PS>all_local_TS",
    "pre_hash_for_each_TS": "hhhhhhhh",
    "cycle": "nnnnnnnnnn",
    "time": "yyyy-mm-dd,HH:MM:SS"
    }
```
