---
title: Reporting Services 屬性 | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- report servers [Reporting Services], properties
- properties [Reporting Services], about properties
- reports [Reporting Services], properties
- Report Server Web service, properties
- report properties [Reporting Services]
- XML Web service [Reporting Services], properties
- Web service [Reporting Services], properties
- properties [Reporting Services]
ms.assetid: 8c855194-4c20-4ecc-a328-5137d54b560c
caps.latest.revision: 33
author: douglaslM
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: e3da3152b0f165fac7b03f40f1b5542712d7115f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36134097"
---
# <a name="reporting-services-properties"></a>Reporting Services 屬性
  報表伺服器會定義一組對於報表伺服器是全域的系統屬性，以及一組與報表伺服器資料庫中儲存的個別項目相關聯的項目屬性。 報表伺服器所定義的屬性無法刪除，而且在某些情況下，它們是唯讀的。 應用程式可以將其他使用者定義的屬性加入系統與項目屬性，以擴充系統屬性與項目屬性。  
  
 下列 Web 服務方法會擷取和設定 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 屬性。  
  
|方法|動作|  
|------------|------------|  
|<xref:ReportService2010.ReportingService2010.GetProperties%2A>|傳回報表伺服器資料庫中項目上一或多個屬性的值。|  
|<xref:ReportService2010.ReportingService2010.GetSystemProperties%2A>|傳回一個或多個系統屬性。|  
|<xref:ReportService2010.ReportingService2010.SetProperties%2A>|在報表伺服器資料庫中設定項目的一或多個屬性。|  
|<xref:ReportService2010.ReportingService2010.SetSystemProperties%2A>|設定一個或多個系統屬性。|  
  
## <a name="in-this-section"></a>本節內容  
  
|主題|描述|  
|-----------|-----------------|  
|[報表伺服器項目屬性](reporting-services-properties-report-server-item-properties.md)|描述在 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 中的項目特定屬性。|  
|[報表伺服器系統屬性](reporting-services-properties-report-server-system-properties.md)|描述在 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 中的系統特定屬性。|  
  
## <a name="see-also"></a>另請參閱  
 [使用 Web 服務和 .NET Framework 建置應用程式](building-applications-using-the-web-service-and-the-net-framework.md)   
 [報表伺服器 Web 服務](../report-server-web-service.md)   
 [技術參考 &#40;SSRS&#41;](../../technical-reference-ssrs.md)  
  
  