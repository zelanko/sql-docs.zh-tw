---
title: "Windows 應用程式記錄檔 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Windows application logs [Reporting Services]
- logs [Reporting Services], Windows application logs
- application logs [Reporting Services]
ms.assetid: 742fd00e-aa6c-4c8a-b58f-c03c489b1699
caps.latest.revision: "32"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 2f34c31f34b79a5e2f40cc88cbf57c35ce582558
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="windows-application-log"></a>Windows 應用程式記錄檔
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 會將事件訊息寫入 Windows 應用程式記錄。 您可以利用寫入應用程式記錄檔的訊息資訊，來了解在本機系統上執行的報表伺服器應用程式所產生的事件。  
  
## <a name="viewing-report-server-events"></a>檢視報表伺服器事件  
 您可以使用 [事件檢視器] 來檢視記錄檔及篩選所包含的訊息。 如需事件訊息的詳細資訊，請參閱 [錯誤和事件參考 &#40;Reporting Services&#41;](../../reporting-services/troubleshooting/errors-and-events-reference-reporting-services.md)。 如需有關 Windows 應用程式記錄或 [事件檢視器] 的詳細資訊，請參閱 Windows 產品文件集。  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 會提供三個事件來源：  
  
-   報表伺服器 (報表伺服器 Windows 服務)  
  
-   報表管理員  
  
-   排程與傳遞處理器  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 不會提供關閉報表伺服器之應用程式事件記錄的方法，或控制所記錄事件的方法。 描述報表伺服器事件記錄的結構描述是固定的。 您無法延伸結構描述以支援自訂事件。  
  
 下表描述報表伺服器寫入應用程式事件記錄的事件類型。  
  
|事件類型|說明|  
|----------------|-----------------|  
|資訊|描述作業成功的事件 (例如，當報表伺服器服務啟動時)。|  
|警告|表示有潛在問題的事件 (例如，磁碟空間不足)。|  
|錯誤|描述嚴重問題的事件 (例如，服務未啟動)。|  
|稽核成功|描述登入成功的安全性事件。|  
|稽核失敗|嘗試登入失敗時所記錄的事件。|  
  
## <a name="see-also"></a>另請參閱  
 [Reporting Services 記錄檔和來源](../../reporting-services/report-server/reporting-services-log-files-and-sources.md)   
 [錯誤和事件參考 &#40;Reporting Services&#41;](../../reporting-services/troubleshooting/errors-and-events-reference-reporting-services.md)  
  
  
