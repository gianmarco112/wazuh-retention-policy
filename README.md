# wazuh-retention-policy
Retention policy for wazuh alerts index
# POLICY
## Delete alerts older than 90d
```json
{
"policy": {
"policy_id": "retention-policy-3M",
"description": "retention policy 3 M ",
"last_updated_time": 1719478953562,
"schema_version": 18,
"error_notification": null,
"default_state": "initial",
"states": [
{
"name": "initial",
"actions": [],
"transitions": [
{
"state_name": "delete_alerts",
"conditions": {
"min_index_age": "90d"
}
}
]
},
{
"name": "delete_alerts",
"actions": [
{
"retry": {
"count": 3,
"backoff": "exponential",
"delay": "1m"
},
"delete": {}
}
],
"transitions": []
}
],
"ism_template": [
{
"index_patterns": [
"wazuh-alerts-*"
],
"priority": 1,
"last_updated_time": 1719478953562
}
]
}
}
```
