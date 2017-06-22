---
title: "部署資料處理延伸模組 |Microsoft 文件"
ms.custom: 
ms.date: 03/18/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- data processing extensions [Reporting Services], deploying
- Extension element
- deploying [Reporting Services], extensions
ms.assetid: e5c0b5a9-1386-47cb-aade-96653ecfaa54
caps.latest.revision: 34
author: sabotta
ms.author: carlasab
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: d312cdf2c5588c8dc12ff000fe4163d7f562ea7f
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="deploying-a-data-processing-extension"></a>部署資料處理延伸模組
  一旦您所撰寫，並編譯您[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]成資料處理延伸模組[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]程式庫，您需要使其可供報表伺服器和報表設計師。 完成此項動作很簡單，只要將伸模組複製到適當的目錄，並將項目加入適當的 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 組態檔即可。  
  
## <a name="configuration-file-extension-element"></a>組態檔延伸模組元素  
 您將部署到報表伺服器或報表設計師中的資料處理延伸模組必須輸入為**延伸**的組態檔中的項目。 這些檔案在報表伺服器中為 RSReportServer.config，在報表設計師中為 RSReportDesigner.config。  
  
 下表描述的屬性**延伸**資料處理延伸模組項目。  
  
|Attribute|說明|  
|---------------|-----------------|  
|**名稱**|例如，就延伸模組的維一名稱而言，"SQL" 為 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料處理延伸模組，或者 "OLEDB" 為 OLE DB 資料處理延伸模組。 **Name** 屬性的最大長度為 255 個字元。 該名稱在組態檔之 **Extension** 元素的所有元素中，必須是唯一的。|  
|**型別**|以逗號分隔的清單，包括完整的命名空間以及組件的名稱。|  
|**Visible**|值為**false**表示資料處理延伸模組不應該顯示在使用者介面中。 如果沒有包括屬性，預設值是 **true**。|  
  
 如需有關 RSReportServer.config 或 RSReportDesigner.config 檔案的詳細資訊，請參閱[Reporting Services 組態檔](../../../reporting-services/report-server/reporting-services-configuration-files.md)。  
  
## <a name="in-this-section"></a>本節內容  
  
|主題|Description|  
|-----------|-----------------|  
|[如何： 將資料處理延伸模組部署到報表伺服器](../../../reporting-services/extensions/data-processing/deploying-a-data-processing-extension-to-a-report-server.md)|描述如何將資料處理延伸模組部署到報表伺服器。|  
|[如何： 將資料處理延伸模組部署到報表設計師](../../../reporting-services/extensions/data-processing/deploying-a-data-processing-extension-to-report-designer.md)|描述如何將資料處理延伸模組部署到報表設計師。|  
  
## <a name="see-also"></a>另請參閱  
 [Reporting Services 延伸模組](../../../reporting-services/extensions/reporting-services-extensions.md)   
 [實作資料處理延伸模組](../../../reporting-services/extensions/data-processing/implementing-a-data-processing-extension.md)   
 [Reporting Services 延伸模組程式庫](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
