---
title: 建立遞迴階層群組 (報表產生器及 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 8b830ba5-4d64-4348-a2b1-76b9338a1462
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 28ccbab8475a2227dbd4dedfb0eb17bcd69dce03
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/15/2019
ms.locfileid: "56288206"
---
# <a name="create-a-recursive-hierarchy-group-report-builder-and-ssrs"></a>建立遞迴階層群組 (報表產生器及 SSRS)
  遞迴階層群組會組織包含多個階層層級之單一報表資料集內的資料，例如組織階層內經理-員工關聯性的報告結構。  
  
 您必須有單一資料集可容納所有階層式資料，而且必須有個別欄位可包含要分組的項目以及做為分組依據的項目，才能將資料表內的資料組織成遞迴階層群組。 例如，在您希望以遞迴方式將員工分組在其經理底下的資料集中，可能包含名稱、員工名稱、員工識別碼和經理識別碼。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-create-a-recursive-hierarchy-group"></a>建立遞迴階層群組  
  
1.  在 [設計] 檢視中加入資料表，並將資料集欄位拖曳至顯示。 一般來說，您想要顯示為階層的欄位會位於第一個資料行中。  
  
2.  以滑鼠右鍵按一下資料表中的任何地方，即可選取它。 [群組] 窗格會顯示選定資料表的詳細資料群組。 在 [資料列群組] 窗格中，以滑鼠右鍵按一下 [詳細資料]，然後按一下 [編輯群組]。 **[群組屬性]** 對話方塊隨即開啟。  
  
3.  在 **[群組運算式]** 中，按一下 **[加入]**。 新的資料列會出現在方格中。  
  
4.  在 [群組對象] 清單中，鍵入或選取要分組的欄位。  
  
5.  按一下 **[進階]**。  
  
6.  在 [遞迴父系] 清單中，輸入或選取要作為分組對象的欄位。  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     執行報表。 報表會顯示遞迴階層群組，但是不會有任何顯示階層的縮排  
  
### <a name="to-format-a-recursive-hierarchy-group-with-indent-levels"></a>以縮排層次格式化遞迴階層群組  
  
1.  按一下文字方塊，其中包含您想要將縮排層次加入其中以顯示階層格式的欄位。 文字方塊的屬性會顯示在 [屬性] 窗格中。  
  
    > [!NOTE]  
    >  如果看不到 [屬性] 窗格，請按一下 [檢視] 索引標籤上的 [屬性]。  
  
2.  在 [屬性] 窗格中，依序展開`Padding`節點中，按一下**左**，然後從下拉式清單中，選取**\<運算式...> >**。  
  
3.  在 [運算式] 窗格中，輸入下列運算式：  
  
     `=CStr(2 + (Level()*10)) + "pt"`  
  
     Padding 屬性全都需要 *nnyy*格式的字串，其中 *nn* 是數字，而 *yy* 是測量單位。 此範例運算式會建立一個利用 `Level` 函數的字串，以便根據遞迴層級來增加填補大小。 例如，層級 1 的資料列會產生 (2 + (1\*10))=12pt 的填補，層級 3 的資料列會產生 (2 + (3\*10))=32pt 的填補。 如需`Level`函式，請參閱 <<c2> [ 層級](report-builder-functions-level-function.md)。  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     執行報表。 報表會以階層檢視來顯示分組的資料。  
  
## <a name="see-also"></a>另請參閱  
 [建立遞迴階層群組 &#40;報表產生器及 SSRS&#41;](creating-recursive-hierarchy-groups-report-builder-and-ssrs.md)   
 [篩選、分組和排序資料 &#40;報表產生器及 SSRS&#41;](filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [彙總函式參考 &#40;報表產生器及 SSRS&#41;](report-builder-functions-aggregate-functions-reference.md)   
 [資料表 &#40;報表產生器及 SSRS&#41;](tables-report-builder-and-ssrs.md)   
 [矩陣 &#40;報表產生器及 SSRS&#41;](create-a-matrix-report-builder-and-ssrs.md)   
 [清單 &#40;報表產生器及 SSRS&#41;](create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)   
 [資料表、矩陣和清單 &#40;報表產生器及 SSRS&#41;](tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
