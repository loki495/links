Opencart 1.5.6.4
================

* check duplicate accounts, show orders by customer_id

```
sql
SELECT 
  c.email, 
  COUNT(c.customer_id) as total, 
  GROUP_CONCAT(CONCAT(o.customer_id, ' - ', c.email, ' - ', c.date_added, ' - ', total_order)) 
FROM 
  oc_customer c 
  JOIN (
    SELECT 
      customer_id, 
      COUNT(order_id) as total_order 
    FROM 
      oc_order 
     GROUP BY customer_id) as o 
  ON o.customer_id = c.customer_id 
WHERE 
  c.date_added > '2018' 
GROUP BY 
  c.email 
HAVING 
  total > 1
```


General MySQL
=============

* create user and database

```
CREATE USER 'admin'@'localhost' IDENTIFIED BY 'mypass';
CREATE DATABASE IF NOT EXISTS foo;
GRANT ALL ON foo.* TO 'admin'@'localhost';
```

LARAVEL
=======

* List queued jobs by class/id

```
select payload, substring_index(job,'"',1) as job, substring_index(business_id,';',1) as business_id
FROM (SELECT payload, SUBSTR(payload,INSTR(payload,'App\\\\Jobs\\\\')+11) as job, SUBSTR(payload,INSTR(payload,'business_id')+16) as business_id FROM `smartend_jobs` WHERE 1) a order by job DESC, business_id DESC
```

* Find duplicate jobs

```
SELECT job_bid, COUNT(id) as total from (select id, CONCAT(job,'-',business_id) as job_bid from (select id, payload, substring_index(job,'"',1) as job, substring_index(business_id,';',1) as business_id
FROM (SELECT id, payload, SUBSTR(payload,INSTR(payload,'App\\\\Jobs\\\\')+11) as job, SUBSTR(payload,INSTR(payload,'business_id')+16) as business_id FROM `smartend_jobs` WHERE 1) a ) b  
ORDER BY CONCAT(job,'-',business_id) ASC) c GROUP BY job_bid HAVING total > 1
```

CentOS
======

* Check with packages provide libs

```
repoquery --repofrompath=centos7,http://mirror.centos.org/centos/7/os/`arch` \ --repoid=centos7 \ # Only consider this specific repository. --qf="%{location}" \ # Output the URL of the RPM file. --whatprovides XXX
```

* Find and show / filter by perm / size /  user

```
find . -type d -printf "depth="%d" sym perm="%M" perm="%m" size="%s" user="%u" group="%g" name="%p" type="%Y\\n | grep -v perm=755
```


Ubuntu
======

* show login info

```
for i in /etc/update-motd.d/*; do if [ "$i" != "/etc/update-motd.d/98-fsck-at-reboot" ]; then $i; fi; done
```
