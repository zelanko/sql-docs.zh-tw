---
title: 快速監看式對話方塊
ms.prod: sql
ms.technology: scripting
ms.topic: conceptual
f1_keywords:
- vs.debug.quickwatch
helpviewer_keywords:
- QuickWatch Dialog [Transact-SQL]
ms.assetid: d6bbb373-1452-41f2-bdc5-86ae689c3dc0
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: ''
ms.date: 03/14/2017
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: af12ca6fb0b8eb0b4461d95e75e8c1a3c62ed77e
ms.sourcegitcommit: add39e028e919df7d801e8b6bb4f8ac877e60e17
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/15/2019
ms.locfileid: "74119244"
---
# <a name="transact-sql-debugger---quickwatch-dialog-box"></a>Transact-SQL 偵錯工具 - 快速監看式對話方塊

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

使用 [快速監看式]  對話方塊可在偵錯 [!INCLUDE[tsql](../../includes/tsql-md.md)] 程式碼時，快速檢視一個 [!INCLUDE[tsql](../../includes/tsql-md.md)] 運算式的資料類型和值，例如變數或參數。 若要監看多個運算式，您也可以將此運算式加入到 [監看式]  視窗。  

[!INCLUDE[ssms-old-versions](../../includes/ssms-old-versions.md)]

## <a name="task-list"></a>工作清單

 **存取快速監看式對話方塊**  
  
-   按一下 [偵錯]  功能表上的 [快速監看式]  。  
  
 **檢視有關運算式的資訊**  
  
1.  在 [運算式]  中，輸入或選取您想要的運算式。 以下為支援的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 運算式：  
  
    -   變數。  
  
    -   參數。  
  
    -   名稱開頭為 @@ 的系統函式。  
  
    -   透過將運算子套用至一或多個變數、參數或系統函式 (例如 @IntegerCounter + 1 或 FirstName + LastName) 的方式建立的運算式。  
  
    -   傳回單一值的 Transact-SQL 陳述式，例如：SELECT CharacterCol FROM MyTable WHERE PrimaryKey = 1。  
  
2.  按一下 [重新評估]  。  
  
 **將快速監看式運算式加入至監看式視窗**  
  
-   按一下 [加入監看式]  。  
  
 **變更快速監看式運算式的值**  
  
-   以滑鼠右鍵按一下運算式，然後選取 [編輯值]  。  
  
## <a name="options"></a>選項。  
 **運算式清單**  
 顯示目前選取的運算式。 此下拉式清單包含您可以選擇顯示的一組運算式。 此清單中的運算式就是目前在 [呼叫堆疊]  視窗內選取之堆疊框架範圍內提供的運算式。 若要顯示不同的運算式，請輸入運算式或是從清單中選取。 [!INCLUDE[tsql](../../includes/tsql-md.md)] 偵錯工具支援以下運算式：名稱以 @@ 開頭的變數、參數和系統函式。  
  
 **值格線**  
 顯示目前所監看之運算式的屬性。  
  
 **名稱**  
 正在監看的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 運算式。  
  
 **ReplTest1**  
 顯示目前指派給運算式的值。 當運算式目前沒有任何值時會顯示空白。  
  
 如果運算式的長度超過 **[值]** 資料行的寬度，當您將指標放在該運算式的 **[值]** 資料格上方時，工具提示會顯示完整的值。  
  
 **[值]** 資料格內的放大鏡圖示表示可使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 偵錯工具視覺化檢視。 在此清單中，您可以指定 **[文字視覺化檢視]** 、 **[XML 視覺化檢視]** 或 **[HTML 視覺化檢視]** 。 若要啟動偵錯工具視覺化檢視，請按一下放大鏡圖示。 [!INCLUDE[tsql](../../includes/tsql-md.md)] 偵錯工具會開啟一個對話方塊，其中會以對資料類型適合的格式顯示資料。  
  
 **型別**  
 顯示此運算式的資料類型。  
  
## <a name="see-also"></a>另請參閱  
 [Transact-SQL 偵錯工具](../../relational-databases/scripting/transact-sql-debugger.md)   
 [Transact-SQL 偵錯工具資訊](../../relational-databases/scripting/transact-sql-debugger-information.md)   
 [監看式視窗](../../relational-databases/scripting/transact-sql-debugger-watch-window.md)   
 [本機視窗](../../relational-databases/scripting/transact-sql-debugger-locals-window.md)   
 [呼叫堆疊視窗](../../relational-databases/scripting/transact-sql-debugger-call-stack-window.md)   
 [運算式 &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)  
  
  
