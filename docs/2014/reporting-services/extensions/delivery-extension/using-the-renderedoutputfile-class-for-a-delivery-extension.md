---
title: 使用傳遞延伸模組的 RenderedOutputFile 類別 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.topic: reference
helpviewer_keywords:
- RenderedOutputFile class
- data streams [Reporting Services]
- delivery extensions [Reporting Services], data streams
ms.assetid: 8b591801-42d5-49fa-b710-bf7e6917accf
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 5c2fa313e594dae2cfac69684770e77908c56eff
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/13/2018
ms.locfileid: "53352602"
---
# <a name="using-the-renderedoutputfile-class-for-a-delivery-extension"></a>使用傳遞延伸模組的 RenderedOutputFile 類別
  <xref:Microsoft.ReportingServices.Interfaces.RenderedOutputFile> 類別代表資料流以及與資料流的相關聯屬性的資訊。 <xref:Microsoft.ReportingServices.Interfaces.RenderedOutputFile> 類別的 **Data** 屬性，會用來代表作為 **Stream** 物件的轉譯報表或是報表資源。  
  
 **Report** 物件的 <xref:Microsoft.ReportingServices.Interfaces.Report.Render%2A> 方法會傳回一或多個 <xref:Microsoft.ReportingServices.Interfaces.RenderedOutputFile> 物件的陣列，這些物件會構成單一的轉譯報表。 第一個 <xref:Microsoft.ReportingServices.Interfaces.RenderedOutputFile> 物件是轉譯報表。 任何其他 <xref:Microsoft.ReportingServices.Interfaces.RenderedOutputFile> 物件都是必須連同報表資料一起傳遞的資源 (例如，HTML 檔案與相關聯的影像)。 屬於單一資料流轉譯延伸模組 (IMAGE、PDF、MHTML 和 EXCEL) 的轉譯延伸模組只會傳回陣列中的一個 <xref:Microsoft.ReportingServices.Interfaces.RenderedOutputFile> 物件。  
  
 如需如何使用 <xref:Microsoft.ReportingServices.Interfaces.RenderedOutputFile> 類別的範例，請參閱 [SQL Server Reporting Services Product Samples](https://go.microsoft.com/fwlink/?LinkId=177889) (SQL Server Reporting Services 產品範例)。  
  
## <a name="see-also"></a>另請參閱  
 [實作傳遞延伸模組](implementing-a-delivery-extension.md)   
 [Reporting Services 延伸模組程式庫](../reporting-services-extension-library.md)  
  
  
