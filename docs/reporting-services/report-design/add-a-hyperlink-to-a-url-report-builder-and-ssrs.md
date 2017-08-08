---
title: "將超連結新增到 URL (報表產生器及 SSRS) | Microsoft Docs"
ms.custom: 
ms.date: 09/07/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d3392c0b-7b62-4d27-bc04-2bd0c5487d08
caps.latest.revision: 11
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: c4d66e7d74d06cbad20351f80a312be95cc253c0
ms.contentlocale: zh-tw
ms.lasthandoff: 08/03/2017

---
# <a name="add-a-hyperlink-to-a-url-report-builder-and-ssrs"></a>將超連結加入到 URL (報表產生器及 SSRS)
了解如何將文字方塊、影像、圖表和量測計的超連結動作加入 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)]  分頁報表。 這些連結可以移至其他報表、移至報表中的書籤，或是移至靜態或動態 URL。 

 您可以將超連結動作新增到任何具有 **Action** 屬性的項目，例如文字方塊、影像或圖表中的計算數列。 當使用者按一下該報表項目時，就會發生您定義的動作。  
  
*   您可以 **加入超連結，以使用您指定的 URL 開啟瀏覽器** 。 此超連結可以是靜態 URL，或是評估為 URL 的運算式。 如果資料庫中有一個包含 URL 的欄位，運算式便能包含這個欄位，結果會在報表中產生超連結的動態清單。 請確定您的報表讀者可以存取您提供的 URL。  
   
*  您也可以在您和您的使用者有權使用報表伺服器之 URL 要求進行檢視的任何報表伺服器上 **指定 URL 以建立報表的鑽研** 。 例如，您可以指定報表，並在使用者最初檢視報表時為他們隱藏文件引導模式。 如需詳細資訊，請參閱 [URL 存取 &#40;SSRS&#41;](../../reporting-services/url-access-ssrs.md) 和[指定外部項目的路徑 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/specifying-paths-to-external-items-report-builder-and-ssrs.md)。
 
 *  而且您可以 **將書籤加入同一份報表中的特定位置** 。 
  
試試看在[教學課程：將文字格式化 &#40;報表產生器&#41;](../../reporting-services/tutorial-format-text-report-builder.md) 中使用相同資料新增超連結。  
  
> [!NOTE]  
>  繫結至資料集欄位的連結可能很容易受到惡意竄改。 如需詳細資訊，請參閱 [保護報表和資源的安全](../../reporting-services/security/secure-reports-and-resources.md)。  
  
## <a name="to-add-a-hyperlink-and"></a>若要加入超連結及...   
  
1.  在報表設計檢視中，以滑鼠右鍵按一下要加入連結的文字方塊、影像或圖表，然後按一下 **[屬性]**。  
  
2.  在 [屬性] 對話方塊中，按一下 [動作] 索引標籤。 請繼續閱讀以了解可用選項的相關資訊。  

## <a name="-add-drillthrough-to-another-report"></a>... 加入其他報表的鑽研

1. 在 [動作] 索引標籤上，選取 [移至報表]。 

2. 指定您要使用的目標報表和參數。 參數名稱必須符合針對目標報表定義的參數。 

3. 使用 [新增] 和 [刪除] 按鈕來新增和移除參數，並使用向上和向下箭號來排列參數清單的順序。

4.  在鑽研報表中，為具名參數輸入或選取要傳遞的 **值** 。 請按一下 [運算式]\(fx) 按鈕來編輯運算式。

5. 選取 [省略] 可防止參數執行。 根據預設，不會勾選也不會啟用此核取方塊。 若要選取此核取方塊，請按一下 [運算式]\(fx) 按鈕，然後輸入 True 或建立一個運算式。 當您按一下 [運算式] 對話方塊中的 [確定] 時，就會選取此核取方塊。
  
   如需詳細資訊，請參閱 [在報表上加入鑽研動作](../../reporting-services/report-design/add-a-drillthrough-action-on-a-report-report-builder-and-ssrs.md) 。 
   
6. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
   
## <a name="-add-a-bookmark"></a>... 加入書籤

您可以連結到指向目前報表中某個位置的書籤。 若要連結到書籤，您必須先設定報表項目的 **Bookmark** 屬性。 若要設定 **Bookmark** 屬性，請選取報表項目，然後在 [屬性] 窗格中鍵入書籤識別碼的值或運算式，例如 SalesChart 或 5TopSales。

1. 在 [動作] 索引標籤上，選取 [移至書籤]。 

2. 輸入或選取報表要跳至的目的地書籤識別碼。 按一下 [運算式]\(fx) 按鈕來變更運算式。 

   書籤識別碼可以是靜態識別碼或者會評估為書籤識別碼的運算式。 此運算式可包含具有書籤識別碼的欄位。
   
   如需詳細資訊，請參閱 [將書籤加入至報表](../../reporting-services/report-design/add-a-bookmark-to-a-report-report-builder-and-ssrs.md) 。
   
3. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  

## <a name="-add-a-hyperlink"></a>... 加入超連結 
  
1. 在 [動作] 索引標籤上，選取 [移至 URL]。 此對話方塊中會出現這個選項的其他區段。  
  
4.  在 **[選取 URL]**中，輸入或選取 URL 或是評估為 URL 的運算式，或者按下拉式箭號，再按一下含有 URL 之欄位的名稱。 

    對於發行到設定為原生模式之報表伺服器的項目，請使用完整或相對路徑， 例如， `http://<servername>/images/image1.jpg`。 
    
    對於發行到設定為 SharePoint 整合模式之報表伺服器的項目，請使用完整 URL， 例如， `http://<SharePointservername>/<site>/Documents/images/image1.jpg`。
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  

## <a name="after-you-add-a-hyperlink"></a>加入超連結後
  
1.  (選擇性) 文字不會自動格式化為連結。 如果是文字，則變更文字色彩及效果來指示該文字為連結，將會是很有協助的作法。 例如，在 [功能區] 的 [主資料夾] 索引標籤上設定 **[字型]** 區段，將色彩變更為藍色並加上底線效果。  
  
7.  若要測試連結，請按一下 **[執行]** 預覽報表，然後按一下這個連結設定所在的報表項目。  
  
## <a name="see-also"></a>請參閱＜  
 [互動式排序、文件引導模式及連結 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/interactive-sort-document-maps-and-links-report-builder-and-ssrs.md)   
 [建立文件引導模式 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/create-a-document-map-report-builder-and-ssrs.md)  
  
  

