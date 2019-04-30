---
title: 改變記憶體最佳化資料表 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 690b70b7-5be1-4014-af97-54e531997839
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: dab550be7e867486d7a155c2113e2d7e3b63a038
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63065616"
---
# <a name="altering-memory-optimized-tables"></a>改變記憶體最佳化資料表
  不支援執行記憶體最佳化資料表上的 ALTER 作業。 這些作業包括變更 bucket_count、加入或移除索引，以及加入或移除資料行等等。 本主題提供如何更新記憶體最佳化之資料表的指導方針。  
  
## <a name="updating-the-definition-of-a-memory-optimized-table"></a>更新記憶體最佳化資料表的定義  
 若要更新記憶體最佳化資料表的定義，則需建立包含更新之資料表定義的新資料表、將資料複製到新資料表，並且開始使用新資料表。 除非資料表是唯讀的，否則就需要停止資料表上的工作負載，以確保複製資料時不會對資料表進行任何變更。  
  
 以下程序概述更新資料表所需的步驟。 在這個範例中，更新會加入索引。 此程序會保留資料表的名稱，並需要進行兩次資料複製作業：一次是複製到暫存資料表，另一次是複製到新的資料表。 變更索引的 bucket_count，或是加入或移除資料行都是以相同方式執行。  
  
1.  停止資料表上的工作負載。  
  
2.  產生資料表的指令碼，並將新索引加入至指令碼。  
  
3.  產生參考 T 之結構描述繫結物件的指令碼 (主要是原生編譯預存程序) 及其權限。  
  
     可使用下列查詢找到參考資料表的結構描述繫結物件：  
  
    ```sql  
    declare @t nvarchar(255) = N'<table name>'  
  
    select r.referencing_schema_name, r.referencing_entity_name  
    from sys.dm_sql_referencing_entities (@t, 'OBJECT') as r join sys.sql_modules m on r.referencing_id=m.object_id  
    where r.is_caller_dependent = 0 and m.is_schema_bound=1;  
    ```  
  
     您可以使用下列 [!INCLUDE[tsql](../../includes/tsql-md.md)] 撰寫預存程序之權限的指令碼：  
  
    ```sql  
    declare @sp nvarchar(255) = N'<procedure name>'  
    declare @permissions nvarchar(max) = N''  
  
    select @permissions += dp.state_desc + N' ' + dp.permission_name + N' ON ' +   
       quotename(schema_name(o.schema_id)) + N'.' + quotename(o.name) + N' TO ' +  
       quotename(u.name) + N'; ' + char(13)  
    from sys.database_permissions as dp  
  
    join sys.database_principals as u  
       on u.principal_id = dp.grantee_principal_id  
  
    join sys.objects as o  
       on o.object_id = dp.major_id  
    where dp.class = 1 /* object */  
       and dp.minor_id = 0 and o.object_id=object_id(@sp);  
  
    select @permissions  
    ```  
  
4.  建立資料表的副本，並且從原始資料表將資料複製到資料表副本。 可以建立複本，使用下列[!INCLUDE[tsql](../../includes/tsql-md.md)] <sup>1</sup>。  
  
    ```sql  
    select * into dbo.T_copy from dbo.T  
    ```  
  
     如果沒有足夠的可用記憶體`T_copy`可能是記憶體最佳化資料表，使資料複製更快速。<sup>2</sup>  
  
5.  卸除參考原始資料表的結構描述繫結物件。  
  
6.  卸除原始資料表。  
  
7.  建立新資料表 (`T`)，其中的指令碼會包含新索引。  
  
8.  從 `T_copy` 將資料複製到 `T`。  
  
9. 重新建立參考的結構描述繫結物件，並套用權限。  
  
10. 在 `T` 上啟動工作負載。  
  
 <sup>1</sup>請注意，`T_copy`會保存到磁碟，在此範例中。 如果有 `T` 的備份可用，`T_copy` 可以是暫存或非持久資料表。  
  
 <sup>2</sup>必須有足夠的記憶體供`T_copy`。 記憶體不會在 `DROP TABLE` 上立即釋放。 如果 `T_copy` 為記憶體最佳化，則必須有足夠的記憶體可供兩個額外的 `T` 副本使用。 如果 `T_copy` 是以磁碟為基礎的資料表，就只需要足夠的記憶體以進行額外一次 `T` 複製，因為卸除舊版 `T` 之後，需讓記憶體回收行程趕上進度。  
  
## <a name="changing-schema-powershell"></a>變更結構描述 (PowerShell)  
 下列 PowerShell 指令碼會藉由撰寫資料庫和相關權限的指令碼，以準備並產生結構描述變更。  
  
 使用方式： prepare_schema_change.ps1 *v e _ * * db_name`schema_name`table_name*  
  
 此指令碼會採用資料表做為引數，並且撰寫在目前資料夾中物件與其權限以及參考結構描述繫結物件與其權限的指令碼。 總共會產生 7 個指令碼用於更新輸入資料表的結構描述：  
  
-   將資料複製到暫存資料表 (堆積)。  
  
-   卸除參考資料表的結構描述繫結物件。  
  
-   卸除資料表。  
  
-   重新建立具有新結構描述的資料表，並重新套用權限。  
  
-   從暫存資料表將資料複製到重新建立的資料表。  
  
-   重新建立參考資料表的結構描述繫結物件與其權限。  
  
-   卸除暫存資料表。  
  
 步驟 4 的指令碼應會更新，以反映所需的結構描述變更。 資料表的資料行中如有變更，也會視需要更新步驟 5 (從暫存資料表複製資料) 和 6 (重新建立預存程序) 的指令碼。  
  
```sql  
# Prepare for schema changes by scripting out the table, as well as associated permissions  
# --------  
# Usage: prepare_schema_change.ps1 server_name db_name schema_name table_name  
# stop execution once an error occurs  
$ErrorActionPreference="Stop"  
  
if($args.Count -le 3)  
{  
   throw "Usage prepare_schema_change.ps1 server_name db_name schema_name table_name"  
}  
  
$servername = $args[0]  
$database = $args[1]  
$schema = $args[2]  
$object = $args[3]  
  
$object_heap = "$object$(Get-Random)"  
  
[System.Reflection.Assembly]::LoadWithPartialName("Microsoft.SqlServer.SMO") | out-null  
  
$server =  New-Object ("Microsoft.SqlServer.Management.SMO.Server") ($servername)  
$scripter = New-Object ("Microsoft.SqlServer.Management.SMO.Scripter") ($server)  
  
## initialize table variable  
$tableUrn = $server.Databases[$database].Tables[$object, $schema]  
if($tableUrn.Count -eq 0)  
{  
   throw "Table or database not found"  
}  
  
## initialize scripting object  
$scriptingOptions = New-Object ("Microsoft.SqlServer.Management.SMO.ScriptingOptions")   
$scriptingOptions.Permissions = $True  
$scriptingOptions.ScriptDrops = $True  
  
$scripter.Options = $scriptingOptions;  
  
write-host "(1) Scripting SELECT INTO $object_heap for table [$object] to 1_copy_to_heap_for_$schema`_$object.sql"  
Echo "SELECT * INTO $schema.$object_heap FROM $schema.$object WITH (SNAPSHOT)" | Out-File "1_copy_to_heap_$schema`_$object.sql";  
write-host "--done--"  
write-host ""  
  
write-host "(2) Scripting DROP for procs schema-bound to [$object] 2_drop_procs_$schema`_$object.sql"  
## query referencing schema-bound objects  
$dt = $server.Databases[$database].ExecuteWithResults("select r.referencing_schema_name, r.referencing_entity_name  
from sys.dm_sql_referencing_entities ('$schema.$object', 'OBJECT') as r join sys.sql_modules m on r.referencing_id=m.object_id  
where r.is_caller_dependent = 0 and m.is_schema_bound=1;")  
  
## initialize out file  
Echo "" | Out-File "2_drop_procs_$schema`_$object.sql"  
## loop through schema-bound objects  
Foreach ($t in $dt.Tables)  
{    
   Foreach ($r in $t.Rows)  
   {    
      ## script object   
      $so =  $server.Databases[$database].StoredProcedures[$r[1], $r[0]]  
      $scripter.Script($so) | Out-File -Append "2_drop_procs_$schema`_$object.sql"  
   }  
}  
write-host "--done--"  
write-host ""  
  
write-host "(3) Scripting DROP table for [$object] to 3_drop_table_$schema`_$object.sql"  
$scripter.Script($tableUrn) | Out-File "3_drop_table_$schema`_$object.sql";  
write-host "--done--"  
write-host ""  
  
## now script creates  
$scriptingOptions.ScriptDrops = $False  
  
write-host "(4) Scripting CREATE table and permissions for [$object] to !please_edit_4_create_table_$schema`_$object.sql"  
write-host "***** rename this script to 4_create_table.sql after completing the updates to the schema"  
$scripter.Script($tableUrn) | Out-File "!please_edit_4_create_table_$schema`_$object.sql";  
write-host "--done--"  
write-host ""  
  
write-host "(5) Scripting INSERT INTO table from heap and UPDATE STATISTICS for [$object] to 5_copy_from_heap_$schema`_$object.sql"  
write-host "[update this script if columns are added to or removed from the table]"  
Echo "INSERT INTO [$schema].[$object] SELECT * FROM [$schema].[$object_heap]; UPDATE STATISTICS [$schema].[$object] WITH FULLSCAN, NORECOMPUTE" | Out-File "5_copy_from_heap_$schema`_$object.sql";  
write-host "--done--"  
write-host ""  
  
write-host "(6) Scripting CREATE PROC and permissions for procedures schema-bound to [$object] to 6_create_procs_$schema`_$object.sql"  
write-host "[update the procedure definitions if columns are renamed or removed]"  
## initialize out file  
Echo "" | Out-File "6_create_procs_$schema`_$object.sql"  
## loop through schema-bound objects  
Foreach ($t in $dt.Tables)  
{    
   Foreach ($r in $t.Rows)  
   {    
      ## script the schema-bound object  
      $so =  $server.Databases[$database].StoredProcedures[$r[1], $r[0]]  
      foreach($s in $scripter.Script($so))  
        {  
            Echo $s | Out-File -Append "6_create_procs_$schema`_$object.sql"  
            Echo "GO" | Out-File -Append "6_create_procs_$schema`_$object.sql"  
        }  
   }  
}  
write-host "--done--"  
write-host ""  
  
write-host "(7) Scripting DROP $object_heap to 7_drop_heap_$schema`_$object.sql"  
Echo "DROP TABLE $schema.$object_heap" | Out-File "7_drop_heap_$schema`_$object.sql";  
write-host "--done--"  
write-host ""  
  
```  
  
 下列 PowerShell 指令碼會執行前述範例中所撰寫的結構描述變更指令碼。 此指令碼會採用資料表做為引數，並執行為該資料表與相關預存程序產生的結構描述變更指令碼。  
  
 Usage: execute_schema_change.ps1 *server_name**db_name`schema_name`table_name*  
  
```sql  
# stop execution once an error occurs  
$ErrorActionPreference="Stop"  
  
if($args.Count -le 3)  
{  
   throw "Usage execute_schema_change.ps1 server_name db_name schema_name table_name"  
}  
  
$servername = $args[0]  
$database = $args[1]  
$schema = $args[2]  
$object = $args[3]  
  
[System.Reflection.Assembly]::LoadWithPartialName("Microsoft.SqlServer.SMO") | out-null  
  
$server =  New-Object ("Microsoft.SqlServer.Management.SMO.Server") ($servername)  
$database = $server.Databases[$database]  
$table = $database.Tables[$object, $schema]  
if($table.Count -eq 0)  
{  
   throw "Table or database not found"  
}  
  
$1 = Get-Item "1_copy_to_heap_$schema`_$object.sql"  
$2 = Get-Item "2_drop_procs_$schema`_$object.sql"  
$3 = Get-Item "3_drop_table_$schema`_$object.sql"  
$4 = Get-Item "4_create_table_$schema`_$object.sql"  
$5 = Get-Item "5_copy_from_heap_$schema`_$object.sql"  
$6 = Get-Item "6_create_procs_$schema`_$object.sql"  
$7 = Get-Item "7_drop_heap_$schema`_$object.sql"  
  
write-host "(1) Running SELECT INTO heap for table [$object] from 1_copy_to_heap_for_$schema`_$object.sql"  
$database.ExecuteNonQuery("$(Echo $1.OpenText().ReadToEnd())")  
write-host "--done--"  
write-host ""  
  
write-host "(2) Running DROP for procs schema-bound from [$object] 2_drop_procs_$schema`_$object.sql"  
$database.ExecuteNonQuery("$(Echo $2.OpenText().ReadToEnd())")  
write-host "--done--"  
write-host ""  
  
write-host "(3) Running DROP table for [$object] to 4_drop_table_$schema`_$object.sql"  
$database.ExecuteNonQuery("$(Echo $3.OpenText().ReadToEnd())")  
write-host "--done--"  
write-host ""  
  
write-host "(4) Running CREATE table and permissions for [$object] from 4_create_table_$schema`_$object.sql"  
$database.ExecuteNonQuery("$(Echo $4.OpenText().ReadToEnd())")  
write-host "--done--"  
write-host ""  
  
write-host "(5) Running INSERT INTO table from heap for [$object] and UPDATE STATISTICS from 5_copy_from_heap_$schema`_$object.sql"  
$database.ExecuteNonQuery("$(Echo $5.OpenText().ReadToEnd())")  
write-host "--done--"  
write-host ""  
  
write-host "(6) Running CREATE PROC and permissions for procedures schema-bound to [$object] from 6_create_procs_$schema`_$object.sql"  
$database.ExecuteNonQuery("$(Echo $6.OpenText().ReadToEnd())")  
write-host "--done--"  
write-host ""  
  
write-host "(7) Running DROP heap from 7_drop_heap_$schema`_$object.sql"  
$database.ExecuteNonQuery("$(Echo $7.OpenText().ReadToEnd())")  
write-host "--done--"  
write-host ""  
```  
  
## <a name="see-also"></a>另請參閱  
 [記憶體最佳化資料表](memory-optimized-tables.md)  
  
  
