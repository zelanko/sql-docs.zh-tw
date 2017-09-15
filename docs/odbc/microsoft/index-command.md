---
title: "INDEX 命令 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- index command [ODBC]
ms.assetid: 694e8cf5-2f69-4001-9c1e-b735a4da3aff
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: cdec619d99c610c75b9b27de710cd4e5913602f6
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="index-command"></a>INDEX 命令
建立索引來顯示和存取資料表會依照邏輯順序記錄檔。  
  
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
 *eExpression*  
 指定索引運算式可包含的欄位或欄位，從目前的資料表名稱。 索引運算式為基礎的索引鍵資料表中的每一筆記錄的索引檔中建立。 Visual FoxPro 會使用這些金鑰，來顯示和存取資料表中的記錄。  
  
> [!NOTE]  
>  雖然不建議這樣做， *eExpression*也可以是記憶體變數、 陣列元素，或欄位或欄位運算式，從另一個工作區中的資料表。 附註欄位不能單獨在索引檔案的運算式。它們必須結合其他字元運算式。 如果您存取包含變數或確實不存在或找不到欄位的索引時，Visual FoxPro 會產生錯誤訊息。  
  
 如果您嘗試建立索引具有索引鍵的長度不同，則會以空格填補索引鍵。 Visual FoxPro 不支援可變長度索引鍵。  
  
 您可建立索引鍵長度為零。 例如，零長度索引鍵被建立時索引運算式是空的備忘 欄位的子字串。 零長度索引鍵會產生錯誤訊息。 當 Visual FoxPro 建立索引時，它會評估資料表中的第一個記錄中的欄位。 如果欄位是空的它可能需要在第一筆記錄，以防止 0 長度索引鍵中的欄位中輸入一些暫存資料。  
  
 若要*IDXFileName*  
 建立.idx 索引檔。 預設副檔名.idx 會是提供索引檔案。  
  
 標記*TagName*[OF *CDXFileName*]  
 建立複合的索引檔。 複合索引檔案是單一索引檔案包含任意數目的個別標記 （索引項目）。 依其唯一的標記名稱識別每個標記。 標記名稱必須以字母或底線開頭，且可包含數最多 10 個字母、 數字或底線的任何組合。 複合的索引檔中的標記數目只受到可用記憶體和磁碟空間。  
  
 多個項目複合索引檔案一律會壓縮。 不需要時建立複合的索引檔案包含壓縮。 .Cdx 延伸模組提供複合的索引檔案的名稱。  
  
 您可以建立複合的索引檔案的兩個類型： 結構化及非結構性。  
  
 **結構化的複合索引檔案**您可以使用標記建立複合的索引結構化檔案*TagName*排除選擇性 OF *CDXFileName*子句。 結構化的複合索引檔案一律具有相同的基底名稱做為資料表，並開啟資料表時就會自動開啟。  
  
 **非結構性複合的索引檔案**您可以建立非結構性複合的索引檔案所包含的*CDXFileName*標記之後*TagName*。 不同於複合的索引結構的檔案，結構性複合的索引檔案必須明確地開啟索引中的子句使用。  
  
 如果是複合的索引檔已建立並開啟，發行索引標籤*TagName*將標記加入至複合的索引檔。  
  
 如*lExpression*  
 讓指定的條件滿足篩選條件運算式的記錄*lExpression*可供顯示及存取; 只記錄符合篩選條件運算式的索引檔中建立索引鍵。  
  
 Visual FoxPro Rushmore 技術最佳化索引...如*lExpression*命令如果*lExpression*是最佳化的查詢運算式。 為了達到最佳效能，請 FOR 子句中使用最佳化的運算式。  
  
 壓縮  
 建立精簡.idx 檔案。  
  
 遞增  
 指定.cdx 檔案以遞增的順序。 根據預設，會建立.cdx 標記，以遞增順序。 （您可以包括遞增提醒您的索引檔案的順序）。資料表可以包含遞減以反向順序進行索引。  
  
 遞減  
 指定遞減順序.cdx 檔案。 建立.idx 索引檔案時，您不能包含遞減。  
  
 UNIQUE  
 指定在.idx 檔案或.cdx 標記包含只具有特定索引鍵值所遇到的第一個記錄。 唯一可以用來防止重複的記錄顯示或存取。 加入具有重複的索引鍵的所有記錄都排除索引檔案。 INDEX 的唯一選項等同於發出重新索引之前執行 SET UNIQUE ON。  
  
 當唯一索引或索引標籤為作用中，重複的記錄中變更其索引鍵的方式變更時就會更新索引或索引標籤。 不過下, 一個重複的記錄與原始索引鍵無法存取，或顯示，直到您重新建立索引使用重新索引的檔案。  
  
 候選項目  
 建立候選結構索引標籤。 候選關鍵字可以包含建立結構的索引標籤; 時，才否則，Visual FoxPro 會產生錯誤訊息。  
  
 候選索引標籤可防止重複的值中的欄位或欄位索引運算式中指定的組合*eExpression*。 詞彙*候選*索引; 的類型是指候選索引會防止重複的值，因為他們有資格加入 」 的候選項目 」 是主要的索引。  
  
 Visual FoxPro 會產生錯誤，如果您建立候選索引標籤之欄位或欄位的已包含重複值的組合。  
  
 加法類  
 保持開啟的任何先前開啟的索引檔。 如果您省略 ADDITIVE 子句的索引建立索引的檔案或資料表的檔案時，會關閉任何先前開啟的索引以外的檔案 （結構化的複合索引）。  
  
## <a name="remarks"></a>備註  
 具備索引檔資料表中的記錄會顯示，而且索引運算式所指定的順序存取。 資料表中記錄的實體順序不會變更的索引檔案。  
  
## <a name="index-types"></a>索引類型  
 Visual FoxPro 可讓您建立兩種類型的索引檔案：  
  
-   複合.cdx 索引檔案包含多個稱為標籤的索引項目  
  
-   .idx 索引檔案包含一個索引項目  
  
 您也可以建立結構化的複合索引檔案，與資料表時，會自動開啟。  
  
> [!NOTE]  
>  開啟資料表時，會自動開啟的檔案結構複合的索引，因為它們是慣用的索引類型。  
  
 包含建立 compact.idx 索引檔案的壓縮。 複合索引檔案一律會壓縮。  
  
## <a name="index-order-and-updating"></a>索引順序及更新  
 只能有一個索引檔案 （主索引檔案） 或標記 （主要標記） 來控制資料表是顯示或存取的順序。 某些命令 （例如搜尋） 會使用標記的主索引的檔案搜尋記錄。 不過，所有開啟.idx，並且隨著資料表的變更更新.cdx 索引檔案。  
  
## <a name="user-defined-functions"></a>使用者定義的函式  
 雖然索引運算式可以包含使用者定義函式，則您不應該在索引運算式中使用使用者定義函數。 索引運算式中的使用者定義函數會增加建立或更新索引所需的時間。 此外，索引可能不會進行更新的使用者定義函數是用來進行索引運算式。  
  
 如果您在索引運算式中使用的使用者定義函式，Visual FoxPro 必須能夠找出在使用者定義函數。 當 Visual FoxPro 建立索引時，索引運算式會儲存在索引檔案，但只在使用者定義函數的參考包含在索引運算式。  
  
## <a name="see-also"></a>另請參閱  
 [ALTER TABLE 的 SQL 命令](../../odbc/microsoft/alter-table-sql-command.md)   
 [刪除標記命令](../../odbc/microsoft/delete-tag-command.md)   
 [SET COLLATE 命令](../../odbc/microsoft/set-collate-command.md)   
 [SET 唯一命令](../../odbc/microsoft/set-unique-command.md)
