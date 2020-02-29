
```shell
select int64_field_6 as hour, count(*) as hitcount from logdata.accesslog
group by hour
order by hour

bq query "select string_field_10 as request, count(*) as requestcount from logdata.accesslog group by request order by requestcount desc"
```
