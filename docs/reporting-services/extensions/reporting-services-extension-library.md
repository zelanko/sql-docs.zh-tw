---
title: "Reporting Services 延伸模組程式庫 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.service: 
ms.component: extensions
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- namespaces [Reporting Services]
- Reporting Services, extending
- extensions [Reporting Services], library
- library [Reporting Services]
ms.assetid: e8eff470-64d6-41c3-b98b-5ec916c121c3
caps.latest.revision: "33"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 921ccbecb3f711daba1b87a8f01a97f903935cf2
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/05/2017
---
# <a name="reporting-services-extension-library"></a>Reporting Services 延伸模組程式庫
  Reporting Services 延伸模組程式庫是一組包括在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 中的類別、介面和值類型。 這個程式庫可以用來存取系統功能，而且是設計成作為 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 應用程式可用以擴充 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 元件的基礎。  
  
## <a name="namespaces"></a>命名空間  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 延伸程式庫提供下列命名空間。  
  
 <xref:Microsoft.ReportingServices.DataProcessing>  
 包含的類別與介面可讓您建立元件並擴充 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 的資料處理功能。  
  
 <xref:Microsoft.ReportingServices.Interfaces>  
 包含的類別與介面，可讓您透過自己的傳遞延伸模組建構和傳送自訂通知給使用者，並為 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 建立自訂安全性延伸模組。  
  
 **Microsoft.ReportingServices.ReportRendering**  
 包含的類別與介面可讓您擴充 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 的轉譯功能。 透過使用此命名空間的成員以及 <xref:Microsoft.ReportingServices.Interfaces> 命名空間的成員，就可以為 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 建立自己的自訂轉譯延伸模組。  
  
## <a name="see-also"></a>另請參閱  
 [Reporting Services 延伸模組](../../reporting-services/extensions/reporting-services-extensions.md)  
  
  
