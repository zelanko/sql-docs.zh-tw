---
title: "SQL Server 2016 中 Analysis Services 功能的行為變更 | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 92ebd5cb-afb6-4b62-968f-39f5574a452b
caps.latest.revision: 17
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 17
---
# SQL Server 2016 中 Analysis Services 功能的行為變更
  *「行為變更」* (behavior change) 會影響功能在目前版本中，與舊版 SQL Server 相較之下的運作或互動方式。  
  
 預設值修訂、完成升級或還原功能所需的手動組態或現有功能的新實作，全部都是產品中的行為變更範例。  
  
 這裡會列出本版本中的已變更但不會中斷現有模型或程式碼後置升級的功能行為。  
  
> [!NOTE]  
>  與 *「行為變更」*(behavior change) 相反， *「中斷變更」* (breaking change) 會防止在升級伺服器、用戶端工具或模型之後執行與 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 整合的資料模型或應用程式。 若要查看清單，請瀏覽 [SQL Server 2016 中 Analysis Services 功能的重大變更](../analysis-services/breaking-changes-to-analysis-services-features-in-sql-server-2016.md)。  
  
## SharePoint 模式的 Analysis Services  
 不再需要執行 [Power Pivot 組態精靈] 作為後續安裝工作。 這適用於從目前 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 版本的 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 中載入模型的所有支援 SharePoint 版本。  
  
## 表格式模型的 DirectQuery 模式  
 *DirectQuery* 是表格式模型的資料存取模式，其中，會對後端關聯式資料庫執行查詢執行，以即時擷取結果集。 這通常用於無法放入記憶體的極大型資料集，或是資料是暫時性的而且您想要有表格式模型的查詢中所傳回的最新資料時。  
  
 DirectQuery 已是最後數個版本的資料存取模式。 在 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]中，已稍微修訂實作，並假設表格式模型為相容性層級 1200。 DirectQuery 的限制比以前少。 它也有不同的資料庫屬性。  
  
 如果您在現有表格式模型中使用 DirectQuery，則可以保留模型的目前相容性層級 1100 或 1103，並繼續使用 DirectQuery 作為這些層級的實作。 或者，您可以升級為 1200 以利用對這版 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]中 DirectQuery 進行的增強。  
  
 DirectQuery 模型無法進行就地升級，因為舊版相容性層級的設定在新版 1200 相容性層級中沒有確切對應項目。 如果您的現有表格式模型是以 DirectQuery 模式執行，則應該在 SQL Server Data Tools 中開啟模型、關閉 DirectQuery、將 [相容性層級]  屬性設定為 1200，然後重新設定針對表格式 1200 模型所定義的 DirectQuery 屬性。 如需詳細資訊，請參閱 [DirectQuery 模式 &#40;SSAS 表格式&#41;](../analysis-services/tabular-models/directquery-mode-ssas-tabular.md)。  
  
## 請參閱＜  
 [回溯相容性_已刪除](../Topic/Backward%20Compatibility_deleted.md)   
 [SQL Server 2016 中 Analysis Services 功能的重大變更](../analysis-services/breaking-changes-to-analysis-services-features-in-sql-server-2016.md)   
 [Analysis Services 中表格式模型的相容性層級](../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)   
 [下載 SQL Server Data Tools](https://msdn.microsoft.com/en-us/library/mt204009.aspx)  
  
  