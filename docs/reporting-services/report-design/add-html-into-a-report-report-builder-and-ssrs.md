---
title: 將 HTML 新增至報表 (報表產生器及 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: report-design
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 30bd631a-f774-48e7-a13a-b6c2eb54d9bb
caps.latest.revision: 8
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 855606bb65d7f6ced16517c67a8034b2abf75ea8
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "33019045"
---
# <a name="add-html-into-a-report-report-builder-and-ssrs"></a>將 HTML 加入至報表 (報表產生器及 SSRS)
  您可以使用預留位置，從資料集的欄位匯入 HTML，以便用於報表中。 根據預設，預留位置代表純文字，所以您必須將預留位置標記類型變更為 HTML。 如需詳細資訊，請參閱[將 HTML 匯入至報表 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/importing-html-into-a-report-report-builder-and-ssrs.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-html-from-a-field-in-your-dataset-into-a-text-box"></a>若要將 HTML 從資料集的欄位加入至文字方塊  
  
1.  在 **[插入]** 索引標籤上，按一下 **[清單]**。 按一下設計介面，然後拖曳滑鼠來建立一個所需大小的方塊。  
  
     **[資料集屬性]** 對話方塊隨即開啟。 您可以使用共用資料集或在報表中內嵌資料集。 如需詳細資訊，請按一下[資料集屬性對話方塊、查詢 &#40;報表產生器&#41;](../../reporting-services/report-data/dataset-properties-dialog-box-query-report-builder.md) 或[資料集屬性對話方塊、查詢](http://msdn.microsoft.com/library/1fa34a4b-7de0-4e92-99fa-bc28a206773f)。  
  
2.  在 **[插入]** 索引標籤上，按一下 **[文字方塊]**。 在清單中按一下，然後拖曳滑鼠來建立一個所需大小的方塊。  
  
3.  將 HTML 欄位從資料集拖曳至文字方塊中。 如此就會針對您的欄位建立預留位置。  
  
4.  以滑鼠右鍵按一下預留位置，然後按一下 [預留位置屬性]。  
  
5.  在 **[一般]** 索引標籤上，確認 **[值]** 方塊包含評估成您在步驟 3 中放置之欄位的運算式。  
  
6.  按一下 [HTML - 將 HTML 標記解譯為樣式]。 這樣就會讓欄位評估成 HTML。  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>另請參閱  
 [格式化數字和日期 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/formatting-numbers-and-dates-report-builder-and-ssrs.md)   
 [格式化線條、色彩和影像 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/formatting-lines-colors-and-images-report-builder-and-ssrs.md)   
 [預留位置屬性對話方塊、一般 &#40;報表產生器及 SSRS&#41;](http://msdn.microsoft.com/library/7a867736-a3b0-4b5a-b3e5-fe7c8d7618a8)  
  
  
