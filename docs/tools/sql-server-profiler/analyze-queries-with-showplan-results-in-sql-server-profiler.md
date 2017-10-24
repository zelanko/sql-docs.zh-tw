---
title: "使用在 SQL Server Profiler SHOWPLAN 結果分析查詢 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- events [SQL Server], Showplan
- Profiler [SQL Server Profiler], Showplan results
- SQL Server Profiler, Showplan results
ms.assetid: 6a2f7727-141c-4f59-8613-2e452bc78467
caps.latest.revision: 30
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: aecf422ca2289b2a417147eb402921bb8530d969
ms.openlocfilehash: 0f43310dfd52210d23bae3a34f22b52845a41706
ms.contentlocale: zh-tw
ms.lasthandoff: 10/24/2017

---
# <a name="analyze-queries-with-showplan-results-in-sql-server-profiler"></a>在 SQL Server Profiler 中使用 SHOWPLAN 結果分析查詢
  您可以將 Showplan 事件類別加入至追蹤定義中，讓 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 蒐集查詢計畫資訊並顯示在追蹤中。 您也可以從追蹤所收集的其他事件中擷取顯示計畫事件，並將這些顯示計畫事件儲存在個別的 XML 檔案中。  
  
 若要從追蹤中擷取顯示計畫事件，可以使用下列其中一個方式來進行：  
  
-   在追蹤組態時，使用 [事件擷取設定] 索引標籤。請注意，必須先選取 [事件選取範圍] 索引標籤上的其中一個 Showplan 事件，此索引標籤才會顯示。  
  
-   使用 [檔案] 功能表上的 [擷取 SQL Server 事件] 選項。  
  
-   您可以用滑鼠右鍵按一下個別事件，然後選擇 [擷取事件資料]，以擷取並儲存個別事件。  
  
## <a name="showplan-events"></a>顯示計畫事件  
 下表列出並說明顯示計畫追蹤事件。  
  
|事件名稱|描述|  
|----------------|-----------------|  
|**Performance statistics**|指出第一次快取已編譯顯示計畫的時間、其重新編譯的時間，以及從計畫快取中卸除的時間。 **TextData** 資料行中包含了 XML 格式的顯示計畫。 如需詳細資訊，請參閱 [Performance Statistics 事件類別](../../relational-databases/event-classes/performance-statistics-event-class.md)。|  
|**Showplan All**|所顯示的查詢計畫，含有已執行之 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式的完整編譯詳細資料。 例如，其中可能會顯示成本估計與資料行清單。 如需詳細資訊，請參閱 [Showplan All 事件類別](../../relational-databases/event-classes/showplan-all-event-class.md)。|  
|**Showplan All For Query Compile**|會在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]上編譯或重新編譯查詢時發生。 這是 **Showplan All** 事件的編譯時間對應項目。 **Showplan All** 在執行查詢時發生。 **Showplan All For Query Compile** 則在編譯查詢時發生。 如需詳細資訊，請參閱 [Showplan All for Query Compile 事件類別](../../relational-databases/event-classes/showplan-all-for-query-compile-event-class.md)。|  
|**Showplan Statistics Profile**|顯示含有執行中 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式之完整執行階段詳細資料的查詢計畫，包括從每個作業所傳遞的實際資料列數目。 如需詳細資訊，請參閱 [Showplan Statistics Profile 事件類別](../../relational-databases/event-classes/showplan-statistics-profile-event-class.md)。|  
|**Showplan Text**|以二進位資料顯示執行中 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式的查詢計畫樹狀目錄。 如需詳細資訊，請參閱 [Showplan Text 事件類別](../../relational-databases/event-classes/showplan-text-event-class.md)。|  
|**Showplan Text (Unencoded)**|以文字形式顯示執行中 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式的查詢計畫樹狀目錄。 此事件類別會顯示與 Showplan Text 相同的資訊，差別在於此事件類別顯示的是文字，而非二進位資料。 如需詳細資訊，請參閱 [Showplan Text &#40;Unencoded&#41; 事件類別](../../relational-databases/event-classes/showplan-text-unencoded-event-class.md)。|  
|**Showplan XML**|顯示的查詢計畫，含有在查詢最佳化期間收集到的完整資料。 只有在查詢計畫最佳化時，才會產生此事件。 如需詳細資訊，請參閱 [Showplan XML 事件類別](../../relational-databases/event-classes/showplan-xml-event-class.md)。|  
|**Showplan XML For Query Compile**|顯示查詢進行編譯時的查詢計畫。 如需詳細資訊，請參閱 [Showplan XML for Query Compile 事件類別](../../relational-databases/event-classes/showplan-xml-for-query-compile-event-class.md)。|  
|**Showplan XML Statistics Profile**|所顯示的查詢計畫，含有 XML 格式的完整執行時間詳細資料。 例如，此事件類別會擷取執行中 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式中，每個運算子所通過的資料列數。 如需詳細資訊，請參閱 [Showplan XML Statistics Profile 事件類別](../../relational-databases/event-classes/showplan-xml-statistics-profile-event-class.md)。|  
  
## <a name="see-also"></a>另請參閱  
 [Performance 事件類別目錄](../../relational-databases/event-classes/performance-event-category.md)  
  
  

