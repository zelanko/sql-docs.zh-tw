---
title: "SQL Server 2016 版本支援的 Analysis Services 功能 | Microsoft Docs"
ms.custom: ""
ms.date: "09/02/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/data-mining"
  - "analysis-services/multidimensional-tabular"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: f09d7be1-bd63-43f8-b91c-bf19166b4457
caps.latest.revision: 4
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 3
---
# SQL Server 2016 版本支援的 Analysis Services 功能
本主題提供不同 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]版本所支援功能的詳細資料。  
  
 SQL Server Evaluation Edition 提供了 180 天的試用期。  
  
 如需最新版本資訊，請參閱 [SQL Server 2016 版本資訊](../sql-server/sql-server-2016-release-notes.md)。 如需新功能的最新資訊，請參閱 [Analysis Services 的新功能](../analysis-services/what-s-new-in-analysis-services.md)。
    
 **試用 SQL Server 2016！**    
    
 > [![從 Evaluation Center 下載](../analysis-services/media/download.png)](https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016) **[從 Evaluation Center 下載 SQL Server 2016](https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016)**    
    
> ![Azure 虛擬機器小型](../analysis-services/media/azure-virtual-machine-small.png) **[使用已安裝的 SQL Server 2016 加速虛擬機器](https://azure.microsoft.com/en-us/marketplace/partners/microsoft/sqlserver2016rtmenterprisewindowsserver2012r2/?wt.mc_id=sqL16_vm)**    
    
  
 如需 Evaluation 和 Developer Edition 所支援的功能，請參閱＜SQL Server Enterprise Edition＞。
  
 若要瀏覽 SQL Server 技術的資料表，請按一下其連結： 
 
 -  [Analysis Services](#SSAS)  
  
-   [BI 語意模型 (多維度)](#BIMD)  
  
-   [BI 語意模型 (表格式)](#BIT)  
  
-   [PowerPivot for SharePoint](#PPSP)  
  
-   [資料採礦](#DM)  
  
-   [商業智慧用戶端](#BIC)  

##  <a name="SSAS"></a> Analysis Services  
  
|功能|Enterprise|Standard|Web|Express with Advanced Services|Express with Tools|Express|開發人員|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|-------------|---------------|  
|可擴充共用資料庫|是||||||是|  
|備份/還原與附加/卸離資料庫|是|是|||||是|  
|同步處理資料庫|是||||||是|  
|AlwaysOn 容錯移轉叢集執行個體|是<br /><br /> 節點數目是作業系統最大值|是<br /><br /> 支援 2 個節點|||||是<br /><br /> 節點數目是作業系統最大值|  
|可程式性 (AMO、ADOMD.Net、OLEDB、XML/A、ASSL、TMSL)|是|是|||||是|  
  
##  <a name="BIMD"></a> BI 語意模型 (多維度)  
  
|功能|Enterprise|Standard|Web|Express with Advanced Services|Express with Tools|Express|開發人員|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|-------------|---------------|  
|局部加總量值|是|否 <sup>1</sup>|||||是|  
|階層|是|是|||||是|  
|KPI|是|是|||||是|  
|檢視方塊|是||||||是|  
|動作|是|是|||||是|  
|帳戶智慧|是|是|||||是|  
|時間智慧|是|是|||||是|  
|自訂積存|是|是|||||是|  
|回寫 Cube|是|是|||||是|  
|回寫維度|是||||||是|  
|回寫資料格|是|是|||||是|  
|鑽研|是|是|||||是|  
|進階階層類型 (父子式和不完全階層)|是|是|||||是|  
|進階維度 (參考維度、多對多維度)|是|是|||||是|  
|連結量值和維度|是|是  <sup>2</sup> |||||是|  
|翻譯|是|是|||||是|  
|Aggregations|是|是|||||是|  
|多個分割區|是|是，最多 3 個|||||是|  
|主動式快取|是||||||是|  
|自訂組件 (預存程序)|是|是|||||是|  
|MDX 查詢和指令碼|是|是|||||是|  
|DAX 查詢|是|是|||||是|  
|以角色為基礎的安全性模型|是|是|||||是|  
|維度和資料格層級安全性|是|是|||||是|  
|可擴充字串儲存體|是|是|||||是|  
|MOLAP、ROLAP 和 HOLAP 儲存體模型|是|是|||||是|  
|二進位和壓縮 XML 傳輸|是|是|||||是|  
|發送模式處理|是||||||是|  
|直接回寫|是||||||是|  
|量值運算式|是||||||是|  
  
 <sup>1</sup> LastChild 局部加總量值在 Standard Edition 中有受到支援，但是其他局部加總量值 (例如 None、FirstChild、FirstNonEmpty、LastNonEmpty、AverageOfChildren 和 ByAccount) 則不受支援。 所有的版本都支援加總量值 (例如 Sum、Count、Min、Max) 和非加總量值 (DistinctCount)。  
  <sup>2</sup> Standard Edition 支援同一個資料庫內的連結量值和維度，但不支援來自其他資料庫或執行個體的連結量值和維度。
   
##  <a name="BIT"></a> BI 語意模型 (表格式)  
  
|功能|Enterprise|Standard|Web|Express with Advanced Services|Express with Tools|Express|開發人員|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|-------------|---------------|  
|階層|是|是|||||是|  
|KPI|是|是|||||是|  
|檢視方塊|是||||||是|  
|翻譯|是|是|||||是|  
|DAX 計算、DAX 查詢、MDX 查詢|是|是|||||是|  
|資料列層級安全性|是|是|||||是|  
|多個分割區|是||||||是|  
|記憶體內部儲存模式|是|是|||||是|  
|DirectQuery 儲存模式|是||||||是|  
  
##  <a name="PPSP"></a> PowerPivot for SharePoint  
  
|功能|Enterprise|Standard|Web|Express with Advanced Services|Express with Tools|Express|開發人員|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|-------------|---------------|  
|以共用服務架構為基礎的 SharePoint 伺服器陣列整合|是||||||是|  
|使用方式報表|是||||||是|  
|健全狀況監視規則|是||||||是|  
|Power Pivot 圖庫|是||||||是|  
|Power Pivot 資料重新整理|是||||||是|  
|Power Pivot 資料摘要|是||||||是|  
  
##  <a name="DM"></a> 資料採礦  
  
|功能名稱|Enterprise|Standard|Web|Express with Advanced Services|Express with Tools|Express|開發人員|  
|------------------|----------------|--------------|---------|------------------------------------|------------------------|-------------|---------------|  
|標準演算法|是|是|||||是|  
|資料採礦工具 (精靈、編輯器、查詢產生器)|是|是|||||是|  
|交叉驗證|是||||||是|  
|已篩選的採礦結構資料子集的模型|是||||||是|  
|時間序列：ARTXP 和 ARIMA 方法之間的自訂混合|是||||||是|  
|時間序列：以新的資料預測|是||||||是|  
|無限制的並行 DM 查詢|是||||||是|  
|資料採礦演算法的進階組態與微調選項|是||||||是|  
|支援外掛程式演算法|是||||||是|  
|平行模型處理|是||||||是|  
|時間序列：跨序列預測|是||||||是|  
|無限制的關聯規則屬性|是||||||是|  
|順序預測|是||||||是|  
|貝氏機率、類神經網路和羅吉斯迴歸的多個預測目標|是||||||是|  
  
##  <a name="BIC"></a> 商業智慧用戶端  
 您可以透過 Microsoft 下載中心取得下列軟體用戶端應用程式，這些應用程式是提供來協助您建立可在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體上執行的商業智慧文件。 當您在伺服器環境中裝載這些文件時，請使用支援該文件類型的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 版本。 下表將識別哪些 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 版本包含裝載在這些用戶端應用程式中建立之文件所需的伺服器功能。  
  
|工具名稱|Enterprise|Standard|Web|Express with Advanced Services|Express with Tools|Express|開發人員|  
|---------------|----------------|--------------|---------|------------------------------------|------------------------|-------------|---------------|  
|適用於 Excel 及 Visio 2010 的資料採礦增益集 (.xlsx、.vsdx)|是|是|||||是|  
|[!INCLUDE[ssGeminiClient](../includes/ssgeminiclient-md.md)] 2010 和 2013 (.xlsx)|是||||||是|  
|[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] [!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)] (.xlsx)|是||||||是|  
  
> [!NOTE]  
>  1.  [!INCLUDE[ssGeminiClient](../includes/ssgeminiclient-md.md)] 是使用資料模型建立活頁簿的 Excel 增益集。  [!INCLUDE[ssGeminiClient](../includes/ssgeminiclient-md.md)] 不依賴 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]，但需要 [!INCLUDE[ssGeminiShort](../includes/ssgeminishort-md.md)] 以共用及協同作業 Excel 活頁簿和 SharePoint 的資料模型。 這項功能附屬於 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Enterprise Edition。  
>   
>      Excel 2016 內建有 Power Pivot 功能，所以您不再需要 Power Pivot 增益集。  
> 2.  上表識別啟用這些用戶端工具所需的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 版本；不過，這些工具可以存取任何 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 版本上裝載的資料。  
  
 ## 另請參閱  
 [SQL Server 2016 版本支援的功能](Features%20Supported%20by%20the%20Editions%20of%20SQL%20Server%202016.md)  
 [SQL Server 2016 的產品規格](../Topic/Product%20Specifications%20for%20SQL%20Server%202016.md)   
 [SQL Server 2016 安裝](../database-engine/install-windows/installation-for-sql-server-2016.md)  

