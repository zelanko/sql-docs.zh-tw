---
title: 新增子報表和參數 (報表產生器及 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- "10093"
- sql12.rtp.rptdesigner.subreportproperties.general.f1
ms.assetid: 94f960f8-a629-4f1e-8277-c3b8f0680d98
caps.latest.revision: 8
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: f99f7baef82824a4af4c9520825043523bb8255d
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36021745"
---
# <a name="add-a-subreport-and-parameters-report-builder-and-ssrs"></a>加入子報表和參數 (報表產生器及 SSRS)
  當您想要建立主報表，而該主報表為多個相關報表的容器時，請在報表中加入子報表。 子報表是另一個報表的參考。 若要透過資料值讓報表產生關聯 (例如，讓多個報表都顯示同一位客戶的資料)，您必須設計參數化報表 (例如，顯示特定客戶之詳細資料的報表) 當做子報表。 當您將子報表加入到主報表時，可以指定要傳遞給子報表的參數。  
  
 您也可以將子報表加入到資料表或矩陣中的動態資料列或資料行。 當處理主報表時，將會針對每一個資料列處理子報表。 在此情況下，請考慮是否可以使用資料區或巢狀資料區來達到所要的效果。  
  
 若要將子報表加入至報表，您必須先建立做為子報表的報表。 如需有關如何建立子報表的詳細資訊，請參閱[子報表&#40;報表產生器及 SSRS&#41;](subreports-report-builder-and-ssrs.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-a-subreport"></a>若要加入子報表  
  
1.  在 **[插入]** 索引標籤上，按一下 **[子報表]**。  
  
2.  在設計介面上，按一下報表上的某個位置，然後將方塊拖曳至所需的子報表大小。 另外，您也可以按一下設計介面來建立預設大小的子報表。  
  
3.  以滑鼠右鍵按一下子報表，然後按一下 [子報表屬性]。  
  
4.  在 **[子報表屬性]** 對話方塊中，於 **[名稱]** 文字方塊內輸入名稱或是接受預設值。 名稱在報表內必須是唯一的。 根據預設，系統會指派一般名稱，例如 Subreport1 或 Subreport2。  
  
5.  在 **[將此報表當成子報表]** 方塊中，按一下 **[瀏覽]**，或輸入報表的名稱。 建議您按一下 **[瀏覽]** ，因為系統將自動指定子報表的路徑。 您可以透過幾種方式指定報表。 如需詳細資訊，請參閱[指定外部項目的路徑 &#40;報表產生器及 SSRS&#41;](specifying-paths-to-external-items-report-builder-and-ssrs.md)。  
  
6.  (選用) 如果子報表橫跨多頁，針對 [省略分頁符號上的框線] 按一下 [是]，就不會在子報表中轉譯框線。  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-specify-parameters-to-pass-to-a-subreport"></a>指定要傳遞給子報表的參數  
  
1.  在 [設計] 檢視中，以滑鼠右鍵按一下子報表，然後按一下 [子報表屬性]。  
  
2.  在 **[子報表屬性]** 對話方塊中，按一下 **[參數]**。  
  
3.  按一下 **[加入]**。 新的資料列就會加入至參數方格。  
  
4.  在 **[名稱]** 文字方塊中，輸入子報表中的參數名稱或從清單方塊加以選擇。 此名稱必須與子報表中的報表參數 (而非查詢參數) 相符。  
  
5.  在 **[值]** 清單方塊中，輸入或選取要傳遞給子報表的值。 這個值可以是靜態文字，也可以是參考主報表中的欄位或其他物件的運算式。  
  
    > [!NOTE]  
    >  在報表產生器中，如果 [參數] 清單遺漏某參數，而子報表中定義了預設值，則系統會正確處理子報表。  
    >   
    >  在報表設計師中，子報表所需要的所有參數都必須包括在 **[參數]** 清單中。 如果遺漏必要的參數，子報表便無法正確顯示在主報表內。  
  
6.  重複步驟 3-5 來指定每個子報表參數的名稱和值。  
  
7.  若要刪除子報表參數，請在參數方格中按一下參數，然後按一下 **[刪除]**。  
  
8.  若要變更子報表參數的順序，請按一下參數，然後按一下向上按鈕或向下按鈕。  
  
     變更子報表參數的順序並不會影響子報表的處理。  
  
## <a name="see-also"></a>另請參閱  
 [子報表&#40;報表產生器和 SSRS&#41;](subreports-report-builder-and-ssrs.md)   
 [轉譯行為 &#40;報表產生器及 SSRS&#41;](rendering-behaviors-report-builder-and-ssrs.md)  
  
  