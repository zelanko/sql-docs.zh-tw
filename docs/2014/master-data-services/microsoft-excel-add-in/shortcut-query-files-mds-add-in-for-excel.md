---
title: 捷徑查詢檔案 (適用於 Excel 的 MDS 增益集) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 1ba0219a-6c40-41fa-aff9-8c8f41ef3220
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 11e875d5b171194c3ac8ba4ad33fad51cacacffe
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "65482663"
---
# <a name="shortcut-query-files-mds-add-in-for-excel"></a>捷徑查詢檔案 (適用於 Excel 的 MDS 增益集)
  在 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]中，使用捷徑查詢檔案來快速連接及載入常用的資料。 當您想要將 MDS 資料與其他人分享時，也可以使用。 您應該儲存捷徑查詢檔案並以電子郵件送出，而不是儲存工作表並以電子郵件送出。 如此可確保您可連接到 MDS 儲存機制來取得最新的資料。  
  
 捷徑查詢檔案是包含以下相關資訊的 XML 檔案：  
  
-   MDS 儲存機制連接。  
  
-   模型、版本和實體。  
  
-   建立捷徑時已套用的任何篩選。  
  
-   建立捷徑時，從左到右的資料行順序。  
  
 您可以將這些檔案儲存在清單中，並在您開啟增益集時從中選擇。 您可以將其匯出到您的電腦或共用位置，或是傳送給其他人。  
  
## <a name="queryopener-application"></a>QueryOpener 應用程式  
 所有安裝 [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)] 的使用者都已安裝稱為 QueryOpener 的應用程式。 此應用程式是用來在 [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]中開啟捷徑查詢檔案。 如果您按兩下捷徑查詢檔案，便會自動使用此應用程式在增益集中開啟檔案。  
  
 當您使用這個應用程式開啟捷徑查詢檔案時，系統會提示您讓連線成為「安全」連線，這表示您信任這個位置的內容。 每當您將連接標示為安全時，它就會加入至清單中。 如果您想要清除此清單，請開啟 **[設定]** 對話方塊，並按一下 **[加入至安全清單的伺服器]** 區段中的 **[全部清除]** 。  
  
 應用程式的預設位置是*磁碟機*: \Program Files\Microsoft SQL Server\120\Master Data Services\Excel Add-In\Microsoft.MasterDataServices.QueryOpener.exe。  
  
 有兩個方式可開啟捷徑查詢檔案：您可以匯入檔案，或是按兩下檔案並自動開啟檔案。  
  
## <a name="related-tasks"></a>相關工作  
  
|工作描述|主題|  
|----------------------|-----------|  
|將使用中工作表的內容儲存為捷徑查詢檔案。|[儲存捷徑查詢檔案 &#40;適用於 Excel 的 MDS 增益集&#41;](save-a-shortcut-query-file-mds-add-in-for-excel.md)|  
|將代表使用中工作表內容的捷徑查詢檔案以電子郵件送出。|[以電子郵件傳送捷徑查詢檔案 &#40;適用於 Excel 的 MDS 增益集&#41;](email-a-shortcut-query-file-mds-add-in-for-excel.md)|  
  
## <a name="related-content"></a>相關內容  
  
-   [連接 &#40;適用於 Excel 的 MDS 增益集&#41;](connections-mds-add-in-for-excel.md)  
  
-   [適用於 Microsoft Excel 的 Master Data Services 增益集](master-data-services-add-in-for-microsoft-excel.md)  
  
-   [安全性 &#40;Master Data Services&#41;](../security-master-data-services.md)  
  
  
