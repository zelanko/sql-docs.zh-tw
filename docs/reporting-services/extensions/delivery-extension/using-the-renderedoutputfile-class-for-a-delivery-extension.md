---
title: "使用傳遞延伸模組的 RenderedOutputFile 類別 |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
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
- RenderedOutputFile class
- data streams [Reporting Services]
- delivery extensions [Reporting Services], data streams
ms.assetid: 8b591801-42d5-49fa-b710-bf7e6917accf
caps.latest.revision: 34
author: sabotta
ms.author: carlasab
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 5ebd5ea1a5a96727a77ea78aa1ee9cbc74e6dd81
ms.contentlocale: zh-tw
ms.lasthandoff: 06/13/2017

---
# <a name="using-the-renderedoutputfile-class-for-a-delivery-extension"></a>使用傳遞延伸模組的 RenderedOutputFile 類別
  <xref:Microsoft.ReportingServices.Interfaces.RenderedOutputFile> 類別代表資料流以及與資料流的相關聯屬性的資訊。 **資料**屬性<xref:Microsoft.ReportingServices.Interfaces.RenderedOutputFile>類別用來表示轉譯的報表或是報表資源**資料流**物件。  
  
 <xref:Microsoft.ReportingServices.Interfaces.Report.Render%2A>方法**報表**物件傳回的一或多個陣列<xref:Microsoft.ReportingServices.Interfaces.RenderedOutputFile>構成單一轉譯報表的物件。 第一個 <xref:Microsoft.ReportingServices.Interfaces.RenderedOutputFile> 物件是轉譯報表。 任何其他 <xref:Microsoft.ReportingServices.Interfaces.RenderedOutputFile> 物件都是必須連同報表資料一起傳遞的資源 (例如，HTML 檔案與相關聯的影像)。 屬於單一資料流轉譯延伸模組 (IMAGE、PDF、MHTML 和 EXCEL) 的轉譯延伸模組只會傳回陣列中的一個 <xref:Microsoft.ReportingServices.Interfaces.RenderedOutputFile> 物件。  
  
 如需如何使用的範例<xref:Microsoft.ReportingServices.Interfaces.RenderedOutputFile>類別，請參閱[SQL Server Reporting Services 產品範例](http://go.microsoft.com/fwlink/?LinkId=177889)。  
  
## <a name="see-also"></a>另請參閱  
 [實作傳遞延伸模組](../../../reporting-services/extensions/delivery-extension/implementing-a-delivery-extension.md)   
 [Reporting Services 延伸模組程式庫](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
