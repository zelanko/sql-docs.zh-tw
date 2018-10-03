---
title: 使用 URL 存取匯出報表 | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
helpviewer_keywords:
- formats [Reporting Services], URL rendering
- URL access [Reporting Services], rendering formats
ms.assetid: 6a3b7fc3-3d91-4d12-8371-42ea12e74517
author: markingmyname
ms.author: maghan
ms.openlocfilehash: a77bc4e35d1aaefe3c1d55fd4be8086a71d5dabb
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47644116"
---
# <a name="export-a-report-using-url-access"></a>使用 URL 存取匯出報表
  您可以使用 *rs:Format* URL 參數，選擇性地指定用於轉譯報表的格式。  HTML4.0 和 HTM5 格式 (轉譯延伸模組) 及其他格式會呈現在瀏覽器中，瀏覽器會提示使用者將報表輸出儲存至本機檔案。  
  
 例如，直接從原生模式報表伺服器取得報表的 PDF 副本。  
  
```  
http://myrshost/ReportServer?/myreport&rs:Format=PDF  
```  
  
 以及，從 SharePoint 整合模式報表伺服器：  
  
```  
http://myspsite/subsite/_vti_bin/reportserver?http://myspsite/subsite/myrereport.rdl&rs:Format=PDF  
```  
  
 例如，您瀏覽器中的以下 URL 命令會從報表伺服器的具名執行個體匯出 PPTX 報表。  
  
```  
http://servername/ReportServer_THESQLINSTANCE/Pages/ReportViewer.aspx?%2freportfolder%2freport+name+with+spaces&rs:Format=pptx  
```  
  
 這個參數的有效值是以安裝在正在存取之報表伺服器上的報表轉譯延伸模組為基礎。 常見的延伸模組為 HTML4.0、MHTML、IMAGE、EXCELOPENXML (xlsx)、WORDOPENXML (docx)、CSV、PDF、XML 及 NULL。 如果報表伺服器上未安裝指定的轉譯延伸模組，則報表不會轉譯，且錯誤會產生並顯示在瀏覽器中。  
  
 如果您未將 *Format* 參數包含為 URL 的一部分，則報表伺服器會偵測瀏覽器，並以適當的 HTML 格式轉譯報表。  
  
## <a name="see-also"></a>另請參閱  
 [URL 存取 &#40;SSRS&#41;](../reporting-services/url-access-ssrs.md)   
 [URL 存取參數參考](../reporting-services/url-access-parameter-reference.md)  
  
  
