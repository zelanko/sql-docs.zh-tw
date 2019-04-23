---
title: Reporting Services 延伸模組程式庫 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- namespaces [Reporting Services]
- Reporting Services, extending
- extensions [Reporting Services], library
- library [Reporting Services]
ms.assetid: e8eff470-64d6-41c3-b98b-5ec916c121c3
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: d09464ce4a61903a3e9b74711482d2ce07bd0c4e
ms.sourcegitcommit: b87c384e10d6621cf3a95ffc79d6f6fad34d420f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/22/2019
ms.locfileid: "60157345"
---
# <a name="reporting-services-extension-library"></a>Reporting Services 延伸模組程式庫
  Reporting Services 延伸模組程式庫是一組包括在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 中的類別、介面和值類型。 這個程式庫可以用來存取系統功能，而且是設計成作為 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 應用程式可用以擴充 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 元件的基礎。  
  
## <a name="namespaces"></a>命名空間  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 延伸程式庫提供下列命名空間。  
  
 <xref:Microsoft.ReportingServices.DataProcessing>  
 包含的類別與介面可讓您建立元件並擴充 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 的資料處理功能。  
  
 <xref:Microsoft.ReportingServices.Interfaces>  
 包含的類別與介面，可讓您透過自己的傳遞延伸模組建構和傳送自訂通知給使用者，並為 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 建立自訂安全性延伸模組。  
  
 `Microsoft.ReportingServices.ReportRendering`  
 包含的類別與介面可讓您擴充 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 的轉譯功能。 透過使用此命名空間的成員以及 <xref:Microsoft.ReportingServices.Interfaces> 命名空間的成員，就可以為 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 建立自己的自訂轉譯延伸模組。  
  
## <a name="see-also"></a>另請參閱  
 [Reporting Services 延伸模組](reporting-services-extensions.md)  
  
  
