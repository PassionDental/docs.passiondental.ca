# Passion Dental Group Snowflake

## How to connect via terminal

`snowsql -a passiondental-td18550 --authenticator externalbrowser`

## How to rotate SCIM key

1. Login to Snowflake (see above)
2. Run `select system$generate_scim_access_token('AAD_PROVISIONING');`
3. Login to admin.microsoft.com and go to Entra ID
4. Go to Enterprise Applications
5. Go to Snowflake
6. Go to Provisioning
7. Click Edit
8. Update credentials