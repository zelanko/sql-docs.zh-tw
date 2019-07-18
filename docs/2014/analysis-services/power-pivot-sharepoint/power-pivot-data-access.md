---
title: PowerPivot 資料存取 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 83dc82da-91fb-4e47-91a8-0e0db67339b8
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 97f5d2045601f72c3536fbf2d4e469eb5eb20fbe
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66071246"
---
# <a name="powerpivot-data-access"></a>PowerPivot 資料存取
  本主題描述從發佈到 SharePoint 文件庫的 PowerPivot 活頁簿擷取資料的方法。  
  
 PowerPivot 資料會儲存在 Excel 活頁簿內。 連接字串是 SharePoint 網站上活頁簿的 URL。  
  
 PowerPivot 資料最常由包含它的活頁簿所使用 (當做樞紐分析表和樞紐分析圖背後的資料)。 此外，PowerPivot 資料也可當做外部資料來源使用，其中活頁簿、儀表板或報表會連接到 SharePoint 中的個別 Excel (.xlsx) 檔案，並且擷取資料以供後續使用。 通常使用 PowerPivot 資料的用戶端工具為 Excel、[!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]、其他 Reporting Services 報表和 PerformancePoint。  
  
 PowerPivot 增益集會在桌面上使用 AMO 與 ADOMD.NET 來建立、處理及查詢用戶端工作空間中的 PowerPivot 資料。  
  
 在 SharePoint 伺服器陣列上，Excel Services 會使用本機 MSOLAP OLE DB 提供者連接到 PowerPivot 資料。 此提供者會將連接要求傳送到伺服器陣列中的 PowerPivot for SharePoint 伺服器。 該伺服器會載入資料、執行查詢，然後傳回結果集。  
  
##  <a name="queryproc"></a> 在 SharePoint 中查詢 PowerPivot 資料  
 當您從 SharePoint 文件庫檢視 PowerPivot 活頁簿時，會在伺服器陣列中的 Analysis Services 伺服器執行個體上，個別偵測、擷取及處理活頁簿內的 PowerPivot 資料，同時 Excel Services 會轉譯展示層。 您可以在瀏覽器視窗或在具有 PowerPivot 增益集的 Excel 2010 桌面應用程式中，檢視已完全處理的活頁簿。  
  
 下圖顯示查詢處理的要求如何透過伺服陣列移動。 因為 PowerPivot 資料是 Excel 2010 活頁簿的一部分，所以對於查詢處理的要求會在使用者從 SharePoint 文件庫開啟 Excel 活頁簿時發生，並與包含 PowerPivot 資料的樞紐分析表或樞紐分析圖互動。  
  
 ![GMNI_DataProcReq](../media/gmni-dataprocreq.gif "GMNI_DataProcReq")  
  
 Excel Services 及 PowerPivot for SharePoint 元件會處理相同活頁簿 (.xlsx) 檔案的不同部分。 Excel Services 會偵測到 PowerPivot 資料，並要求從伺服陣列中的 PowerPivot 伺服器進行處理。 PowerPivot 伺服器會將要求配置到 [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)] 執行個體，這將會從內容文件庫的活頁簿中擷取資料並載入資料。 儲存在記憶體中的資料會合併至轉譯的活頁簿，並傳回給 Excel Web Access，以便在瀏覽器視窗中顯示。  
  
 並非在 PowerPivot 活頁簿中的所有資料都是由 PowerPivot for SharePoint 進行處理。 Excel Services 會處理工作表中的資料表與資料格資料。 只有與 PowerPivot 資料相反的樞紐分析表、樞紐分析圖和交叉分析篩選器，是由 PowerPivot for SharePoint 所處理。  
  
## <a name="see-also"></a>另請參閱  
 [連接到 Analysis Services](../instances/connect-to-analysis-services.md)   
 [表格式模型資料存取](../tabular-models/tabular-model-data-access.md)  
  
  
