---
title: CREATE TABLE-SQL 命令 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2f979ccb5a44ada8e86424e0f6134f39d28a021d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68096605"
---
# <a name="create-table---sql-command"></a>CREATE TABLE - SQL 命令
建立具有指定欄位的資料表。  
  
 Visual FoxPro ODBC 驅動程式支援此命令的原生 Visual FoxPro 語言語法。 如需驅動程式特定的資訊，請參閱**驅動程式備註**。  
  
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
 CREATE TABLE &#124; DBF *TableName1*  
 指定要建立之資料表的名稱。 資料表和 DBF 選項都相同。  
  
 名稱*LongTableName*  
 指定資料表的完整名稱。 只有在資料庫已開啟時，才可以指定長資料表名稱，因為長資料表名稱會儲存在資料庫中。  
  
 長名稱最多可包含128個字元，而且可以用來取代資料庫中的簡短檔案名。  
  
 可用  
 指定資料表不會加入至開啟的資料庫。 如果未開啟資料庫，則不需要釋放。  
  
 *（FieldName1 FieldType* [（ *NFieldWidth* [， *nPrecision*]）]  
 分別指定功能變數名稱、欄位類型、欄位寬度和欄位有效位數（小數位數）。  
  
 *FieldType*是單一字母，表示欄位的[資料類型](../../odbc/microsoft/visual-foxpro-field-data-types.md)。 某些欄位資料類型需要您指定*nFieldWidth*或*nPrecision*或兩者。  
  
 D、G、I、L、M、P、T 和 Y 類型都會忽略*nFieldWidth*和*nPrecision* 。 如果 B、F 或 N 類型未包含*nPrecision* ，則*nPrecision*預設為零（不含小數位數）。  
  
 NULL  
 允許欄位中有 null 值。  
  
 NOT NULL  
 防止欄位中出現 null 值。  
  
 如果您省略 Null 和 NOT Null，則 SET Null 的目前設定會決定欄位中是否允許 Null 值。 不過，如果您省略 Null 和 NOT Null 並包含 PRIMARY KEY 或 UNIQUE 子句，則會忽略 SET Null 的目前設定，且欄位的預設值為 NOT Null。  
  
 檢查*lExpression1*  
 指定欄位的驗證規則。 *lExpression1*可以是使用者定義函數。 每當附加空白記錄時，就會檢查驗證規則。 如果驗證規則不允許附加記錄中的空白域值，則會產生錯誤。  
  
 錯誤*cMessageText1*  
 指定當欄位規則產生錯誤時，Visual FoxPro 所顯示的錯誤訊息。 只有當資料在 [流覽] 視窗或 [編輯] 視窗中變更時，才會顯示此訊息。  
  
 預設*eExpression1*  
 指定欄位的預設值。 *EExpression1*的資料類型必須與欄位的資料類型相同。  
  
 PRIMARY KEY  
 建立欄位的主要索引。 主要索引標記的名稱與欄位相同。  
  
 UNIQUE  
 建立欄位的候選索引。 候選索引標記的名稱與欄位相同。  
  
> [!NOTE]  
>  候選索引（藉由在 CREATE TABLE 或 ALTER TABLE-SQL 中包含 UNIQUE 選項所建立）與在 INDEX 命令中以 UNIQUE 選項建立的索引不同。 在 INDEX 命令中使用 UNIQUE 選項所建立的索引，允許重複的索引鍵;候選索引不允許重複的索引鍵。 如需其 UNIQUE 選項的其他資訊，請參閱[索引](../../odbc/microsoft/index-command.md)。  
  
 在用於主要或候選索引的欄位中，不允許使用 Null 值和重複的記錄。 不過，如果您為支援 null 值的欄位建立主要或候選索引，Visual FoxPro 將不會產生錯誤。 如果您嘗試在用於主要或候選索引的欄位中輸入 null 或重複的值，Visual FoxPro 將會產生錯誤。  
  
 參考*TableName2*[TAG *TagName1*]  
 指定要建立持續性關聯性的父資料表。 如果您省略 TAG *TagName1*，則會使用父資料表的主要索引鍵來建立關聯性。 如果父資料表沒有主要索引，Visual FoxPro 會產生錯誤。  
  
 包含標記*TagName1* ，可根據父資料表的現有索引標記來建立關聯性。 索引標記名稱最多可包含10個字元。  
  
 父資料表不可以是可用的資料表。  
  
 NOCPTRANS  
 防止轉譯成字元和備忘欄位的不同字碼頁。 如果資料表轉換成另一個字碼頁，則不會轉譯已指定 NOCPTRANS 的欄位。 只能針對字元和備忘欄位指定 NOCPTRANS。  
  
 下列範例會建立名為 mytable 的資料表，其中包含兩個字元欄位和兩個備忘欄位。 第二個字元欄位 char2 和第二個備忘欄位 memo2 包括 NOCPTRANS，以防止轉譯。  
  
```  
CREATE TABLE mytable (char1 C(10), char2 C(10) NOCPTRANS,;  
   memo1 M, memo2 M NOCPTRANS)  
```  
  
 主要金鑰*eExpression2*標記*TagName2*  
 指定要建立的主要索引。 *eExpression2*指定資料表中的任何欄位或欄位組合。 標記*TagName2*指定所建立之主要索引標記的名稱。 索引標記名稱最多可包含10個字元。  
  
 因為資料表只能有一個主要索引，所以如果您已經建立欄位的主要索引，就不能包含這個子句。 如果您在 CREATE TABLE 中包含一個以上的 PRIMARY KEY 子句，Visual FoxPro 會產生錯誤。  
  
 唯一的*eExpression3*標記*TagName3*  
 建立候選索引。 *eExpression3*指定資料表中的任何欄位或欄位組合。 不過，如果您已使用其中一個主鍵選項建立主要索引，則不能包含為主要索引指定的欄位。 標記*TagName3*指定所建立候選索引標記的標記名稱。 索引標記名稱最多可包含10個字元。  
  
 資料表可以有多個候選索引。  
  
 外鍵*eExpression4*標記*TagName4*[NODUP]  
 建立外部（非主要）索引，並建立與父資料表的關聯性。 *eExpression4*會指定外部索引鍵運算式，而*TagName4*會指定所建立之外部索引鍵標記的名稱。 索引標記名稱最多可包含10個字元。 包含 NODUP 以建立候選外部索引。  
  
 您可以為資料表建立多個外部索引，但外部索引運算式必須在資料表中指定不同的欄位。  
  
 參考*TableName3*[TAG *TagName5*]  
 指定要建立持續性關聯性的父資料表。 包含標記*TagName5* ，可根據父資料表的索引標記來建立關聯性。 索引標記名稱最多可包含10個字元。 根據預設，如果您省略 TAG *TagName5，* 則會使用父資料表的主要索引鍵來建立關聯性。  
  
 檢查*eExpression2*[錯誤*cMessageText2*]  
 指定資料表驗證規則。 錯誤*cMessageText2*指定當執行資料表驗證規則時，Visual FoxPro 所顯示的錯誤訊息。 只有在 [流覽] 視窗或 [編輯] 視窗中變更資料時，才會顯示此訊息。  
  
 從陣列*ArrayName*  
 指定現有陣列的名稱，其內容為數據表中每個欄位的名稱、類型、有效位數和小數位數。 陣列的內容可以使用**AFIELDS**（）函數來定義。  
  
## <a name="remarks"></a>備註  
 新的資料表會在最小的可用工作區域中開啟，而且可以透過其別名來存取。 新的資料表會以獨佔方式開啟，不論目前設定的專有設定為何。  
  
 如果資料庫已開啟，而您未包含 FREE 子句，則會將新的資料表加入至資料庫。 您無法使用與資料庫中資料表相同的名稱來建立新的資料表。  
  
 如果資料庫已開啟，CREATE TABLE-SQL 需要獨佔使用資料庫。 若要開啟資料庫以供獨佔使用，請在開啟的資料庫中包含獨佔的。  
  
 當您建立新的資料表時，如果資料庫未開啟，包括 NAME、CHECK、DEFAULT、FOREIGN KEY、PRIMARY KEY 或 REFERENCES 子句會產生錯誤。  
  
> [!NOTE]  
>  CREATE TABLE 語法會使用逗號來分隔特定的 CREATE TABLE 選項。 此外，Null、NOT Null、CHECK、DEFAULT、PRIMARY KEY 和 UNIQUE 子句必須放在包含資料行定義的括弧內。  
  
## <a name="driver-remarks"></a>驅動程式備註  
 當您的應用程式將 ODBC SQL 語句 CREATE TABLE 傳送至資料來源時，Visual FoxPro ODBC 驅動程式會使用下表所示的語法，將命令轉譯成 Visual FoxProCREATE TABLE 命令。  
  
|ODBC 語法|Visual FoxPro 語法|  
|-----------------|--------------------------|  
|CREATE TABLE*的基礎-資料表名稱*<br /><br /> （*資料行識別碼資料類型*<br /><br /> [NOT Null]<br /><br /> [，*資料行識別碼資料類型*<br /><br /> [NOT Null] ...）|CREATE TABLE *TableName1* [名稱*LongTableName*]<br /><br /> （*FieldName1* *FieldType*<br /><br /> [（*nFieldWidth* [， *nPrecision*]）]<br /><br /> [NOT Null]）|  
  
 當您使用驅動程式建立資料表時，驅動程式會在建立之後立即關閉資料表，以允許其他使用者存取資料表。 這不同于 Visual FoxPro，這會使資料表在建立時獨佔開啟。 不過，如果包含 CREATE TABLE 語句之資料來源上的預存程式執行，則資料表會保持開啟。  
  
 如果資料來源是資料庫（. dbc 檔案），則 Visual FoxPro ODBC 驅動程式會建立名為*LongTableName*的資料表，其名稱與*基表名稱*相同。  
  
### <a name="using-data-definition-language-ddl"></a>使用資料定義語言（DDL）  
 您不能在下列位置包含 DDL：  
  
-   在需要交易的批次 SQL 語句中  
  
-   在手動認可模式中，在需要交易的語句之後，除非您的應用程式先呼叫**SQLTransact**。  
  
 例如，如果您想要建立臨時表，您應該在開始需要交易的語句之前，先建立資料表。 如果您在需要交易的批次 SQL 語句中包含 CREATE TABLE 語句，驅動程式會傳回錯誤訊息。  
  
## <a name="see-also"></a>另請參閱  
 [ALTER TABLE-SQL 命令](../../odbc/microsoft/alter-table-sql-command.md)   
 [支援的資料類型（Visual FoxPro ODBC Driver）](../../odbc/microsoft/supported-data-types-visual-foxpro-odbc-driver.md)   
 [INSERT-SQL 命令](../../odbc/microsoft/insert-sql-command.md)   
 [SELECT - SQL 命令](../../odbc/microsoft/select-sql-command.md)
