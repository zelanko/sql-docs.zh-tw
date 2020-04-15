---
title: INDEX 指令 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- index command [ODBC]
ms.assetid: 694e8cf5-2f69-4001-9c1e-b735a4da3aff
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bcb30a49cb9f11ddd4c61621116aa4bd8ddcf186
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300028"
---
# <a name="index-command"></a>INDEX 命令
建立索引檔以按邏輯順序顯示和訪問表記錄。  
  
## <a name="syntax"></a>語法  
  
```  
  
INDEX ON eExpression TO IDXFileName | TAG TagName [OF CDXFileName]  
   [FOR lExpression]  
   [COMPACT]  
   [ASCENDING | DESCENDING]  
   [UNIQUE | CANDIDATE]  
   [ADDITIVE]  
```  
  
## <a name="arguments"></a>引數  
 *e運算式*  
 指定索引表示式,該表示式可以包含當前表中的欄位或欄位的名稱。 在表中每個記錄的索引檔中創建基於索引表達式的索引鍵。 Visual FoxPro 使用這些鍵來顯示和訪問表中的記錄。  
  
> [!NOTE]  
>  儘管不推薦*eExpression,* 但也可以是記憶體變數、陣列元素或來自另一個工作區表中的字段或欄位表達式。 備忘錄欄位不能單獨用於索引檔運算式;因此,在索引檔表達式中,不能單獨使用備忘錄欄位。它們必須與其他字元表達式組合。 如果您造訪包含不再存在或找不到的變數或欄位的索引,Visual FoxPro 將生成錯誤訊息。  
  
 如果嘗試使用長度不同的鍵生成索引,則該鍵將填充空格。 Visual FoxPro 不支援可變長度索引鍵。  
  
 可以創建長度為零的索引鍵。 例如,當索引表達式是空備忘錄欄位的子字串時,將創建零長度索引鍵。 零長度索引鍵生成錯誤消息。 當 Visual FoxPro 創建索引時,它會評估表中第一條記錄中的欄位。 如果欄位為空,則可能需要在第一個記錄中的欄位中輸入一些臨時數據,以防止 0 長索引鍵。  
  
 在*IDX 檔名*  
 建立 .idx 索引檔。 索引檔為預設副檔名 .idx 指定。  
  
 *標籤標籤名稱* *[CDX 檔案名稱 ]*  
 創建複合索引檔。 複合索引檔是一個索引檔,由任意數量的單獨的標記(索引條目)組成。 每個標記都由其唯一的標記名稱標識。 標記名稱必須以字母或下劃線開頭,並且可以由最多 10 個字母、數位或下劃線組成的任意組合組成。 複合索引檔中的標記數僅受可用記憶體和磁碟空間的限制。  
  
 多條目複合索引文件始終緊湊。 創建複合索引檔時,無需包括 COMPACT。 複合索引檔的名稱為 .cdx 副檔名。  
  
 可以創建兩種類型的複合索引檔:結構和非結構。  
  
 **結構複合索引檔案**您可以透過排除可選取的 OF *CDXFileName*子句來建立帶有*TAG Name*的結構複合索引檔。 結構複合索引文件始終與表具有相同的基本名稱,並在打開表時自動打開。  
  
 **非結構複合索引檔案**您可以透過在 TAG *TagName*後包括 OF *CDXFileName*來建立非結構複合索引檔。 與結構複合索引檔不同,非結構複合索引檔必須使用 USE 中的 INDEX 子句顯式打開。  
  
 如果已建立並打開複合索引檔,則使用*TAG TagName*發出 INDEX 會向複合索引檔添加標記。  
  
 對*l 表示式*  
 指定一個條件,即只有滿足篩選器運算式*lExpression*的記錄才能顯示和訪問;索引鍵在索引檔中只為與篩選器表達式匹配的記錄創建。  
  
 可視化福克斯Pro拉什莫爾技術優化INDEX...對於*lExpression 命令*(如果*lExpression*是可優化的運算式)。 為獲得最佳性能,請使用 FOR 子句中的可優化運算式。  
  
 緊湊  
 建立緊湊的 .idx 檔。  
  
 上升  
 指定 .cdx 檔案的升序。 預設情況下,.cdx 標記按升序創建。 (您可以包括 ASCENDING 作為索引檔訂單的提醒。可以通過包括降序,以相反的順序對表進行索引。  
  
 降  
 指定 .cdx 檔案的降序。 創建 .idx 索引檔時,不能包括降序。  
  
 UNIQUE  
 指定僅在 .idx 檔或 .cdx 標記中包含與特定索引鍵值遇到的第一個記錄。 UNIQUE 可用於防止顯示或造訪重複記錄。 使用重複索引鍵添加的所有記錄都從索引檔中排除。 使用 INDEX 的「唯一」選項與在發出 INDEX 或 REINDEX 之前執行 SET UNIQUE ON 相同。  
  
 當 UNIQUE 索引或索引標記處於活動狀態,並且重複記錄以更改其索引鍵的方式更改時,將更新索引或索引標記。 但是,在使用 REINDEX 重新索引檔之前,無法訪問或顯示具有原始索引鍵的下一個重複記錄。  
  
 候選人  
 創建候選結構索引標記。 僅當創建結構索引標記時,才能包含候選關鍵字;否則,Visual FoxPro 會生成錯誤消息。  
  
 候選索引標記可防止欄位中重複的值或索引*運算式 eExpression*中指定的欄位的組合。 術語 *「候選」* 是指索引的類型;由於候選索引可防止重複值,因此它們有資格作為"候選"作為主索引。  
  
 如果為欄位或已包含重複值的欄位組合創建候選索引標記,則 Visual FoxPro 將生成錯誤。  
  
 新增劑  
 保持打開任何以前打開的索引檔。 如果在為索引檔或具有 INDEX 的表建立索引檔時省略了 ADDITIVE 子句,則關閉以前打開的任何索引檔(結構複合索引除外)。  
  
## <a name="remarks"></a>備註  
 具有索引檔的表中的記錄按索引表達式指定的順序顯示和訪問。 索引檔不會更改表中記錄的物理順序。  
  
## <a name="index-types"></a>索引型別  
 Visual FoxPro 允許您建立兩種類型的索引檔:  
  
-   包含多個稱為標記的索引項目的複合 .cdx 索引檔  
  
-   .idx 索引檔包含索引項目  
  
 您還可以創建結構複合索引檔,該檔會自動打開表。  
  
> [!NOTE]  
>  由於結構複合索引檔在打開表時會自動打開,因此它們是首選索引類型。  
  
 包括 COMPACT 以建立緊湊的 .idx 索引檔。 複合索引檔總是緊湊的。  
  
## <a name="index-order-and-updating"></a>索引順序和更新  
 只有一個索引檔(主索引檔)或標記(主標記)控制表的顯示或訪問順序。 某些命令 (例如,SEEK) 使用主索引檔或標記來搜尋記錄。 但是,所有打開的 .idx 和 .cdx 索引檔都隨著對表的更改而更新。  
  
## <a name="user-defined-functions"></a>使用者定義的函式  
 儘管索引表示式可以包含使用者定義的函數,但不應在索引運算式中使用使用者定義的函數。 索引表示式中的使用者定義的函數會增加創建或更新索引所需的時間。 此外,當使用者定義的函數用於索引表達式時,可能不會發生索引更新。  
  
 如果在索引表示式中使用使用者定義的函數,Visual FoxPro 必須能夠找到使用者定義的函數。 當 Visual FoxPro 創建索引時,索引表示式將保存在索引檔中,但索引表達式中僅包含對使用者定義的函數的引用。  
  
## <a name="see-also"></a>另請參閱  
 [變更表 - SQL 指令](../../odbc/microsoft/alter-table-sql-command.md)   
 [移除 TAG 命令](../../odbc/microsoft/delete-tag-command.md)   
 [設定隔離命令](../../odbc/microsoft/set-collate-command.md)   
 [SET UNIQUE 命令](../../odbc/microsoft/set-unique-command.md)
