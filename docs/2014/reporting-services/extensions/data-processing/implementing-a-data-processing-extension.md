---
title: 實作資料處理延伸模組 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.topic: reference
helpviewer_keywords:
- custom data processing extensions [Reporting Services]
- data sources [Reporting Services], data processing extensions
- data processing extensions [Reporting Services]
- extensions [Reporting Services], data processing
ms.assetid: 8dc2b44e-5ad9-411d-a29f-7213e29321a9
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 919f77d0f2295091133203de2474cf81a070d956
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48162188"
---
# <a name="implementing-a-data-processing-extension"></a>實作資料處理延伸模組
  在 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 中的資料處理延伸模組，可讓您連接到資料來源並擷取資料。 它們也可當做資料來源與資料集之間的橋樑。 因為 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 資料處理延伸模組是依照 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 資料提供者介面子集建立的。  
  
## <a name="in-this-section"></a>本節內容  
 [資料處理延伸模組概觀](data-processing-extensions-overview.md)  
 介紹如何為 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 撰寫自訂資料處理延伸模組。  
  
 [準備實作資料處理延伸模組](preparing-to-implement-a-data-processing-extension.md)  
 描述實作 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 資料處理延伸模組時可用的介面，以及您何時需要實作特定的介面。  
  
 [建立資料處理延伸模組程式庫](creating-a-data-processing-extension-library.md)  
 描述為 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 資料處理延伸模組指派命名空間，以及將資料處理延伸模組編譯成為程式庫 DLL。  
  
 [為資料處理延伸模組實作連接類別](implementing-a-connection-class-for-a-data-processing-extension.md)  
 描述連線的屬性，以及如何為您的資料處理延伸模組實作自己的 **Connection** 類別。  
  
 [為資料處理延伸模組實作命令類別](implementing-a-command-class-for-a-data-processing-extension.md)  
 描述命令的屬性，以及如何為您的資料處理延伸模組實作自己的 **Command** 類別。  
  
 [為資料處理延伸模組實作資料讀取元類別](implementing-a-datareader-class-for-a-data-processing-extension.md)  
 描述資料讀取器的屬性，以及如何為您的資料處理延伸模組實作自己的 **DataReader** 類別。  
  
 [透過 Reporting Services 使用外部資料集](using-an-external-dataset-with-reporting-services.md)  
 描述如何向要取用的報表伺服器公開自訂 **DataSet** 物件。  
  
 [部署資料處理延伸模組](deploying-a-data-processing-extension.md)  
 描述如何部署您的資料處理延伸模組。  
  
 [對資料處理延伸模組程式碼進行偵錯](debugging-data-processing-extension-code.md)  
 描述如何在資料處理延伸模組中偵錯程式碼。  
  
 [移除資料處理延伸模組](removing-a-data-processing-extension.md)  
 描述如何從報表伺服器或是報表設計師移除資料處理延伸模組。  
  
 如需完全實作的資料處理延伸模組的範例，請參閱 [SQL Server Reporting Services Product Samples](http://go.microsoft.com/fwlink/?LinkId=177889) (SQL Server Reporting Services 產品範例)。  
  
## <a name="see-also"></a>另請參閱  
 [Reporting Services 延伸模組](../reporting-services-extensions.md)   
 [Reporting Services 延伸模組程式庫](../reporting-services-extension-library.md)  
  
  
