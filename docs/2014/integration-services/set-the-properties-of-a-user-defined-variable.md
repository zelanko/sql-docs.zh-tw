---
title: 設定使用者定義變數的屬性 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- modifying variables
- variables [Integration Services], properties
ms.assetid: f98ddbec-f668-4dba-a768-44ac3ae0536f
caps.latest.revision: 26
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 526a5fef8883d34c281ee6c1cec51d29a6b9508c
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37331872"
---
# <a name="set-the-properties-of-a-user-defined-variable"></a>設定使用者定義變數的屬性
  若要在 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 中設定使用者定義變數的屬性，您可以使用下列其中一項功能：  
  
-   [變數] 視窗。  
  
-   [屬性] 視窗。 [屬性] 視窗會列出屬性，以供您設定 [變數] 視窗中無法使用的變數：Description、EvaluateAsExpression、Expression、ReadOnly、ValueType 和 IncludeInDebugDump。  
  
> [!NOTE]  
>  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 也提供一組無法更新屬性的系統變數，但屬性 RaiseChangedEvent 除外。  
  
 **在變數上設定運算式**  
  
 當您使用 [屬性] 視窗設定使用者定義變數的運算式時：  
  
-   變數的值可以由 Value 或 Expression 屬性設定。 根據預設，EvaluateAsExpression 屬性會設定為`False`和 Value 屬性會設定變數的值。 若要使用運算式來設定值，您必須先將 EvaluateAsExpression `True`，然後提供 [運算式] 屬性中的運算式。 Value 屬性會自動設為運算式的評估結果。  
  
-   ValueType 屬性包含 Value 屬性中之值的資料類型。 運算式設定 Value 之後，ValueType 就會自動更新為與運算式之評估結果相容的資料類型。 例如，如果 Value 包含 0 且 ValueType 屬性包含**Int32** ，則設 getdate （） 的運算式值包含目前日期和時間，ValueType 會設為`DateTime`。  
  
-   透過變數的 [屬性] 視窗，可以存取 [運算式產生器] 對話方塊。 您可使用此工具建立、驗證和評估運算式。 如需詳細資訊，請參閱[運算式產生器](expressions/expression-builder.md)和 [Integration Services &#40;SSIS&#41; 運算式](expressions/integration-services-ssis-expressions.md)。  
  
 當您使用 [變數] 視窗設定使用者定義變數的運算式時：  
  
-   若要使用運算式設定變數的值，先確認變數資料類型是否與運算式的評估結果相容，然後提供中的運算式`Expression`資料行**變數**視窗。 中的 EvaluateAsExpression 屬性**屬性** 視窗會自動設為`True`。  
  
-   當您將運算式指派給變數時，會在變數旁邊顯示特殊圖示標記。 此特殊圖示標記也會顯示在已經設定運算式的連接管理員及工作旁邊。  
  
-   透過變數的 [變數] 視窗，可以存取 [運算式產生器] 對話方塊。 您可使用此工具建立、驗證和評估運算式。 如需詳細資訊，請參閱[運算式產生器](expressions/expression-builder.md)和 [Integration Services &#40;SSIS&#41; 運算式](expressions/integration-services-ssis-expressions.md)。  
  
 在這兩**變數**並**屬性**視窗中，如果您將運算式指派給變數，並`EvaluateAsExpression`設為`True`，您無法變更變數資料類型。  
  
 **設定命名空間和名稱屬性**  
  
 值`Name`和`Namespace`Unicode Standard 2.0 或底線 (_) 所定義的屬性必須以字母字元開頭。 後續的字元可以是 Unicode Standard 2.0 中定義的字母或數字，或是底線 (\_)。  
  
## <a name="using-the-variables-window-to-set-properties"></a>使用變數視窗來設定屬性  
  
#### <a name="to-set-the-properties-of-a-variable-by-using-the-variables-window"></a>使用變數視窗來設定變數的屬性  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，開啟包含所需封裝的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案。  
  
2.  在 [方案總管] 中，以滑鼠右鍵按一下封裝將其開啟。  
  
3.  在 **[SSIS]** 功能表上，按一下 **變數**。  
  
     您可以將 View.Variables 命令對應到您在 [選項] 對話方塊的 [鍵盤] 頁面中所選擇的組合鍵，以選擇性地顯示 [變數] 視窗。  
  
4.  選擇性地在 [變數] 視窗中按一下 [方格選項]，然後選取要在 [變數] 視窗中顯示的資料行，並選取要套用到此變數清單的篩選。  
  
5.  在清單中，選取變數，然後再更新中的值`Name`，**資料類型**， `Value`， `Namespace`，**引發變更事件**，**描述 」、 「** 和`Expression`資料行。  
  
6.  選擇清單中的變數，然後按一下 [移動變數] 以變更範圍。  
  
7.  若要儲存已更新的封裝，請按一下 [檔案] 功能表上的 [儲存選取項目]。  
  
## <a name="using-the-properties-window-to-set-properties"></a>使用屬性視窗來設定屬性  
  
#### <a name="to-set-the-properties-of-a-variable-by-using-the-properties-window"></a>使用屬性視窗來設定變數的屬性  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，開啟包含所需封裝的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案。  
  
2.  在 [方案總管] 中，以滑鼠右鍵按一下封裝將其開啟。  
  
3.  在 [檢視]  功能表上，按一下 [屬性視窗] 。  
  
4.  在 [!INCLUDE[ssIS](../includes/ssis-md.md)] 設計師中，按一下 [封裝總管] 索引標籤，並展開 [封裝] 節點。  
  
5.  若要修改具有封裝範圍的變數，請展開 [變數] 節點；否則，展開 [事件處理常式] 或 [可執行檔] 節點，直到找到包含想要修改之變數的 [變數] 節點為止。  
  
6.  按一下想要修改其屬性的變數。  
  
7.  在 [屬性] 視窗中，更新讀取/寫入變數屬性。 有些使用者自訂變數的屬性為讀取/唯讀。  
  
     如需屬性的詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 變數](integration-services-ssis-variables.md)。  
  
8.  若要儲存已更新的封裝，請按一下 [檔案] 功能表上的 [儲存選取項目]。  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services &#40;SSIS&#41;變數](integration-services-ssis-variables.md)   
 [在封裝中使用變數](../../2014/integration-services/use-variables-in-packages.md)   
 [新增、刪除、變更套件中使用者定義變數的範圍](../../2014/integration-services/add-delete-change-scope-of-user-defined-variable-in-a-package.md)  
  
  
