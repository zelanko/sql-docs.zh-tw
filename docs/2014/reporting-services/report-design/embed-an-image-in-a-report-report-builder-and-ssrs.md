---
title: 在報表中內嵌影像 (報表產生器及 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.rtp.rptdesigner.embeddedimages.f1
- "10060"
ms.assetid: aed77345-5eeb-41f0-96c9-db6b4a11ec6f
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: b1541073379aa27c932fcadf7558de7d34c57e8d
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/22/2019
ms.locfileid: "59938864"
---
# <a name="embed-an-image-in-a-report-report-builder-and-ssrs"></a>在報表中內嵌影像 (報表產生器及 SSRS)
  報表可以包含內嵌影像。 內嵌影像可確保影像隨時可供報表使用，但是可能會影響報表定義 (定義報表的檔案) 的大小。 內嵌在報表中的影像會列在 [報表資料] 窗格中。  
  
 您可以在將影像加入至設計介面之前，先將影像內嵌在報表定義中。 如需詳細資訊，請參閱[新增背景影像 &#40;報表產生器及 SSRS&#41;](add-a-background-image-report-builder-and-ssrs.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-embed-an-image-in-a-report"></a>若要在報表中內嵌影像  
  
1.  在報表設計檢視的 **[插入]** 索引標籤上，按一下 **[影像]**。  
  
2.  在設計介面上，按一下然後將方塊拖曳至所需的影像大小。  
  
3.  在 **[影像屬性]** 對話方塊的 **[一般]** 頁面上，於 **[名稱]** 文字方塊內輸入名稱，或是接受預設值。  
  
4.  (選擇性) 在 [工具提示] 文字方塊中，鍵入您希望使用者將滑鼠停留在轉譯報表內的影像上方時，所要出現的文字。  
  
5.  在 **[選取影像來源]** 中，選取 **[內嵌]**。  
  
6.  按一下 **[使用此影像]** 文字方塊旁邊的 **[匯入]** 按鈕。  
  
7.  在 **[檔案類型]** 中，選取影像檔類型，瀏覽到該檔案，然後按一下 **[開啟]**。  
  
8.  在 **[影像屬性]** 對話方塊中，按一下 **[確定]**。  
  
     影像隨即顯示在您在設計介面上繪製的方塊中，而且檔案會顯示在 [報表資料] 窗格的 [影像] 資料夾底下。  
  
    > [!NOTE]  
    >  MIME 類型 (例如 bmp) 是在影像匯入時自動衍生的。 若要變更 MIME 類型，請參閱下一個程序。  
  
### <a name="optional-to-change-the-mime-type-of-an-imported-image"></a>(選擇性) 若要變更匯入之影像的 MIME 類型  
  
1.  在 [設計] 檢視中開啟報表。  
  
2.  在設計介面上選取影像。 **[屬性]** 窗格會顯示影像屬性。  
  
    > [!NOTE]  
    >  如果看不到 [屬性] 窗格，請按一下 [檢視] 索引標籤上的 [屬性]。  
  
3.  在 [MIMEType] 屬性旁邊的文字方塊內按一下，然後從下拉式清單中選取新的 MIME 類型。  
  
## <a name="see-also"></a>另請參閱  
 [影像 &#40;報表產生器及 SSRS&#41;](images-report-builder-and-ssrs.md)   
 [加入資料繫結影像 &#40;報表產生器及 SSRS&#41;](add-a-data-bound-image-report-builder-and-ssrs.md)   
 [影像屬性對話方塊、一般 &#40;報表產生器及 SSRS&#41;](../image-properties-dialog-box-general-report-builder-and-ssrs.md)  
  
  
