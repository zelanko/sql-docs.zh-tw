---
title: "ALTER TABLE 的 SQL 命令 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: alter table [ODBC]
ms.assetid: 3a01a291-f4d9-43bc-a725-5a95546ff364
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 79fbb4e4f6c143d693e1b41cc1660938bc61cde1
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2017
---
# <a name="alter-table---sql-command"></a>ALTER TABLE 的 SQL 命令
以程式設計方式修改資料表的結構。  
  
## <a name="syntax"></a>語法  
  
```  
  
ALTER TABLE TableName1  
   ADD | ALTER [COLUMN] FieldName1  
      FieldType [(nFieldWidth [, nPrecision])]  
      [NULL | NOT NULL]  
      [CHECK lExpression1 [ERROR cMessageText1]]  
      [DEFAULT eExpression1]  
      [PRIMARY KEY | UNIQUE]  
      [REFERENCES TableName2 [TAG TagName1]]  
      [NOCPTRANS]  
 - Or -  
ALTER TABLE TableName1  
   ALTER [COLUMN] FieldName2  
      [NULL | NOT NULL]  
      [SET DEFAULT eExpression2]  
      [SET CHECK lExpression2 [ERROR cMessageText2]]  
      [DROP DEFAULT]  
      [DROP CHECK]  
 - Or -  
ALTER TABLE TableName1  
   [DROP [COLUMN] FieldName3]  
   [SET CHECK lExpression3 [ERROR cMessageText3]]  
   [DROP CHECK]  
   [ADD PRIMARY KEY eExpression3 TAG TagName2]  
   [DROP PRIMARY KEY]  
   [ADD UNIQUE eExpression4 [TAG TagName3]]  
   [DROP UNIQUE TAG TagName4]  
   [ADD FOREIGN KEY [eExpression5] TAG TagName4  
      REFERENCES TableName2 [TAG TagName5]]  
   [DROP FOREIGN KEY TAG TagName6 [SAVE]]  
   [RENAME COLUMN FieldName4 TO FieldName5]  
   [NOVALIDATE]  
```  
  
## <a name="arguments"></a>引數  
 *TableName1*  
 指定其結構會修改的資料表的名稱。  
  
 加入 [資料行] *FieldName1*  
 指定要加入的欄位名稱。  
  
 ALTER [COLUMN] *FieldName1*  
 指定要修改現有欄位的名稱。  
  
 *FieldType* [( *nFieldWidth* [， *nPrecision*]])  
 新增或修改欄位的指定欄位類型、 欄位寬度和欄位有效位數 （小數位數）。  
  
 *FieldType*表示的欄位是單一字母[資料型別](../../odbc/microsoft/visual-foxpro-field-data-types.md)。 某些欄位資料型別會要求您指定*nFieldWidth*或*nPrecision*或兩者。  
  
 *nFieldWidth*和*nPrecision*也會被忽略 D、 G、 I、 L、 M、 P、 T 與 Y 型別。 根據預設， *nPrecision*不是零 （任何小數位數），如果*nPrecision*不包含 B、 F 或 N 類型。  
  
 NULL &#124;不是 NULL  
 允許或避免在欄位中的 null 值。  
  
 如果您省略 NULL 和 NOT NULL、 SET NULL 的目前設定會決定欄位中是否允許 null 值。 不過，如果您省略 NULL 和 NOT NULL，而且包含主索引鍵或唯一的子句，SET NULL 的目前設定會被忽略，欄位不是預設為 NULL。  
  
 請檢查*lExpression1*  
 指定欄位的驗證規則。 *lExpression1*必須評估為邏輯運算式，而且可以是使用者定義函式或預存程序。 每當空白記錄會附加，則會檢查驗證規則。 如果驗證規則不允許空白欄位中的值附加的記錄，會產生錯誤。  
  
 錯誤*cMessageText1*  
 指定欄位驗證規則會產生錯誤時顯示錯誤訊息。  
  
 預設*eExpression1*  
 指定欄位的預設值。 資料型別*eExpression1*必須是欄位的資料類型相同。  
  
 PRIMARY KEY  
 建立主要索引標籤。 索引標籤的欄位具有相同的名稱。  
  
 UNIQUE  
 具有相同名稱做為欄位建立候選索引標籤。  
  
> [!NOTE]  
>  候選索引命令中使用的唯一選項所建立的索引與不同的索引 （包括唯一的選項，提供 ANSI 相容性，ALTER TABLE 或 CREATE TABLE 中所建立）。 使用 UNIQUE 索引命令中建立的索引可允許重複的索引鍵。候選索引不允許重複的索引鍵。  
  
 使用主要或候選索引的欄位中不允許 null 值和重複的記錄。  
  
 如果您要建立新的欄位，使用 加入資料行，Visual FoxPro 不會產生錯誤如果您建立主要或候選索引，支援 null 值的欄位。 不過，Visual FoxPro 會產生錯誤，如果您嘗試使用主要或候選索引欄位中輸入 null 值或重複值。  
  
 如果您要修改現有欄位和主要或候選索引運算式包含資料表中的欄位，Visual FoxPro 會檢查以查看其中是否包含 null 值或重複的記錄欄位。 如果沒有的話，Visual FoxPro 會產生錯誤，而且資料表不會改變。  
  
 參考*TableName2*標記*TagName1*  
 指定要建立持續性的關聯性的父資料表。 標記*TagName1*指定關聯性所依據的父資料表的索引標籤。 索引標籤名稱可以包含最多 10 個字元。  
  
 NOCPTRANS  
 防止轉譯成不同的字碼頁的字元和註解欄位。 如果該資料表會轉換為另一個字碼頁，將不會轉譯到指定 NOCPTRANS 的欄位。 NOCPTRANS 可以指定只適用於字元和註解欄位。  
  
 下列範例會建立名為 mytable，其中包含兩個字元的欄位和附註的兩個欄位的資料表。 第二個字元的欄位、 char2 和第二個的備忘欄位 memo2，包含 NOCPTRANS 若要避免轉譯。  
  
```  
CREATE TABLE mytable (char1 C(10), char2 C(10) NOCPTRANS,;  
   memo1 M, memo2 M NOCPTRANS)  
```  
  
 ALTER [COLUMN] *FieldName2*  
 指定要修改現有欄位的名稱。  
  
 設定預設*eExpression2*  
 指定與現有欄位的新預設值。 資料型別*eExpression2*必須是欄位的資料類型相同。  
  
 設定檢查*lExpression2*  
 指定與現有欄位的新驗證規則。 *lExpression2*必須評估為邏輯運算式，而且可能是使用者定義函數或預存程序。  
  
 錯誤*cMessageText2*  
 指定欄位驗證規則會產生錯誤時顯示錯誤訊息。 瀏覽或編輯視窗內變更資料時，才會顯示訊息。  
  
 DROP DEFAULT  
 移除與現有欄位的預設值。  
  
 卸除檢查  
 移除與現有欄位的驗證規則。  
  
 拖放 [COLUMN] *FieldName3*  
 指定要從資料表移除的欄位。 從資料表中移除欄位也會移除該欄位的預設值和欄位驗證規則。  
  
 如果索引鍵或觸發程序運算式參考欄位，將會移除欄位時的運算式變成無效。 在此情況下，將會移除欄位，但不正確的索引鍵或觸發程序運算式將會在執行階段產生錯誤時，會不產生錯誤。  
  
 設定檢查*lExpression3*  
 指定資料表驗證規則。 *lExpression3*必須評估為邏輯運算式，而且可能是使用者定義函數或預存程序。  
  
 錯誤*cMessageText3*  
 指定資料表驗證規則會產生錯誤時顯示錯誤訊息。 瀏覽或編輯視窗內變更資料時，才會顯示訊息。  
  
 卸除檢查  
 移除資料表的驗證規則。  
  
 加入主索引鍵*eExpression3*標記*TagName2*  
 將主索引鍵加入至資料表。 *eExpression3*指定主索引鍵的運算式，並*TagName2*指定主要索引標籤的名稱。 索引標籤名稱可以包含最多 10 個字元。 如果標記*TagName2*省略和*eExpression3*是單一欄位中，主要索引標籤中指定之欄位與具有相同名稱*eExpression3*。  
  
 卸除主索引鍵  
 移除主索引鍵和其索引標籤。 資料表只能有一個主索引鍵，因為它不需要指定主索引鍵的名稱。 移除主要索引也會刪除任何持續性的關聯性主索引鍵為基礎。  
  
 新增 UNIQUE *eExpression4*[標記*TagName3*]  
 將候選索引加入資料表。 *eExpression4*指定候選索引鍵運算式，並*TagName3*指定候選索引標籤的名稱。 索引標籤名稱可以包含最多 10 個字元。 如果您省略標記*TagName3*如果*eExpression4*是單一欄位中，候選索引標籤中指定的欄位具有相同名稱*eExpression4*。  
  
 卸除唯一的標記*TagName4*  
 移除候選索引和其索引標籤。 因為資料表可以有多個候選索引鍵，您必須指定 候選索引標籤的名稱。  
  
 加入外部索引鍵 [ *eExpression5*] 標記*TagName4*  
 將外部 （非主要） 索引加入資料表。 *eExpression5*指定外部索引鍵的運算式，並*TagName4*指定外部索引的索引標籤的名稱。 索引標籤名稱可以包含最多 10 個字元。  
  
 參考*TableName2*[標記*TagName5*]  
 指定要建立持續性的關聯性的父資料表。 Include 標記*TagName5*建立父資料表現有的索引標籤為基礎的關聯性。 索引標籤名稱可以包含最多 10 個字元。 如果您省略標記*TagName5*，使用父資料表的主要索引標籤來建立關聯性。  
  
 卸除的外部索引鍵標記*TagName6*[儲存]  
 刪除外部索引鍵，其索引標籤是*TagName6*。 如果您省略儲存時，索引標籤會刪除從結構化的索引。 包含儲存至導致無法刪除從結構化之索引的索引標籤。  
  
 重新命名資料行*FieldName4*TO *FieldName5*  
 可讓您變更資料表中的欄位名稱。 *FieldName4*指定重新命名欄位的名稱。 *FieldName5*指定欄位的新名稱。  
  
> [!CAUTION]  
>  重新命名資料表欄位，因為索引運算式、 欄位和資料表的驗證規則、 命令及函式可能會參考原始的欄位名稱時，請務必小心。  
  
 NOVALIDATE  
 指定 Visual FoxPro 允許進行表格的結構變更這些變更可能會違反資料表中資料的完整性。 根據預設，Visual FoxPro 防止 ALTER TABLE 違反的資料表中的資料完整性的變更。 包含 NOVALIDATE 覆寫這個預設行為。  
  
## <a name="remarks"></a>備註  
 ALTER TABLE 可以用來修改尚未加入至資料庫資料表的結構。 不過，如果您包含預設值、 外部索引鍵、 主索引鍵，參考資料，或修改可用的資料表時，設定子句 Visual FoxPro 產生錯誤。  
  
 ALTER TABLE 會重建此資料表建立新的資料表標頭，以及將記錄附加至資料表標頭。 例如，變更欄位的型別或寬度可能會導致重建的資料表。  
  
 重建資料表之後，欄位的驗證規則會執行任何會變更其類型或寬度的欄位。 如果您變更資料表中的任何欄位寬度的類型，會在執行資料表的規則。  
  
 如果您修改欄位或資料表的記錄資料表中的驗證規則時，Visual FoxPro 測試的新欄位或資料表驗證規則針對現有的資料，並發出上第一次出現的欄位或資料表的驗證規則或觸發程序違規的警告。  
  
 如果您修改的資料表是在資料庫中，ALTER TABLE-SQL 需要獨佔使用的資料庫。 若要開啟用於專用資料庫，包含獨佔開啟資料庫中。  
  
## <a name="see-also"></a>請參閱＜  
 [建立資料表的 SQL 命令](../../odbc/microsoft/create-table-sql-command.md)   
 [INDEX 命令](../../odbc/microsoft/index-command.md)
