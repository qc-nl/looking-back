# Analytics - Staff augmentation
这算是我重回这家咨询公司之后参与的第一个billable项目，business itelligence类型的项目算是自己的舒适区，没想到这个项目会持续一年。\

背景：
salesforce migration -》 reporting rebuild
investors reporting

technology involved
- redshift
- tableau
- jira, confluence



## fun takeawys:
salesforce data extract 
ingest into redshift

## something new for me:
**sql with statements**\
虽然下面的code snippet不是这个项目的，不过可以表达我的意思

```sql
with map_table  as (
    select * from (
        SELECT 
        e.gkg_mid, 
        e.name, 
        row_number() over(partition by e.gkg_mid order by length(e.name) desc) as first_record
    FROM `pg-xx-n-app-xxxxxx.table.table_dev` cross join
    UNNEST (entities) as e
    where e.gkg_mid != 'na'  
    order by e.name) 
where first_record =1 
)

select distinct 
ent.name as org_name, 
ent.gkg_mid as id1, 
map_table.* from `pg-xx-n-app-xxxxxx.table.table_dev` 
cross join UNNEST (entities) as ent
left join map_table 
on ent.gkg_mid = map_table.gkg_mid
```

tableau row level securty using username（）

