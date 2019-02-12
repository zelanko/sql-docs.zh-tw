---
title: 影像屬性對話方塊、 一般 （報表產生器及 SSRS） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10051"
- sql12.rtp.rptdesigner.pictureproperties.general.f1
ms.assetid: c2218b93-f7fe-46ef-995f-d7dadf9752ec
author: maggiesmsft
ms.author: maghan
manager: kfile
ms.openlocfilehash: cbbe4fe5917419bc07cef81629c7b2e38b7cff15
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/11/2019
ms.locfileid: "56019631"
---
# <a name="image-properties-dialog-box-general-report-builder-and-ssrs"></a>影像屬性對話方塊、一般 (報表產生器及 SSRS)
  選取 [影像屬性] 對話方塊上的 [一般] 來加入圖片、變更影像的預設名稱，以及加入工具提示文字。  
  
## <a name="options"></a>選項。  
 **名稱**  
 輸入項目的名稱。 名稱在報表內必須是唯一的。 根據預設，系統會指派一個一般名稱 (例如，Image1 或 Image2)。  
  
 **Tooltip**  
 輸入文字或評估為工具提示的運算式。 請按一下 [運算式] (*fx*) 按鈕來編輯運算式。 使用者在 HTML 報表中將指標暫停在項目上時，[工具提示] 會顯示。  
  
 **選取影像來源**  
 指出影像儲存的位置，以便在轉譯報表時，讓報表處理器知道要從哪裡取得影像。  
  
-   **外部** ：當您希望影像在報表伺服器或網頁伺服器上繼續當作檔案存在時，選擇此選項。  
  
-   **內嵌** ：當您要將影片內嵌到報表中時，選擇此選項。  
  
-   **資料庫** ：當您要加入的資料庫欄位名稱代表您要包含在報表中的影像時，選擇此選項。  
  
 **使用此映像**  
 此選項會在您選取 [內嵌] 或 [外部] 選項時出現。  
  
 如果您要內嵌影像，從下拉式清單中選擇您要加入報表的影像。 按一下 [匯入] 按鈕，將影像加入到下拉式清單中。  
  
 如果您選取 [外部] 選項，輸入影像的 URL。 對於發行到設定為原生模式之報表伺服器的報表，請使用完整或相對路徑， 例如 http://\<伺服器名稱 > / images/image1.jpg。 對於發行到設定為 SharePoint 整合模式之報表伺服器的報表，請使用完整 URL， 例如 http://\<*SharePointservername*>/\<*網站*> / Documents/images/image1.jpg。  
  
 **匯入**  
 按一下此選項，即可將影像加入到 [使用此影像] 下拉式清單中。  
  
 **使用此欄位**  
 此選項會在您選取 [資料庫] 選項時出現。 選取欄位名稱。  
  
 **使用此 MIME 類型**  
 選擇資料庫中包含的適當影像格式 (例如，.bmp、.jpeg、.gif、.png 和 .x-png)。  
  
## <a name="see-also"></a>另請參閱  
 [運算式範例 &#40;報表產生器及 SSRS&#41;](report-design/expression-examples-report-builder-and-ssrs.md)   
 [影像 &#40;報表產生器及 SSRS&#41;](report-design/images-report-builder-and-ssrs.md)   
 [對話方塊、窗格和精靈的報表產生器說明](../../2014/reporting-services/report-builder-help-for-dialog-boxes-panes-and-wizards.md)  
  
  
