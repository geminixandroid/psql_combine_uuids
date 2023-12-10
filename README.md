combine_uuids
=
### PostgreSQL function to combine(munge, merge) two uuids into one
The result is always the same for the same parameters, the order of the parameters does not matter.
```sql
CREATE FUNCTION combine_uuids(uuid1 uuid, uuid2 uuid) RETURNS uuid
LANGUAGE plpgsql
AS $$
DECLARE
    text1 text = uuid1::text;
    text2 text = uuid2::text;
BEGIN  
    RETURN 
        CONCAT( 
            LPAD(TO_HEX((('x' || SUBSTRING (text1,1,2))::BIT(8) # ('x' || SUBSTRING (text2,1,2))::BIT(8))::int),2,'0'),
            LPAD(TO_HEX((('x' || SUBSTRING (text1,3,2))::BIT(8) # ('x' || SUBSTRING (text2,3,2))::BIT(8))::int),2,'0'),
            LPAD(TO_HEX((('x' || SUBSTRING (text1,5,2))::BIT(8) # ('x' || SUBSTRING (text2,5,2))::BIT(8))::int),2,'0'),
            LPAD(TO_HEX((('x' || SUBSTRING (text1,7,2))::BIT(8) # ('x' || SUBSTRING (text2,7,2))::BIT(8))::int),2,'0'),
            '-',
            LPAD(TO_HEX((('x' || SUBSTRING (text1,10,2))::BIT(8) # ('x' || SUBSTRING (text2,10,2))::BIT(8))::int),2,'0'),
            LPAD(TO_HEX((('x' || SUBSTRING (text1,12,2))::BIT(8) # ('x' || SUBSTRING (text2,12,2))::BIT(8))::int),2,'0'),
            '-',
            LPAD(TO_HEX((('x' || SUBSTRING (text1,15,2))::BIT(8) # ('x' || SUBSTRING (text2,15,2))::BIT(8))::int),2,'0'),
            LPAD(TO_HEX((('x' || SUBSTRING (text1,17,2))::BIT(8) # ('x' || SUBSTRING (text2,17,2))::BIT(8))::int),2,'0'),
            '-',
            LPAD(TO_HEX((('x' || SUBSTRING (text1,20,2))::BIT(8) # ('x' || SUBSTRING (text2,20,2))::BIT(8))::int),2,'0'),
            LPAD(TO_HEX((('x' || SUBSTRING (text1,22,2))::BIT(8) # ('x' || SUBSTRING (text2,22,2))::BIT(8))::int),2,'0'),
            '-',
            LPAD(TO_HEX((('x' || SUBSTRING (text1,25,2))::BIT(8) # ('x' || SUBSTRING (text2,25,2))::BIT(8))::int),2,'0'),
            LPAD(TO_HEX((('x' || SUBSTRING (text1,27,2))::BIT(8) # ('x' || SUBSTRING (text2,27,2))::BIT(8))::int),2,'0'),
            LPAD(TO_HEX((('x' || SUBSTRING (text1,29,2))::BIT(8) # ('x' || SUBSTRING (text2,29,2))::BIT(8))::int),2,'0'),
            LPAD(TO_HEX((('x' || SUBSTRING (text1,31,2))::BIT(8) # ('x' || SUBSTRING (text2,31,2))::BIT(8))::int),2,'0'),
            LPAD(TO_HEX((('x' || SUBSTRING (text1,33,2))::BIT(8) # ('x' || SUBSTRING (text2,33,2))::BIT(8))::int),2,'0'),
            LPAD(TO_HEX((('x' || SUBSTRING (text1,35,2))::BIT(8) # ('x' || SUBSTRING (text2,35,2))::BIT(8))::int),2,'0')
        )::uuid; 
END;  
$$;
```
## Example
```sql
SELECT combine_uuids('866a796f-1c47-479f-bb5b-bd423d42603d','4670a105-5f4d-40bd-9084-fcb74c1ea624')
-- c01ad86a-430a-0722-2bdf-41f5715cc619
```
