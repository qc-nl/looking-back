# Analytics - Staff augmentation
这算是我重回这家咨询公司之后参与的第一个billable项目，business itelligence类型的项目算是自己的舒适区，没想到这个项目会持续一年。
顾客是家国外的科技初创公司，快速扩张中，千把人的公司，几个月的时间通过招聘达到上万人的员工规模。
顾客原本的分析团队20人上下，我们项目组8-10人通过合同工的方式加入顾客的分析团队，成为表哥表姐，帮顾客写sql，画tableau报表。
技术上这本不是最有趣的项目，实施起来却无比的费心，尤其是顾客开始纠结“好不好看”的时候，比较好看与否都是千人千面的问题。
我当时所在的workstream要稍微走运一些，工作的范围相对确定：
因为业务流程的变化，顾客当时的salesforce instance正在迁移到一个新的instance。
数据源发生了变化，bi这一层自然也要跟上，我们的workstream要对salesforce相关的一系列报表进行更新，更上salesforce新instance。
2020年11月中旬加入的项目，go-live的日子定在了2021元月四号周一。
这是一家初创公司，每周日下午都由公司高层和投资者回报销售相关的指标，这些数据都出自于我们项目组研发和维护的tableau报表。


technology involved
- redshift
- tableau
- jira, confluence
- salesforce



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

