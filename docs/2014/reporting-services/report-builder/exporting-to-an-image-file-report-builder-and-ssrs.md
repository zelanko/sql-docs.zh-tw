---
title: 匯出至影像檔 (報表產生器及 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 020d8ea2-de07-4212-a2bb-2ed0df2c8db8
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 3bdbed10df5dd2d8b52fdaa49d04758d150098b5
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/22/2019
ms.locfileid: "59946614"
---
# <a name="exporting-to-an-image-file-report-builder-and-ssrs"></a>匯出至影像檔 (報表產生器及 SSRS)
  影像轉譯延伸模組會將報表轉譯成點陣圖或中繼檔。 依預設，影像轉譯延伸模組會產生報表的 TIFF 檔，可在多個頁面中檢視。 當用戶端接收到影像時，可以在影像檢視器中顯示和列印影像。 本主題提供影像轉譯器的特定資訊並描述轉譯延伸模組的例外狀況。  
  
 影像轉譯延伸模組可以在任何支援的格式產生檔案[!INCLUDE[ndptecgdiplus](../../includes/ndptecgdiplus-md.md)]:BMP、 EMF、 EMFPlus、 GIF、 JPEG、 PNG 和 TIFF。 針對 TIFF 格式，主要資料流的檔案名稱為 *ReportName*.tif。 針對每個檔案轉譯成單一頁面的其他所有格式，檔案名稱為 *ReportName_Page.ext* ，其中 *ext* 是所選格式的副檔名。 若要以影像支援的其他格式產生檔案，請在 **OutputFormatDeviceInfo** 設定中指定以上列出的任何字串。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="SupportedImageFormats"></a> 支援的影像格式  
 下表顯示每個影像轉譯器格式的副檔名和 MimeType。  
  
|**型別**|**副檔名**|**MIMEType**|  
|--------------|-------------------|------------------|  
|BMP|BMP|image/bmp|  
|GIF|GIF|image/gif|  
|JPEG|JPEG|image/jpeg|  
|PNG|PNG|image/png|  
|TIFF|tif|image/tiff|  
|EMF|EMF|image/emf|  
|EMFPlus|EMF|image/emf|  
  
  
##  <a name="RenderingMultiplePages"></a> 轉譯多頁  
 TIFF 是在單一檔案中，支援多頁文件的唯一格式。 JPG 或 PNG 之類的其他格式一次輸出一頁，而且需要為每一頁個別呼叫轉譯延伸模組。  
  
  
##  <a name="Interactivity"></a> 互動性  
 此轉譯器產生的任何影像格式都不支援互動性。 系統不會轉譯下列互動項目：  
  
-   超連結  
  
-   顯示或隱藏  
  
-   文件引導模式  
  
-   鑽研或點選連結的連結  
  
-   使用者排序  
  
-   固定頁首  
  
-   書籤  
  
  
##  <a name="DeviceInfo"></a> 裝置資訊設定  
 您可以透過變更裝置資訊設定，變更此轉譯器的某些預設設定。 如需詳細資訊，請參閱＜ [Image Device Information Settings](../image-device-information-settings.md)＞。  
  
  
## <a name="see-also"></a>另請參閱  
 [Reporting Services 中的分頁 &#40;報表產生器及 SSRS&#41;](../report-design/pagination-in-reporting-services-report-builder-and-ssrs.md)   
 [轉譯行為 &#40;報表產生器及 SSRS&#41;](../report-design/rendering-behaviors-report-builder-and-ssrs.md)   
 [不同報表轉譯延伸模組的互動式功能 &#40;報表產生器及 SSRS&#41;](interactive-functionality-different-report-rendering-extensions.md)   
 [轉譯報表項目 &#40;報表產生器及 SSRS&#41;](../report-design/rendering-report-items-report-builder-and-ssrs.md)   
 [資料表、矩陣和清單 &#40;報表產生器及 SSRS&#41;](../report-design/create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)  
  
  
