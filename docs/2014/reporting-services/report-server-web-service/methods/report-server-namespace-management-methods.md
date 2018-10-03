---
title: 報表伺服器命名空間管理方法 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.topic: reference
helpviewer_keywords:
- reports [Reporting Services], managing
- management methods [Reporting Services]
- methods [Reporting Services], about methods
- methods [Reporting Services]
ms.assetid: 2aa43ce9-f51e-408a-8ce0-b40d3dd62561
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 0203866f4c8d7380e0590ad843e52432a0fcf119
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48100468"
---
# <a name="report-server-namespace-management-methods"></a>報表伺服器命名空間管理方法
  報表伺服器管理 Web 服務中包含許多方法，可用來管理報表伺服器資料庫中的報表、資料夾和資源。  
  
|方法|動作|  
|------------|------------|  
|<xref:ReportService2010.ReportingService2010.CancelJob%2A>|取消執行作業。|  
|<xref:ReportService2010.ReportingService2010.CreateFolder%2A>|將資料夾加入至報表伺服器資料庫或 SharePoint 文件庫。|  
|<xref:ReportService2010.ReportingService2010.CreateCatalogItem%2A>|將新項目加入至報表伺服器資料庫或 SharePoint 文件庫。 這個方法適用於`Report`， `Model`， `Dataset`， `Component`， `Resource`，和`DataSource`項目類型。|  
|M:ReportService2010.ReportingService2010.CreateReportEditSession(System.String,System.String,System.Byte[],ReportService2010.Warning[]@)|建立新的報表編輯工作階段。|  
|<xref:ReportService2010.ReportingService2010.DeleteItem%2A>|從報表伺服器資料庫或 SharePoint 文件庫移除項目。|  
|<xref:ReportService2010.ReportingService2010.FindItems%2A>|傳回報表伺服器資料庫或 SharePoint 文件庫中符合指定搜尋準則的項目。|  
|<xref:ReportService2010.ReportingService2010.FireEvent%2A>|根據提供的參數觸發事件。|  
|<xref:ReportService2010.ReportingService2010.GetExtensionSettings%2A>|傳回給定延伸模組的設定清單。|  
|<xref:ReportService2010.ReportingService2010.GetItemType%2A>|如果項目存在，便擷取報表伺服器資料庫或 SharePoint 文件庫中的項目類型。|  
|<xref:ReportService2010.ReportingService2010.GetProperties%2A>|傳回報表伺服器資料庫或 SharePoint 文件庫中項目上的一個或多個屬性值。|  
|<xref:ReportService2010.ReportingService2010.GetItemDefinition%2A>|擷取項目的定義或內容。 這個方法適用於`Report`， `Model`， `Dataset`， `Component`， `Resource`，和`DataSource`項目類型。|  
|<xref:ReportService2010.ReportingService2010.GetItemReferences%2A>|傳回與項目關聯的目錄項目參考清單。|  
|<xref:ReportService2010.ReportingService2010.GetReportServerConfigInfo%2A>|傳回有關向外延展部署中，已連接之報表伺服器執行個體或所有報表伺服器執行個體的資訊。|  
|<xref:ReportService2010.ReportingService2010.GetSystemProperties%2A>|傳回一個或多個系統屬性。|  
|<xref:ReportService2010.ReportingService2010.ListChildren%2A>|取得指定之資料夾的子系清單。|  
|<xref:ReportService2010.ReportingService2010.ListDatabaseCredentialRetrievalOptions%2A>|傳回支援的認證擷取選項清單。|  
|<xref:ReportService2010.ReportingService2010.ListEvents%2A>|當事件延伸模組出現在報表伺服器組態檔中時，傳回這些延伸模組的清單。|  
|<xref:ReportService2010.ReportingService2010.ListJobs%2A>|傳回在報表伺服器上執行的作業清單。|  
|<xref:ReportService2010.ReportingService2010.ListExtensions%2A>|傳回為給定延伸模組類型所設定的延伸模組清單。|  
|<xref:ReportService2010.ReportingService2010.ListExtensionTypes%2A>|傳回支援的延伸模組類型清單。|  
|<xref:ReportService2010.ReportingService2010.ListItemTypes%2A>|傳回支援的目錄項目類型清單。|  
|<xref:ReportService2010.ReportingService2010.ListJobActions%2A>|傳回支援的作業動作清單。|  
|<xref:ReportService2010.ReportingService2010.ListJobStates%2A>|傳回支援的作業狀態清單。|  
|<xref:ReportService2010.ReportingService2010.ListJobTypes%2A>|傳回支援的作業類型清單。|  
|<xref:ReportService2010.ReportingService2010.ListParents%2A>|擷取給定項目的父項目。|  
|<xref:ReportService2010.ReportingService2010.ListSecurityScopes%2A>|傳回支援的安全性範圍清單。|  
|<xref:ReportService2010.ReportingService2010.Logoff%2A>|將提出 Web 服務要求的目前使用者登出。 這個方法只適用於原生模式。|  
|<xref:ReportService2010.ReportingService2010.LogonUser%2A>|登入使用者，並向報表伺服器 Web 服務驗證使用者的要求。 這個方法只適用於原生模式。|  
|<xref:ReportService2010.ReportingService2010.SetItemReferences%2A>|設定與項目關聯的目錄項目。|  
|<xref:ReportService2010.ReportingService2010.MoveItem%2A>|移動及 (或) 重新命名項目。|  
|<xref:ReportService2010.ReportingService2010.SetProperties%2A>|設定項目的一個或多個屬性。|  
|<xref:ReportService2010.ReportingService2010.SetItemDefinition%2A>|設定指定之項目的定義或內容。 這個方法適用於`Report`， `Model`， `Dataset`， `Component`， `Resource`，和`DataSource`項目類型。|  
|<xref:ReportService2010.ReportingService2010.SetSystemProperties%2A>|設定報表伺服器或 SharePoint 伺服器陣列中的一個或多個系統屬性。|  
|<xref:ReportService2010.ReportingService2010.ValidateExtensionSettings%2A>|驗證 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 延伸模組設定。|  
  
## <a name="see-also"></a>另請參閱  
 [使用 Web 服務和 .NET Framework 建置應用程式](../net-framework/building-applications-using-the-web-service-and-the-net-framework.md)   
 [報表伺服器 Web 服務](../report-server-web-service.md)   
 [報表伺服器 Web 服務方法](report-server-web-service-methods.md)   
 [技術參考 &#40;SSRS&#41;](../../technical-reference-ssrs.md)  
  
  
