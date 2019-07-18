---
title: 新增資料繫結影像 (報表產生器及 SSRS) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: df4c38d4-bfcc-41c4-aa6d-952ca6fd7a2e
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: e9ec6a57c73367439953a9172ec038439f0f92ac
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "65582258"
---
# <a name="add-a-data-bound-image-report-builder-and-ssrs"></a>加入資料繫結影像 (報表產生器及 SSRS)
  報表可以包含儲存在資料庫內之影像的參考。 這類影像稱為「資料繫結影像」  。 出現在產品清單中產品名稱旁邊的圖片就是資料繫結影像的範例。  
  
 將資料繫結影像加入至頁首或頁尾時，需要其他步驟。 如需詳細資訊，請參閱[頁首和頁尾 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/page-headers-and-footers-report-builder-and-ssrs.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-a-data-bound-image"></a>若要加入資料繫結影像  
  
1.  在報表設計檢視中，建立具有資料來源連線的資料表，以及具有包含二進位影像資料之欄位的資料集。 如需詳細資訊，請參閱[資料表 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/tables-report-builder-and-ssrs.md)。  
  
2.  將資料行插入資料表中。 如需詳細資訊，請參閱[插入或刪除資料行 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/insert-or-delete-a-column-report-builder-and-ssrs.md)。  
  
3.  在 **[插入]** 功能表上，按一下 **[插入]** ，然後按一下新資料行的資料列。  
  
4.  在 **[影像屬性]** 對話方塊的 [一般] 頁面上，於 **[名稱]** 文字方塊內輸入名稱，或是接受預設值。  
  
5.  (選擇性) 在 [工具提示]  文字方塊中，鍵入您希望使用者將滑鼠停留在轉譯成 HTML 之報表內的影像上方時，所要顯示的文字。  
  
6.  在 **[選取影像來源]** 中，選取 **[資料庫]** 。  
  
7.  在 **[使用此欄位]** 中，選取包含您報表中之影像的欄位。  
  
8.  在 [使用此 MIME 類型]  中，選取影像的 MIME 類型或檔案格式，例如 bmp。  
  
9. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     影像預留位置會出現在報表設計介面上。  
  
## <a name="see-also"></a>另請參閱  
 [影像 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/images-report-builder-and-ssrs.md)   
 [在報表中內嵌影像 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/embed-an-image-in-a-report-report-builder-and-ssrs.md)   
 [加入外部影像 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/add-an-external-image-report-builder-and-ssrs.md)   
 [影像屬性對話方塊、一般 &#40;報表產生器及 SSRS&#41;](https://msdn.microsoft.com/library/c2218b93-f7fe-46ef-995f-d7dadf9752ec)  
  
  
