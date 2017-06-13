---
title: "項目層級工作 |Microsoft 文件"
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
- item-level tasks [Reporting Services]
ms.assetid: fdeb7bc3-167a-4342-84e3-32e3faa1fa39
caps.latest.revision: 37
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 067a0b9d4f33e20625fb796fa98f7b4ec6184f3e
ms.contentlocale: zh-tw
ms.lasthandoff: 06/13/2017

---
# <a name="tasks-and-permissions---item-level-tasks"></a>工作和權限的項目層級工作
  項目層級工作是與報表、資料夾、報表模型、資源或共用資料來源關聯的權限集合。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 也包括套用至整個報表伺服器網站的系統層級工作。 如需詳細資訊，請參閱 [系統層級工作](../../reporting-services/security/tasks-and-permissions-system-level-tasks.md)。 如需一般工作和權限的詳細資訊，請參閱 [工作和權限](../../reporting-services/security/tasks-and-permissions.md)。  
  
> [!NOTE]  
>  如果您是以程式設計的方式使用這些工作，就必須使用支援項目層級工作的方法。 如需詳細資訊，請參閱<xref:ReportService2010.ReportingService2010.ListTasks%2A>和<xref:ReportService2010.ReportingService2010.ListRoles%2A>。  
  
## <a name="permissions-in-item-level-tasks"></a>項目層級工作中的權限  
 下表列出項目層級工作、每個工作中包含的權限，以及權限套用的項目。 列出權限只是為了參考用途，以提供每項工作可以使用之功能的更準確描述。  
  
 共用資料集使用與報表相同的權限集合。 報表組件使用與資源相同的權限集合。  
  
|工作|適用於項目|Permissions|  
|----------|---------------------|-----------------|  
|取用報表|報表|讀取內容<br /><br /> 讀取報表定義<br /><br /> 讀取屬性|  
|取用報表|共用資料集|讀取內容<br /><br /> 讀取報表定義<br /><br /> 讀取屬性|  
|建立連結報表|報表|建立連結<br /><br /> 讀取屬性|  
|管理所有訂閱|報表|讀取屬性<br /><br /> 讀取任何訂閱<br /><br /> 建立任何訂閱<br /><br /> 刪除任何訂閱<br /><br /> 更新任何訂閱|  
|管理資料來源|資料夾|建立資料來源|  
|管理資料來源|資料來源|更新屬性<br /><br /> 刪除更新內容<br /><br /> 讀取屬性|  
|管理資料夾|資料夾|建立資料夾<br /><br /> 刪除更新屬性<br /><br /> 讀取屬性|  
|管理個別訂閱|報表|讀取屬性<br /><br /> 建立訂閱<br /><br /> 刪除訂閱<br /><br /> 讀取訂閱<br /><br /> 更新訂閱|  
|管理模型|資料夾|建立模型|  
|管理模型|模型|讀取屬性<br /><br /> 讀取內容<br /><br /> 刪除更新內容<br /><br /> 讀取資料來源<br /><br /> 更新資料來源<br /><br /> 讀取模型項目授權原則<br /><br /> 更新模型項目授權原則<br /><br /> 刪除更新屬性|  
|管理報表記錄|報表|讀取屬性<br /><br /> 建立報表記錄<br /><br /> 刪除報表記錄<br /><br /> 執行讀取原則<br /><br /> 更新原則<br /><br /> 列出報表記錄|  
|管理報表|資料夾|建立報表<br /><br /> 也適用於建立共用資料集|  
|管理報表|報表|讀取屬性<br /><br /> 刪除更新屬性<br /><br /> 更新參數<br /><br /> 讀取資料來源<br /><br /> 更新資料來源<br /><br /> 讀取報表定義<br /><br /> 更新報表定義<br /><br /> 執行讀取原則<br /><br /> 更新原則|  
|管理報表|共用資料集|讀取屬性<br /><br /> 刪除更新屬性<br /><br /> 更新參數<br /><br /> 讀取資料來源<br /><br /> 更新資料來源<br /><br /> 讀取報表定義<br /><br /> 更新報表定義<br /><br /> 執行讀取原則<br /><br /> 更新原則|  
|管理資源|資料夾|建立資源|  
|管理資源|資源|更新屬性<br /><br /> 刪除更新內容<br /><br /> 讀取屬性|  
|管理資源|報表組件|更新屬性<br /><br /> 刪除更新內容<br /><br /> 讀取屬性|  
|設定個別項目的安全性|報表、資源、資料來源、共用資料集、資料夾|讀取安全性原則更新安全性原則|  
|檢視資料來源|資料來源|讀取內容<br /><br /> 讀取屬性|  
|檢視資料夾|資料夾|讀取屬性<br /><br /> 執行和檢視<br /><br /> 列出報表記錄|  
|檢視模型|報表模型|讀取屬性<br /><br /> 讀取內容<br /><br /> 讀取資料來源|  
|檢視報表|報表|讀取內容<br /><br /> 讀取屬性|  
|檢視報表|共用資料集|讀取內容<br /><br /> 讀取屬性|  
|檢視資源|資源|讀取內容<br /><br /> 讀取屬性|  
|檢視資源|報表組件|讀取內容<br /><br /> 讀取屬性|  
  
## <a name="see-also"></a>請參閱＜  
 [在原生模式報表伺服器上授與權限](../../reporting-services/security/granting-permissions-on-a-native-mode-report-server.md)  
  
  
