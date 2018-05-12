---
title: Analysis Services 的 SQL Server 2016 版本支援的功能 |Microsoft 文件
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 19618fc0311de28184e3a95c5e57e423d121f085
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="analysis-services-features-supported-by-sql-server-editions"></a>SQL Server 版本所支援的 analysis Services 功能
[!INCLUDE[ssas-appliesto-sql2016-later](../includes/ssas-appliesto-sql2016-later.md)]

本主題提供 SQL Server 2016 Analysis Services 不同版本所支援功能的詳細資料。 如需 Evaluation 和 Developer edition 所支援的功能，請參閱 Enterprise edition。

## <a name="analysis-services-servers"></a>Analysis Services （伺服器）
  
|功能|Enterprise|Standard|Web|Express with Advanced Services|Express with Tools|Express|開發人員|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|-------------|---------------|  
|可擴充共用資料庫|是||||||是|  
|備份/還原與附加/卸離資料庫|是|是|||||是|  
|同步處理資料庫|是||||||是|  
|AlwaysOn 容錯移轉叢集執行個體|是<br /><br /> 節點數目是作業系統最大值|是<br /><br /> 支援 2 個節點|||||是<br /><br /> 節點數目是作業系統最大值|  
|可程式性 (AMO、ADOMD.Net、OLEDB、XML/A、ASSL、TMSL)|是|是|||||是|  
  
## <a name="tabular-models"></a>表格式模型 
  
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

## <a name="multidimensional-models"></a>多維度模型 
  
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
  <sup>2</sup> standard edition 支援連結的量值和維度，在相同的資料庫，而不是從其他資料庫或執行個體。
  
## <a name="power-pivot-for-sharepoint"></a>PowerPivot for SharePoint  
  
|功能|Enterprise|Standard|Web|Express with Advanced Services|Express with Tools|Express|開發人員|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|-------------|---------------|  
|以共用服務架構為基礎的 SharePoint 伺服器陣列整合|是||||||是|  
|使用方式報表|是||||||是|  
|健全狀況監視規則|是||||||是|  
|Power Pivot 圖庫|是||||||是|  
|Power Pivot 資料重新整理|是||||||是|  
|Power Pivot 資料摘要|是||||||是|  
  
## <a name="data-mining"></a>資料採礦  
  
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
  
 ## <a name="see-also"></a>另請參閱  
 [SQL Server 2016 的產品規格](http://msdn.microsoft.com/library/6445fd53-6844-4170-a86b-7fe76a9f64cb)   
 [SQL Server 安裝](../database-engine/install-windows/installation-for-sql-server-2016.md)  


