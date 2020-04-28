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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 587d721522503f9b392bb8be7433850fd7449efb
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81304709"
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
 指定其結構已修改之資料表的名稱。  
  
 ADD [COLUMN] *FieldName1*  
 指定要加入之欄位的名稱。  
  
 ALTER [COLUMN] *FieldName1*  
 指定要修改之現有欄位的名稱。  
  
 *FieldType* [（ *NFieldWidth* [， *nPrecision*]]）  
 針對新的或修改過的欄位，指定欄位類型、欄位寬度和欄位有效位數（小數位數）。  
  
 *FieldType*是單一字母，表示欄位的[資料類型](../../odbc/microsoft/visual-foxpro-field-data-types.md)。 某些欄位資料類型需要您指定*nFieldWidth*或*nPrecision*或兩者。  
  
 D、G、I、L、M、P、T 和 Y 類型都會忽略*nFieldWidth*和*nPrecision* 。 根據預設，如果 B、F 或 N 類型未包含*nPrecision* ，則*nPrecision*為零（沒有小數位數）。  
  
 NULL &#124; NOT NULL  
 允許或防止欄位中出現 null 值。  
  
 如果您省略 Null 和 NOT Null，則 SET Null 的目前設定會決定欄位中是否允許 Null 值。 不過，如果您省略 Null 和 NOT Null 並包含 PRIMARY KEY 或 UNIQUE 子句，則會忽略 SET Null 的目前設定，而欄位預設為非 Null。  
  
 檢查*lExpression1*  
 指定欄位的驗證規則。 *lExpression1*必須評估為邏輯運算式，而且可以是使用者定義函數或預存程式。 每當附加空白記錄時，就會檢查驗證規則。 如果驗證規則不允許附加記錄中的空白域值，則會產生錯誤。  
  
 錯誤*cMessageText1*  
 指定當欄位驗證規則產生錯誤時所顯示的錯誤訊息。  
  
 預設*eExpression1*  
 指定欄位的預設值。 *EExpression1*的資料類型必須與欄位的資料類型相同。  
  
 PRIMARY KEY  
 建立主要索引標記。 索引標記的名稱與欄位相同。  
  
 UNIQUE  
 使用與欄位相同的名稱來建立候選索引標記。  
  
> [!NOTE]  
>  候選索引（藉由包含 ALTER TABLE 或 CREATE TABLE 中 ANSI 相容性所建立的唯一選項）不同于在 INDEX 命令中使用 UNIQUE 選項所建立的索引。 在 INDEX 命令中使用 UNIQUE 建立的索引，允許重複的索引鍵;候選索引不允許重複的索引鍵。  
  
 在用於主要或候選索引的欄位中，不允許 Null 值和重複的記錄。  
  
 如果您要使用 [加入資料行] 來建立新的欄位，如果您為支援 null 值的欄位建立主要或候選索引，Visual FoxPro 就不會產生錯誤。 不過，如果您嘗試在用於主要或候選索引的欄位中輸入 null 或重複的值，Visual FoxPro 將會產生錯誤。  
  
 如果您要修改現有的欄位，而且主要或候選索引運算式包含資料表中的欄位，則 Visual FoxPro 會檢查欄位，以查看它們是否包含 null 值或重複的記錄。 如果有的話，Visual FoxPro 會產生錯誤，而且不會改變數據表。  
  
 參考*TableName2*標記*TagName1*  
 指定要建立持續性關聯性的父資料表。 TAG *TagName1*指定以關聯性為基礎的父資料表的索引標記。 索引標記名稱最多可包含10個字元。  
  
 NOCPTRANS  
 防止轉譯成字元和備忘欄位的不同字碼頁。 如果資料表轉換成另一個字碼頁，則不會轉譯已指定 NOCPTRANS 的欄位。 只能針對字元和備忘欄位指定 NOCPTRANS。  
  
 下列範例會建立名為 mytable 的資料表，其中包含兩個字元欄位和兩個備忘欄位。 第二個字元欄位 char2 和第二個備忘欄位 memo2 包括 NOCPTRANS，以防止轉譯。  
  
```  
CREATE TABLE mytable (char1 C(10), char2 C(10) NOCPTRANS,;  
   memo1 M, memo2 M NOCPTRANS)  
```  
  
 ALTER [COLUMN] *FieldName2*  
 指定要修改之現有欄位的名稱。  
  
 設定預設*eExpression2*  
 為現有的欄位指定新的預設值。 *EExpression2*的資料類型必須與欄位的資料類型相同。  
  
 設定檢查*lExpression2*  
 為現有的欄位指定新的驗證規則。 *lExpression2*必須評估為邏輯運算式，而且可以是使用者定義函數或預存程式。  
  
 錯誤*cMessageText2*  
 指定當欄位驗證規則產生錯誤時所顯示的錯誤訊息。 只有在 [流覽] 或 [編輯] 視窗中變更資料時，才會顯示此訊息。  
  
 DROP DEFAULT  
 移除現有欄位的預設值。  
  
 捨棄檢查  
 移除現有欄位的驗證規則。  
  
 DROP [COLUMN] *FieldName3*  
 指定要從資料表中移除的欄位。 從資料表中移除欄位也會移除欄位的預設值設定和欄位驗證規則。  
  
 如果索引鍵或觸發程式運算式參考欄位，當移除欄位時，運算式就會變成無效。 在此情況下，當移除欄位但不正確索引鍵或觸發程式運算式在執行時間產生錯誤時，不會產生錯誤。  
  
 設定檢查*lExpression3*  
 指定資料表驗證規則。 *lExpression3*必須評估為邏輯運算式，而且可以是使用者定義函數或預存程式。  
  
 錯誤*cMessageText3*  
 指定當資料表驗證規則產生錯誤時所顯示的錯誤訊息。 只有在 [流覽] 或 [編輯] 視窗中變更資料時，才會顯示此訊息。  
  
 捨棄檢查  
 移除資料表的驗證規則。  
  
 新增主要金鑰*eExpression3*標記*TagName2*  
 將主要索引加入至資料表。 *eExpression3*指定主要索引鍵運算式，而*TagName2*指定主要索引標記的名稱。 索引標記名稱最多可包含10個字元。 如果省略了 TAG *TagName2* ，而且*eExpression3*是單一欄位，則主要索引標籤的名稱與*eExpression3*中指定的欄位相同。  
  
 捨棄主要金鑰  
 移除主要索引和其索引標記。 因為一個資料表只能有一個主鍵，所以不需要指定主鍵的名稱。 移除主要索引也會刪除以主要金鑰為基礎的任何持續性關聯。  
  
 新增唯一的*eExpression4*[TAG *TagName3*]  
 將候選索引加入至資料表。 *eExpression4*指定候選索引鍵運算式，而*TagName3*指定候選索引標記的名稱。 索引標記名稱最多可包含10個字元。 如果您省略 TAG *TagName3* ，而且如果*eExpression4*是單一欄位，則候選索引標記的名稱與*eExpression4*中指定的欄位相同。  
  
 DROP UNIQUE TAG *TagName4*  
 移除候選索引和其索引標記。 因為資料表可以有多個候選索引鍵，所以您必須指定候選索引標記的名稱。  
  
 新增外鍵 [ *eExpression5*] 標記*TagName4*  
 將外部（非主要）索引加入至資料表。 *eExpression5*指定外部索引鍵運算式，而*TagName4*指定外部索引標記的名稱。 索引標記名稱最多可包含10個字元。  
  
 參考*TableName2*[TAG *TagName5*]  
 指定要建立持續性關聯性的父資料表。 包含標記*TagName5* ，可根據父資料表的現有索引標記來建立關聯性。 索引標記名稱最多可包含10個字元。 如果您省略 TAG *TagName5*，則會使用父資料表的主要索引標記來建立關聯性。  
  
 卸載外鍵標記*TagName6*[儲存]  
 刪除索引標籤為*TagName6*的外鍵。 如果您省略 [儲存]，則會從結構化索引中刪除索引標記。 包含 [儲存] 以防止從結構化索引中刪除索引標記。  
  
 將資料行*FieldName4*重新命名為*FieldName5*  
 可讓您變更資料表中的功能變數名稱。 *FieldName4*指定重新命名的功能變數名稱。 *FieldName5*指定欄位的新名稱。  
  
> [!CAUTION]  
>  在重新命名資料表欄位時請小心，因為索引運算式、欄位和資料表驗證規則、命令和函式可能會參考原始的功能變數名稱。  
  
 NOVALIDATE  
 指定 Visual FoxPro 允許對資料表的結構進行變更;這些變更可能會違反資料表中資料的完整性。 根據預設，Visual FoxPro 會防止 ALTER TABLE 進行變更，違反資料表中資料的完整性。 包含 NOVALIDATE 以覆寫此預設行為。  
  
## <a name="remarks"></a>備註  
 ALTER TABLE 可用來修改尚未加入至資料庫之資料表的結構。 不過，如果您在修改免費資料表時包含 DEFAULT、FOREIGN KEY、PRIMARY KEY、REFERENCES 或 SET 子句，Visual FoxPro 會產生錯誤。  
  
 ALTER TABLE 可能會建立新的資料表標頭，並將記錄附加至資料表標頭，以重建資料表。 例如，變更欄位的類型或寬度可能會造成資料表重建。  
  
 重建資料表之後，會針對其類型或寬度變更的任何欄位執列欄位驗證規則。 如果您變更資料表中任何欄位的類型或寬度，就會執行資料表規則。  
  
 如果您針對具有記錄的資料表修改欄位或資料表驗證規則，Visual FoxPro 會針對現有的資料測試新的欄位或資料表驗證規則，並在第一次出現的欄位或資料表驗證規則或觸發程式違規時發出警告。  
  
 如果您修改的資料表是在資料庫中，則 ALTER TABLE-SQL 需要獨佔使用資料庫。 若要開啟資料庫以供獨佔使用，請在開啟的資料庫中包含獨佔的。  
  
## <a name="see-also"></a>另請參閱  
 [CREATE TABLE-SQL 命令](../../odbc/microsoft/create-table-sql-command.md)   
 [INDEX 命令](../../odbc/microsoft/index-command.md)
