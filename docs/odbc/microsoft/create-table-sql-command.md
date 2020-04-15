---
title: 建立表 - SQL 指令 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- CREATE TABLE [ODBC]
ms.assetid: be2143ba-fc16-42c9-84f7-8985cd924860
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: dfc80a56a021b1bfeda38115e79f7086632900c8
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298688"
---
# <a name="create-table---sql-command"></a>CREATE TABLE - SQL 命令
建立具有指定欄位的表。  
  
 Visual FoxPro ODBC 驅動程式支援此命令的本機 Visual FoxPro 語言文法。 有關特定於驅動程式的資訊,請參閱**驅動程式備註**。  
  
## <a name="syntax"></a>語法  
  
```  
  
CREATE TABLE | DBF TableName1 [NAME LongTableName] [FREE]  
   (FieldName1FieldType [(nFieldWidth [, nPrecision])]  
      [NULL | NOT NULL]   
      [CHECK lExpression1 [ERROR cMessageText1]]  
      [DEFAULT eExpression1]  
      [PRIMARY KEY | UNIQUE]  
      [REFERENCES TableName2 [TAG TagName1]]  
      [NOCPTRANS]  
   [, FieldName2 ...]  
      [, PRIMARY KEY eExpression2 TAG TagName2  
      |, UNIQUE eExpression3 TAG TagName3]  
      [, FOREIGN KEY eExpression4 TAG TagName4 [NODUP]  
            REFERENCES TableName3 [TAG TagName5]]  
      [, CHECK lExpression2 [ERROR cMessageText2]])  
| FROM ARRAY ArrayName  
```  
  
## <a name="arguments"></a>引數  
 建立表&#124; DBF*表格名稱1*  
 指定要建立的表的名稱。 TABLE 和 DBF 選項相同。  
  
 名稱*長表名稱*  
 指定表的長名稱。 僅當資料庫打開時才能指定長表名稱,因為長表名稱存儲在資料庫中。  
  
 長名稱最多可以包含 128 個字元,並可用於代替資料庫中的短檔名。  
  
 FREE  
 指定表不會添加到打開的資料庫。 如果資料庫未打開,則不是免費的。  
  
 *(欄位名稱1 欄位類型* *[(n欄位寬度* *[,n 精度*=)]  
 分別指定欄位名稱、欄位類型、欄位寬度和欄位精度(小數位數)。  
  
 *欄位型態*是指示欄位[資料類型](../../odbc/microsoft/visual-foxpro-field-data-types.md)的單個字母。 某些欄位資料類型要求您指定*nFieldWidth*或*nPrecision*或兩者。  
  
 *nFieldWidth*和*nPrecision*被忽略 D、G、I、L、M、P、T 和 Y 類型。 *nPrecision*預設為零(沒有小數位數),如果 B、F 或 N 類型不包括*nPrecision。*  
  
 NULL  
 允許欄位中的空值。  
  
 NOT NULL  
 防止欄位中的空值。  
  
 如果省略 NULL 和 NOT NULL,則"設置 NULL"的當前設定將確定欄位中是否允許空值。 但是,如果省略 NULL 和 NOT NULL 並包含「主密鑰」或「獨立」子句,則將忽略 SET NULL 的當前設定,並且欄位預設為「非 NULL」。。  
  
 CHECK *lExpression1*  
 指定欄位的驗證規則。 *lExpression1*可以是使用者定義的函數。 每當追加空白記錄時,都會檢查驗證規則。 如果驗證規則不允許追加記錄中的空白欄位值,則生成錯誤。  
  
 錯誤*cMessage 文字1*  
 指定欄位規則生成錯誤時顯示的錯誤消息" Visual FoxPro" 僅當在「瀏覽」視窗或「編輯」視窗中更改數據時,才會顯示該消息。  
  
 DEFAULT *eExpression1*  
 指定欄位的預設值。 *eExpression1*的數據類型必須與欄位的數據類型相同。  
  
 PRIMARY KEY  
 為欄位創建主索引。 主索引標記的名稱與欄位相同。  
  
 UNIQUE  
 為欄位創建候選索引。 候選索引標記的名稱與欄位相同。  
  
> [!NOTE]  
>  候選索引(透過在"建立表"或"更改表 -SQL"中包含"唯一"選項而建立)與 INDEX 命令中使用「唯一」選項創建的索引不同。 使用 INDEX 命令中的「UNIQUE」選項創建的索引允許重複索引鍵;候選索引不允許重複的索引鍵。 有關其"獨特"選項的其他資訊,請參閱[INDEX。](../../odbc/microsoft/index-command.md)  
  
 對於用於主索引或候選索引的欄位,不允許使用空值和重複記錄。 但是,如果為支援空值的欄位創建主索引或候選索引,Visual FoxPro 不會生成錯誤。 如果您嘗試在用於主索引或候選索引的欄位中輸入空值或重複值,Visual FoxPro 將生成錯誤。  
  
 參考*表格名稱2*[TAG*標籤名稱1*]  
 指定建立持久關係的父表。 如果省略 TAG *TagName1,* 則使用父表的主索引鍵建立關係。 如果父表沒有主索引,則 Visual FoxPro 將生成錯誤。  
  
 包括 TAG *TagName1,* 以基於父表的現有索引標記建立關係。 索引標記名稱最多可以包含 10 個字元。  
  
 父表不能是可用表。  
  
 NOCPTRANS  
 防止將字元和備忘錄欄位翻譯成其他代碼頁。 如果表轉換為另一個代碼頁,則不會轉換指定 NOCPTRANS 的欄位。 NOCPTRANS 只能為字元和備忘錄欄位指定。  
  
 下面的範例創建一個名為 mytable 的表,其中包含兩個字元欄位和兩個備忘錄欄位。 第二個字元字段 char2 和第二個備忘錄欄位備忘錄 2 包括 NOCPTRANS 以防止翻譯。  
  
```  
CREATE TABLE mytable (char1 C(10), char2 C(10) NOCPTRANS,;  
   memo1 M, memo2 M NOCPTRANS)  
```  
  
 主鍵*eExpression2* *標籤標籤名稱2*  
 指定要建立的主索引。 *eExpression2*指定表中欄位的任何欄位或組合。 TAG *TagName2*指定所建立的主要索引標記的名稱。 索引標記名稱最多可以包含 10 個字元。  
  
 由於表只能有一個主索引,因此,如果已為欄位創建了主索引,則無法包含此子句。 如果在"創建表"中包含多個主要密鑰子句,Visual FoxPro 將生成錯誤。  
  
 唯*一個電子表示式3**分頁標籤名稱3*  
 創建候選索引。 *eExpression3*指定表中欄位的任何欄位或組合。 但是,如果已創建具有其中一個"主要密鑰"選項的主索引,則無法包括為主索引指定的欄位。 TAG *TagName3*為創建的候選索引標記指定標記名稱。 索引標記名稱最多可以包含 10 個字元。  
  
 表可以有多個候選索引。  
  
 外國金鑰*eExpression4* *TAG 標籤名稱4*[NODUP]  
 創建外(非主)索引並建立與父表的關係。 *eExpression4*指定外索引鍵運算式 *,TagName4*指定所創建的外索引鍵標記的名稱。 索引標記名稱最多可以包含 10 個字元。 包括 NODUP 以創建候選的外來索引。  
  
 可以為表創建多個外來索引,但外索引表達式必須在表中指定不同的欄位。  
  
 參考*表格名稱3*[TAG*標籤名稱5*]  
 指定建立持久關係的父表。 包括 TAG *TagName5*以建立基於父表的索引標記的關係。 索引標記名稱最多可以包含 10 個字元。 預設情況下,如果省略*TAG TagName5,* 則使用父表的主索引鍵建立關係。  
  
 CHECK *eExpression2*[錯誤*cMessage文字2*]  
 指定表驗證規則。 錯誤*cMessageText2*指定執行表驗證規則時顯示的錯誤訊息 Visual FoxPro。 僅當在「瀏覽」視窗或「編輯」視窗中更改數據時,才會顯示該消息。  
  
 從*陣列陣列名稱*  
 指定現有陣列的名稱,其內容為表中每個欄位的名稱、類型、精度和比例。 陣列的內容可以使用**AFIELDS**() 函數進行定義。  
  
## <a name="remarks"></a>備註  
 新表在最低可用工作區中打開,可通過其別名訪問。 無論 SET 獨佔的當前設置如何,新表都是獨佔打開的。  
  
 如果資料庫處於打開狀態,並且不包括 FREE 子句,則新錶將添加到資料庫中。 不能創建與資料庫中的表同名的新錶。  
  
 如果資料庫處於打開狀態,則創建表 - SQL 需要獨佔使用資料庫。 要打開資料庫供獨佔使用,請在 OPEN 資料庫中包括獨佔。  
  
 如果在創建新表時資料庫未打開,包括名稱、檢查、DEFAULT、外鍵、主鍵或參考子句都會生成錯誤。  
  
> [!NOTE]  
>  建立表語法使用逗號分隔某些 CREATE TABLE 選項。 此外,NULL、非 NULL、CHECK、DEFAULT、主鍵和 UNIQUE 子句必須放置在包含列定義的括弧內。  
  
## <a name="driver-remarks"></a>驅動程式備註  
 當應用程式將 ODBC SQL 語句 CREATE TABLE 傳送到資料來源時,Visual FoxPro ODBC 驅動程式使用下表中顯示的語法將該命令轉換為 Visual FoxProCREATE TABLE 命令。  
  
|ODBC 語法|視覺化 FoxPro 語法|  
|-----------------|--------------------------|  
|建立表*格表名稱*<br /><br /> (*欄識別子資料類型*<br /><br /> [非空]<br /><br /> *,*列識別子資料類型*<br /><br /> [不作空]|建立*表格名稱1* [名稱*長表名稱*]<br /><br /> (*欄位名稱1* *欄位類型*<br /><br /> *[(nFieldWidth* *[,n精度*]]<br /><br /> [非空])|  
  
 使用驅動程式創建表時,驅動程式在創建後立即關閉該表,以允許其他使用者訪問該表。 這與 Visual FoxPro 不同,後者僅在創建時打開表。 但是,如果資料來源上包含 CREATE TABLE 語句的儲存過程執行,則表將保持打開狀態。  
  
 如果資料來源是資料庫 (.dbc 檔案),Visual FoxPro ODBC 驅動程式將建立名為*LongTableName*的表,其名稱與*基表名稱*相同。  
  
### <a name="using-data-definition-language-ddl"></a>使用資料定義語言 (DDL)  
 您不能在以下位置包含 DDL:  
  
-   在需要事務的批次處理 SQL 語句中  
  
-   在手動提交模式下,在需要事務的語句之後,除非應用程式首先呼叫**SQLTransact**。  
  
 例如,如果要創建臨時表,則應在開始需要事務的語句之前創建該表。 如果在需要事務的批處理 SQL 語句中包含 CREATE TABLE 語句,驅動程式將返回一條錯誤消息。  
  
## <a name="see-also"></a>另請參閱  
 [變更表 - SQL 指令](../../odbc/microsoft/alter-table-sql-command.md)   
 [支援的資料型態 (視覺化福斯 Pro ODBC 驅動程式)](../../odbc/microsoft/supported-data-types-visual-foxpro-odbc-driver.md)   
 [插入 - SQL 指令](../../odbc/microsoft/insert-sql-command.md)   
 [SELECT - SQL 命令](../../odbc/microsoft/select-sql-command.md)
