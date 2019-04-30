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
manager: craigg
ms.openlocfilehash: 62d13bdc9d1a0fc030dc33bf982f6561b454c4ea
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63232287"
---
# <a name="create-table---sql-command"></a>CREATE TABLE - SQL 命令
建立資料表，具有指定的欄位。  
  
 Visual FoxPro ODBC Driver 支援原生 Visual FoxPro 語言語法，此命令。 驅動程式專屬資訊，請參閱**驅動程式備註**。  
  
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
 指定要建立之資料表的名稱。 資料表 和 DBF 選項都相同。  
  
 名稱*LongTableName*  
 指定資料表的完整名稱。 只有當資料庫開啟時，因為長資料表名稱會儲存在資料庫中，可以指定很長的資料表名稱。  
  
 長名稱可以包含最多可有 128 個字元，而且可用來取代在資料庫中的短檔名。  
  
 FREE  
 指定的資料表不會加入至開啟的資料庫。 如果資料庫尚未開啟，不需要免費。  
  
 *(FieldName1 FieldType* [( *nFieldWidth* [, *nPrecision*])]  
 請指定欄位名稱、 欄位型別、 欄位寬度和欄位的有效位數 （小數位數），分別。  
  
 *FieldType*指出欄位的是單一字母[資料型別](../../odbc/microsoft/visual-foxpro-field-data-types.md)。 某些欄位資料類型會要求您指定*nFieldWidth*或是*nPrecision*或兩者。  
  
 *nFieldWidth*並*nPrecision*會忽略 D、 G、 我、 L、 M、 P、 T、 和 Y 的型別。 *nPrecision*預設為零 （任何小數位數），如果*nPrecision*不包含 B、 F 或 N 的類型。  
  
 NULL  
 允許在欄位中的 null 值。  
  
 NOT NULL  
 避免在欄位中的 null 值。  
  
 如果您省略 NULL 和 NOT NULL、 SET NULL 目前設定會決定欄位中是否允許 null 值。 不過，如果您省略 NULL 和 NOT NULL，而且包含主索引鍵或唯一的子句，會忽略的目前設定的 SET NULL 和欄位預設為 NOT NULL。  
  
 CHECK *lExpression1*  
 指定欄位的驗證規則。 *lExpression1*可以是使用者定義函式。 每當附加空的記錄，則會檢查驗證規則。 如果驗證規則不允許附加的記錄中的空白欄位值，則會產生錯誤。  
  
 ERROR *cMessageText1*  
 指定欄位規則會產生錯誤時，會顯示 Visual FoxPro 的錯誤訊息。 瀏覽 視窗或 編輯 視窗中變更資料時，才會顯示訊息。  
  
 預設*eExpression1*  
 指定欄位的預設值。 資料類型*eExpression1*必須是欄位的資料型別相同。  
  
 PRIMARY KEY  
 建立主要索引的欄位。 主要索引標籤會有相同名稱做為欄位。  
  
 UNIQUE  
 建立欄位的候選項目索引。 候選索引標籤會有相同名稱做為欄位。  
  
> [!NOTE]  
>  候選版 （加上唯一的選項在 CREATE TABLE 或 ALTER TABLE-SQL 中建立） 的索引不是使用索引命令中的唯一選項建立的索引相同。 使用中索引命令的唯一選項建立索引可讓重複的索引鍵;候選索引不允許重複的索引鍵。 請參閱[INDEX](../../odbc/microsoft/index-command.md)如需其他有關其唯一的選項。  
  
 針對主要或候選索引所使用的欄位中不允許 null 值和重複的記錄。 不過，Visual FoxPro 不會產生錯誤，如果您建立主要或候選索引支援 null 值的欄位。 Visual FoxPro 會產生錯誤，如果您嘗試將輸入欄位，用於主要或候選索引中的空值或重複的值。  
  
 REFERENCES *TableName2*[TAG *TagName1*]  
 指定要建立持續性的關聯性的父資料表。 如果您省略標記*TagName1*，使用父資料表的主索引鍵建立關聯性。 如果父資料表沒有主索引鍵，則 Visual FoxPro 會產生錯誤。  
  
 包含標記*TagName1*建立根據現有的索引標籤的父資料表的關聯性。 索引標籤名稱可以包含最多 10 個字元。  
  
 父資料表不能是免費的資料表。  
  
 NOCPTRANS  
 可避免轉譯成不同的字碼頁的字元和註解欄位。 如果該資料表會轉換為另一個字碼頁，將不會翻譯已指定 NOCPTRANS 的欄位。 NOCPTRANS 可以指定只適用於字元和註解的欄位。  
  
 下列範例會建立名為 mytable 包含兩個字元的欄位和附註的兩個欄位的資料表。 第二個字元的欄位、 char2 和第二個的備忘欄位 memo2，包含以避免轉譯 NOCPTRANS。  
  
```  
CREATE TABLE mytable (char1 C(10), char2 C(10) NOCPTRANS,;  
   memo1 M, memo2 M NOCPTRANS)  
```  
  
 主索引鍵*eExpression2*標記*TagName2*  
 指定要建立主要索引。 *eExpression2*指定資料表中的任何欄位的組合。 標記*TagName2*指定建立主要索引標籤的名稱。 索引標籤名稱可以包含最多 10 個字元。  
  
 資料表只能有一個主要的索引，因為您不能包含這個子句，如果您已經建立主要索引的欄位。 Visual FoxPro 會產生錯誤，如果您在 CREATE TABLE 中包含多個 PRIMARY KEY 子句。  
  
 UNIQUE *eExpression3*TAG *TagName3*  
 建立候選項目索引。 *eExpression3*指定資料表中的任何欄位的組合。 不過，如果您已經建立主要索引與其中一個主索引鍵的選項，您不能包含主索引鍵所指定的欄位。 標記*TagName3*指定建立的候選項目索引標籤的標記名稱。 索引標籤名稱可以包含最多 10 個字元。  
  
 資料表可以有多個候選項目索引。  
  
 FOREIGN KEY *eExpression4*TAG *TagName4*[NODUP]  
 建立外部 （非主要） 索引，並建立父資料表之關聯性。 *eExpression4*指定外部索引鍵運算式，並*TagName4*指定名稱之外部索引鍵標記的建立 *。* 索引標籤名稱可以包含最多 10 個字元。 包含 NODUP 建立候選項目外部的索引。  
  
 您可以建立多個外部索引的索引資料表，但外部索引的索引運算式必須指定資料表中的不同欄位。  
  
 REFERENCES *TableName3*[TAG *TagName5*]  
 指定要建立持續性的關聯性的父資料表。 包含標記*TagName5*建立父資料表的索引標籤為基礎的關聯性。 索引標籤名稱可以包含最多 10 個字元。 根據預設，如果您省略標記*TagName5，* 使用父資料表的主索引鍵建立關聯性。  
  
 CHECK *eExpression2*[ERROR *cMessageText2*]  
 指定資料表驗證規則。 錯誤*cMessageText2*指定資料表驗證規則執行時，會顯示 Visual FoxPro 的錯誤訊息。 只有當資料瀏覽 視窗中變更或編輯視窗時，會顯示訊息。  
  
 FROM ARRAY *ArrayName*  
 指定現有的陣列，其內容是名稱、 類型、 有效位數和小數位數資料表中的每個欄位的名稱。 可以使用定義陣列的內容**AFIELDS**（） 函式。  
  
## <a name="remarks"></a>備註  
 新的資料表開啟最低可用的工作區域中，並可存取的別名。 不論設定專屬的目前設定，開啟新的資料表。  
  
 如果資料庫已開啟，而且您未包含免費的子句，新的資料表會加入至資料庫。 您無法建立新的資料表與資料庫中的資料表名稱相同。  
  
 如果資料庫已開啟，則 CREATE TABLE-SQL 需要獨佔使用的資料庫。 若要開啟獨佔使用的資料庫，請開啟資料庫中包含排除。  
  
 如果資料庫尚未開啟，當您建立新的資料表，包括名稱、 檢查、 預設、 外部索引鍵、 主索引鍵或參考子句會產生錯誤。  
  
> [!NOTE]  
>  CREATE TABLE 語法會使用逗號來分隔特定 CREATE TABLE 的選項。 此外，NULL、 沒有 NULL、 核取、 預設、 主索引鍵和唯一的子句必須放置包含的資料行定義以括弧括住。  
  
## <a name="driver-remarks"></a>驅動程式備註  
 當您的應用程式傳送的 ODBC SQL 陳述式建立的資料表，資料來源，而 Visual FoxPro ODBC Driver 轉譯為命令 Visual FoxProCREATE 資料表命令，使用下表所示的語法。  
  
|ODBC 語法|Visual FoxPro 語法|  
|-----------------|--------------------------|  
|CREATE TABLE*基底資料表名稱*<br /><br /> (*資料行識別碼資料型別*<br /><br /> [非 NULL]<br /><br /> [，*資料行識別碼資料型別*<br /><br /> [NOT NULL]...)|CREATE TABLE *TableName1* [NAME *LongTableName*]<br /><br /> (*FieldName1* *FieldType*<br /><br /> [(*nFieldWidth* [, *nPrecision*])]<br /><br /> [不是 NULL])|  
  
 當您建立資料表，使用驅動程式時，驅動程式會以允許其他使用者資料表的存取權的建立後立即關閉資料表。 這不同於 Visual FoxPro，讓資料表保持在開啟以獨佔方式在建立時。 不過，如果您包含 CREATE TABLE 陳述式的資料來源上預存程序執行時，資料表是處於開啟狀態。  
  
 如果資料來源是資料庫 （.dbc 檔案），Visual FoxPro ODBC Driver 會建立一個名為資料表*LongTableName*同名*基底資料表名稱*。  
  
### <a name="using-data-definition-language-ddl"></a>使用資料定義語言 (DDL)  
 您不能包含 DDL，在下列位置：  
  
-   批次 SQL 陳述式中所需要的交易  
  
-   在手動認可模式下，需要交易，除非您的應用程式第一次呼叫的陳述式之後**SQLTransact**。  
  
 比方說，如果您想要建立暫存資料表，您應該在建立資料表之前需要使用交易陳述式。 如果您需要的交易的 SQL 陳述式批次中包含 CREATE TABLE 陳述式，則驅動程式會傳回錯誤訊息。  
  
## <a name="see-also"></a>另請參閱  
 [ALTER TABLE-SQL 命令](../../odbc/microsoft/alter-table-sql-command.md)   
 [支援的資料類型 (Visual FoxPro ODBC Driver)](../../odbc/microsoft/supported-data-types-visual-foxpro-odbc-driver.md)   
 [INSERT-SQL 命令](../../odbc/microsoft/insert-sql-command.md)   
 [SELECT - SQL 命令](../../odbc/microsoft/select-sql-command.md)
