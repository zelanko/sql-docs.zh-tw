---
title: "授權方法 | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.service: 
ms.component: report-server-web-service
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- security [Reporting Services], reports
- authorization [Reporting Services]
- reports [Reporting Services], security
- tasks [Reporting Services]
- roles [Reporting Services], methods
ms.assetid: 45e9cf2c-facf-4801-9482-c855403f42a8
caps.latest.revision: "42"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 91d3763a199950bb11d1c7c066a07ba16dfed6e3
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/05/2017
---
# <a name="authorization-methods"></a>授權方法
  您可以使用這些方法在報表伺服器上管理工作、角色和原則。  
  
|方法|動作|  
|------------|------------|  
|<xref:ReportService2010.ReportingService2010.CreateRole%2A>|將新角色加入至報表伺服器資料庫。 這個方法只適用於原生模式。|  
|<xref:ReportService2010.ReportingService2010.DeleteRole%2A>|從報表伺服器資料庫刪除角色。 這個方法只適用於原生模式。|  
|<xref:ReportService2010.ReportingService2010.GetPermissions%2A>|傳回與報表伺服器資料庫或 SharePoint 文件庫中特定項目關聯的使用者權限。|  
|<xref:ReportService2010.ReportingService2010.GetPolicies%2A>|傳回與報表伺服器資料庫或 SharePoint 文件庫中特定項目關聯的原則。|  
|<xref:ReportService2010.ReportingService2010.GetRoleProperties%2A>|傳回角色中繼資料屬性與關聯工作的集合。|  
|<xref:ReportService2010.ReportingService2010.GetSystemPermissions%2A>|傳回使用者的系統權限。 這個方法只適用於原生模式。|  
|<xref:ReportService2010.ReportingService2010.GetSystemPolicies%2A>|傳回系統原則，包括關聯的群組與角色。 這個方法只適用於原生模式。|  
|<xref:ReportService2010.ReportingService2010.InheritParentSecurity%2A>|刪除與報表伺服器資料庫中特定項目關聯的原則，並將項目的安全性原則設定為其父項的安全性原則。|  
|<xref:ReportService2010.ReportingService2010.IsSSLRequired%2A>|傳回布林值，指出是否需要安全通訊端層 (SSL) 通訊協定，以便使用 <xref:ReportService2010> 端點。|  
|<xref:ReportService2010.ReportingService2010.ListRoles%2A>|傳回報表伺服器所管理角色的名稱與描述。|  
|<xref:ReportExecution2005.ReportExecutionService.ListSecureMethods%2A>|傳回在叫用時需要安全連接的 <xref:ReportExecution2005> 端點中，簡易物件存取通訊協定 (SOAP) 方法的清單。 報表伺服器的 **SecureConnectionLevel** 設定是用以決定所要傳回的方法。|  
|<xref:ReportService2010.ReportingService2010.ListTasks%2A>|傳回由報表伺服器所管理的工作。|  
|<xref:ReportService2010.ReportingService2010.SetPolicies%2A>|設定與指定之項目關聯的原則。|  
|<xref:ReportService2010.ReportingService2010.SetRoleProperties%2A>|設定角色中繼資料屬性，並將一組工作與角色相關聯。 這個方法只適用於原生模式。|  
|<xref:ReportService2010.ReportingService2010.SetSystemPolicies%2A>|設定系統原則，以定義群組及其關聯的角色。 這個方法只適用於原生模式。|  
  
## <a name="see-also"></a>另請參閱  
 [使用 Web 服務和 .NET Framework 建置應用程式](../../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)   
 [報表伺服器 Web 服務](../../../reporting-services/report-server-web-service/report-server-web-service.md)   
 [報表伺服器 Web 服務方法](../../../reporting-services/report-server-web-service/methods/report-server-web-service-methods.md)   
 [技術參考 &#40;SSRS&#41;](../../../reporting-services/technical-reference-ssrs.md)  
  
  
