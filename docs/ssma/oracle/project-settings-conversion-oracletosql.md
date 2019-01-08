---
title: 專案設定 （轉換） (OracleToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: a98a5e07-eb5e-47b9-a6f2-e2cb3a18309c
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: bff48432749d6886f58c985adc9cb779303edb17
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/27/2018
ms.locfileid: "52410305"
---
# <a name="project-settings-conversion-oracletosql"></a>專案設定 (轉換) (OracleToSQL)
[轉換] 頁面**專案設定** 對話方塊中包含自訂 SSMA 如何轉換 Oracle 語法來設定[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]語法。  
  
[轉換] 窗格位於**專案設定**並**預設專案設定**對話方塊：  
  
-   若要指定所有的 SSMA 專案設定**工具**功能表上，按一下**預設專案設定**，選取移轉的專案類型，則需要可以檢視或變更設定**移轉目標版本**下拉式清單，然後按一下 **一般**底部的左的窗格和 **轉換**。  
  
-   若要指定目前的專案中，設定**工具**功能表上，按一下**專案設定**，然後按一下**一般**底部的左窗格中，然後按一下  **轉換**。  
  
## <a name="conversion-messages"></a>轉換訊息  
  
|||  
|-|-|  
|詞彙|定義|  
|**產生訊息套用的問題**|指定是否 SSMA 轉換期間產生參考用訊息，顯示在 [輸出] 窗格中，並將它們加入至轉換的程式碼。<br /><br />當您選取的轉換模式**模式** 方塊中，SSMA 會套用下列設定：<br /><br />**預設/開放式模式：** 否<br /><br />**完整模式：** 否|  
  
## <a name="miscellaneous-options"></a>其他選項  
  
|||  
|-|-|  
|詞彙|定義|  
|**轉型為整數的 ROWNUM 運算式**|當 SSMA 會將轉換 ROWNUM 運算式時，它會將運算式轉換成 TOP 子句，後面接著運算式中。 下列範例會示範 ROWNUM Oracle 刪除陳述式中：<br /><br />`DELETE FROM Table1`<br /><br />`WHERE ROWNUM < expression and Field1 >= 2`<br /><br />下列範例會示範產生[!INCLUDE[tsql](../../includes/tsql-md.md)]:<br /><br />`DELETE TOP (expression-1)`<br /><br />`FROM Table1`<br /><br />`WHERE Field1>=2`<br /><br />頂端需要 TOP 子句運算式判斷值為整數。 如果整數是負數，則陳述式會產生錯誤。<br /><br />如果您選取**是**，SSMA 會轉換為整數的運算式。<br /><br />如果您選取**No**，SSMA 會將所有的非整數運算式標示為已轉換的程式碼中的錯誤。<br /><br />當您選取的轉換模式**模式** 方塊中，SSMA 會套用下列設定：<br /><br />**預設/Full 模式：** 否<br /><br />**開放式的模式：** 是|  
|**預設結構描述對應**|此設定會指定如何將 Oracle 結構描述對應至 SQL Server 結構描述。 此設定中有兩個選項：<br /><br />**資料庫的結構描述：** 在這個模式 Oracle 結構描述 'sch1' 將 'dbo' 中 'sch1' 的 SQL Server 資料庫的 SQL Server 結構描述的預設對應。<br /><br />**結構描述的結構描述：** 在此模式中 Oracle 結構描述 'sch1' 將會對應至 [連接] 對話方塊中提供的預設 SQL Server 資料庫中的 'sch1' SQL Server 結構描述的預設。<br /><br />當您選取的轉換模式**模式** 方塊中，SSMA 會套用下列設定：<br /><br />**預設/開放式/Full 模式：** 資料庫的結構描述|  
|**MERGE 陳述式的轉換方式**|如果您選取**使用 INSERT、 UPDATE、 DELETE 陳述式**、 SSMA 會將合併陳述式轉換成 INSERT、 UPDATE、 DELETE 陳述式。<br /><br />如果您選取**使用 MERGE 陳述式**，SSMA 會將合併陳述式中的 MERGE 陳述式轉換[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。<br /><br />**注意：** 此專案設定選項是僅適用於[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2008年[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2012年[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2014年。<br /><br />當您選取的轉換模式**模式** 方塊中，SSMA 會套用下列設定：<br /><br />**預設/開放式/Full 模式：** 使用 MERGE 陳述式|  
|**將使用預設引數的複來呼叫轉換**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 函式不支援函數呼叫中省略的參數。 此外，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]函式和程序不支援做為預設參數值的運算式。<br /><br />如果您選取 **[是]** 函式呼叫會省略參數，SSMA 會插入關鍵字**預設**函式和呼叫的正確位置。 然後，它會將標記的呼叫，但有警告。<br /><br />如果您選取**No**，SSMA 會將標示為錯誤的函式呼叫。<br /><br />當您選取的轉換模式**模式** 方塊中，SSMA 會套用下列設定：<br /><br />**預設/開放式/Full 模式：** 是|  
|**將 COUNT 函式轉換成 COUNT_BIG**|如果 COUNT 函數可能會傳回值大於 2147483647，其為 2<sup>31</sup>-1，您應該將函式轉換成 COUNT_BIG。<br /><br />如果您選取**是**，SSMA 會將所有使用的計數都轉換成 COUNT_BIG。<br /><br />如果您選取**No**，函式會保留為 計數。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會傳回錯誤，如果函式的傳回值大於 2<sup>31</sup>-1。<br /><br />當您選取的轉換模式**模式** 方塊中，SSMA 會套用下列設定：<br /><br />**預設/Full 模式：** 是<br /><br />**開放式的模式：** 否|  
|**FORALL 陳述式轉換 WHILE 陳述式**|定義如何 SSMA 會將 FORALL 迴圈 PL/SQL 集合項目上。<br /><br />如果您選取**是**，SSMA 會建立集合的項目所在位置，擷取的一個接著一個 WHILE 迴圈。<br /><br />如果您選取**No**，SSMA 使用節點 （） 方法，從集合中產生資料列集，並且將它視為單一資料表。 這會更有效率，但可讓輸出程式碼更不容易閱讀。<br /><br />當您選取的轉換模式**模式** 方塊中，SSMA 會套用下列設定：<br /><br />**預設/開放式模式：** 否<br /><br />**完整模式：** 是|  
|**轉換的外部索引鍵資料行上的 SET NULL 參考動作 NOT NULL**|Oracle 可讓您建立 foreign key 條件約束，其中 SET NULL 不執行動作，可能是因為參考的資料行中不允許 null 值。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不允許這類外部索引鍵的組態。<br /><br />如果您選取 **[是]**，SSMA 會產生參考的動作，如 Oracle，但您必須手動變更條件約束，以在載入之前[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 例如，您可以選擇 NO ACTION，而不是設定為 NULL。<br /><br />如果您選取**No**，條件約束將會標示為錯誤。<br /><br />當您選取的轉換模式**模式** 方塊中，SSMA 會套用下列設定：<br /><br />**預設/開放式/Full 模式：** 否|  
|**轉換程序呼叫的函式呼叫**|某些 Oracle 函式定義為獨立的交易，或包含不是有效的陳述式[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 在這些情況下，SSMA 會建立的程序和程序的包裝函式的函式。 已轉換的函式呼叫的實作程序。<br /><br />SSMA 可以轉換的程序呼叫的包裝函式的呼叫。 這會建立更容易閱讀的程式碼，並可改善效能。 不過，內容不一定允許使用它;例如，您無法將選取清單中的函式呼叫取代程序呼叫。 SSMA 會有幾個選項，以涵蓋常見的案例：<br /><br />如果您選取**永遠**，SSMA 嘗試轉換程序呼叫的包裝函式的函式呼叫。 如果目前的內容不允許這項轉換，則會產生一則錯誤訊息。 如此一來，任何函式呼叫會不留在產生的程式碼。<br /><br />如果您選取**盡可能**，SSMA 能讓移至程序呼叫的函式具有輸出參數時，才。 不可能移動時，會移除參數的輸出屬性。 在所有其他情況下 SSMA 會離開函式呼叫。<br /><br />如果您選取**永不**，SSMA 會將所有函式呼叫的函式呼叫。 有時候這項選擇可能是無法接受效能的原因。<br /><br />當您選取的轉換模式**模式** 方塊中，SSMA 會套用下列設定：<br /><br />**預設/開放式/Full 模式：** 如果可能的話|  
|**轉換鎖定 TABLE 陳述式**|SSMA 都可以將許多鎖定資料表陳述式轉換資料表提示。 SSMA 無法轉換包含資料分割，SUBPARTITION，任何鎖定 TABLE 陳述式@dblink，和 NOWAIT 子句，並將標示這類陳述式，並轉換的錯誤訊息。<br /><br />如果您選取**是**，SSMA 會將支援的鎖定 TABLE 陳述式轉換成資料表提示。<br /><br />如果您選取**No**，SSMA 會將標示為使用轉換的錯誤訊息的所有鎖定 TABLE 陳述式。<br /><br />下表顯示如何 SSMA 轉換 Oracle 鎖定模式：<br /><br />**Oracle 的鎖定模式**<br /><br />資料列共用<br /><br />獨佔的資料列<br /><br />SHARE UPDATE = 資料列共用<br /><br />共用<br /><br />共用<br /><br />獨佔<br /><br />**SQL Server 資料表提示**<br /><br />ROWLOCK HOLDLOCK<br /><br />ROWLOCK、 XLOCK，HOLDLOCK<br /><br />ROWLOCK HOLDLOCK<br /><br />TABLOCK HOLDLOCK<br /><br />TABLOCK、 XLOCK，HOLDLOCK<br /><br />TABLOCKX HOLDLOCK<br /><br />當您選取的轉換模式**模式** 方塊中，SSMA 會套用下列設定：<br /><br />**預設/開放式/Full 模式：** 是|  
|**轉換開啟 FOR 陳述式中的 REF CURSOR OUT 參數**|在 Oracle 中，開啟 FOR 陳述式可用來傳回結果集，子程式的 OUT 參數的型別 REF CURSOR。 在  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，預存程序會直接傳回 SELECT 陳述式的結果。<br /><br />SSMA 可以將許多開放 FOR 陳述式轉換成 SELECT 陳述式。<br /><br />如果您選取**是**，SSMA 會將開啟 FOR 陳述式轉換成 SELECT 陳述式，結果集傳回給用戶端。<br /><br />如果您選取**No**，SSMA 中轉換的程式碼和輸出窗格中，將會產生一則錯誤訊息。<br /><br />當您選取的轉換模式**模式** 方塊中，SSMA 會套用下列設定：<br /><br />**預設/開放式/Full 模式：** 是|  
|**將記錄轉換為分隔變數的清單**|SSMA 可轉換 Oracle 記錄，為分隔的變數，並為具有特定結構的 XML 變數。<br /><br />如果您選取**是**，SSMA 轉換成一份分隔變數時可能的記錄。<br /><br />如果您選取**No**，SSMA 會將記錄轉換成具有特定結構的 XML 變數。<br /><br />當您選取的轉換模式**模式** 方塊中，SSMA 會套用下列設定：<br /><br />**預設/開放式/Full 模式：** 是|  
|**轉換 SUBSTR 函式呼叫子函式呼叫**|SSMA 可以將轉換函式呼叫 Oracle SUBSTR [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **子字串**函式呼叫，根據參數數目。 如果 SSMA 無法轉換 SUBSTR 函式呼叫，或不支援的參數數目，SSMA 會將 SUBSTR 函式呼叫轉換成自訂的 SSMA 函式呼叫。<br /><br />如果您選取 **[是]**，SSMA 會將使用到的三個參數的 SUBSTR 函式呼叫轉換[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **substring**。 其他 SUBSTR 函式會轉換成呼叫自訂的 SSMA 函式。<br /><br />如果您選取**No**，SSMA 會將 SUBSTR 函式呼叫轉換成自訂的 SSMA 函式呼叫。<br /><br />當您選取的轉換模式**模式** 方塊中，SSMA 會套用下列設定：<br /><br />**預設/開放式模式：** 是<br /><br />**完整模式：** 否|  
|**轉換子類型**|SSMA 可轉換 PL/SQL 子類型，有兩種：<br /><br />如果您選取 **[是]**，SSMA 會建立[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用者定義類型從子型別，並將它用於此子類型的每個變數。<br /><br />如果您選取**No**，SSMA 會取代所有來源宣告子類型的基礎類型，並如往常般將轉換結果。 在此情況下，在不建立任何其他類型 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]<br /><br />當您選取的轉換模式**模式** 方塊中，SSMA 會套用下列設定：<br /><br />**預設/開放式/Full 模式：** 否|  
|**將轉換的同義字**|下列的 Oracle 物件的同義字可以移轉至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:<br /><br />資料表和物件的資料表<br /><br />檢視和物件的檢視<br /><br />預存程序和函式<br /><br />具體化的檢視<br /><br />**下列的同義字**Oracle 物件可由物件的直接參考取代：<br /><br />序列<br /><br />Packages<br /><br />Java 類別結構描述物件<br /><br />使用者定義的物件類型<br /><br />無法移轉其他的同義字。 SSMA 會產生錯誤訊息為同義字] 和 [使用同義字的所有參考。<br /><br />如果您選取 **[是]**，將建立 SSMA[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]同義字和直接物件參考，根據先前的清單。<br /><br />如果您選取**No**，SSMA 會建立所有的同義字，此處所列的直接物件參考。<br /><br />當您選取的轉換模式**模式** 方塊中，SSMA 會套用下列設定：<br /><br />**預設/開放式/Full 模式：** 是|  
|**轉換 （「 日期 」、 「 格式 」） 時，發生 TO_CHAR**|SSMA 都可以將 Oracle TO_CHAR(date, format) 轉換從 sysdb 資料庫的程序。<br /><br />如果您選取**使用 TO_CHAR_DATE 函式**，SSMA 會將 TO_CHAR （日期，格式） 轉換成 TO_CHAR_DATE 函式使用的英文語言進行轉換。<br /><br />如果您選取**使用 TO_CHAR_DATE_LS 函式 （NLS 照護）**，SSMA 會將 TO_CHAR （日期，格式） 轉換成 TO_CHAR_DATE_LS 函式使用的工作階段語言轉換<br /><br />當您選取的轉換模式**模式** 方塊中，SSMA 會套用下列設定：<br /><br />**預設/開放式模式：** 使用 TO_CHAR_DATE 函式<br /><br />**完整模式：** 使用 TO_CHAR_DATE_LS 函式 （NLS 照護）|  
|**將轉換的交易處理陳述式**|SSMA 可轉換 Oracle 交易處理陳述式：<br /><br />如果您選取 **[是]**，SSMA 會將 Oracle 交易處理陳述式來轉換[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]陳述式。<br /><br />如果您選取**No**，SSMA 會將標示的交易處理陳述式稱為轉換錯誤。<br /><br />**注意：** Oracle 會隱含開啟交易。 若要模擬此行為在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，您必須 BEGIN TRANSACTION 陳述式手動新增您想要啟動交易。 或者，您可以執行 SET IMPLICIT_TRANSACTIONS ON 命令，在您的工作階段的開頭。 SSMA 會自動加入 SET IMPLICIT_TRANSACTIONS ON，將轉換與自發交易的副程式時。<br /><br />當您選取的轉換模式**模式** 方塊中，SSMA 會套用下列設定：<br /><br />**預設/開放式/Full 模式：** 是|  
|**模擬在 ORDER BY 子句中的 Oracle null 行為**|NULL 值會以不同的方式在排列[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]和 Oracle:<br /><br />在  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，NULL 值是已排序的清單中的最小值。 在遞增的清單中，NULL 值最先出現。<br /><br />在 Oracle 中，NULL 值會是已排序的清單中的最高值。 根據預設，NULL 值會出現在遞增順序 清單中最後一個。<br /><br />Oracle 會有 NULL 第一個和最後一個 NULL 子句，這可讓您變更 Oracle 如何排序 Null。<br /><br />SSMA 可以檢查 NULL 的值，以模擬 Oracle ORDER BY 的行為。 它接著先排序所指定的順序，然後再訂單的其他值的 NULL 值。<br /><br />如果您選取**是**，SSMA 會將轉換 Oracle 中的陳述式，來模擬 Oracle ORDER BY 行為的方式。<br /><br />如果您選取**No**，SSMA 會略過 Oracle 規則，並產生錯誤訊息，當它遇到的第一個 NULL 與 NULL 最後一個子句。<br /><br />當您選取的轉換模式**模式** 方塊中，SSMA 會套用下列設定：<br /><br />**預設/開放式模式：** 否<br /><br />**完整模式：** 是|  
|**模擬中選取的資料列計數例外狀況**|如果 INTO 子句的 SELECT 陳述式未傳回任何資料列，Oracle 會引發 NO_DATA_FOUND 例外狀況。 如果陳述式會傳回兩個或多個資料列，則會引發 TOO_MANY_ROWS 例外狀況。 已轉換的陳述式中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]不會引發任何例外狀況，如果資料列計數不同。<br /><br />如果您選取**是**，SSMA 會將呼叫 sysdb 程序 db_error_exact_one_row_check 加入每個 SELECT 陳述式後面。 此程序會模擬 NO_DATA_FOUND 和 TOO_MANY_ROWS 例外狀況。 這是預設值，它可讓您重新產生 Oracle 行為盡可能接近。 您應該一律選擇**是**原始程式碼是否處理這些錯誤的例外狀況處理常式。 請注意，是否 SELECT 陳述式就會發生在使用者定義函式，此模組將會轉換成預存程序中，因為在執行預存程序，並引發例外狀況並不相容[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]函式的內容。<br /><br />如果您選取**No**，將會產生任何例外狀況。 有助於進行 SSMA 會將轉換的使用者定義函式，以及您想要保留中的函式 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]<br /><br />當您選取的轉換模式**模式** 方塊中，SSMA 會套用下列設定：<br /><br />**預設/開放式/Full 模式：** 是|  
|**針對 DBMS_SQL 會產生錯誤。剖析**|如果您選取**錯誤**，SSMA 產生轉換 DBMS_SQL 發生錯誤。剖析。<br /><br />如果您選取**警告**，SSMA 產生在轉換 DBMS_SQL 的警告。剖析。<br /><br />當您選取的轉換模式**模式** 方塊中，SSMA 會套用下列設定：<br /><br />**預設/開放式/Full 模式：** 錯誤|  
|**產生 ROWID 資料行**|SSMA 當建立資料表中的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，它可以建立 ROWID 資料行。 資料移轉時，每個資料列就會取得新的 UNIQUEIDENTIFIER 值 newid （） 函數所產生。<br /><br />如果您選取 **[是]**，ROWID 資料行建立的所有資料表和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]插入值時，會產生 Guid。 一律選擇**是**如果您打算使用 SSMA 測試人員。<br /><br />如果您選取**No**，ROWID 資料行不會新增至資料表。<br /><br />**加入具有觸發程序之資料表的 ROWID 資料行**ROWID 新增包含觸發程序的資料表。<br /><br />**注意：** 在 SQL Server 2005，SQL Server 2008 和 SQL Server 2012 和 2014年的情況下的預設值是**新增 ROWID 資料行的資料表使用觸發程序**。<br /><br />當您選取的轉換模式**模式** 方塊中，SSMA 會套用下列設定：<br /><br />**預設/開放式模式：** 加入具有觸發程序之資料表的 ROWID 資料行<br /><br />**完整模式：** 是|  
|**產生 ROWID 資料行上的唯一索引**|指定是否 SSMA 是否會產生唯一的索引資料行上產生的 ROWID 資料行。 如果選項設定為 [是]，產生唯一的索引，如果它設定為 [否]，唯一的索引不會產生 ROWID 資料行上。<br /><br />當您選取的轉換模式**模式** 方塊中，SSMA 會套用下列設定：<br /><br />**預設/開放式/Full 模式：** 是|  
|**區域模組轉換**|定義巢狀的 oracle （獨立預存程序或函式中宣告） 的子程式轉換的類型。<br /><br />如果您選取**內嵌**，巢狀的子程式呼叫將會取代其主體。<br /><br />如果您選取**預存程序**、 巢狀的子程式將會轉換成 SQL Server 預存程序和其呼叫將會被取代，在此程序呼叫。<br /><br />當您選取的轉換模式**模式** 方塊中，SSMA 會套用下列設定：<br /><br />**預設/開放式/Full 模式：** 內嵌|  
|**在 字串串連中使用 ISNULL**|Oracle 和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]字串串連包含 NULL 值時傳回不同的結果。 Oracle 會將 NULL 值，像是空的字元組。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會傳回 NULL。<br /><br />如果您選取 **[是]**，SSMA 取代 Oracle 串連字元 (&#124;&#124;) 與[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]串連字元 （+）。 SSMA 也會檢查 NULL 值串連這兩端的運算式。<br /><br />如果您選取**No**，SSMA 會取代串連字元，但不會檢查 NULL 值。<br /><br />當您選取的轉換模式**模式** 方塊中，SSMA 會套用下列設定：<br /><br />**預設/開放式/Full 模式：** 是|  
|**取代函式呼叫中使用 ISNULL**|ISNULL 陳述式用於取代函式呼叫中，以模擬 Oracle 行為。 此設定有下列選項：<br /><br />YES<br /><br />否<br /><br />當您選取的轉換模式**模式** 方塊中，SSMA 會套用下列設定：<br /><br />**預設/開放式模式：** 否<br /><br />**完整模式：** 是|  
|**CONCAT 函式呼叫中使用 ISNULL**|CONCAT 函式呼叫會使用 ISNULL 陳述式來模擬 Oracle 行為。 此設定有下列選項：<br /><br />YES<br /><br />否<br /><br />當您選取的轉換模式**模式** 方塊中，SSMA 會套用下列設定：<br /><br />**預設/開放式模式：** 否<br /><br />**完整模式：** 是|  
|**使用原生的轉換函式如果可能的話**|如果您選取**是**，SSMA 會將 TO_CHAR （日期，格式） 轉換成原生的 convert 函式如果可能的話。<br /><br />如果您選取**No**，SSMA 會將 TO_CHAR （日期，格式） 轉換成 TO_CHAR_DATE 或 TO_CHAR_DATE_LS （它 「 轉換 TO_CHAR(date, format) 」 選項所定義的）。<br /><br />當您選取的轉換模式**模式** 方塊中，SSMA 會套用下列設定：<br /><br />**預設/開放式模式：** 是<br /><br />**完整模式：** 否|  
|**使用 SELECT...FOR XML 轉換時選取...INTO 記錄變數**|指定是否要產生的 XML 結果集，當您選取成記錄的變數。<br /><br />如果您選取**是**，SELECT 陳述式傳回的 XML。<br /><br />如果您選取**No**，SELECT 陳述式傳回結果集。<br /><br />當您選取的轉換模式**模式** 方塊中，SSMA 會套用下列設定：<br /><br />**預設/開放式/Full 模式：** 否|  
  
## <a name="returning-clause-conversion"></a>傳回子句轉換  
  
|||  
|-|-|  
|詞彙|定義|  
|**將 DELETE 陳述式中的 RETURNING 子句轉換成輸出**|Oracle 提供的 RETURNING 子句來立即取得已刪除的值。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 搭配 OUTPUT 子句中提供該功能。<br /><br />如果您選取**是**，SSMA 會將轉換的 DELETE 陳述式中的 RETURNING 子句的 OUTPUT 子句。 因為資料表上的觸發程序可能會變更值，傳回的值可能會在不同[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]比在 Oracle 中。<br /><br />如果您選取**No**，SSMA 會產生 SELECT 陳述式來擷取傳回的值的 DELETE 陳述式之前。<br /><br />當您選取的轉換模式**模式** 方塊中，SSMA 會套用下列設定：<br /><br />**預設/開放式/Full 模式：** 是|  
|**將 INSERT 陳述式中的 RETURNING 子句轉換成輸出**|Oracle 提供的 RETURNING 子句來立即取得插入的值。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 搭配 OUTPUT 子句中提供該功能。<br /><br />如果您選取**是**，SSMA 會將 INSERT 陳述式中的 RETURNING 子句轉換成輸出。 因為資料表上的觸發程序可能會變更值，傳回的值可能會在不同[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]比在 Oracle 中。<br /><br />如果您選取**No**，SSMA 模擬 Oracle 功能插入，然後從參考資料表中選取值。<br /><br />當您選取的轉換模式**模式** 方塊中，SSMA 會套用下列設定：<br /><br />**預設/開放式/Full 模式：** 是|  
|**將 UPDATE 陳述式中的 RETURNING 子句轉換成輸出**|Oracle 提供的 RETURNING 子句來立即取得更新後的值。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 搭配 OUTPUT 子句中提供該功能。<br /><br />如果您選取**是**，SSMA 會將 UPDATE 陳述式中的 RETURNING 子句轉換成的 OUTPUT 子句。 因為資料表上的觸發程序可能會變更值，傳回的值可能會在不同[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]比在 Oracle 中。<br /><br />如果您選取**No**，SSMA 會產生 SELECT 陳述式來擷取傳回值的 UPDATE 陳述式之後。<br /><br />當您選取的轉換模式**模式** 方塊中，SSMA 會套用下列設定：<br /><br />**預設/開放式/Full 模式：** 是|  
  
## <a name="sequence-conversion"></a>順序轉換  
  
|||  
|-|-|  
|詞彙|定義|  
|**轉換序列產生器**|在 Oracle 中，您可以使用順序，產生唯一的識別碼。<br /><br />SSMA 可以轉換成以下的順序。<br /><br />使用 SQL Server （這個選項時才可用轉換成 SQL Server 2012 和 SQL Server 2014） 的順序產生器。<br /><br />使用 SSMA 順序產生器。<br /><br />使用資料行的身分識別。<br /><br />轉換成 SQL Server 2012 或 SQL Server 2014 時的預設選項是使用 SQL Server 序列產生器。 不過，SQL Server 2012 和 SQL Server 2014 不支援取得目前的順序值 （例如，Oracle 序列 currval 方法）。 請參閱 SSMA 團隊部落格網站，如需移轉 Oracle 序列 currval 方法的指引。<br /><br />SSMA 也提供將 Oracle 序列轉換為 SSMA 序列模擬器選項。 這是預設選項，當您將轉換成 SQL Server 2012 之前<br /><br />最後，您也可以轉換指派給 SQL Server 的識別值的資料表中的資料行的順序。 您必須指定要在 Oracle 的身分識別資料行之順序之間的對應**資料表** 索引標籤|  
|**轉換 CURRVAL 外部觸發程序**|設為轉換順序產生器時，才會顯示**使用資料行識別**。 Oracle 序列是個別資料表中的物件，因為使用順序的許多資料表會使用觸發程序來產生及插入新的序列值。 SSMA 註解化這些陳述式，或將其標示為錯誤，當註解外會產生錯誤。<br /><br />如果您選取**是**，SSMA 會將標示為外部觸發程序已轉換序列 CURRVAL 但有警告的所有參考。<br /><br />如果您選取**No**，SSMA 會將標示為外部觸發程序已轉換序列 CURRVAL 並產生錯誤的所有參考。|  
  
## <a name="see-also"></a>另請參閱  
[使用者介面參考&#40;OracleToSQL&#41;](../../ssma/oracle/user-interface-reference-oracletosql.md)  
  
