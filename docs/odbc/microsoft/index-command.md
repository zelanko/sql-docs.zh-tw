---
description: INDEX 命令
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
ms.openlocfilehash: ec9ed3c0ec0e91f3c4fd3a0019c8ac463a8620c2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88449520"
---
# <a name="index-command"></a>INDEX 命令
建立索引檔，以邏輯順序顯示及存取資料表記錄。  
  
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
 指定索引運算式，其中可包含欄位名稱或目前資料表中的欄位。 系統會在資料表中每一筆記錄的索引檔中，建立以索引運算式為基礎的索引鍵。 Visual FoxPro 會使用這些索引鍵來顯示及存取資料表中的記錄。  
  
> [!NOTE]  
>  雖然不建議，但 *eExpression* 也可以是記憶體變數、陣列元素，或是來自另一個工作區中之資料表的欄位或欄位運算式。 在索引檔運算式中不能單獨使用備忘錄欄位;它們必須與其他字元運算式結合。 如果您存取的索引中包含的變數或欄位不存在或找不到，則 Visual FoxPro 會產生錯誤訊息。  
  
 如果您嘗試使用長度不同的索引鍵來建立索引，則會以空格填補該索引鍵。 Visual FoxPro 不支援可變長度的索引鍵。  
  
 您可以建立長度為零的索引鍵。 例如，當索引運算式是空白備忘錄欄位的子字串時，就會建立長度為零的索引鍵。 長度為零的索引鍵會產生錯誤訊息。 當 Visual FoxPro 建立索引時，它會評估資料表中第一筆記錄的欄位。 如果欄位是空的，可能需要在第一筆記錄的欄位中輸入一些暫存資料，以避免使用0長度的索引鍵。  
  
 *IDXFileName*  
 建立 idx 索引檔。 索引檔會指定預設副檔名。 idx。  
  
 標記 *TagName*[of *CDXFileName*]  
 建立複合索引檔案。 複合索引檔案是單一索引檔案，其中包含)  (索引項目的任意數目的個別標記。 每個標記都是由其唯一的標記名稱來識別。 標籤名稱必須以字母或底線開頭，且最多可包含10個字母、數位或底線的任意組合。 複合索引檔案中的標記數目只受限於可用的記憶體和磁碟空間。  
  
 多個輸入的複合索引檔案一律為 compact。 建立複合索引檔案時，不需要包含 COMPACT。 複合索引檔案的名稱會指定 cdx 副檔名。  
  
 您可以建立兩種類型的複合索引檔案：結構化和 nonstructural。  
  
 **結構化複合索引**檔案您可以排除選擇性的*CDXFileName*子句，以建立具有標記*TagName*的結構化複合索引檔案。 結構化複合索引檔案一律具有和資料表相同的基底名稱，而且會在開啟資料表時自動開啟。  
  
 **Nonstructural 複合索引**檔案您可以*在標記標記*之後包含*CDXFileName* ，以建立 nonstructural 複合索引檔案。 不同于結構化複合索引檔案，必須使用使用中的 INDEX 子句來明確開啟 nonstructural 複合索引檔案。  
  
 如果已建立並開啟複合索引檔案，則發行具有標記 *TagName* 的索引會將標記新增至複合索引檔案。  
  
 針對 *lExpression*  
 指定條件，其中只會顯示符合篩選運算式 *lExpression* 的記錄，以供顯示及存取;只有符合篩選條件運算式的記錄，才會在索引檔中建立索引鍵。  
  
 Visual FoxPro Rushmore 技術會將索引優化 .。。如果*lExpression*是可優化的運算式，則為*lExpression*命令。 為了達到最佳效能，請在 FOR 子句中使用可優化的運算式。  
  
 緊湊  
 建立 compact 檔。  
  
 上升  
 指定 cdx 檔案的遞增順序。 依預設，會以遞增順序建立 cdx 標記。  (您可以將遞增的形式包含在索引檔的順序中 ) 。您可以在資料表中包含遞減的方式，以相反的順序來編制資料表的索引。  
  
 降  
 指定 cdx 檔案的遞減順序。 建立時，您不能包含遞減。  
  
 UNIQUE  
 指定只有使用特定索引鍵值所遇到的第一個記錄會包含在 idx 檔案或 cdx 標記中。 UNIQUE 可以用來防止顯示或存取重複的記錄。 以重複的索引鍵加入的所有記錄都會從索引檔中排除。 使用 INDEX 的 UNIQUE 選項等同于發出索引或重新索引之前，在上執行 SET UNIQUE。  
  
 當唯一索引或索引標記為使用中，且重複的記錄變更其索引鍵的方式變更時，就會更新索引或索引標記。 不過，在您使用重新索引編制檔案的索引之前，無法存取或顯示下一個具有原始索引鍵的重複記錄。  
  
 候選人  
 建立候選的結構化索引標記。 只有在建立結構化索引標記時，才可以包含候選關鍵字;否則，Visual FoxPro 會產生錯誤訊息。  
  
 候選索引標記可防止在索引運算式 *eExpression*中指定的欄位或欄位組合中出現重複的值。 *候選*詞彙指的是索引的類型;因為候選索引會防止重複的值，所以會將其作為主要索引的「候選」。  
  
 如果您為已包含重複值的欄位或欄位組合建立候選索引標記，Visual FoxPro 會產生錯誤。  
  
 添加劑  
 保持開啟任何先前開啟的索引檔案。 如果您在為具有索引的資料表建立索引檔或檔案時省略加法子句，則任何先前開啟的索引檔 (除了結構化複合索引) 關閉之外。  
  
## <a name="remarks"></a>備註  
 具有索引檔的資料表中的記錄會以索引運算式所指定的順序顯示和存取。 索引檔案不會變更資料表中記錄的實體順序。  
  
## <a name="index-types"></a>索引類型  
 Visual FoxPro 可讓您建立兩種類型的索引檔案：  
  
-   Cdx 包含多個索引項目的索引檔案，稱為標記  
  
-   。 idx 包含一個索引項目的索引檔  
  
 您也可以建立結構化複合索引檔案，此檔案會自動以資料表開啟。  
  
> [!NOTE]  
>  當資料表開啟時，會自動開啟結構化複合索引檔案，因此是慣用的索引類型。  
  
 包含 COMPACT 以建立 compact. idx index 檔。 複合索引檔案一律為 compact。  
  
## <a name="index-order-and-updating"></a>索引順序和更新  
 只有一個索引檔案 (主要索引檔) 或標記 (主要標籤) 控制顯示或存取資料表的順序。 某些命令 (搜尋，例如) 使用主要索引檔或標記來搜尋記錄。 不過，在變更資料表時，所有開啟的. idx 和. cdx 索引檔案都會更新。  
  
## <a name="user-defined-functions"></a>使用者定義的函式  
 雖然索引運算式可以包含使用者定義函數，但您不應該在索引運算式中使用使用者定義函數。 索引運算式中的使用者定義函數會增加建立或更新索引所需的時間。 此外，當索引運算式使用使用者自訂函數時，可能不會發生索引更新。  
  
 如果您在索引運算式中使用使用者定義函數，Visual FoxPro 必須能夠找到使用者定義函數。 當 Visual FoxPro 建立索引時，索引運算式會儲存在索引檔中，但是索引運算式中只會包含使用者定義函數的參考。  
  
## <a name="see-also"></a>另請參閱  
 [ALTER TABLE-SQL 命令](../../odbc/microsoft/alter-table-sql-command.md)   
 [刪除標記命令](../../odbc/microsoft/delete-tag-command.md)   
 [SET COLLATE 命令](../../odbc/microsoft/set-collate-command.md)   
 [SET UNIQUE 命令](../../odbc/microsoft/set-unique-command.md)
