---
title: INDEX 命令 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 864f6fa78ab1ef23b7db3a0be4c85738b95ea72d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62471256"
---
# <a name="index-command"></a>INDEX 命令
建立索引檔案來顯示和存取資料表記錄，依照邏輯順序。  
  
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
 指定可以包含從目前資料表的欄位名稱的索引運算式。 索引運算式為基礎的索引鍵會建立在資料表中的每一筆記錄的索引檔。 Visual FoxPro 會使用這些金鑰，來顯示和存取資料表中的記錄。  
  
> [!NOTE]  
>  不過我們不建議*eExpression*也可以是記憶體變數、 陣列元素，或欄位或欄位運算式，從另一個工作區中的資料表。 附註欄位不能單獨在索引檔案運算式;它們必須結合其他字元運算式。 如果您存取索引，其中包含的變數或欄位，不再存在或找不到，則 Visual FoxPro 會產生錯誤訊息。  
  
 如果您嘗試建立索引與長度的索引鍵，則會以空格填補索引鍵。 Visual FoxPro 並不支援可變長度索引鍵。  
  
 您可建立索引鍵長度為零。 例如，索引運算式是空的備忘 欄位的子字串時，會建立零長度索引鍵。 零長度索引鍵會產生一則錯誤訊息。 當 Visual FoxPro 建立索引時，它會評估資料表中的第一個記錄中的欄位。 如果欄位是空的它可能必須在第一筆記錄，以防止某個 0 長度索引鍵欄位中輸入一些暫存的資料。  
  
 TO *IDXFileName*  
 建立.idx 索引檔案。 索引檔案指定預設延伸模組.idx。  
  
 TAG *TagName*[OF *CDXFileName*]  
 建立複合的索引檔。 是複合的索引檔是單一索引檔案，其中包含任意數目的個別標記 （索引項目）。 每個標記是由其唯一的標記名稱識別。 標記名稱必須以字母或底線開頭，且可以包含最多 10 個字母、 數字或底線的任意組合。 是複合的索引檔中的標記數目只受到可用記憶體和磁碟空間。  
  
 多個項目的複合的索引檔案都壓縮。 它不需要在建立複合的索引檔案時加入 COMPACT。 .Cdx 延伸模組提供的複合的索引檔案的名稱。  
  
 您可以建立複合的索引檔的兩種類型： 結構化及非結構性。  
  
 **結構化的複合索引檔案**您可以使用標記來建立複合的索引結構化檔案*TagName*排除選擇性 OF *CDXFileName*子句。 結構化的複合索引檔案一律具有相同的基底名稱做為資料表，並會在開啟的資料表時自動開啟。  
  
 **非結構性複合的索引檔案**您可以建立非結構性複合的索引檔案包括 OF *CDXFileName*標記之後*TagName*。 不同於結構化的複合索引檔案，非結構性複合的索引檔案必須明確開啟與 INDEX 子句中使用。  
  
 如果是複合的索引檔已建立並開啟，發出標記的索引*TagName*將標記加入至複合的索引檔案。  
  
 針對*lExpression*  
 藉此指定的條件只符合篩選條件運算式中的記錄*lExpression*可供顯示及存取權，只記錄符合篩選條件運算式的索引檔中建立索引鍵。  
  
 Visual FoxPro Rushmore 技術最佳化索引...針對*lExpression*命令，如果*lExpression*是最佳化的查詢運算式。 為了達到最佳效能，請 FOR 子句中使用最佳化的運算式。  
  
 壓縮  
 建立精簡.idx 檔案。  
  
 遞增  
 指定遞增順序.cdx 檔案。 根據預設，.cdx 標記會以遞增順序。 （您可以包含遞增索引檔案的順序來提醒）。資料表可以編製索引以反向順序包括遞減排序。  
  
 遞減  
 指定遞減順序.cdx 檔案。 建立.idx 索引檔案時，您不能包含遞減排序。  
  
 UNIQUE  
 指定只有具有特定索引鍵值所遇到的第一筆記錄，會包含在.idx 檔案或.cdx 標記。 唯一可用來防止重複的記錄顯示或存取。 加入具有重複的索引鍵的所有記錄會都排除索引檔案。 INDEX 的唯一選項等同於執行 SET UNIQUE ON 之前發行的索引。  
  
 當唯一索引或索引標籤為作用中並重複的記錄中變更其索引鍵的方式變更時，會更新索引或索引標籤。 不過下, 一個重複的記錄與原始索引鍵無法存取，或顯示，直到您重新建立索引使用索引的檔案。  
  
 候選項目  
 建立候選結構化的索引標籤。 只有在建立結構化的索引標籤; 時，才候選關鍵字可以包含否則，Visual FoxPro 會產生一則錯誤訊息。  
  
 候選索引標籤可防止重複的值中的欄位或索引運算式中指定的欄位的組合*eExpression*。 詞彙*候選*索引; 的類型是指候選索引避免重複的值，因為他們有資格加入為 「 候選 」 是主要的索引。  
  
 Visual FoxPro 會產生錯誤，如果您建立欄位或欄位的已包含重複值的組合的候選項目索引標籤。  
  
 加法類  
 保持開啟先前開啟的索引中的任何檔案。 如果您省略加法類子句，當您建立具有索引的索引檔案或資料表的檔案時，會關閉任何先前開啟的索引以外的檔案 （結構化的複合索引）。  
  
## <a name="remarks"></a>備註  
 具備索引檔資料表中的記錄會顯示，並存取索引運算式所指定的順序。 資料表中記錄的實體順序不變的索引檔案。  
  
## <a name="index-types"></a>索引類型  
 Visual FoxPro 可讓您建立兩種類型的索引檔案：  
  
-   複合.cdx 索引檔案包含多個稱為標記的索引項目  
  
-   .idx 索引檔案包含一個索引的項目  
  
 您也可以建立結構化的複合索引檔案，與資料表時，會自動開啟。  
  
> [!NOTE]  
>  開啟資料表時，會自動開啟的檔案結構複合的索引，因為它們是慣用的索引類型。  
  
 包含建立 compact.idx 索引檔案的壓縮。 複合的索引檔案都壓縮。  
  
## <a name="index-order-and-updating"></a>索引順序和更新  
 只能有一個索引的檔案 （主索引檔案） 或標記 （主要標記） 會控制資料表是顯示或存取的順序。 特定命令 （例如搜尋） 使用的主索引的檔案或標記來搜尋記錄。 不過，所有開啟.idx 和.cdx 索引檔案會更新資料表的變更。  
  
## <a name="user-defined-functions"></a>使用者定義的函式  
 雖然索引運算式可以包含使用者定義函式，則您不應該在索引運算式中使用使用者定義函式。 索引運算式中的 使用者定義函式會增加建立或更新索引花費的時間。 此外，索引可能不會進行更新的使用者定義函數是用來進行索引運算式。  
  
 如果您在索引運算式中使用的使用者定義函式，Visual FoxPro 必須找不到使用者定義函式。 當 Visual FoxPro 建立索引時，索引運算式會儲存在索引檔案，但只在使用者定義函數的參考包含在索引運算式。  
  
## <a name="see-also"></a>另請參閱  
 [ALTER TABLE-SQL 命令](../../odbc/microsoft/alter-table-sql-command.md)   
 [DELETE TAG 命令](../../odbc/microsoft/delete-tag-command.md)   
 [SET COLLATE 命令](../../odbc/microsoft/set-collate-command.md)   
 [SET UNIQUE 命令](../../odbc/microsoft/set-unique-command.md)
