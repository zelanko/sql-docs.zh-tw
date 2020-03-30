---
title: 將收集項新增至收集組 (T-SQL)
ms.custom: seo-lt-2019
ms.date: 03/07/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- collection items [SQL Server]
- collection sets [SQL Server], adding items
ms.assetid: 9fe6454e-8c0e-4b50-937b-d9871b20fd13
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 8b6a17bf6732221787bda5e34d42b01046b3f828
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "74055583"
---
# <a name="add-a-collection-item-to-a-collection-set-transact-sql"></a>將收集項加入收集組 (Transact-SQL)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  您可以使用資料收集器所提供的預存程序，將收集項加入到現有的收集組中。  
  
 請在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中使用查詢編輯器來完成以下步驟。  
  
### <a name="add-a-collection-item-to-a-collection-set"></a>將收集項加入收集組  
  
1.  執行 **sp_syscollector_stop_collection_set** 預存程序，停止您想要加入此項目的收集組。 例如，若要停止名為 "Test Collection Set" 的收集組，請執行下列陳述式：  
  
    ```sql  
    USE msdb  
    DECLARE @csid int  
    SELECT @csid = collection_set_id  
    FROM syscollector_collection_sets  
    WHERE name = 'Test Collection Set'  
    SELECT @csid  
    EXEC dbo.sp_syscollector_stop_collection_set @collection_set_id = @csid  
    ```  
  
    > [!NOTE]  
    >  您也可以使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中的 [物件總管] 來停止收集組。 如需詳細資訊，請參閱 [啟動或停止收集組](../../relational-databases/data-collection/start-or-stop-a-collection-set.md)。  
  
2.  宣告您想要加入收集項的收集組。 下列程式碼會提供如何宣告收集組識別碼的範例。  
  
    ```sql  
    DECLARE @collection_set_id_1 int  
    SELECT @collection_set_id_1 = collection_set_id FROM [msdb].[dbo].[syscollector_collection_sets]  
    WHERE name = N'Test Collection Set'; -- name of collection set  
    ```  
  
3.  宣告收集器型別。 下列程式碼會提供如何宣告一般 T-SQL 查詢收集器型別的範例。  
  
    ```sql  
    DECLARE @collector_type_uid_1 uniqueidentifier  
    SELECT @collector_type_uid_1 = collector_type_uid FROM [msdb].[dbo].[syscollector_collector_types]   
       WHERE name = N'Generic T-SQL Query Collector Type';  
    ```  
  
     您可以執行下列程式碼來取得已安裝的收集器型別清單：  
  
    ```sql  
    USE msdb  
    SELECT * from syscollector_collector_types  
    GO  
    ```  
  
4.  執行 **sp_syscollector_create_collection_item** 預存程序來建立收集項。 您必須宣告收集項的結構描述，好讓它對應到所需收集器型別的必要結構描述。 下列範例會使用一般 T-SQL 查詢輸入結構描述。  
  
    ```sql  
    DECLARE @collection_item_id int;  
    EXEC [msdb].[dbo].[sp_syscollector_create_collection_item]   
    @name=N'OS Wait Stats', --name of collection item  
    @parameters=N'  
    <ns:TSQLQueryCollector xmlns:ns="DataCollectorType">  
     <Query>  
      <Value>select * from sys.dm_os_wait_stats</Value>  
      <OutputTable>os_wait_stats</OutputTable>  
    </Query>  
    </ns:TSQLQueryCollector>',  
    @collection_item_id = @collection_item_id OUTPUT,  
    @frequency = 60,  
    @collection_set_id = @collection_set_id_1, --- Provides the collection set ID number  
    @collector_type_uid = @collector_type_uid_1 -- Provides the collector type UID  
    SELECT @collection_item_id     
    ```  
  
5.  在啟動更新的收集組之前，請執行下列查詢來確認新的收集項確實已經建立：  
  
    ```xaml  
    USE msdb  
    SELECT * from syscollector_collection_sets  
    SELECT * from syscollector_collection_items  
    GO  
    ```  
  
     收集組及其收集項都會顯示在 [結果]  索引標籤上。  
  
## <a name="see-also"></a>另請參閱  
 [建立使用一般 T-SQL 查詢收集器型別的自訂收集組 &#40;Transact-SQL&#41;](../../relational-databases/data-collection/create-custom-collection-set-generic-t-sql-query-collector-type.md)   
 [資料收集器預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)  
  
  
