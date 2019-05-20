---
title: 在報表上新增鑽研動作 (報表產生器及 SSRS) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 153729c4-d01e-4629-b78f-0cfd5a7f83da
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: cfae70562bf244ba9294f31f1dcba9d85f5699f6
ms.sourcegitcommit: dda9a1a7682ade466b8d4f0ca56f3a9ecc1ef44e
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 05/14/2019
ms.locfileid: "65574866"
---
# <a name="add-a-drillthrough-action-on-a-report-report-builder-and-ssrs"></a>在報表上加入鑽研動作 (報表產生器及 SSRS)
  當您按一下主報表中的連結所開啟的報表稱為 *「鑽研報表」*(Drillthrough Report)。 此鑽研連結會啟用一個鑽研動作。  
  
 鑽研報表必須與主報表發行至相同的報表伺服器，但是可位於不同的資料夾中。 您可以將鑽研連結加入到具有 **Action** 屬性的任何項目，例如文字方塊、影像或是圖表的資料點。  
  
 若要將鑽研連結加入到報表，您必須先建立主報表將連結的鑽研報表。 鑽研報表通常包含有關原始摘要報表之項目的詳細資料，而且經常包含參數，這些參數會根據主報表傳遞過來的參數來篩選鑽研報表。 如需建立鑽研報表的詳細資訊，請參閱[鑽研報表 &#40;報表產生器和 SSRS&#41;](../../reporting-services/report-design/drillthrough-reports-report-builder-and-ssrs.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-a-drillthrough-action"></a>若要加入鑽研動作  
  
1.  在 [設計] 檢視中，以滑鼠右鍵按一下要新增連結的文字方塊、影像或圖表，然後按一下 [屬性]。  
  
2.  在項目的 **[屬性]** 對話方塊中，按一下 **[動作]**。  
  
3.  選取 **[移至報表]**。 對話方塊中會出現這個選項的其他區段。  
  
4.  在 **[指定報表]** 中，按一下 **[瀏覽]** ，找出您想要跳至的報表，或輸入報表的名稱。 或者，您也可以按一下運算式 (**fx**) 按鈕來建立報表名稱的運算式。  
  
     鑽研報表的路徑格式會因原生和 SharePoint 整合模式而不同。 如果您瀏覽至報表，就會提供正確格式的路徑。 如需詳細資訊，請參閱[指定外部項目的路徑 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/specifying-paths-to-external-items-report-builder-and-ssrs.md)。  
  
     如果您必須指定鑽研報表的參數，請遵循下一個步驟。  
  
5.  在 **[使用這些參數執行報表]** 中，按一下 **[加入]**。 新的資料列就會加入至參數方格。  
  
    -   在 [名稱] 文字方塊中，按一下下拉式清單或鍵入鑽研報表內的報表參數名稱。  
  
        > [!NOTE]  
        >  參數清單中的名稱必須與目標報表中預期的參數完全相符。 例如，參數名稱的大小寫必須相符。 如果名稱不相符，或是未列出預期的參數，鑽研報表就會失敗。  
  
    -   在 **[值]** 中，輸入或選取要傳遞給鑽研報表內之參數的值。  
  
        > [!NOTE]  
        >  值可以包含運算式，此運算式必須評估為傳遞至報表參數的值。 值清單中的運算式包含目前報表的欄位清單。  
  
     如需如何隱藏報表中參數的資訊，請參閱[新增、變更或刪除報表參數 &#40;報表產生器和 SSRS&#41;](../../reporting-services/report-design/add-change-or-delete-a-report-parameter-report-builder-and-ssrs.md)。  
  
6.  (選擇性) 如果是文字方塊，在 [功能區] 的 [主資料夾] 索引標籤上變更文字的色彩和效果，向使用者指示該文字為連結，將會很有協助。  
  
7.  若要測試連結，請執行報表，然後按一下這個連結設定所在的報表項目。  
  
## <a name="see-also"></a>另請參閱  
 [動作屬性對話方塊 &#40;報表產生器和 SSRS&#41;](https://msdn.microsoft.com/library/2c5d915b-4f97-42cf-b8f1-49ca3ff3d0f9)   
 [格式化圖表上的資料點 &#40;報表產生器和 SSRS&#41;](../../reporting-services/report-design/formatting-data-points-on-a-chart-report-builder-and-ssrs.md)   
 [在數列上顯示工具提示 &#40;報表產生器和 SSRS&#41;](../../reporting-services/report-design/show-tooltips-on-a-series-report-builder-and-ssrs.md)  
  
  
