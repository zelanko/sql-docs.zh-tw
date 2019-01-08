---
title: ALTER TABLE-SQL 命令 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- alter table [ODBC]
ms.assetid: 3a01a291-f4d9-43bc-a725-5a95546ff364
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5f656396455a8d5669debc158c3edc866491fcb5
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/11/2018
ms.locfileid: "53207007"
---
# <a name="alter-table---sql-command"></a>ALTER TABLE - SQL 命令
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
 指定在修改其結構的資料表名稱。  
  
 新增 [COLUMN] *FieldName1*  
 指定要加入的欄位名稱。  
  
 ALTER [COLUMN] *FieldName1*  
 指定要修改現有欄位的名稱。  
  
 *FieldType* [( *nFieldWidth* [， *nPrecision*]])  
 指定新的或修改欄位的欄位型別、 欄位寬度和欄位的有效位數 （小數位數）。  
  
 *FieldType*表示的欄位是單一字母[資料型別](../../odbc/microsoft/visual-foxpro-field-data-types.md)。 某些欄位資料類型會要求您指定*nFieldWidth*或是*nPrecision*或兩者。  
  
 *nFieldWidth*並*nPrecision*會忽略 D、 G、 我、 L、 M、 P、 T、 和 Y 的型別。 根據預設， *nPrecision*為零 （任何小數位數），如果*nPrecision*就不會包含 B、 F 或 N 的類型。  
  
 NULL &#124; NOT NULL  
 允許或避免在欄位中的 null 值。  
  
 如果您省略 NULL 和 NOT NULL、 SET NULL 目前設定會決定欄位中是否允許 null 值。 不過，如果您省略 NULL 和 NOT NULL，而且包含主索引鍵或唯一的子句，設定為 NULL 的目前設定會被忽略，該欄位不是預設為 NULL。  
  
 檢查*lExpression1*  
 指定欄位的驗證規則。 *lExpression1*必須評估為邏輯運算式，而且可以是使用者定義函式或預存程序。 每當附加空的記錄，則會檢查驗證規則。 如果驗證規則不允許附加的記錄中的空白欄位值，則會產生錯誤。  
  
 錯誤*cMessageText1*  
 指定欄位的驗證規則會產生錯誤時，會顯示錯誤訊息。  
  
 預設*eExpression1*  
 指定欄位的預設值。 資料類型*eExpression1*必須是欄位的資料類型相同。  
  
 PRIMARY KEY  
 建立主要索引標籤。 索引標籤會有相同名稱做為欄位。  
  
 UNIQUE  
 建立具有相同名稱做為欄位的候選項目索引標籤。  
  
> [!NOTE]  
>  候選索引 （加上唯一的選項，提供 ANSI 相容性，ALTER TABLE 或 CREATE TABLE 中建立） 不同於索引命令中使用唯一的選項所建立的索引。 建立索引命令中使用唯一的索引可讓重複的索引鍵;候選索引不允許重複的索引鍵。  
  
 使用主要或候選索引的欄位中不允許 null 值和重複的記錄。  
  
 如果您要使用加入資料行，以建立新的欄位，Visual FoxPro 不會產生錯誤如果您建立主要或候選索引支援 null 值的欄位。 不過，Visual FoxPro 會產生錯誤，如果您嘗試使用主要或候選索引欄位中輸入的空值或重複的值。  
  
 如果您要修改現有的欄位和主要或候選索引運算式是由資料表中的欄位所組成，Visual FoxPro 檢查欄位，以查看它們是否包含 null 值或重複的記錄。 如果沒有的話，Visual FoxPro 產生錯誤，並不會改變資料表。  
  
 參考*TableName2*標記*TagName1*  
 指定要建立持續性的關聯性的父資料表。 標記*TagName1*指定關聯性所依據的父資料表的索引標籤。 索引標籤名稱可以包含最多 10 個字元。  
  
 NOCPTRANS  
 可避免轉譯成不同的字碼頁的字元和註解欄位。 如果該資料表會轉換為另一個字碼頁，將不會翻譯已指定 NOCPTRANS 的欄位。 NOCPTRANS 可以指定只適用於字元和註解的欄位。  
  
 下列範例會建立名為 mytable，其中包含兩個字元的欄位和附註的兩個欄位的資料表。 第二個字元的欄位、 char2 和第二個的備忘欄位 memo2，包含以避免轉譯 NOCPTRANS。  
  
```  
CREATE TABLE mytable (char1 C(10), char2 C(10) NOCPTRANS,;  
   memo1 M, memo2 M NOCPTRANS)  
```  
  
 ALTER [COLUMN] *FieldName2*  
 指定要修改現有欄位的名稱。  
  
 設為預設值*eExpression2*  
 指定與現有欄位的新預設值。 資料類型*eExpression2*必須是欄位的資料類型相同。  
  
 設定核取*lExpression2*  
 指定新的驗證規則，對於現有的欄位。 *lExpression2*必須評估為邏輯運算式，而且可能是使用者定義函數或預存程序。  
  
 錯誤*cMessageText2*  
 指定欄位的驗證規則會產生錯誤時，會顯示錯誤訊息。 瀏覽 或 編輯 視窗中變更資料時，才會顯示訊息。  
  
 DROP DEFAULT  
 移除現有欄位的預設值。  
  
 卸除檢查  
 移除現有欄位的驗證規則。  
  
 拖放 [COLUMN] *FieldName3*  
 指定要移除資料表中的欄位。 移除資料表中的欄位也會移除該欄位的預設值和欄位驗證規則。  
  
 如果索引鍵或觸發程序的運算式參考欄位，運算式將會移除欄位時變成無效。 在此情況下，將會移除欄位，但不正確的索引鍵或觸發程序運算式將會在執行階段產生錯誤時，會不產生錯誤。  
  
 設定核取*lExpression3*  
 指定資料表驗證規則。 *lExpression3*必須評估為邏輯運算式，而且可能是使用者定義函數或預存程序。  
  
 錯誤*cMessageText3*  
 指定資料表驗證規則會產生錯誤時，會顯示錯誤訊息。 瀏覽 或 編輯 視窗中變更資料時，才會顯示訊息。  
  
 卸除檢查  
 移除資料表的驗證規則。  
  
 加入主索引鍵*eExpression3*標記*TagName2*  
 將資料表中的主要索引。 *eExpression3*指定的主要索引鍵運算式，並*TagName2*指定主要索引標籤的名稱。 索引標籤名稱可以包含最多 10 個字元。 如果標記*TagName2*省略並*eExpression3*是單一欄位中，主要的索引標籤中指定的欄位具有相同的名稱*eExpression3*。  
  
 卸除主索引鍵  
 移除主索引鍵和它的索引標籤。 資料表只能有一個主索引鍵，因為它不需要指定主索引鍵的名稱。 移除主索引鍵時，也會刪除任何持續性的關聯性的主索引鍵為基礎。  
  
 新增 UNIQUE *eExpression4*[標記*TagName3*]  
 將資料表中的候選項目索引。 *eExpression4*指定 候選索引鍵運算式，並*TagName3*指定候選項目索引標籤的名稱。 索引標籤名稱可以包含最多 10 個字元。 如果您省略標記*TagName3*如果*eExpression4*是單一欄位中，候選項目索引標籤中指定的欄位具有相同的名稱*eExpression4*。  
  
 卸除唯一的標記*TagName4*  
 移除的候選項目索引和它的索引標籤。 因為資料表可以有多個候選索引鍵，您必須指定候選項目索引標籤的名稱。  
  
 新增外部索引鍵 [ *eExpression5*] 標籤*TagName4*  
 將資料表中的外部 （非主要） 索引。 *eExpression5*指定外部索引鍵運算式，並*TagName4*指定外部索引的索引標籤的名稱。 索引標籤名稱可以包含最多 10 個字元。  
  
 參考*TableName2*[標記*TagName5*]  
 指定要建立持續性的關聯性的父資料表。 包含標記*TagName5*建立根據現有的索引標籤的父資料表的關聯性。 索引標籤名稱可以包含最多 10 個字元。 如果您省略標記*TagName5*，使用父資料表的主索引鍵標記建立關聯性。  
  
 卸除的外部索引鍵標記*TagName6*[儲存]  
 刪除外部索引鍵的索引標籤*TagName6*。 如果您省略儲存時，索引標籤會刪除從結構化的索引。 包含儲存，以防止刪除的索引標籤，從結構化的索引。  
  
 重新命名資料行*FieldName4*TO *FieldName5*  
 可讓您變更資料表中的欄位名稱。 *FieldName4*指定重新命名欄位的名稱。 *FieldName5*指定欄位的新名稱。  
  
> [!CAUTION]  
>  重新命名資料表欄位，因為索引運算式、 欄位和資料表的驗證規則、 命令及函式可能會參考原始欄位名稱時，請務必小心。  
  
 NOVALIDATE  
 指定 Visual FoxPro 允許對資料表的結構所做的變更這些變更可能會違反資料表中的資料的完整性。 根據預設，Visual FoxPro 可以防止 ALTER TABLE 在變更違反的資料表中的資料完整性。 包含 NOVALIDATE 覆寫這個預設行為。  
  
## <a name="remarks"></a>備註  
 ALTER TABLE 可用來修改尚未加入至資料庫資料表的結構。 不過，Visual FoxPro 產生錯誤，如果您包含預設值、 外部索引鍵、 主索引鍵，參考，或修改可用的資料表時，SET 子句。  
  
 ALTER TABLE 會重建此資料表，藉由建立新的資料表標頭，並將記錄附加至資料表標頭。 例如，變更欄位的型別或寬度可能會導致重建資料表。  
  
 重建資料表之後，欄位的驗證規則會執行任何會變更其類型或寬度的欄位。 如果您變更類型或資料表中的任何欄位的寬度，則會執行資料表的規則。  
  
 如果您修改記錄資料表的欄位或資料表驗證規則時，Visual FoxPro 測試的新欄位或資料表驗證規則針對現有的資料，並發出第一個出現的欄位或資料表的驗證規則或觸發程序違反的警告。  
  
 如果您修改的資料表是在資料庫中，ALTER TABLE-SQL 需要獨佔使用的資料庫。 若要開啟獨佔使用的資料庫，請開啟資料庫中包含排除。  
  
## <a name="see-also"></a>另請參閱  
 [CREATE TABLE-SQL 命令](../../odbc/microsoft/create-table-sql-command.md)   
 [INDEX 命令](../../odbc/microsoft/index-command.md)
