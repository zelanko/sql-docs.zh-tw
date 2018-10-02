---
title: rsServerConfigurationError - Reporting Services 錯誤 | Microsoft Docs
ms.date: 03/20/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: troubleshooting
ms.topic: conceptual
helpviewer_keywords:
- rsServerConfigurationError
ms.assetid: 0913afc2-34b4-4713-b570-cfd5718975ac
author: markingmyname
ms.author: maghan
ms.openlocfilehash: a03e276df871e7949ac01b7e0f1698dafcb36bf2
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47793082"
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
  
 若要檢閱伴隨著 **rsServerConfiguration** 錯誤的其他錯誤訊息資訊，請檢閱位於 \Microsoft SQL Server\MSRS12.\<執行個體名稱>\Reporting Services\LogFiles 中的報表伺服器追蹤記錄檔。 如需詳細資訊，請參閱 [Reporting Services 記錄檔和來源](../../reporting-services/report-server/reporting-services-log-files-and-sources.md)。  
  
## <a name="internal-only"></a>僅供內部使用  
  
## <a name="see-also"></a>另請參閱  
 [Reporting Services 組態檔](../../reporting-services/report-server/reporting-services-configuration-files.md)   
 [修改 Reporting Services 設定檔 &#40;RSreportserver.config&#41;](../../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md)  
  
  
