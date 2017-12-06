---
title: "Reporting Services 延伸模組 | Microsoft Docs"
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
- SQL Server Reporting Services, extending
- extensions [Reporting Services], about extensions
- SSIS, extending
- Reporting Services, extending
- extensions [Reporting Services]
ms.assetid: 2bf17ae4-2292-4a58-a1f0-56e99abd9b69
caps.latest.revision: "45"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: f6a2b3f080997ecfe554c713757d94764c582785
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/05/2017
---
# <a name="reporting-services-extensions"></a>Reporting Services 延伸模組
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 的模組化架構是針對擴充性所設計。 現在可以使用 Managed 程式碼 API，這樣您就可以輕鬆地開發、安裝和管理許多 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 元件取用的延伸模組。 您可以使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 建立私人或共用組件，並新增新的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 功能以滿足不斷成長的商務需求。  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 獨特的擴充性架構可讓開發人員擴充產品及其元件的特定功能。 目前，有許多方式可用來擴充 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 的資料處理功能。 資料處理 API 包括熟悉的 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 資料提供者建構與慣例，可讓開發人員在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 中建立其他的資料處理延伸模組。 這些資料處理延伸模組會將功能加入報表伺服器與報表設計師，以將自訂資料緊密整合到報表中。  
  
 傳遞延伸模組為另一個支援的延伸模組。 傳遞 API 會完整整合至 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 架構，以便在傳送報表通知給使用者時使用廣泛的傳遞機制。 您可以擴充報表伺服器以提供自訂傳遞給使用者，也能夠擴充報表管理員的訂閱管理頁面，以啟用使用自訂傳遞延伸模組的訂閱。  
  
 報表定義自訂延伸模組 (RDCE) 為另一個報表伺服器延伸模組，它可以動態地自訂報表定義，再將其傳遞至處理引擎。 您可以根據使用者或語言等因素來自訂報表。 例如，您可能會想要為各個使用者 (例如經理或是部門成員) 實作不同的檢視，或是自訂報表，讓報表在轉譯為法文或阿拉伯文時，可以具有不同的配置。  
  
## <a name="in-this-section"></a>本節內容  
 [延伸模組的安全性考量](../../reporting-services/extensions/security-considerations-for-extensions.md)  
 描述與開發和部署 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 延伸模組相關的安全性問題。  
  
 [實作資料處理延伸模組](../../reporting-services/extensions/data-processing/implementing-a-data-processing-extension.md)  
 描述實作 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 之資料處理延伸模組的需求與步驟。  
  
 [實作傳遞延伸模組](../../reporting-services/extensions/delivery-extension/implementing-a-delivery-extension.md)  
 描述實作 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 之傳遞延伸模組的需求與步驟。  
  
 [實作轉譯延伸模組](../../reporting-services/extensions/rendering-extension/implementing-a-rendering-extension.md)  
 包含開發轉譯延伸模組的簡介。  
  
 [實作安全性延伸模組](../../reporting-services/extensions/security-extension/implementing-a-security-extension.md)  
 描述實作 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 安全性延伸模組的需求與步驟。  
  
 [Reporting Services 延伸模組程式庫](../../reporting-services/extensions/reporting-services-extension-library.md)  
 包含 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 擴充性功能之延伸模組 API 程式庫的程式設計參考。  
  
  
