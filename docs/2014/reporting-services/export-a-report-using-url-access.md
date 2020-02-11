---
title: 使用 URL 存取匯出報表 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- formats [Reporting Services], URL rendering
- URL access [Reporting Services], rendering formats
ms.assetid: 6a3b7fc3-3d91-4d12-8371-42ea12e74517
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 69f340855e37ffde49aec0af096c094a142659d1
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66109188"
---
# <a name="export-a-report-using-url-access"></a>使用 URL 存取匯出報表
  您可以使用*rs： format*參數，選擇性地指定用來轉譯報表的格式。 例如，直接從原生模式報表伺服器取得報表的 PDF 副本。  
  
```  
http://myrshost/ReportServer?/myreport&rs:Format=PDF  
```  
  
 以及，從 SharePoint 整合模式報表伺服器：  
  
```  
http://myspsite/subsite/_vti_bin/reportserver?http://myspsite/subsite/myrereport.rdl&rs:Format=PDF  
```  
  
 這個參數的有效值是以安裝在正在存取之報表伺服器上的報表轉譯延伸模組為基礎。 常見的延伸模組為 HTML4.0、MHTML、IMAGE、EXCEL、WORD、CSV、PDF、XML 及 NULL。 如果報表伺服器上未安裝指定的轉譯延伸模組，則報表不會轉譯，且錯誤會產生並顯示在瀏覽器中。  
  
 如果您未將 *Format* 參數包含為 URL 的一部分，則報表伺服器會偵測瀏覽器，並以適當的 HTML 格式轉譯報表。  
  
## <a name="see-also"></a>另請參閱  
 [URL 存取 &#40;SSRS&#41;](url-access-ssrs.md)   
 [URL 存取參數參考](url-access-parameter-reference.md)  
  
  
