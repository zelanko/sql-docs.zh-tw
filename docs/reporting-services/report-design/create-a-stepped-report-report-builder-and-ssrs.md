---
title: 建立階梯狀報表 (報表產生器及 SSRS) | Microsoft Docs
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
ms.assetid: 5933c4f0-c713-4ecb-b521-ff46c9c63fff
caps.latest.revision: 8
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 7644c7d01ea8d12864cf402543f031f137aed383
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "33021815"
---
# <a name="create-a-stepped-report-report-builder-and-ssrs"></a>建立階梯狀報表 (報表產生器及 SSRS)
階梯狀報表是一種  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 分頁報表類型，會在相同的資料行中，顯示父群組底下縮排的詳細資料列或子群組，如以下範例所示：  
  
 ![已轉譯的階梯狀報表](../../reporting-services/report-design/media/steppedreportrendered.gif "已轉譯的階梯狀報表")  
  
 傳統的資料表報表會將父群組放在報表的相鄰資料行中。 新的 Tablix 資料區可讓您將群組和詳細資料列或子群組加入到相同的資料行中。 若要區分群組資料列與詳細資料列或子群組資料列，您可以套用格式 (如字型色彩)，也可以讓詳細資料列縮排。  
  
 本主題中的程序示範如何手動建立階梯狀報表，但是您也可以使用「新增資料表和矩陣精靈」。 此精靈會提供階梯狀報表的配置，讓您更容易建立階梯狀報表。 完成精靈後，您可以進一步增強報表。  
  
> [!NOTE]  
>  您只能在報表產生器中使用此精靈。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="to-create-a-stepped-report"></a>若要建立階梯狀報表  
  
1.  建立資料表報表。 例如，插入 Tablix 資料區，然後將欄位加入到資料列。  
  
2.  將父群組加入到報表中。  
  
    1.  按一下資料表中的任何地方，即可選取它。 在 [群組] 窗格會顯示 [資料列群組] 窗格中的詳細資料群組。  
  
    2.  在 [群組] 窗格中，以滑鼠右鍵按一下 [詳細資料群組]，然後指向 [新增群組]，再按一下 [父群組]。  
  
    3.  在 [Tablix 群組] 對話方塊中，為群組提供一個名稱，然後在下拉式清單中鍵入或選取一個群組運算式。 此下拉式清單會顯示 [報表資料] 窗格中提供的簡單欄位運算式。 例如，[PostalCode] 是資料集中 PostalCode 欄位的簡單欄位運算式。  
  
    4.  選取 [新增群組頁首]。 這個選項會在群組標籤和群組總計的群組上方加入靜態資料列。 同樣地，您可以選取 [新增群組頁尾] 在群組底下新增靜態資料列。 [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     您現在擁有一個基本的表格式報表。 轉譯報表時，您會看到一個包含群組執行個體值的資料行，以及一個或多個包含群組詳細資料的資料行。 下圖顯示資料區可能會在設計介面上呈現的外觀。  
  
     ![含有群組的資料表資料區域](../../reporting-services/report-design/media/tabledataregionwithgroup.gif "含有群組的資料表資料區域")  
  
     下圖顯示當您檢視報表時，轉譯的資料區可能的外觀。  
  
     ![已轉譯的群組報表](../../reporting-services/report-design/media/tablereportrendered.gif "已轉譯的群組報表")  
  
3.  如果是階梯狀報表，您不需要第一個顯示群組執行個體的資料行， 請改為複製群組首資料格中的值、刪除群組資料行，然後貼到群組首資料列中的第一個文字方塊。 若要移除群組資料行，請以滑鼠右鍵按一下群組資料行或資料格，然後按一下 [刪除資料行]。 下圖顯示資料區可能會在設計介面上呈現的外觀。  
  
     ![含有群組頁首資料列的資料區域](../../reporting-services/report-design/media/tabledataregiongroupheader.gif "含有群組頁首資料列的資料區域")  
  
4.  若要將詳細資料列縮排到相同資料行的群組頁首資料列之下，請變更詳細資料資料格的填補。  
  
    1.  選取包含您要縮排之詳細資料欄位的資料格。 該資料格的文字方塊屬性會出現在 [屬性] 窗格中。  
  
    2.  在 [屬性] 窗格的 [對齊] 底下，展開 [填補] 的屬性。  
  
    3.  在 [左] 中，鍵入新的填補值，例如 **.5in**。 填補會將資料格中的文字縮排您所指定的值。 預設填補為 2 點。 [填補] 屬性的有效值為零或正數，後面接著一個大小指示項。  
  
         大小指示項包括：  
  
        |||  
        |-|-|  
        |**in**|英吋 (1 英吋 = 2.54 公分)|  
        |**cm**|公分|  
        |**mm**|公釐|  
        |**pt**|點 (1 點 = 1/72 英吋)|  
        |**pc**|Picas (1 pica = 12 點)|  
  
     您的資料區域外觀將與下列範例類似。  
  
     ![階梯狀報表的資料區域](../../reporting-services/report-design/media/steppedreportdataregion.gif "階梯狀報表的資料區域")  
  
     **階梯狀報表配置的資料區**  
  
     在 [主資料夾] 索引標籤上，按一下 [執行]。 報表在顯示群組時，將會包含子群組值的縮排層級。  
  
## <a name="to-create-a-stepped-report-with-multiple-groups"></a>若要建立包含多個群組的階梯狀報表  
  
1.  如前一個程序所述來建立報表。  
  
2.  將其他群組加入到您的報表中。  
  
    1.  在 [資料列群組] 窗格中，以滑鼠右鍵按一下群組，然後按一下 [新增群組]，再選擇您想要新增的群組類型。  
  
        > [!NOTE]  
        >  有幾個方法可以將群組加入到資料區域。 如需詳細資訊，請參閱 [在資料區中加入或刪除群組 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/add-or-delete-a-group-in-a-data-region-report-builder-and-ssrs.md)。  
  
    2.  在 [Tablix 群組] 對話方塊中，鍵入名稱。  
  
    3.  在 [群組運算式] 中，鍵入運算式，或是選取分組所依據的資料集欄位。 若要建立運算式，請按一下運算式 (**fx**) 按鈕，開啟 [運算式] 對話方塊。  
  
    4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
3.  變更顯示群組資料之資料格的填補。  
  
## <a name="see-also"></a>另請參閱  
 [頁首和頁尾 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/page-headers-and-footers-report-builder-and-ssrs.md)   
 [設定報表項目的格式 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/formatting-report-items-report-builder-and-ssrs.md)   
 [Tablix 資料區 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/tablix-data-region-report-builder-and-ssrs.md)   
 [資料表 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/tables-report-builder-and-ssrs.md)   
 [矩陣 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/create-a-matrix-report-builder-and-ssrs.md)   
 [清單 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)   
 [資料表、矩陣和清單 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
