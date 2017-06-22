---
title: "指定合併發行項的處理順序 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- articles [SQL Server replication], processing order
- merge replication [SQL Server replication], article processing order
ms.assetid: d151e2c5-cf50-4cb3-a829-8f32455dbd66
caps.latest.revision: 34
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 8682c27e9d94410f8ffc902d2c03af491ec758ba
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="specify-the-processing-order-of-merge-articles"></a>指定合併發行項的處理順序
  從 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]開始，可以覆寫合併式發行集之發行項處理的預設順序。 這非常有用，例如，如果您透過觸發程序定義參考完整性，並且那些觸發程序必須以特定順序引發。  
  
 **若要指定發行項處理順序**  
  
-   複寫 Transact-SQL 程式設計：[指定合併資料表發行項的處理順序 &#40;複寫 Transact-SQL 程式設計&#41;](../../../relational-databases/replication/publish/specify-the-processing-order-of-merge-table-articles.md)  
  
## <a name="how-processing-order-is-determined"></a>如何確定處理順序  
 在合併同步處理期間，依預設，發行項將按物件間相依性所需的順序處理，包括在基底資料表上定義的宣告式參考完整性 (DRI) 條件約束。 處理包括列舉對資料表所作的變更，然後套用這些變更。 如果沒有 DRI，但資料表發行項之間存在聯結篩選或邏輯記錄，發行項將以篩選和邏輯記錄所需的順序處理。 透過 DRI、聯結篩選、邏輯記錄或其他相依性與任何其他發行項無關的發行項，按照 [sysmergearticles &#40;Transact-SQL&#41;](../../../relational-databases/system-tables/sysmergearticles-transact-sql.md) 系統資料表中的發行項暱稱處理。  
  
 假設發行集包含在 **SalesOrderHeader** 資料表中含主索引鍵資料行 **SalesOrderID** ，並且在 **SalesOrderDetail** 資料表中含相應外部索引鍵資料行 **SalesOrderID** 的資料表 **SalesOrderHeader** 與 **SalesOrderDetail** 。 在同步處理期間，合併式複寫透過在 **SalesOrderDetail** 中插入相關資料列之前於 **SalesOrderHeader**中插入任何新資料列，以防止外部索引鍵違規。 同樣地，在從 **SalesOrderHeader** 中刪除關聯資料列之前，可從 **SalesOrderDetail**決定中刪除資料列。  
  
 但是，在某些應用程式中，參照完整性透過資料庫觸發程序強化，或使用應用程式層級而不是透過 DRI 來強化。 以上所述的指定發行集 (而不是 DRI)， **SalesOrderDetail** 資料表具有插入觸發程序，可確保在允許插入前於 **SalesOrderHeader** 資料表中存在關聯資料列。 **SalesOrderHeader** 具有刪除觸發程序，可確保在允許刪除前於 **SalesOrderDetail** 中沒有關聯資料列。 合併式複寫在確定發行項處理順序時，不會考慮觸發程序，因為它無法在引發觸發程序前確定其結果。 同樣地，複寫不會考慮在應用程式層級上定義的條件約束。  
  
 當透過觸發程序或在應用程式層級上維護參考完整性時，您應該指定處理發行項的順序。 在使用觸發程序的範例中，您應該指定在處理 **SalesOrderDetail** 之前處理 **SalesOrderHeader**資料表，因為發行項排序是以插入順序為基礎的。 合併式複寫將自動反轉刪除順序。 沒有發行項排序，合併式複寫也不會失敗，因為如果條件約束出現違規，「合併代理程式」會繼續處理發行項；然後重試在處理其他發行項後失敗的任何作業。 只需指定發行項順序即可避免重試以及與其相關的其他處理。 如果您指定了錯誤順序 (例如，導致在標頭記錄前處理詳細記錄的順序)，合併式複寫將會重試處理，直到它成功。  
  
## <a name="see-also"></a>另請參閱  
 [合併式複寫的發行項選項](../../../relational-databases/replication/merge/article-options-for-merge-replication.md)   
 [使用邏輯記錄分組相關資料列的變更](../../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md)   
 [Join Filters](../../../relational-databases/replication/merge/join-filters.md)  
  
  
