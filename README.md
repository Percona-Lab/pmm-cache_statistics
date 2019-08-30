# pmm-cache_statistics
1) On your MySQL server, change directories into pmm-client (/usr/local/percona/pmm-client/).
2) In the file queries-mysqld.yml, add the information from the mysql.yml from here.
3) On your PMM Server, on the left hand side of the screen, click the + icon and select Import. 
4) Select Upload .json file.
5) Navigate on to the MySQL InnoDB Index Statistics.json, select it, and click open.

You should now have the dashboard working.
