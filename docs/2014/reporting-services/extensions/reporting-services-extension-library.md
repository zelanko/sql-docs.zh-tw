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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "62985757"
---
# <a name="reporting-services-extension-library"></a>Reporting Services 延伸模組程式庫
  Reporting Services 延伸模組程式庫是一組包括在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 中的類別、介面和值類型。 此程式庫提供對系統功能的存取，並設計為可以使用[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]應用程式來擴充[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]元件的基礎。  
  
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
  
  
