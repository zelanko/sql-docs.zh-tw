---
title: "rsServerConfigurationError-Reporting Services 錯誤 |Microsoft 文件"
ms.custom: 
ms.date: 03/20/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- rsServerConfigurationError
ms.assetid: 0913afc2-34b4-4713-b570-cfd5718975ac
caps.latest.revision: 12
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 78d4fd567ce57dba6d78c45a543a68725742d686
ms.contentlocale: zh-tw
ms.lasthandoff: 08/09/2017

---
# <a name="rsserverconfigurationerror---reporting-services-error"></a>rsServerConfigurationError - Reporting Services 錯誤
    
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|事件識別碼|rsServerConfiguration|  
|事件來源|Microsoft.ReportingServices.Diagnostics.Utilities.ErrorStrings|  
|元件|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|  
|訊息文字|報表伺服器發生組態錯誤。|  
  
## <a name="explanation"></a>說明  
 這是一般用途錯誤，當報表伺服器或報表撰寫工具具有無效的組態設定時，就會發生此錯誤。 此錯誤通常伴隨著陳述錯誤之實際原因的第二則訊息。  
  
 下列清單摘要列出可能的原因：  
  
-   找不到或無法讀取 RSReportServer.config 或 RSReportDesigner.config 檔案。  
  
-   組態檔中的 XML 元素遺失或無效。  
  
-   一或多個 XML 元素的值遺失或無效。  
  
-   登錄設定無效。  
  
## <a name="user-action"></a>使用者動作  
 如果當您在手動編輯組態檔之後開始發生這個錯誤，請移除您的變更並輸入之前的值，或者如果您有備份則還原舊版。  
  
 若要檢閱伴隨其他錯誤訊息資訊**rsServerConfiguration**錯誤，請檢閱位於 \Microsoft SQL Server\MSRS12 報表伺服器追蹤記錄檔。\<執行個體名稱 > services\logfiles。 如需詳細資訊，請參閱 [Reporting Services 記錄檔和來源](../../reporting-services/report-server/reporting-services-log-files-and-sources.md)。  
  
## <a name="internal-only"></a>僅供內部使用  
  
## <a name="see-also"></a>請參閱＜  
 [Reporting Services 組態檔](../../reporting-services/report-server/reporting-services-configuration-files.md)   
 [修改 Reporting Services 組態檔 &#40;RSreportserver.config &#41;](../../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md)  
  
  

