---
title: 變更表 - SQL 指令 |微軟文件
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 587d721522503f9b392bb8be7433850fd7449efb
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304709"
---
# <a name="alter-table---sql-command"></a>ALTER TABLE - SQL 命令
以程式設計方式修改表的結構。  
  
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
 *表格名稱1*  
 指定其結構被修改的表的名稱。  
  
 新增 [COLUMN]*欄位名稱1*  
 指定要新增的欄位的名稱。  
  
 變更 [COLUMN]*欄位名稱1*  
 指定要修改的現有欄位的名稱。  
  
 *欄位型態* *[(n欄位寬度* *[,n 精度*])  
 指定新欄位或修改欄位的欄位類型、欄位寬度和欄位精度(小數位數)。  
  
 *欄位型態*是指示欄位[資料類型](../../odbc/microsoft/visual-foxpro-field-data-types.md)的單個字母。 某些欄位資料類型要求您指定*nFieldWidth*或*nPrecision*或兩者。  
  
 *nFieldWidth*和*nPrecision*被忽略 D、G、I、L、M、P、T 和 Y 類型。 預設情況下,如果 B、F 或 N 類型不包括*nPrecision,**則 nPrecision*為零(無小數位數)。  
  
 NULL &#124; NOT NULL  
 允許或阻止欄位中的空值。  
  
 如果省略 NULL 和 NOT NULL,則"設置 NULL"的當前設定將確定欄位中是否允許空值。 但是,如果省略 NULL 和 NOT NULL 並包含「主密鑰」或「獨立」子句,則將忽略 SET NULL 的目前設定,預設情況下該欄位不是 NULL。  
  
 CHECK *lExpression1*  
 指定欄位的驗證規則。 *lExpression1*必須計算到邏輯運算式,並且可以是使用者定義的函數或存儲過程。 每當追加空白記錄時,都會檢查驗證規則。 如果驗證規則不允許追加記錄中的空白欄位值,則生成錯誤。  
  
 錯誤*cMessage 文字1*  
 指定欄位驗證規則產生錯誤時顯示的錯誤訊息。  
  
 DEFAULT *eExpression1*  
 指定欄位的預設值。 *eExpression1*的數據類型必須與欄位的數據類型相同。  
  
 PRIMARY KEY  
 建立主索引標記。 索引標記的名稱與欄位相同。  
  
 UNIQUE  
 創建與欄位同名的候選索引標記。  
  
> [!NOTE]  
>  候選索引(透過包含'唯一'選項(在 ALTER TABLE 或 CREATE TABLE 中提供 ANSI 相容性)與在 INDEX 命令中使用「唯一」選項創建的索引不同。 在 INDEX 命令中使用 UNIQUE 創建的索引允許重複索引鍵;候選索引不允許重複的索引鍵。  
  
 對於用於主索引或候選索引的欄位,不允許使用空值和重複記錄。  
  
 如果使用 ADD COLUMN 創建新欄位,則如果為支援空值的欄位創建主索引或候選索引,Visual FoxPro 將不會生成錯誤。 但是,如果您嘗試在用於主索引或候選索引的欄位中輸入空值或重複值,則 Visual FoxPro 將生成錯誤。  
  
 如果要修改現有欄位,並且主索引表示式由表中的欄位組成,Visual FoxPro 將檢查欄位以查看這些欄位是否包含空值或重複記錄。 如果這樣做,Visual FoxPro 將生成錯誤,並且表不會更改。  
  
 參考*表格名稱2* *標籤名稱1*  
 指定建立持久關係的父表。 TAG *TagName1*指定關係所基於的父表的索引標記。 索引標記名稱最多可以包含 10 個字元。  
  
 NOCPTRANS  
 防止將字元和備忘錄欄位翻譯成其他代碼頁。 如果表轉換為另一個代碼頁,則不會轉換指定 NOCPTRANS 的欄位。 NOCPTRANS 只能為字元和備忘錄欄位指定。  
  
 下面的範例創建一個名為 mytable 的表,其中包含兩個字元欄位和兩個備忘錄欄位。 第二個字元字段 char2 和第二個備忘錄欄位備忘錄 2 包括 NOCPTRANS 以防止翻譯。  
  
```  
CREATE TABLE mytable (char1 C(10), char2 C(10) NOCPTRANS,;  
   memo1 M, memo2 M NOCPTRANS)  
```  
  
 變更 [COLUMN]*欄位名稱2*  
 指定要修改的現有欄位的名稱。  
  
 設定預設*e 運算式2*  
 為現有欄位指定新的預設值。 *eExpression2*的資料類型必須與欄位的數據類型相同。  
  
 設定 CHECK *l 表示式2*  
 為現有欄位指定新的驗證規則。 *lExpression2*必須計算到邏輯運算式,並且可能是使用者定義的函數或存儲過程。  
  
 錯誤*cMessage 文字2*  
 指定欄位驗證規則產生錯誤時顯示的錯誤訊息。 僅當在「瀏覽」或「編輯」視窗中更改數據時,才會顯示該消息。  
  
 DROP DEFAULT  
 刪除現有欄位的預設值。  
  
 掉落檢查  
 刪除現有欄位的驗證規則。  
  
 DROP (欄位)*欄位名稱3*  
 指定要從表中移除的欄位。 從表中刪除欄位還會刪除欄位的預設值設置和欄位驗證規則。  
  
 如果索引鍵或觸發器表達式引用該欄位,則刪除該欄位時,表達式將變為無效。 在這種情況下,刪除欄位時不會生成錯誤,但無效的索引鍵或觸發器表達式將在運行時生成錯誤。  
  
 設定 CHECK *l 表示式3*  
 指定表驗證規則。 *lExpression3*必須計算到邏輯運算式,並且可能是使用者定義的函數或存儲過程。  
  
 錯誤*cMessage 文字3*  
 指定表驗證規則產生錯誤時顯示的錯誤訊息。 僅當在「瀏覽」或「編輯」視窗中更改數據時,才會顯示該消息。  
  
 掉落檢查  
 刪除表的驗證規則。  
  
 新增主鍵*eExpression3*標籤*名稱2*  
 向表添加主索引。 *eExpression3*指定主索引鍵運算式 *,TagName2*指定主索引標記的名稱。 索引標記名稱最多可以包含 10 個字元。 如果省略*了 TAG TagName2,* 並且*eExpression3*是單個字段,則主索引標記的名稱與*eExpression3*中指定的欄位的名稱相同。  
  
 刪除主鍵  
 刪除主索引及其索引標記。 由於表只能有一個主鍵,因此不必指定主鍵的名稱。 刪除主索引還會刪除基於主鍵的任何持久關係。  
  
 新增獨立*電子運算式4* *[TAG 標籤名稱3*]  
 向表添加候選索引。 *eExpression4*指定候選索引鍵運算式 *,TagName3*指定候選索引標記的名稱。 索引標記名稱最多可以包含 10 個字元。 如果省略 TAG *TagName3,* 並且*eExpression4*是單個字段,則候選索引標記的名稱與*eExpression4*中指定的欄位的名稱相同。  
  
 刪除唯一*標籤名稱4*  
 刪除候選索引及其索引標記。 由於表可以有多個候選鍵,因此必須指定候選索引標記的名稱。  
  
 新增外鍵 = *eExpression5*[TAG*標籤名稱4*  
 向表添加外來(非主)索引。 *eExpression5*指定外索引鍵運算式 *,TagName4*指定外索引標記的名稱。 索引標記名稱最多可以包含 10 個字元。  
  
 參考*表格名稱2*[TAG*標籤名稱5*]  
 指定建立持久關係的父表。 包括 TAG *TagName5,* 以基於父表的現有索引標記建立關係。 索引標記名稱最多可以包含 10 個字元。 如果省略 TAG *TagName5,* 則使用父表的主索引標記建立關係。  
  
 刪除外國鍵*標籤名稱6*[儲存]  
 刪除索引標記為*TagName6*的外鍵。 如果省略 SAVE,索引標記將從結構索引中刪除。 包括 SAVE 以防止從結構索引中刪除索引標記。  
  
 重新命名欄*位名稱4*到*欄位名稱5*  
 允許您更改表中欄位的名稱。 *FieldName4*指定重新命名的欄位的名稱。 *欄位Name5*指定欄位的新名稱。  
  
> [!CAUTION]  
>  重命名表欄位時要小心謹慎,因為索引運算式、欄位和表驗證規則、命令和函數可能引用原始字段名稱。  
  
 沒有認證  
 指定 Visual FoxPro 允許對表的結構進行更改;這些更改可能會違反表中數據的完整性。 默認情況下,Visual FoxPro 可防止 ALTER TABLE 進行更改,這些更改會違反表中數據的完整性。 包括 NOVALIDATE 以覆蓋此默認行為。  
  
## <a name="remarks"></a>備註  
 ALTER TABLE 可用於修改尚未添加到資料庫的表的結構。 但是,如果在修改可用表時包含 DEFAULT、外鍵、主密鑰、參考或 SET 子句,則 Visual FoxPro 將生成錯誤。  
  
 ALTER TABLE 可以通過創建新的錶標頭並將記錄追加到錶標頭來重建表。 例如,更改欄位的類型或寬度可能會導致重建表。  
  
 重建表後,將針對任何類型或寬度更改的欄位執行欄位驗證規則。 如果更改表中任何欄位的類型或寬度,則執行表規則。  
  
 如果修改具有記錄的表的欄位或表驗證規則,Visual FoxPro 會針對現有資料測試新的欄位或表驗證規則,並針對首次出現欄位或表驗證規則或觸發器衝突發出警告。  
  
 如果修改的表位於資料庫中,則 ALTER TABLE - SQL 需要獨佔使用資料庫。 要打開資料庫供獨佔使用,請在 OPEN 資料庫中包括獨佔。  
  
## <a name="see-also"></a>另請參閱  
 [建立表 - SQL 指令](../../odbc/microsoft/create-table-sql-command.md)   
 [INDEX 命令](../../odbc/microsoft/index-command.md)
