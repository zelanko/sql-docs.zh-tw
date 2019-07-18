---
title: 部署資料處理延伸模組 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- data processing extensions [Reporting Services], deploying
- Extension element
- deploying [Reporting Services], extensions
ms.assetid: e5c0b5a9-1386-47cb-aade-96653ecfaa54
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: d4741c822dab24026d823a0e08571ac6aacea9ce
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63165179"
---
# <a name="deploying-a-data-processing-extension"></a>部署資料處理延伸模組
  一旦您撰寫 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 資料處理延伸模組並將其編譯成 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 程式庫之後，需要使其可供報表伺服器和報表設計師探索。 完成此項動作很簡單，只要將伸模組複製到適當的目錄，並將項目加入適當的 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 組態檔即可。  
  
## <a name="configuration-file-extension-element"></a>組態檔延伸模組元素  
 部署到報表伺服器或是報表設計師的資料處理延伸模組，需要在設定檔中輸入成 **Extension** 項目。 這些檔案在報表伺服器中為 RSReportServer.config，在報表設計師中為 RSReportDesigner.config。  
  
 下表描述資料處理延伸模組之 **Extension** 項目的屬性。  
  
|屬性|描述|  
|---------------|-----------------|  
|`Name`|例如，就延伸模組的維一名稱而言，"SQL" 為 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料處理延伸模組，或者 "OLEDB" 為 OLE DB 資料處理延伸模組。 `Name` 屬性的最大長度為 255 個字元。 該名稱在組態檔之 **Extension** 元素的所有元素中，必須是唯一的。|  
|`Type`|以逗號分隔的清單，包括完整的命名空間以及組件的名稱。|  
|`Visible`|`false` 的值指出在使用者介面中應該看不到資料處理延伸模組。 如果沒有包括屬性，預設值是 `true`。|  
  
 如需 RSReportServer.config 或 RSReportDesigner.config 檔的詳細資訊，請參閱 [Reporting Services 設定檔](../../report-server/reporting-services-configuration-files.md)。  
  
## <a name="in-this-section"></a>本節內容  
  
|主題|描述|  
|-----------|-----------------|  
|[如何：將資料處理延伸模組部署到報表伺服器](deploying-a-data-processing-extension-to-a-report-server.md)|描述如何將資料處理延伸模組部署到報表伺服器。|  
|[如何：將資料處理延伸模組部署到報表設計師](deploying-a-data-processing-extension-to-report-designer.md)|描述如何將資料處理延伸模組部署到報表設計師。|  
  
## <a name="see-also"></a>另請參閱  
 [Reporting Services 延伸模組](../reporting-services-extensions.md)   
 [實作資料處理延伸模組](implementing-a-data-processing-extension.md)   
 [Reporting Services 延伸模組程式庫](../reporting-services-extension-library.md)  
  
  
