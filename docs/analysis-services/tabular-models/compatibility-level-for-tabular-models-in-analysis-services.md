---
title: "Analysis Services 中表格式模型的相容性層級 | Microsoft Docs"
ms.custom: ""
ms.date: "03/02/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.asvs.bidtoolset.versioncompat.f1"
ms.assetid: 8943d78d-4a73-4be8-ad14-3d428f5abd06
caps.latest.revision: 27
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 27
---
# Analysis Services 中表格式模型的相容性層級
  模型或資料庫的「相容性層級」是指 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 引擎中一組特定版本的行為。 您可以在任何支援的相容性層級建立模型，以取得特定版本的行為。 例如，根據相容性層級指派，DirectQuery 和表格式物件中繼資料會有不同的實作。  
  
 **SQL Server 2016 RTM (1200)** (或簡稱 1200 相容性層級) 是 SQL Server 2016 的新功能，僅適用於表格式模型。  在 1200 相容性層級的表格式模型將只會在 [!INCLUDE[ssASCurrent](../../includes/ssascurrent-md.md)] 表格式執行個體上執行。  
  
 若要建立或升級表格式模型，請使用 SQL Server Data Tools (SSDT)，並在建立專案時設定**相容性層級**屬性，或在專案建立之後於 **model.bim** 檔案上設定該屬性。  
  
> [!NOTE]  
>  多維度模型會根據相容性層級來遵循獨立的版本路徑。 若數字恰巧相同 (在本例中為 1103)，純屬巧合。 如需詳細資訊，請參閱[多維度資料庫的相容性層級 &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/compatibility-level-of-a-multidimensional-database-analysis-services.md)。  
  
## 表格式模型資料庫支援的相容性層級  
 Analysis Services 支援下列相容性層級 (適用於模型和資料庫)。  用來建立模型的工具版本會決定是否有較高的相容性層級可供使用。  
  
||||  
|-|-|-|  
|相容性層級|伺服器版本|模型化工具版本|  
|1200|只可在 SQL Server 2016 執行個體上執行|[僅限 SQL Server Data Tools for Visual Studio 2015](http://go.microsoft.com/fwlink/?LinkID=690931) <sup>1</sup><br /><br /> [What's New in Analysis Services](../../analysis-services/what-s-new-in-analysis-services.md) 說明在此層級提供的功能。|  
|1103|SQL Server 2016<br /><br /> SQL Server 2014<br /><br /> SQL Server 2012 SP1|[Visual Studio 2015 的 SQL Server Data Tools](http://go.microsoft.com/fwlink/?LinkID=690931) <sup>2</sup><br /><br /> [SQL Server Data Tools - Business Intelligence (Visual Studio 2013)](https://www.microsoft.com/en-us/download/details.aspx?id=42313)<br /><br /> [SQL Server Data Tools - Business Intelligence (Visual Studio 2012)](http://www.microsoft.com/en-us/download/details.aspx?id=36843)|  
|1100|SQL Server 2016<br /><br /> SQL Server 2014<br /><br /> SQL Server 2012 SP1<br /><br /> SQL Server 2012|[Visual Studio 2015 的 SQL Server Data Tools](http://go.microsoft.com/fwlink/?LinkID=690931) <sup>1</sup><br /><br /> [SQL Server Data Tools - Business Intelligence (Visual Studio 2013)](https://www.microsoft.com/en-us/download/details.aspx?id=42313)<br /><br /> [SQL Server Data Tools - Business Intelligence (Visual Studio 2012)](http://www.microsoft.com/en-us/download/details.aspx?id=36843)<br /><br /> Business Intelligence Development Studio (在 Visual Studio 2010 介面中執行並透過 SQL Server 安裝程式安裝)|  
  
 <sup>1</sup> 您可以使用 SQL Server Data Tools for Visual Studio 2015，將 1100 或 1103 表格式模型部署到舊版的 Analysis Services。  
  
 <sup>2</sup> 相容性層級 1100、1103 和 1200 全都是 SQL Server Data Tools for Visual Studio 2015 中有效的表格式模型專案，但您只能在 Analysis Services 的 SQL Server 2016 執行個體上部署和執行 1200 模型。  
  
## 在 SSDT 中建立或升級表格式時設定相容性層級  
 在 SQL Server Data Tools (SSDT) 中建立新的表格式模型專案時，您可以在 [新表格式專案選項] 對話方塊中指定相容性層級：  
  
 ![ssas_tabularproject_compat1200](../../analysis-services/tabular-models/media/ssas-tabularproject-compat1200.jpg "ssas_tabularproject_compat1200")  
  
 您也可以透過選取 **[不要再顯示此訊息]** 選項指定預設相容性層級。 所有後續專案都將使用您指定的相容性層級。 您可以在 SSDT 的 [工具] > [選項] 中變更預設相容性層級。  
  
 若要升級表格式模型專案，可將模型 [屬性] 視窗中的 [相容性層級] 屬性設定為 [SQL Server 2016 RTM (1200)]。  如需相關資訊，請參閱 [Upgrade Analysis Services](../../database-engine/install-windows/upgrade-analysis-services.md) 。  
  
> [!NOTE]  
>  建立表格式模型的方法之一是，將匯入的 Power Pivot 活頁簿當作它的基礎。 根據預設，Power BI Desktop 會在 1200 相容性層級自動建立表格式模型。 不過，較早版本的 Power Pivot 活頁簿可能是在 1100 層級。 使用舊版活頁簿時，請記得要變更 [相容性層級]  以進行升級。  
  
## 在 SSMS 中檢查表資料庫的相容性層級  
 在 SSMS 中，以滑鼠右鍵按一下資料庫名稱 > [屬性] > [相容性層級] 屬性。  
  
## 在 SSMS 中檢查伺服器支援的相容性層級  
 在 SSMS 中，以滑鼠右鍵按一下伺服器名稱 > [屬性] > [支援的相容性層級]。  
  
 此屬性會指定將在伺服器上執行之資料庫的最高相容性層級。  支援的相容性層級是唯讀且無法變更。  
  
## 請參閱＜  
 [多維度資料庫的相容性層級 &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/compatibility-level-of-a-multidimensional-database-analysis-services.md)   
 [Analysis Services 的新功能](../../analysis-services/what-s-new-in-analysis-services.md)   
 [從 Power Pivot 匯入 &#40;SSAS 表格式&#41;](../../analysis-services/tabular-models/import-from-power-pivot-ssas-tabular.md)   
 [建立新的表格式模型專案 &#40;Analysis Services&#41;](../../analysis-services/tabular-models/create-a-new-tabular-model-project-analysis-services.md)  
  
  