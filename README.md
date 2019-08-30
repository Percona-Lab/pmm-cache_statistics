# pmm-cache_statistics
1) On your MySQL server, change directories into pmm-client.

cd /usr/local/percona/pmm-client/ 

2) In the file queries-mysqld.yml, add the following custom query:

mysql_innodb_cached_indexes:
   query: " SELECT SUBSTRING_INDEX(tables.name, '/', +1 ) AS schema_name, SUBSTRING_INDEX(tables.name, '/', -1 ) AS table_name,   indexes.NAME AS index_name,   cached.N_CACHED_PAGES*(select variable_value from performance_schema.global_variables where variable_name  = 'innodb_page_size') AS cached_bytes FROM   INFORMATION_SCHEMA.INNODB_CACHED_INDEXES AS cached,   INFORMATION_SCHEMA.INNODB_INDEXES AS indexes,   INFORMATION_SCHEMA.INNODB_TABLES AS tables WHERE   cached.INDEX_ID = indexes.INDEX_ID   AND indexes.TABLE_ID = tables.TABLE_ID;"
   metrics:
    - table_name:
        usage: "LABEL"
        description: "Table name"
    - cached_bytes:
        usage: "GAUGE"
        description: "InnoDB Page sizes"
    - schema_name:
        usage: "LABEL"
        description: "Schema Name"
    - index_name:
        usage: "LABEL"
        description: "Index name"
        
3) On your PMM Server, on the left hand side of the screen, click the + icon and select Import. 
4) Select Upload .json file.
5) Navigate on to the MySQL InnoDB Index Statistics.json, select it, and click open.

You should now have the dashboard working.
