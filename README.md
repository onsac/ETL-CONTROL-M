

<h3 align="center">ETL-CONTROL-M</h3>
<h4 align="center">Extracción de información de Control-M Enterprise Manager</h4>
<h4 align="center">Base de datos - PostgreSQL</h4>

## ETL – net_report

Archivo com sql : net.sql

```sh
select 'select * from net_report where net_name = ' ||''''||max(net_name)||'''' from net_report  group by code\gexec
```
Comando para generar el archivo "net.txt"

Ajuste los parámetros : (dbname) (username) (password)
	
```sh
> sql --file=net.sql --dbname=<emdb> --username=<emuser> --no-password=<password> -A -q -o net.txt
```

## ETL – runinfo_history

Archivo com sql : history.sql

```sh
select 'select * from runinfo_history where order_date = ' ||''''|| 
       max(date (substring(ctm_odate from 1 for 4)||'-'||
	    substring(ctm_odate from 5 for 2)||'-'||
	    substring(ctm_odate from 7 for 2)) - integer '1')||''''||
	   ' or start_time >= ' ||''''||
       max(date (substring(ctm_odate from 1 for 4)||'-'||
	   substring(ctm_odate from 5 for 2)||'-'||
	   substring(ctm_odate from 7 for 2)) - integer '1')||''''
       from comm\gexec
```
Comando para generar el archivo "history.txt"
	
Ajuste los parámetros : (dbname) (username) (password)
	
```sh
> sql --file=history.sql --dbname=<emdb> --username=<emuser> --no-password=<password> -A -q -o history.txt  
```
## ETL – net_name

Archivo com sql : ajf.sql

```sh
select 'select * from a' || max(net_name) || 'job' from net_report group by code\gexec
```

Comando para generar el archivo "ajf.txt"
	
Ajuste los parámetros : (dbname) (username) (password)
	
```sh
> sql --file=ajf.sql --dbname=<emdb> --username=<emuser> --no-password=<password> -A -q -o ajf.txt  
```


