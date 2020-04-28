---
title: 索引命令 |Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81300028"
---
# <a name="index-command"></a>INDEX 命令
建立索引檔，以邏輯順序顯示和存取資料表記錄。  
  
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
 指定可包含目前資料表中之欄位或欄位名稱的索引運算式。 系統會針對資料表中的每筆記錄，在索引檔案中建立以索引運算式為基礎的索引鍵。 Visual FoxPro 會使用這些索引鍵來顯示及存取資料表中的記錄。  
  
> [!NOTE]  
>  雖然不建議這麼做，但*eExpression*也可以是記憶體變數、陣列元素，或是來自另一個工作區中資料表的欄位或欄位運算式。 備忘欄位不能單獨用於索引檔運算式中;它們必須與其他字元運算式合併使用。 如果您存取的索引包含不存在或找不到的變數或欄位，Visual FoxPro 會產生錯誤訊息。  
  
 如果您嘗試使用長度不同的金鑰來建立索引，則會以空格填補金鑰。 Visual FoxPro 中不支援可變長度的索引鍵。  
  
 您可以建立長度為零的索引鍵。 例如，當索引運算式是空白備忘欄位的子字串時，就會建立長度為零的索引鍵。 長度為零的索引鍵會產生錯誤訊息。 當 Visual FoxPro 建立索引時，它會評估資料表中第一筆記錄的欄位。 如果欄位是空的，則可能需要在第一筆記錄的欄位中輸入一些暫存資料，以避免有0長度的索引鍵。  
  
 至*IDXFileName*  
 建立 idx 索引檔案。 會為索引檔案提供預設的副檔名。 idx。  
  
 標記*TagName*[of *CDXFileName*]  
 建立複合索引檔案。 複合索引檔案是由任意數目的個別標記（索引項目）所組成的單一索引檔案。 每個標記都是由其唯一的標記名稱所識別。 標記名稱的開頭必須是字母或底線，而且可以包含最多10個字母、數位或底線的任意組合。 複合索引檔案中的標記數目僅受限於可用的記憶體和磁碟空間。  
  
 多個專案的複合索引檔案一律為 compact。 建立複合索引檔案時，不需要包含 COMPACT。 複合索引檔案的名稱會指定 cdx 副檔名。  
  
 可以建立兩種類型的複合索引檔案：結構化和 nonstructural。  
  
 **結構化複合索引**檔案您可以排除選擇性的*CDXFileName*子句，以建立具有標記*TagName*的結構化複合索引檔案。 結構化複合索引檔案一律具有與資料表相同的基底名稱，而且會在開啟資料表時自動開啟。  
  
 **Nonstructural 複合索引**檔案您可以在標記*TagName*之後包含*CDXFileName* ，藉以建立 nonstructural 複合索引檔案。 不同于結構化複合索引檔案，必須以使用中的索引子句明確開啟 nonstructural 複合索引檔案。  
  
 如果已建立並開啟複合索引檔案，發出具有標記*TagName*的索引，就會將標記加入至複合索引檔案。  
  
 針對*lExpression*  
 指定條件，其中只有滿足篩選運算式*lExpression*的記錄可供顯示和存取;只有符合篩選條件運算式的記錄，才會在索引檔案中建立索引鍵。  
  
 Visual FoxPro Rushmore 技術優化索引 .。。如果*lExpression*是可優化的運算式，則為*lExpression*命令。 為了達到最佳效能，請使用 FOR 子句中的可優化運算式。  
  
 小巧  
 建立 compact 的 idx 檔案。  
  
 排序  
 指定 cdx 檔案的遞增順序。 根據預設，會以遞增順序建立 cdx 標記。 （您可以包含遞增的，以提醒您索引檔案的順序）。資料表可以藉由包含遞減的順序，以反向的方式編制索引。  
  
 遞減  
 指定 cdx 檔案的遞減順序。 建立 idx 索引檔案時，您不能包含遞減。  
  
 UNIQUE  
 指定只包含特定索引鍵值的第一筆記錄會包含在 idx 檔案或 cdx 標記中。 UNIQUE 可以用來防止顯示或存取重複的記錄。 以重複的索引鍵新增的所有記錄都會從索引檔中排除。 在發出索引或重新索引之前，使用 INDEX 的 UNIQUE 選項等同于執行 SET UNIQUE。  
  
 當唯一索引或索引標籤為使用中，且重複的記錄變更為其索引鍵的方式時，就會更新索引或索引標記。 不過，在您使用重新索引重新編制檔案索引之前，無法存取或顯示具有原始索引鍵的下一個重複記錄。  
  
 適用  
 建立候選結構索引標記。 只有在建立結構化索引標記時，才可以包含候選關鍵字;否則，Visual FoxPro 會產生錯誤訊息。  
  
 候選索引標記可防止在索引運算式*eExpression*中指定的欄位或欄位組合中出現重複的值。 *候選*詞彙是指索引的類型;因為候選索引會防止重複的值，所以它們會以「候選」的形式限定為主要索引。  
  
 如果您為已包含重複值的欄位或欄位組合建立候選索引標籤，Visual FoxPro 會產生錯誤。  
  
 附加  
 保持開啟任何先前開啟的索引檔案。 如果您在建立索引檔案或具有索引之資料表的檔案時省略加法類子句，任何先前開啟的索引檔案（結構化複合索引除外）都會關閉。  
  
## <a name="remarks"></a>備註  
 具有索引檔案之資料表中的記錄會以索引運算式所指定的順序顯示和存取。 索引檔案不會變更資料表中記錄的實體順序。  
  
## <a name="index-types"></a>索引類型  
 Visual FoxPro 可讓您建立兩種類型的索引檔案：  
  
-   Cdx 索引檔案包含多個稱為標記的索引項目  
  
-   。 idx 包含一個索引項目的索引檔  
  
 您也可以建立具有資料表自動開啟的結構化複合索引檔案。  
  
> [!NOTE]  
>  因為結構化複合索引檔案會在開啟資料表時自動開啟，所以它們是慣用的索引類型。  
  
 包含 COMPACT 以建立 compact. idx 索引檔案。 複合索引檔案一律為 compact。  
  
## <a name="index-order-and-updating"></a>索引順序和更新  
 只有一個索引檔案（主要索引檔案）或標記（主要標記）會控制資料表的顯示或存取順序。 某些命令（例如，搜尋）會使用主要索引檔案或標記來搜尋記錄。 不過，當對資料表進行變更時，所有開啟的. idx 和. cdx 索引檔案都會更新。  
  
## <a name="user-defined-functions"></a>使用者定義的函式  
 雖然索引運算式可以包含使用者自訂函數，但您不應該在索引運算式中使用使用者自訂函數。 索引運算式中的使用者定義函數會增加建立或更新索引所花費的時間。 此外，將使用者自訂函數用於索引運算式時，可能不會進行索引更新。  
  
 如果您在索引運算式中使用使用者定義函數，Visual FoxPro 必須能夠找到使用者定義函數。 當 Visual FoxPro 建立索引時，索引運算式會儲存在索引檔案中，但是索引運算式中只會包含使用者定義函數的參考。  
  
## <a name="see-also"></a>另請參閱  
 [ALTER TABLE-SQL 命令](../../odbc/microsoft/alter-table-sql-command.md)   
 [DELETE TAG 命令](../../odbc/microsoft/delete-tag-command.md)   
 [SET COLLATE 命令](../../odbc/microsoft/set-collate-command.md)   
 [SET UNIQUE 命令](../../odbc/microsoft/set-unique-command.md)
