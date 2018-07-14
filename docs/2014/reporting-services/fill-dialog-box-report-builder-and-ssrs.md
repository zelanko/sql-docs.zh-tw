---
title: 填滿對話方塊 （報表產生器及 SSRS） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.rtp.rptdesigner.reportbody.fill.f1
- "10065"
- "10501"
- sql12.rtp.rptdesigner.shared.filldv.f1
- sql12.rtp.rptdesigner.rectangleproperties.fill.f1
- "10064"
- sql12.rtp.rptdesigner.textboxproperties.fill.f1
- "10124"
ms.assetid: 93a91d02-d558-4a0e-8d17-3fdf21e208d3
caps.latest.revision: 11
author: maggiesmsft
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 135a2d1d7ac4a9783bf2cc66f26dc60953ec2f76
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37262294"
---
# <a name="fill-dialog-box-report-builder-and-ssrs"></a>填滿對話方塊 (報表產生器及 SSRS)
  在 [填滿] 索引標籤上，您可以指定資料區或文字方塊內，單一資料格或多個資料格的背景選項。  
  
## <a name="options"></a>選項。  
 **填滿色彩**  
 按一下色彩按鈕，為矩形選取一個填滿色彩。 按一下 **Expression***(fx)* 按鈕來編輯運算式，它可以是 RGB 色彩，或其中一個預先定義的色彩名稱中所提供的十六進位值**運算式** 對話方塊。 若要查看預先定義之色彩的清單，選取 [項目] 窗格中的 [Web]。 您可以將列在 [標題] 窗格中的色彩名稱輸入到運算式文字窗格中。 輸入色彩名稱時，請勿使用等號 (=) 或引號 ("")。  
  
 **選取影像來源**  
 指出影像儲存的位置，以便在轉譯報表時，讓報表處理器可以顯示該影像。  
  
-   **外部** ：當您希望影像在報表伺服器或網頁伺服器上繼續當做檔案存在時，選擇此選項。  
  
-   **內嵌** ：當您要將影片內嵌到報表中時，選擇此選項。  
  
-   **資料庫** ：當您要加入的資料庫欄位名稱代表您要包含在報表中的影像時，選擇此選項。  
  
 **使用此映像**  
 此選項會在您選取 [內嵌] 或 [外部] 選項時出現。  
  
 如果您要內嵌影像，從下拉式清單中選擇您要加入報表的圖片。 按一下 [匯入]，將影像加入到下拉式清單中。 如果您要將影像加入到 [資料] 窗格中，您可以選擇 [內嵌]，然後從下拉式清單中選取影像，就可以選取該影像。  
  
 如果您選取 [外部] 選項，輸入影像的 URL。 對於發行到設定為原生模式報表伺服器報表，使用完整或相對路徑 (例如 http://*\<伺服器名稱 >* images/image1.jpg)。 對於發行到設定為 SharePoint 整合模式報表伺服器報表，則使用完整的 URL (例如 http://*\<//<sharepoint 伺服器名稱 > /\<站台 >*  /記載/影像 /image1.jpg)。  
  
 **匯入**  
 適用於選取 [內嵌] 時。 按一下此選項，即可將影像加入到 [使用此影像] 下拉式清單中。  
  
 **使用此欄位**  
 適用於選取 [資料庫] 時。 選取欄位名稱。  
  
 **使用此 MIME 類型**  
 選擇資料庫中包含的適當圖片格式 (例如，.bmp、.jpeg、.gif、.png 或 .x-png)。  
  
## <a name="see-also"></a>另請參閱  
 [設定報表項目的格式 &#40;報表產生器及 SSRS&#41;](report-design/formatting-report-items-report-builder-and-ssrs.md)   
 [格式化文字和預留位置&#40;報表產生器及 SSRS&#41;](report-design/formatting-text-and-placeholders-report-builder-and-ssrs.md)   
 [映像&#40;報表產生器及 SSRS&#41;](report-design/images-report-builder-and-ssrs.md)  
  
  
