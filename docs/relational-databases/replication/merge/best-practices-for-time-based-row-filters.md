---
title: "以時間為基礎之資料列篩選的最佳做法 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: best practices
ms.assetid: 773c5c62-fd44-44ab-9c6b-4257dbf8ffdb
caps.latest.revision: "15"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ecfd4a72f00c5b8199f7db64ec0c9175c2487e7e
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/18/2018
---
# <a name="best-practices-for-time-based-row-filters"></a>以時間為基礎之資料列篩選的最佳做法
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] 應用程式使用者通常需要來自資料表中以時間為基礎的資料子集。 例如，業務員可能需要上週的訂單資料，或事件計劃者可能需要未來一週的事件資料。 許多狀況下，應用程式會使用包含 **GETDATE()** 函數的查詢來達成這個目的。 請考量下列資料列篩選陳述式：  
  
```  
WHERE SalesPersonID = CONVERT(INT,HOST_NAME()) AND OrderDate >= (GETDATE()-6)  
```  
  
 使用這種類型的篩選時，通常假設合併代理程式執行時一律會發生兩件事：滿足這個篩選的資料列會複寫至訂閱者，以及不再滿足這個篩選的資料列會從訂閱者端清除 (如需使用 **HOST_NAME()** 篩選的詳細資訊，請參閱[參數化資料列篩選](../../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)。然而，不論您為資料所定義的資料列篩選為何，合併式複寫只能複寫和清除自上次同步處理後已變更的資料。  
  
 若要合併式複寫處理資料列，資料列中的資料必須滿足資料列篩選，並且自上次同步處理後必須已變更。 在 **SalesOrderHeader** 資料表的案例中， **OrderDate** 是在插入資料列時所輸入的。 資料列會如預期複寫至訂閱者，因為插入動作是資料變更。 然而，如果訂閱者端有不再滿足篩選的資料列 (超過七天以上的訂單資料列)，除非這些資料列因其他原因而更新，否則不會從訂閱者端移除。  
  
 事件計劃者的案例更進一步強調這種篩選類型的問題。 請考量 **Events** 資料表的下列篩選：  
  
```  
WHERE EventCoordID = CONVERT(INT,HOST_NAME()) AND EventDate <= (GETDATE()+6)  
```  
  
 對於包含事件的資料表，可能在事件日期前提早進行插入動作。 如果提前在一個月前進行未來一週事件的插入動作，並且資料列沒有因為其他原因而更新，即使該資料列滿足資料列篩選，也不會複寫至訂閱者。  
  
 此外，視發行集的設定方式而定，合併式複寫會在不同時間評估篩選：  
  
-   如果發行集使用預先計算的資料分割 (預設值)，篩選會在插入或更新資料列時進行評估。  
  
-   如果發行集沒有使用預先計算的資料分割，篩選會在執行 [合併代理程式] 時進行評估。  
  
 如需預先計算之資料分割的詳細資訊，請參閱[使用預先計算的資料分割最佳化參數化篩選效能](../../../relational-databases/replication/merge/parameterized-filters-optimize-for-precomputed-partitions.md)。 評估篩選的時間會影響哪些資料會滿足篩選。 例如，如果發行集使用預先計算的資料分割，並且您每兩天會同步處理資料一次，業務員的資料子集可能會包含比預期早兩天的資料列。  
  
## <a name="recommendations-for-using-time-based-row-filters"></a>以時間為基礎的資料列篩選使用建議  
 下列方法為以時間為基礎的篩選提供了完善直接的作法：  
  
-   將資料行加入至 **bit**資料類型的資料表。 這個資料行是用來指出資料列是否應複寫。  
  
-   使用會參考新資料行 (而不是以時間為基礎的資料行) 的資料列篩選。  
  
-   建立 SQL Server Agent 作業 (或透過另一個機制排程的作業)，這個作業會在合併代理程式已排程執行之前更新資料行。  
  
 這個作法針對使用 **GETDATE()** 或另一個以時間為基礎之方法的缺點，可避免必須決定何時評估資料分割篩選的問題。 請考量 **Events** 資料表的下列範例：  
  
|**EventID**|**EventName**|**EventCoordID**|**EventDate**|**複寫**|  
|-----------------|-------------------|----------------------|-------------------|-------------------|  
|@shouldalert|Reception|112|2006-10-04|@shouldalert|  
|2|Dinner|112|2006-10-10|0|  
|3|Party|112|2006-10-11|0|  
|4|Wedding|112|2006-10-12|0|  
  
 這個資料表的資料列篩選可能如下：  
  
```  
WHERE EventCoordID = CONVERT(INT,HOST_NAME()) AND Replicate = 1  
```  
  
 SQL Server Agent 作業可在每次合併代理程式執行之前執行 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 陳述式，如下：  
  
```  
UPDATE Events SET Replicate = 0 WHERE Replicate = 1  
GO  
UPDATE Events SET Replicate = 1 WHERE EventDate <= GETDATE()+6  
GO  
```  
  
 第一行會將 **Replicate** 資料行重設為 **0**，而第二行則會針對接下來七天發生的事件將資料行設為 **1** 。 如果在 10/07/2006 執行這個 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 陳述式，資料表會更新成：  
  
|**EventID**|**EventName**|**EventCoordID**|**EventDate**|**複寫**|  
|-----------------|-------------------|----------------------|-------------------|-------------------|  
|@shouldalert|Reception|112|2006-10-04|0|  
|2|Dinner|112|2006-10-10|@shouldalert|  
|3|Party|112|2006-10-11|@shouldalert|  
|4|Wedding|112|2006-10-12|@shouldalert|  
  
 下一週的事件現在會標幟為複寫準備就緒。 下次合併代理程式針對事件協調者 112 所使用的訂閱而執行時，資料列 2、3 及 4 將會下載至訂閱者，並且資料列 1 將會從訂閱者移除。  
  
## <a name="see-also"></a>另請參閱  
 [GETDATE &#40;Transact-SQL&#41;](../../../t-sql/functions/getdate-transact-sql.md)   
 [實作作業](http://msdn.microsoft.com/library/69e06724-25c7-4fb3-8a5b-3d4596f21756)   
 [Parameterized Row Filters](../../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)  
  
  
