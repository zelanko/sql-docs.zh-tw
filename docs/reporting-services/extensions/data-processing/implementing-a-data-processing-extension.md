---
title: "實作資料處理延伸模組 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- custom data processing extensions [Reporting Services]
- data sources [Reporting Services], data processing extensions
- data processing extensions [Reporting Services]
- extensions [Reporting Services], data processing
ms.assetid: 8dc2b44e-5ad9-411d-a29f-7213e29321a9
caps.latest.revision: 35
author: sabotta
ms.author: carlasab
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 372d21a412efec6306912950e7f9f5a6f577ee3f
ms.contentlocale: zh-tw
ms.lasthandoff: 06/13/2017

---
# <a name="implementing-a-data-processing-extension"></a>實作資料處理延伸模組
  在 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 中的資料處理延伸模組，可讓您連接到資料來源並擷取資料。 它們也可當做資料來源與資料集之間的橋樑。 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]資料處理延伸模組為模型的子集[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]資料提供者介面。  
  
## <a name="in-this-section"></a>本節內容  
 [資料處理延伸模組概觀](../../../reporting-services/extensions/data-processing/data-processing-extensions-overview.md)  
 介紹如何為 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 撰寫自訂資料處理延伸模組。  
  
 [準備實作資料處理延伸模組](../../../reporting-services/extensions/data-processing/preparing-to-implement-a-data-processing-extension.md)  
 描述實作 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 資料處理延伸模組時可用的介面，以及您何時需要實作特定的介面。  
  
 [建立資料處理延伸模組程式庫](../../../reporting-services/extensions/data-processing/creating-a-data-processing-extension-library.md)  
 描述為 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 資料處理延伸模組指派命名空間，以及將資料處理延伸模組編譯成為程式庫 DLL。  
  
 [資料處理延伸模組實作 Connection 類別](../../../reporting-services/extensions/data-processing/implementing-a-connection-class-for-a-data-processing-extension.md)  
 描述連接，以及如何實作自己的屬性**連接**類別為您的資料處理延伸模組。  
  
 [資料處理延伸模組實作命令類別](../../../reporting-services/extensions/data-processing/implementing-a-command-class-for-a-data-processing-extension.md)  
 說明的命令，以及如何實作您自己的屬性**命令**類別為您的資料處理延伸模組。  
  
 [實作資料處理延伸模組的 DataReader 類別](../../../reporting-services/extensions/data-processing/implementing-a-datareader-class-for-a-data-processing-extension.md)  
 描述資料讀取器，以及如何實作您自己的屬性**DataReader**類別為您的資料處理延伸模組。  
  
 [Reporting services 使用外部資料集](../../../reporting-services/extensions/data-processing/using-an-external-dataset-with-reporting-services.md)  
 說明如何公開您的自訂**資料集**耗用量的報表伺服器的物件。  
  
 [部署資料處理延伸模組](../../../reporting-services/extensions/data-processing/deploying-a-data-processing-extension.md)  
 描述如何部署您的資料處理延伸模組。  
  
 [偵錯資料處理延伸模組程式碼](../../../reporting-services/extensions/data-processing/debugging-data-processing-extension-code.md)  
 描述如何在資料處理延伸模組中偵錯程式碼。  
  
 [移除資料處理延伸模組](../../../reporting-services/extensions/data-processing/removing-a-data-processing-extension.md)  
 描述如何從報表伺服器或是報表設計師移除資料處理延伸模組。  
  
 如需完全實作的資料處理延伸模組的範例，請參閱[SQL Server Reporting Services 產品範例](http://go.microsoft.com/fwlink/?LinkId=177889)。  
  
## <a name="see-also"></a>另請參閱  
 [Reporting Services 延伸模組](../../../reporting-services/extensions/reporting-services-extensions.md)   
 [Reporting Services 延伸模組程式庫](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
