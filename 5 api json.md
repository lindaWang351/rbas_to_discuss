# heart-beat cycle start

```json
[
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
	{	
		"api_type": "DB_C>all_local_PS(DB_T)",
		"prv_hash_for_each_PS": "hhhhhhhh",//use of previous hash->talking to the correct PS
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
		"T_hash_this_cycle_local_PS" : "nnnnnnnnnn",
		"total-T_hash": "nnnnnnnnnn",
		"PS(DB_T)-hash": "hhhhhhhh"
	},
	//At this stage, only has 1 layer of PS
	//Later, might add layers of PS
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
	{
		"api_type":"TC>TS",
		"transaction_json":"json_for_transaction_info"
	},
	{
		"api_type":"TS>TC",
		"upload_success": true //true for success, false for fail
	}
	
	
	//***********Query
	
	
	{
		"api_type": "DB_C>QS",
		"valid": true, // valid of DB_C?
		"cycle": "nnnnnnnnnn",
		"time": "yyyy-mm-dd,HH:MM:SS"
		//how to know time of upload?
	},
	{
		"api_type": "QS>DB_C",
		"RS_QS_ID": "RSid_QSid",
		"?hash": "hhhhhhhh.hhhhhhhh.hhhhhhhh.hhhhhhhh.hhhhhhhh.hhhhhhhh.hhhhhhhh.hhhhhhhh"//"Q_hash"?
	},

	{
		"api_type": "QC>QS",
		"Q_hash": "hhhhhhhh.hhhhhhhh.hhhhhhhh.hhhhhhhh.hhhhhhhh.hhhhhhhh.hhhhhhhh.hhhhhhhh"
	},
	{
		"api_type": "QS>QC",
		"Q_hash_valid":true,
		"time_of_upload": "yyyy-mm-dd,HH:MM:SS"
	},
	{
		"api_type": "RS>all_dashboard",
		"cycle": "nnnnnnnnnn",
		"time": "yyyy-mm-dd,HH:MM:SS",
		"RS_info": [
			{ "name": "nnnnnn" },
			{ "geo_Long": "nn.nn" },
			{ "geo_lad": "nn.nn" }
		],
		"T_hash_this_cycle_local_RS": "nnnnnnnnnn",
		"total-T_hash": "nnnnnnnnnnnn",//can be calculated?
		"DB_T-hash": "hhhhhhhh.hhhhhhhh.hhhhhhhh.hhhhhhhh.hhhhhhhh.hhhhhhhh.hhhhhhhh.hhhhhhhh",//delete this one?
		"query_this_cycle": "nnnnnn",
		"fault_query_this_cycle": "nnnnnn",
		"DB_C-hash": "hhhhhhhh.hhhhhhhh.hhhhhhhh.hhhhhhhh.hhhhhhhh.hhhhhhhh.hhhhhhhh.hhhhhhhh"
	}
]
```

# TS upload t_hash

```json
//Later one layer of PS -> multiple layers of PS

//DB_C>PS', PS'>DB_C, PS'>PS", PS">PS', PS">TS, TS>PS"
{
	"api_type":"PS_1>all_local_PS_2",
	"previous_hash_for_PS_2": "hhhhhhhh",
	"cycle": "nnnnnnnnnn",
	"time": "yyyy-mm-dd,HH:MM:SS"

},
{
	"api_type":"PS_2>PS_1",
	"cycle": "nnnnnnnnnn",
	"RS_PS_ID": "RSid_PSid",//Does this need to be changed to identify belong to which PS1? which PS1id_PS2id?
	"add T_hash": [
		"hhhhhhhh.hhhhhhhh.hhhhhhhh.hhhhhhhh.hhhhhhhh.hhhhhhhh.hhhhhhhh.hhhhhhhh",
		"hhhhhhhh.hhhhhhhh.hhhhhhhh.hhhhhhhh.hhhhhhhh.hhhhhhhh.hhhhhhhh.hhhhhhhh"
	],
	"T_hash_this_cycle_local_PS_2" : "nnnnnnnnnn",
	"total-T_hash": "nnnnnnnnnn",//can this be calculated?
	"PS(DB_T)-hash": "hhhhhhhh"
}
//PS'>DB_C changed to
{
	"api_type":"PS_1>DB_C",
	"cycle":"nnnnnnnnnn",
	"RS_PS_ID": "RSid_PSid",
	"T_hash_this_cycle_local_PS_2": "nnnnnnnnnn",
	"total-T_hash":"nnnnnnnnnn",
	"PS2-hash":"hhhhhhhh"
}
/*
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
	*/
```
