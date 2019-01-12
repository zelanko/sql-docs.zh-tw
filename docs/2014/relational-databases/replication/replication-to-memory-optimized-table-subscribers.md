---
title: 複寫至記憶體最佳化資料表訂閱者 | Microsoft 文件
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
ms.assetid: 1a8e6bc7-433e-471d-b646-092dc80a2d1a
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0ee585f9773858848f213b3eeef6e995aedfb53f
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/09/2019
ms.locfileid: "54127768"
---
# <a name="replication-to-memory-optimized-table-subscribers"></a>複寫至記憶體最佳化資料表訂閱者
  做為異動複寫訂閱者的資料表 (不包括點對點異動複寫) 可以設定為記憶體最佳化資料表。 其他複寫組態與記憶體最佳化資料表不相容。  
  
## <a name="configuring-a-memory-optimized-table-as-a-subscriber"></a>將記憶體最佳化資料表設定為訂閱者  
 若要設定記憶體最佳化資料表做為訂閱者，請執行下列步驟。  
  
 **建立並啟用發行集**  
  
1.  建立發行集。  
  
2.  將發行項加入至發行集。 針對 `@upd_cmd` 參數，請使用 SCALL 或 SQL 慣例。  
  
    ```  
    EXEC sp_addarticle  
        @publication = N'Publication1',  
        @article = N'Mem_Table',  
        @source_owner = N'dbo',  
        @source_object = N'Mem_Table',  
        @type = N'logbased',  
        @description = null,  
        @creation_script = null,  
        @pre_creation_cmd = N'none',  
        @schema_option = 0x00000000080050DF,  
        @identityrangemanagementoption = N'manual',  
        @destination_table = N'Mem_Table',  
        @destination_owner = N'dbo',  
        @vertical_partition = N'false',  
        @ins_cmd = N'CALL sp_MSins_Mem_Table',  
        @del_cmd = N'CALL sp_MSdel_Mem_Table',  
        @upd_cmd = N'SCALL sp_MSupd_Mem_Table';  
    GO  
    ```  
  
 **產生快照集，並調整結構描述**  
  
1.  建立快照集工作，並產生快照集。  
  
    ```  
    EXEC sp_addpublication_snapshot @publication = N'Publication1', @frequency_type = 1;  
    EXEC sp_startpublication_snapshot @publication = N'Publication1';  
    ```  
  
2.  導覽到快照集資料夾。 預設位置是"C:\Program Files\Microsoft SQL Server\MSSQL12。\<執行個體 > \MSSQL\repldata\unc\XXX\YYYYMMDDHHMMSS\\"。  
  
3.  找出 **。SCH**檔案資料表，然後在 Management Studio 中開啟它。 變更資料表結構描述並更新預存程序，如下所述。  
  
     評估 IDX 檔案中定義的索引。 修改 `CREATE TABLE`，以指定必要的索引、條件約束、主索引鍵和記憶體最佳化語法。 對於記憶體最佳化資料表，索引資料行應該是 NOT NULL，而字元類型的索引資料行必須是 Unicode 並且使用 BIN2 定序。 請參閱以下範例：  
  
    ```  
    SET ANSI_PADDING ON;  
    GO  
  
    SET ANSI_NULLS ON;  
    GO  
  
    SET QUOTED_IDENTIFIER ON;  
    GO  
  
    CREATE TABLE [dbo].[Mem_Table]([c1] [int] NOT NULL,  
        [c2] [float] NOT NULL,  
        [c3] [decimal](10, 2) NOT NULL,  
        [c4] [nvarchar](5) COLLATE SQL_Latin1_General_CP850_BIN2 NOT NULL,  
        INDEX [hash_index_sample_memoryoptimizedtable_c2] HASH (c2) WITH (BUCKET_COUNT = 1024),  
        INDEX [index_sample_memoryoptimizedtable_c3] NONCLUSTERED ([c3]),  
        INDEX [nvarchar_index_sample_memoryoptimizedtable_c4] ([c4]),  
        CONSTRAINT [PK_sample_memoryoptimizedtable] PRIMARY KEY NONCLUSTERED ([c1])) WITH (MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_AND_DATA);  
    GO  
    ```  
  
4.  使用 SCALL 慣例做為 `@upd_cmd` 參數時，請移至結構描述 (.SCH) 檔案並變更 `create procedure [sp_MSupd_<SCHEMA><TABLE_NAME>]` 中的資料表更新陳述式，以移除主索引鍵資料行。  
  
     若要支援主索引鍵更新，請使用自訂更新預存程序取代主索引鍵更新陳述式，如下所述：  
  
    1.  選取遺漏的資料行值 (SCALL 僅對更新作業提供包含的資料行)。  
  
    2.  刪除現有記錄。  
  
    3.  插入新記錄並提供新值，包括新的主索引鍵。  
  
     原始更新程序如下所示：  
  
    ```  
    create procedure [sp_MSupd_Mem_Table]  
                   @c1 int = NULL,  
                   @c2 float = NULL,  
                   @c3 decimal(10,2) = NULL,  
                   @c4 nvarchar(5) = NULL,  
                   @pkc1 int = NULL,  
                   @bitmap binary(1)  
    as  
    begin    
    if (substring(@bitmap,1,1) & 1 = 1)  
    begin   
    update [dbo].[Mem_Table] set  
                   [c1] = case substring(@bitmap,1,1) & 1 when 1 then @c1 else [c1] end,  
                   [c2] = case substring(@bitmap,1,1) & 2 when 2 then @c2 else [c2] end,  
                   [c3] = case substring(@bitmap,1,1) & 4 when 4 then @c3 else [c3] end,  
                   [c4] = case substring(@bitmap,1,1) & 8 when 8 then @c4 else [c4] end  
    where [c1] = @pkc1  
    if @@rowcount = 0  
        if @@microsoftversion>0x07320000  
            exec sp_MSreplraiserror 20598  
    end    
    else  
    begin   
    update [dbo].[Mem_Table] set  
                   [c2] = case substring(@bitmap,1,1) & 2 when 2 then @c2 else [c2] end,  
                   [c3] = case substring(@bitmap,1,1) & 4 when 4 then @c3 else [c3] end,  
                   [c4] = case substring(@bitmap,1,1) & 8 when 8 then @c4 else [c4] end  
    where [c1] = @pkc1  
    if @@rowcount = 0  
        if @@microsoftversion>0x07320000  
            exec sp_MSreplraiserror 20598  
    end   
    end   
    go  
    ```  
  
     如果發行者的主索引鍵應永遠不更新， 請在更新程序中，將對這類資料行的更新設為註解，如下所示：  
  
    ```  
    create procedure [sp_MSupd_Mem_Table]  
                   @c1 int = NULL,  
                   @c2 float = NULL,  
                   @c3 decimal(10,2) = NULL,  
                   @c4 nvarchar(5) = NULL,  
                   @pkc1 int = NULL,  
                   @bitmap binary(1)  
    as  
    begin    
    if (substring(@bitmap,1,1) & 1 = 1)  
    begin   
    update [dbo].[Mem_Table] set  
    --             [c1] = case substring(@bitmap,1,1) & 1 when 1 then @c1 else [c1] end,  
                   [c2] = case substring(@bitmap,1,1) & 2 when 2 then @c2 else [c2] end,  
                   [c3] = case substring(@bitmap,1,1) & 4 when 4 then @c3 else [c3] end,  
                   [c4] = case substring(@bitmap,1,1) & 8 when 8 then @c4 else [c4] end  
    where [c1] = @pkc1  
    if @@rowcount = 0  
        if @@microsoftversion>0x07320000  
            exec sp_MSreplraiserror 20598  
    end    
    else  
    begin   
    update [dbo].[Mem_Table] set  
                   [c2] = case substring(@bitmap,1,1) & 2 when 2 then @c2 else [c2] end,  
                   [c3] = case substring(@bitmap,1,1) & 4 when 4 then @c3 else [c3] end,  
                   [c4] = case substring(@bitmap,1,1) & 8 when 8 then @c4 else [c4] end  
    where [c1] = @pkc1  
    if @@rowcount = 0  
        if @@microsoftversion>0x07320000  
            exec sp_MSreplraiserror 20598  
    end   
    end   
    go  
    ```  
  
     若要允許支援更新主索引鍵，請修改更新程序，如下所示  
  
    ```  
    create procedure [sp_MSupd_Mem_Table]  
                   @c1 int = NULL,  
                   @c2 float = NULL,  
                   @c3 decimal(10,2) = NULL,  
                   @c4 nvarchar(5) = NULL,  
                    @pkc1 int = NULL,  
                   @bitmap binary(1)  
    as  
    begin    
    if (substring(@bitmap,1,1) & 1 = 1)  
    begin   
    select  
                   @c1 = case substring(@bitmap,1,1) & 1 when 1 then @c1 else [c1] end,  
                   @c2 = case substring(@bitmap,1,1) & 2 when 2 then @c2 else [c2] end,  
                   @c3 = case substring(@bitmap,1,1) & 4 when 4 then @c3 else [c3] end,  
                   @c4 = case substring(@bitmap,1,1) & 8 when 8 then @c4 else [c4] end  
    from [dbo].[Mem_Table] where [c1] = @pkc1  
    if @@rowcount <> 0 begin  
            delete [dbo].[Mem_Table] where [c1] = @pkc1  
            if @@rowcount <> 0  
                   insert into [dbo].[Mem_Table]([c1],  
                           [c2],  
                           [c3],  
                           [c4]) values (  
                           @c1,  
                           @c2,  
                           @c3,  
                           @c4  
                   )   
    end  
    if @@rowcount = 0  
        if @@microsoftversion>0x07320000  
            exec sp_MSreplraiserror 20598  
    end    
    else  
    begin   
    update [dbo].[Mem_Table] set  
                   [c2] = case substring(@bitmap,1,1) & 2 when 2 then @c2 else [c2] end,  
                   [c3] = case substring(@bitmap,1,1) & 4 when 4 then @c3 else [c3] end,  
                   [c4] = case substring(@bitmap,1,1) & 8 when 8 then @c4 else [c4] end  
    where [c1] = @pkc1  
    if @@rowcount = 0  
        if @@microsoftversion>0x07320000  
            exec sp_MSreplraiserror 20598  
    end   
    end   
    go  
    ```  
  
5.  建立訂閱者資料庫**提升為快照隔離**選項，然後將預設定序設定為 Latin1_General_CS_AS_KS_WS，以防使用非 Unicode 字元資料類型。  
  
    ```  
    CREATE DATABASE [Sub]   
    CONTAINMENT = NONE   
    ON PRIMARY ( NAME = [Sub], FILENAME = [C:\Program Files\Microsoft SQL Server\MSSQL12\MSSQL\DATA\Sub.mdf]),   
    FILEGROUP [mem] CONTAINS MEMORY_OPTIMIZED_DATA ( NAME = [mem],   
    FILENAME = [C:\Program Files\Microsoft SQL Server\MSSQL12\MSSQL\DATA\Sub])  
    LOG ON ( NAME = [Sub_log], FILENAME = [C:\Program Files\Microsoft SQL Server\MSSQL12\MSSQL\DATA\Sub.ldf])  
    COLLATE Latin1_General_CS_AS_KS_WS;  
  
    ALTER DATABASE [Sub] SET MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT = ON;  
    GO  
    ```  
  
6.  將結構描述套用至訂閱者的資料庫，並儲存供日後使用的結構描述。  
  
7.  將發行者 (來源) 資料載入至訂閱者。 資料在發行者端應該不會變更，除非您加入訂閱。  您可以使用 BCP，如下所示：  
  
    ```  
    bcp Pub.dbo.Mem_Table out Mem_Table.bcp -S. -T -C1252 -n  
    bcp Sub.dbo.Mem_Table in Mem_Table.bcp -S. -T -C1252 -n  
    ```  
  
8.  將發行項重新設定為停用訂閱者端的結構描述變更：  
  
    ```  
    EXEC sp_changearticle  
        @publication = N'Publication1',  
        @article = N'Mem_Table',  
        @property = N'schema_option',  
        @value = 0,  
        @force_invalidate_snapshot = 1,  
        @force_reinit_subscription = 1;  
    GO  
    ```  
  
 **加入非同步訂閱**  
  
 加入 nosync 訂閱。  
  
```  
EXEC sp_addsubscription  
    @publication = N' Publication1',  
    @subscriber = @@ServerName,  
    @destination_db = N'Sub',  
    @subscription_type = N'Push',  
    @sync_type = N'replication support only',  
    @article = N'all',  
    @update_mode = N'read only',  
    @subscriber_type = 0;  
GO  
```  
  
 記憶體最佳化資料表現在應該會開始接收來自發行者的更新。  
  
## <a name="restrictions"></a>限制  
 僅支援單向異動複寫。 不支援點對點異動複寫。  
  
 無法發行記憶體最佳化資料表。  
  
 散發者端的複寫資料表無法設定為記憶體最佳化資料表。  
  
 合併式複寫無法包含記憶體最佳化資料表。  
  
 在訂閱者端，異動複寫中包含的資料表可以設定為記憶體最佳化資料表，但是訂閱者資料表必須符合記憶體最佳化資料表的需求。 需求的限制如下。  
  
-   若要在異動複寫訂閱者上建立記憶體最佳化資料表，必須手動修改用來建立記憶體最佳化資料表的快照集結構描述檔案。 如需詳細資訊，請參閱 <<c0> [ 修改結構描述檔案](#Schema)。  
  
-   複寫至訂閱者端記憶體最佳化資料表的資料表限制，會是記憶體最佳化資料表每一個資料列限制的 8060 個位元組。  
  
-   複寫至訂閱者端記憶體最佳化資料表的資料表限制，則為記憶體最佳化資料表中允許的資料類型。 如需詳細資訊，請參閱 < [Supported Data Types](../in-memory-oltp/supported-data-types-for-in-memory-oltp.md)。  
  
-   對於更新複寫至訂閱者端之記憶體最佳化資料表的資料表主索引鍵也有些限制。 如需詳細資訊，請參閱 <<c0> [ 將變更複寫至主索引鍵](#PrimaryKey)。  
  
-   記憶體最佳化資料表中不支援外部索引鍵、唯一條件約束、觸發程序、結構描述修改、ROWGUIDCOL、計算資料行、資料壓縮、別名資料類型、版本設定及鎖定。 如需詳細資訊，請參閱＜ [Transact-SQL Constructs Not Supported by In-Memory OLTP](../in-memory-oltp/transact-sql-constructs-not-supported-by-in-memory-oltp.md) ＞。  
  
##  <a name="Schema"></a> 修改結構描述檔案  
  
-   不支援叢集索引。 請將任何叢集索引變更為非叢集索引。  
  
-   索引之索引鍵中的所有資料行都必須指定為 `NOT NULL`。  
  
-   如果使用記憶體最佳化資料表選項 `DURABILITY = SCHEMA_AND_DATA` ，則資料表必須具有非叢集主索引鍵索引。  
  
-   ANSI_PADDING 必須為 ON。  
  
##  <a name="PrimaryKey"></a> 將變更複寫至主索引鍵  
 記憶體最佳化資料表的主索引鍵無法更新。 若要複寫訂閱者端的主索引鍵更新，請修改更新預存程序，將更新做為刪除和插入組傳遞。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server 複寫](sql-server-replication.md)  
  
  
