---
title: 建立資料表的 SQL 命令 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- CREATE TABLE [ODBC]
ms.assetid: be2143ba-fc16-42c9-84f7-8985cd924860
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 35a23b8c648b5ffbf2a2000c949f1cb097ba91ca
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32905083"
---
# <a name="create-table---sql-command"></a>建立資料表的 SQL 命令
建立具有指定的欄位的資料表。  
  
 Visual FoxPro ODBC 驅動程式支援的原生 Visual FoxPro 語言語法，此命令。 驅動程式特定資訊，請參閱**驅動程式註解**。  
  
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
 建立資料表&#124;DBF *TableName1*  
 指定要建立資料表的名稱。 資料表和 DBF 選項都相同。  
  
 名稱*LongTableName*  
 指定資料表的完整名稱。 資料庫是開啟的因為長資料表名稱會儲存在資料庫時，才可以指定很長的資料表名稱。  
  
 長名稱可以包含最多 128 個字元，而且可用來代替資料庫中的短檔名。  
  
 FREE  
 指定的資料表不會加入至開啟的資料庫。 如果資料庫尚未開啟，免費並非必要條件。  
  
 *(FieldName1 FieldType* [( *nFieldWidth* [， *nPrecision*])]  
 請指定欄位名稱、 欄位類型、 欄位寬度和欄位有效位數 （小數位數），分別。  
  
 *FieldType*指出欄位的是單一字母[資料型別](../../odbc/microsoft/visual-foxpro-field-data-types.md)。 某些欄位資料型別會要求您指定*nFieldWidth*或*nPrecision*或兩者。  
  
 *nFieldWidth*和*nPrecision*也會被忽略 D、 G、 I、 L、 M、 P、 T 與 Y 型別。 *nPrecision*預設為零 （任何小數位數），如果*nPrecision*不包含 B、 F 或 N 類型。  
  
 NULL  
 允許 null 值的欄位中。  
  
 NOT NULL  
 避免在欄位中的 null 值。  
  
 如果您省略 NULL 和 NOT NULL、 SET NULL 的目前設定會決定欄位中是否允許 null 值。 不過，如果您省略 NULL 和 NOT NULL，而且包含主索引鍵或唯一的子句，會忽略的目前設定的 SET NULL 和欄位預設為 NOT NULL。  
  
 請檢查*lExpression1*  
 指定欄位的驗證規則。 *lExpression1*可以是使用者定義函式。 每當空白記錄會附加，則會檢查驗證規則。 如果驗證規則不允許空白欄位中的值附加的記錄，會產生錯誤。  
  
 錯誤*cMessageText1*  
 指定當欄位規則會產生錯誤時，會顯示 Visual FoxPro 的錯誤訊息。 瀏覽視窗或 [編輯] 視窗內變更資料時，才會顯示訊息。  
  
 預設*eExpression1*  
 指定欄位的預設值。 資料型別*eExpression1*必須是欄位的資料型別相同。  
  
 PRIMARY KEY  
 建立主索引的欄位。 主要索引標籤的欄位具有相同的名稱。  
  
 UNIQUE  
 會建立欄位的候選項目索引。 候選索引標籤有相同名稱的欄位。  
  
> [!NOTE]  
>  候選索引 （包括 CREATE TABLE 或 ALTER TABLE-SQL 中的唯一選項所建立） 並不使用索引命令中的唯一選項建立的索引一樣。 使用 INDEX 命令中的唯一選項建立索引可允許重複的索引鍵。候選索引不允許重複的索引鍵。 請參閱[索引](../../odbc/microsoft/index-command.md)如需有關其唯一的選項。  
  
 針對主要或候選索引所使用的欄位中不允許 null 值和重複的記錄。 不過，Visual FoxPro 不會產生錯誤，如果您建立主要或候選索引，支援 null 值的欄位。 Visual FoxPro 會產生錯誤，如果您嘗試用於主要或候選索引欄位中輸入 null 值或重複值。  
  
 參考*TableName2*[標記*TagName1*]  
 指定要建立持續性的關聯性的父資料表。 如果您省略標記*TagName1*，建立使用父資料表的主索引鍵關聯性。 如果父資料表沒有主索引鍵，Visual FoxPro 會產生錯誤。  
  
 Include 標記*TagName1*建立父資料表現有的索引標籤為基礎的關聯性。 索引標籤名稱可以包含最多 10 個字元。  
  
 父資料表不能是可用的資料表。  
  
 NOCPTRANS  
 防止轉譯成不同的字碼頁的字元和註解欄位。 如果該資料表會轉換為另一個字碼頁，將不會轉譯到指定 NOCPTRANS 的欄位。 NOCPTRANS 可以指定只適用於字元和註解欄位。  
  
 下列範例會建立名為 mytable 包含兩個字元的欄位和附註的兩個欄位的資料表。 第二個字元的欄位、 char2 和第二個的備忘欄位 memo2，包含 NOCPTRANS 若要避免轉譯。  
  
```  
CREATE TABLE mytable (char1 C(10), char2 C(10) NOCPTRANS,;  
   memo1 M, memo2 M NOCPTRANS)  
```  
  
 主索引鍵*eExpression2*標記*TagName2*  
 指定要建立主要索引。 *eExpression2*指定資料表中的任何欄位的組合。 標記*TagName2 的*指定建立主要索引標籤的名稱。 索引標籤名稱可以包含最多 10 個字元。  
  
 資料表只能有一個主要的索引，因為您不能包含這個子句，如果您已經建立主要索引的欄位。 Visual FoxPro 會產生錯誤，如果您在 CREATE TABLE 中包含多個 PRIMARY KEY 子句。  
  
 唯一*eExpression3*標記*TagName3*  
 建立候選項目索引。 *eExpression3*指定資料表中的任何欄位的組合。 不過，如果您已經建立主索引鍵與主索引鍵選項的其中一個，您不能包含已指定做為主要索引的欄位。 標記*TagName3 的*指定建立的候選項目索引標籤的標記名稱。 索引標籤名稱可以包含最多 10 個字元。  
  
 資料表可以有多個候選項目索引。  
  
 外部索引鍵*eExpression4*標記*TagName4*[NODUP]  
 建立外部 （非主要） 索引，並建立父資料表之關聯性。 *eExpression4*指定外部索引鍵的運算式，並*TagName4*指定建立外部索引鍵標記名稱 *。* 索引標籤名稱可以包含最多 10 個字元。 包含 NODUP 建立外部索引候選的索引。  
  
 您可以建立多個外部索引的索引的資料表，但外部索引的索引運算式必須指定資料表中的不同欄位。  
  
 參考*TableName3*[標記*TagName5*]  
 指定要建立持續性的關聯性的父資料表。 Include 標記*TagName5*建立父資料表的索引標籤為基礎的關聯性。 索引標籤名稱可以包含最多 10 個字元。 根據預設，如果您省略標記*TagName5，* 建立使用父資料表的主索引鍵關聯性。  
  
 請檢查*eExpression2*[錯誤*cMessageText2*]  
 指定資料表驗證規則。 錯誤*cMessageText2*指定資料表驗證規則執行時，Visual FoxPro 會顯示錯誤訊息。 瀏覽視窗中變更或編輯視窗的資料時，只會顯示訊息。  
  
 從陣列*ArrayName*  
 指定現有陣列內容的名稱、 類型、 有效位數和小數位數的資料表中每個欄位的名稱。 陣列的內容可以使用定義**AFIELDS**（） 函數。  
  
## <a name="remarks"></a>備註  
 新的資料表會在最低可用的工作區中開啟，而且可以存取的別名。 不論設定獨佔的目前設定獨佔模式開啟新的資料表。  
  
 如果資料庫已開啟，而且您不想加入可用的子句，新資料表加入至資料庫。 您無法建立新的資料表與同名的資料庫中的資料表。  
  
 如果資料庫是開啟時，CREATE TABLE-SQL 需要獨佔使用的資料庫。 若要開啟用於專用資料庫，包含獨佔開啟資料庫中。  
  
 如果資料庫尚未開啟，當您建立新的資料表，包括名稱、 核取、 預設值、 外部索引鍵、 主索引鍵或參考子句會產生錯誤。  
  
> [!NOTE]  
>  CREATE TABLE 語法會使用逗號來分隔特定 CREATE TABLE 的選項。 此外，NULL、 不 NULL、 核取、 預設值、 主索引鍵和唯一子句必須放在包含資料行定義括號內。  
  
## <a name="driver-remarks"></a>驅動程式註解  
 當您的應用程式傳送的 ODBC SQL 陳述式到資料來源，Visual FoxPro ODBC 驅動程式的 CREATE TABLE 轉譯為命令 Visual FoxProCREATE 資料表命令，使用下表所示的語法。  
  
|ODBC 語法|Visual FoxPro 語法|  
|-----------------|--------------------------|  
|CREATE TABLE*基底資料表名稱*<br /><br /> (*資料行識別碼資料型別*<br /><br /> [非 NULL]<br /><br /> [，*資料行識別碼資料型別*<br /><br /> [NOT NULL]...)|建立資料表*TableName1* [名稱*LongTableName*]<br /><br /> (*FieldName1* *FieldType*<br /><br /> [(*nFieldWidth* [， *nPrecision*])]<br /><br /> [非 NULL])|  
  
 當您建立資料表，使用驅動程式時，驅動程式會建立允許其他使用者資料表的存取權之後立即關閉資料表。 這不同於 Visual FoxPro，讓資料表保持開啟以獨佔方式在建立時。 不過，如果您包含 CREATE TABLE 陳述式的資料來源上預存程序執行時，資料表會保持開啟狀態。  
  
 如果資料來源是資料庫 （.dbc 檔案），Visual FoxPro ODBC 驅動程式會建立名為*LongTableName*與同名*基底資料表名稱*。  
  
### <a name="using-data-definition-language-ddl"></a>使用資料定義語言 (DDL)  
 您不能包含 DDL 在下列位置：  
  
-   SQL 陳述式批次中所需要的交易  
  
-   在手動認可模式下，需要交易，除非您的應用程式第一次呼叫的陳述式之後**SQLTransact**。  
  
 比方說，如果您想要建立暫存資料表，您應該建立資料表之前需要使用交易陳述式。 如果您需要的交易的 SQL 陳述式批次中包含 CREATE TABLE 陳述式，則驅動程式會傳回錯誤訊息。  
  
## <a name="see-also"></a>另請參閱  
 [ALTER TABLE 的 SQL 命令](../../odbc/microsoft/alter-table-sql-command.md)   
 [支援的資料類型 （Visual FoxPro ODBC 驅動程式）](../../odbc/microsoft/supported-data-types-visual-foxpro-odbc-driver.md)   
 [插入的 SQL 命令](../../odbc/microsoft/insert-sql-command.md)   
 [SELECT - SQL 命令](../../odbc/microsoft/select-sql-command.md)
