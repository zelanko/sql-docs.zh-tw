---
title: "專案設定 （轉換） (OracleToSQL) |Microsoft 文件"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016 Preview
ms.assetid: a98a5e07-eb5e-47b9-a6f2-e2cb3a18309c
caps.latest.revision: 15
author: sabotta
ms.author: carlasab
manager: v-thobro
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: afd652370653f4642162fb596bdab88313366354
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="project-settings-conversion-oracletosql"></a>專案設定 （轉換） (OracleToSQL)
[轉換] 頁面的**專案設定**對話方塊包含自訂 SSMA 如何轉換 Oracle 語法來設定[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]語法。  
  
[轉換] 窗格位於**專案設定**和**預設專案設定**對話方塊：  
  
-   若要指定所有的 SSMA 專案設定**工具**功能表上，按一下**預設專案設定**，選取移轉專案類型，不需要檢視或變更設定**移轉的目標版本**下拉式清單，然後按一下 **一般**左的窗格中，然後再按一下底部**轉換**。  
  
-   若要指定目前的專案中，設定**工具**功能表上，按一下**專案設定**，然後按一下 **一般**左的窗格中，然後再按一下底部**轉換**。  
  
## <a name="conversion-messages"></a>轉換訊息  
  
|||  
|-|-|  
|詞彙|定義|  
|**產生有關套用之問題的訊息**|指定是否 SSMA 轉換期間產生參考用訊息，顯示在 [輸出] 窗格中，並將它們加入至轉換的程式碼。<br /><br />當您選取中的轉換模式**模式** 方塊中，SSMA 會套用下列設定：<br /><br />**預設/開放式模式：**否<br /><br />**完整模式：**否|  
  
## <a name="miscellaneous-options"></a>其他選項  
  
|||  
|-|-|  
|詞彙|定義|  
|**轉型 ROWNUM 運算式為整數**|SSMA 會將轉換 ROWNUM 運算式，它會將運算式轉換成 TOP 子句，後面的運算式。 下列範例會顯示 ROWNUM Oracle DELETE 陳述式中：<br /><br />`DELETE FROM Table1`<br /><br />`WHERE ROWNUM < expression and Field1 >= 2`<br /><br />下列範例會顯示所產生[!INCLUDE[tsql](../../includes/tsql_md.md)]:<br /><br />`DELETE TOP (expression-1)`<br /><br />`FROM Table1`<br /><br />`WHERE Field1>=2`<br /><br />頂端需要 TOP 子句運算式判斷值為整數。 如果整數為負數，此陳述式都會產生錯誤。<br /><br />如果您選取**是**，SSMA 會轉換為整數運算式。<br /><br />如果您選取**否**，SSMA 會將所有的非整數運算式標示為轉換的程式碼中的錯誤。<br /><br />當您選取中的轉換模式**模式** 方塊中，SSMA 會套用下列設定：<br /><br />**預設全模式：**否<br /><br />**開放式模式：** [是]|  
|**預設結構描述對應**|此設定指定如何將 Oracle 結構描述對應至 SQL Server 結構描述。 此設定中有兩個選項：<br /><br />**資料庫的結構描述：**在此模式 Oracle 結構描述 'sch1' 會對應至 SQL Server 資料庫 'sch1' 中 'dbo' SQL Server 結構描述預設。<br /><br />**結構描述的結構描述：**在此模式中 Oracle 結構描述 'sch1' 將 'sch1' SQL Server 結構描述 [連接] 對話方塊中提供的預設 SQL Server 資料庫中的預設對應。<br /><br />當您選取中的轉換模式**模式** 方塊中，SSMA 會套用下列設定：<br /><br />**預設/Optimistic/完整模式：**到資料庫的結構描述|  
|**MERGE 陳述式的轉換方式**|如果您選取**使用 INSERT、 UPDATE、 DELETE 陳述式**、 SSMA 會將合併陳述式轉換成 INSERT、 UPDATE、 DELETE 陳述式。<br /><br />如果您選取**使用 MERGE 陳述式**，SSMA 會將合併陳述式轉換成 MERGE 陳述式中[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。<br /><br />**注意：**此專案設定選項是僅適用於[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]2008年[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]2012年[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]2014年。<br /><br />當您選取中的轉換模式**模式** 方塊中，SSMA 會套用下列設定：<br /><br />**預設/Optimistic/完整模式：**使用 MERGE 陳述式|  
|**將使用預設引數的子的呼叫轉換**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]函式不支援函式呼叫中省略參數。 此外，[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]函數和程序不支援做為預設參數值的運算式。<br /><br />如果您選取**是**函式呼叫會省略參數，SSMA 會插入關鍵字**預設**函式與呼叫中的正確位置。 然後，它會將標記的呼叫，但出現警告。<br /><br />如果您選取**否**，SSMA 會將標示為錯誤的函式呼叫。<br /><br />當您選取中的轉換模式**模式** 方塊中，SSMA 會套用下列設定：<br /><br />**預設開放式/全模式：** [是]|  
|**COUNT 函數轉換成 COUNT_BIG**|如果您計數的函式可能會傳回值大於 2147483647，其為 2<sup>31</sup>-1，您應該將函式轉換 COUNT_BIG。<br /><br />如果您選取**是**，SSMA 會將所有使用計數都轉換成 COUNT_BIG。<br /><br />如果您選取**否**，函式會保留為計數。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]如果函式傳回的值大於 2，會傳回錯誤<sup>31</sup>-1。<br /><br />當您選取中的轉換模式**模式** 方塊中，SSMA 會套用下列設定：<br /><br />**預設全模式：** [是]<br /><br />**開放式模式：**否|  
|**FORALL 陳述式轉換成 WHILE 陳述式**|定義如何 SSMA 會將 FORALL 迴圈 PL/SQL 集合項目上。<br /><br />如果您選取**是**，SSMA 建立集合項目所在位置，擷取的一個 WHILE 迴圈。<br /><br />如果您選取**否**，SSMA 使用節點 > （） 方法，從集合中產生資料列集，然後將它當做單一資料表。 這會更有效率，但是讓輸出的程式碼較不容易讀取。<br /><br />當您選取中的轉換模式**模式** 方塊中，SSMA 會套用下列設定：<br /><br />**預設/開放式模式：**否<br /><br />**完整模式：** [是]|  
|**NOT NULL 轉換的外部索引鍵資料行上 SET NULL 參考動作**|Oracle 允許建立 foreign key 條件約束，其中 SET NULL 不執行動作，可能是因為參考的資料行中不允許 null 值。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]不允許這類外部索引鍵的組態。<br /><br />如果您選取**是**、 SSMA 將會產生與 Oracle 中，參考動作，但您必須進行手動變更，然後再載入條件約束[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。 例如，您可以選擇 NO ACTION，而不是設定為 NULL。<br /><br />如果您選取**否**，條件約束將會標示為錯誤。<br /><br />當您選取中的轉換模式**模式** 方塊中，SSMA 會套用下列設定：<br /><br />**預設開放式/全模式：**否|  
|**轉換程序呼叫的函式呼叫**|某些 Oracle 函式定義為自發交易，或包含不是有效的陳述式[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。 在這些情況下，SSMA 會建立的程序和程序的包裝函式的函式。 已轉換的函式呼叫的實作程序。<br /><br />SSMA 可以將呼叫包裝函式的函式轉換的程序呼叫。 這會更容易閱讀的程式碼，並且可以改善效能。 不過，內容不一律允許。例如，您無法將選取清單中的函式呼叫取代程序呼叫。 SSMA 會有幾個選項，以涵蓋常見案例：<br /><br />如果您選取**永遠**，SSMA 嘗試轉換程序呼叫的包裝函式的函式呼叫。 如果目前的內容不允許這項轉換時，會產生錯誤訊息。 如此一來，產生的程式碼中也會不保留任何函式呼叫。<br /><br />如果您選取**盡可能**，SSMA 對移動程序呼叫才函式具有輸出參數。 不可能在移動時，會移除參數的輸出屬性。 在所有其他情況下 SSMA 離開函式呼叫。<br /><br />如果您選取**永不**，SSMA 會將保留在所有函式呼叫的函式呼叫。 有時候這項選擇可能是無法接受因為效能的考量。<br /><br />當您選取中的轉換模式**模式** 方塊中，SSMA 會套用下列設定：<br /><br />**預設/Optimistic/完整模式：**盡可能|  
|**轉換鎖定 TABLE 陳述式**|SSMA 可以將許多鎖定資料表陳述式轉換成資料表提示中。 SSMA 無法轉換包含資料分割，SUBPARTITION，任何鎖定 TABLE 陳述式@dblink，並且使用 NOWAIT 子句，並會將標示為這類陳述式，並轉換的錯誤訊息。<br /><br />如果您選取**是**，SSMA 會將支援的鎖定資料表陳述式轉換成資料表提示。<br /><br />如果您選取**否**，SSMA 會將所有的鎖定 TABLE 陳述式，並轉換的錯誤訊息。<br /><br />下表顯示如何 SSMA 轉換 Oracle 鎖定模式：<br /><br />**Oracle 的鎖定模式**<br /><br />資料列共用<br /><br />獨佔資料列<br /><br />共用更新 = 資料列共用<br /><br />共用<br /><br />共用<br /><br />獨佔<br /><br />**SQL Server 資料表提示**<br /><br />ROWLOCK HOLDLOCK<br /><br />ROWLOCK、 XLOCK，HOLDLOCK<br /><br />ROWLOCK HOLDLOCK<br /><br />TABLOCK HOLDLOCK<br /><br />TABLOCK、 XLOCK，HOLDLOCK<br /><br />TABLOCKX HOLDLOCK<br /><br />當您選取中的轉換模式**模式** 方塊中，SSMA 會套用下列設定：<br /><br />**預設開放式/全模式：** [是]|  
|**轉換開啟 FOR 陳述式的 REF CURSOR OUT 參數**|在 Oracle 中，開啟 FOR 陳述式可用來傳回結果集，子程式的 OUT 參數的型別 REF CURSOR。 在[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，預存程序會直接傳回 SELECT 陳述式的結果。<br /><br />SSMA 可以將許多開啟 FOR 陳述式轉換成 SELECT 陳述式中。<br /><br />如果您選取**是**，SSMA 會將開啟 FOR 陳述式轉換成結果集傳回給用戶端的 SELECT 陳述式。<br /><br />如果您選取**否**，SSMA 會產生錯誤訊息，已轉換的程式碼和輸出窗格。<br /><br />當您選取中的轉換模式**模式** 方塊中，SSMA 會套用下列設定：<br /><br />**預設開放式/全模式：** [是]|  
|**將記錄轉換為分隔變數的清單**|SSMA 可轉換 Oracle 記錄，到分隔的變數，並置於與特定結構的 XML 變數。<br /><br />如果您選取**是**，SSMA 會將記錄轉換成盡可能分隔變數的清單。<br /><br />如果您選取**否**，SSMA 會將記錄轉換成具有特定結構的 XML 變數。<br /><br />當您選取中的轉換模式**模式** 方塊中，SSMA 會套用下列設定：<br /><br />**預設開放式/全模式：** [是]|  
|**轉換 SUBSTR 函式呼叫子函式呼叫**|SSMA 可轉換成 Oracle SUBSTR 函式呼叫[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **substring**函式呼叫，而是根據參數數目。 如果 SSMA 無法轉換 SUBSTR 函式呼叫，或不支援的參數數目，SSMA 會將 SUBSTR 函式呼叫轉換到自訂的 SSMA 函式呼叫。<br /><br />如果您選取**是**，SSMA 會將轉換 SUBSTR 使用三個參數的函式呼叫[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **substring**。 其他 SUBSTR 函式會轉換成呼叫自訂的 SSMA 函式。<br /><br />如果您選取**否**，SSMA 會將 SUBSTR 函式呼叫轉換成自訂 SSMA 函式呼叫。<br /><br />當您選取中的轉換模式**模式** 方塊中，SSMA 會套用下列設定：<br /><br />**預設/開放式模式：** [是]<br /><br />**完整模式：**否|  
|**轉換的子類型**|SSMA 可以轉換 PL/SQL 子類型有兩種：<br /><br />如果您選取**是**，SSMA 會建立[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]使用者定義類型從子型別，並將它用於此子類型的每個變數。<br /><br />如果您選取**否**，SSMA 會取代所有來源宣告子類型的基礎類型，並如往常般將轉換結果。 在此情況下中, 不建立任何其他類型[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]<br /><br />當您選取中的轉換模式**模式** 方塊中，SSMA 會套用下列設定：<br /><br />**預設開放式/全模式：**否|  
|**轉換同義字**|下列的 Oracle 物件的同義字可以移轉到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]:<br /><br />資料表和物件的資料表<br /><br />檢視和物件的檢視<br /><br />預存程序和函式<br /><br />具體化的檢視<br /><br />**下列的同義字**Oracle 物件可能會取代物件的直接參考：<br /><br />序列<br /><br />Packages<br /><br />Java 類別的結構描述物件<br /><br />使用者定義的物件類型<br /><br />無法移轉其他同義字。 SSMA 會產生錯誤訊息，同義字和所有使用同義字的參考。<br /><br />如果您選取**是**，SSMA 會建立[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]同義字和直接物件參考，根據先前的清單。<br /><br />如果您選取**否**，SSMA 會建立所有同義字，此處所列的直接物件參考。<br /><br />當您選取中的轉換模式**模式** 方塊中，SSMA 會套用下列設定：<br /><br />**預設開放式/全模式：** [是]|  
|**轉換 （日期，格式） 時，發生 TO_CHAR**|SSMA 可以將 Oracle TO_CHAR(date, format) 轉換成 sysdb 資料庫中的程序。<br /><br />如果您選取**使用 TO_CHAR_DATE 函式**，SSMA 會將時，發生 TO_CHAR （日期，格式） 轉換成 TO_CHAR_DATE 函式使用英文語言的轉換。<br /><br />如果您選取**使用 TO_CHAR_DATE_LS 函式 （NLS 照護）**，SSMA 會將時，發生 TO_CHAR （日期，格式） 轉換成 TO_CHAR_DATE_LS 函式使用的工作階段語言轉換<br /><br />當您選取中的轉換模式**模式** 方塊中，SSMA 會套用下列設定：<br /><br />**預設/Optimistic 模式：**使用 TO_CHAR_DATE 函式<br /><br />**完整模式：**使用 TO_CHAR_DATE_LS 函式 （NLS 照護）|  
|**轉換的交易處理陳述式**|SSMA 可以轉換 Oracle 交易處理陳述式：<br /><br />如果您選取**是**，SSMA 會將 Oracle 交易處理陳述式，以轉換[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]陳述式。<br /><br />如果您選取**否**，SSMA 會將標示的交易處理轉換錯誤的陳述式。<br /><br />**注意：** Oracle 會隱含開啟交易。 為了模擬此行為上[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，您必須 BEGIN TRANSACTION 陳述式手動新增您想要啟動交易。 或者，您可以執行 SET IMPLICIT_TRANSACTIONS ON 命令，在您的工作階段的開頭。 SSMA 會自動加入 SET IMPLICIT_TRANSACTIONS ON，轉換副程式與自發交易時。<br /><br />當您選取中的轉換模式**模式** 方塊中，SSMA 會套用下列設定：<br /><br />**預設開放式/全模式：** [是]|  
|**模擬在 ORDER BY 子句中的 Oracle null 行為**|NULL 值會以不同的方式在排序[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]和 Oracle:<br /><br />在[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，NULL 值是已排序的清單中的最低值。 在遞增的清單中，NULL 值最先出現。<br /><br />在 Oracle 中，NULL 值會是已排序的清單中最高的值。 根據預設，NULL 值出現於最後遞增的順序清單中。<br /><br />在 oracle 中可以 NULL 第一個和最後一個 NULL 子句，可讓您變更 Oracle 如何排序 Null。<br /><br />SSMA 可以模擬 Oracle ORDER BY 行為，藉由檢查 NULL 值。 它然後先排列所指定的順序，然後再訂單的 NULL 值，其他值。<br /><br />如果您選取**是**，SSMA 會將轉換 Oracle 中的陳述式的方式，來模擬 Oracle ORDER BY 行為。<br /><br />如果您選取**否**，SSMA 會忽略 Oracle 規則，並產生錯誤訊息，當它遇到 null 值第一個和最後一個 NULL 子句。<br /><br />當您選取中的轉換模式**模式** 方塊中，SSMA 會套用下列設定：<br /><br />**預設/開放式模式：**否<br /><br />**完整模式：** [是]|  
|**模擬選取的資料列計數例外狀況**|如果 INTO 子句的 SELECT 陳述式未傳回任何資料列，則 Oracle 引發 NO_DATA_FOUND 例外狀況。 如果陳述式會傳回兩個或多個資料列，會引發 TOO_MANY_ROWS 例外狀況。 已轉換的陳述式中[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]不會引發任何例外狀況，如果其中一個不同的資料列計數。<br /><br />如果您選取**是**，SSMA 會將呼叫 sysdb 程序 db_error_exact_one_row_check 每個 SELECT 陳述式後面。 此程序會模擬 NO_DATA_FOUND 和 TOO_MANY_ROWS 例外狀況。 這是預設值，它可讓您重現盡可能接近 Oracle 行為。 您應該一律選擇**是**如果的原始程式碼已經處理這些錯誤的例外狀況處理常式。 請注意，是否 SELECT 陳述式就會發生在使用者定義函式，此模組將被轉換成預存程序，因為在執行預存程序，並引發例外狀況與不相容[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]函式的內容。<br /><br />如果您選取**否**，將會產生任何例外狀況。 有助於進行 SSMA 會將轉換的使用者定義函式和您想要保留中的函式[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]<br /><br />當您選取中的轉換模式**模式** 方塊中，SSMA 會套用下列設定：<br /><br />**預設開放式/全模式：** [是]|  
|**如 DBMS_SQL 會產生錯誤。剖析**|如果您選取**錯誤**，SSMA 產生轉換 DBMS_SQL 發生錯誤。剖析。<br /><br />如果您選取**警告**，SSMA 產生轉換 DBMS_SQL 警告。剖析。<br /><br />當您選取中的轉換模式**模式** 方塊中，SSMA 會套用下列設定：<br /><br />**預設開放式/全模式：**錯誤|  
|**產生 ROWID 資料行**|SSMA 當建立資料表中的[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，它可以建立 ROWID 資料行。 當您移轉資料時，每個資料列會取得 newid （） 函數所產生的新 UNIQUEIDENTIFIER 值。<br /><br />如果您選取**是**，ROWID 資料行建立的所有資料表和[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]插入值時，會產生 Guid。 一定會選擇**是**如果您打算使用 SSMA 測試人員。<br /><br />如果您選取**否**，ROWID 資料行不會加入至資料表。<br /><br />**加入 ROWID 資料行的資料表與觸發程序**ROWID 加入包含觸發程序的資料表。<br /><br />**注意：**在 SQL Server 2005、 SQL Server 2008 和 SQL Server 2012 和 2014年案例中的預設值是**新增 ROWID 資料行的資料表與觸發程序**。<br /><br />當您選取中的轉換模式**模式** 方塊中，SSMA 會套用下列設定：<br /><br />**預設/Optimistic 模式：**加入 ROWID 資料行的資料表與觸發程序<br /><br />**完整模式：** [是]|  
|**產生 ROWID 資料行上的唯一索引**|指定是否 SSMA 或不產生唯一的索引資料行產生 ROWID 資料行上。 如果選項設定為"YES"時，會產生唯一的索引，如果它設定為 [否]，唯一的索引不會產生 ROWID 資料行上。<br /><br />當您選取中的轉換模式**模式** 方塊中，SSMA 會套用下列設定：<br /><br />**預設開放式/全模式：** [是]|  
|**區域模組轉換**|定義巢狀的 oracle 子程式 （宣告於獨立預存程序或函數） 轉換的類型。<br /><br />如果您選取**內嵌**，巢狀的子程式呼叫將會取代其主體。<br /><br />如果您選取**預存程序**、 巢狀的子程式將會轉換成 SQL Server 預存程序，和其呼叫將會被取代，在此程序呼叫。<br /><br />當您選取中的轉換模式**模式** 方塊中，SSMA 會套用下列設定：<br /><br />**預設開放式/全模式：**內嵌|  
|**字串串連中使用 ISNULL**|Oracle 和[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]字串串連的方式包含 NULL 值時傳回不同的結果。 Oracle 會將 NULL 值，像是空的字元集。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]會傳回 NULL。<br /><br />如果您選取**是**，SSMA 取代 Oracle 串連字元 (&#124; &#124;) 與[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]串連字元 （+）。 SSMA 還會檢查 NULL 值串連兩邊的運算式。<br /><br />如果您選取**否**，SSMA 會取代串連字元，但不是檢查是否有 NULL 值。<br /><br />當您選取中的轉換模式**模式** 方塊中，SSMA 會套用下列設定：<br /><br />**預設開放式/全模式：** [是]|  
|**取代函式呼叫中應使用 ISNULL**|ISNULL 陳述式用於取代函式呼叫，以模擬 Oracle 行為。 此設定有下列選項：<br /><br />YES<br /><br />否<br /><br />當您選取中的轉換模式**模式** 方塊中，SSMA 會套用下列設定：<br /><br />**預設/開放式模式：**否<br /><br />**完整模式：** [是]|  
|**CONCAT 函式呼叫中應使用 ISNULL**|CONCAT 函式呼叫使用 ISNULL 陳述式來模擬 Oracle 行為。 此設定有下列選項：<br /><br />YES<br /><br />否<br /><br />當您選取中的轉換模式**模式** 方塊中，SSMA 會套用下列設定：<br /><br />**預設/開放式模式：**否<br /><br />**完整模式：** [是]|  
|**使用原生 convert 函數時可能**|如果您選取**是**，SSMA 會將時，發生 TO_CHAR （日期，格式） 轉換成原生 convert 函數時可能。<br /><br />如果您選取**否**，SSMA 會將時，發生 TO_CHAR （日期，格式） 轉換成 TO_CHAR_DATE 或 TO_CHAR_DATE_LS （它由 「 轉換 TO_CHAR(date, format) 」 選項所定義）。<br /><br />當您選取中的轉換模式**模式** 方塊中，SSMA 會套用下列設定：<br /><br />**預設/開放式模式：** [是]<br /><br />**完整模式：**否|  
|**使用 SELECT...FOR XML 轉換時選取...記錄變數的 INTO**|指定是否產生 XML 結果集，當您選取放入記錄變數中。<br /><br />如果您選取**是**，SELECT 陳述式傳回的 XML。<br /><br />如果您選取**否**，SELECT 陳述式會傳回結果集。<br /><br />當您選取中的轉換模式**模式** 方塊中，SSMA 會套用下列設定：<br /><br />**預設開放式/全模式：**否|  
  
## <a name="returning-clause-conversion"></a>傳回子句轉換  
  
|||  
|-|-|  
|詞彙|定義|  
|**將 DELETE 陳述式中的 RETURNING 子句轉換成輸出**|Oracle 提供的 RETURNING 子句來立即取得已刪除的值。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]搭配 OUTPUT 子句中提供該功能。<br /><br />如果您選取**是**，SSMA 會將轉換 DELETE 陳述式中的 RETURNING 子句的 OUTPUT 子句。 因為資料表上的觸發程序可以變更值，傳回的值可能會在不同[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]比它在 Oracle 中。<br /><br />如果您選取**否**，SSMA 會產生 SELECT 陳述式來擷取傳回的值的 DELETE 陳述式之前。<br /><br />當您選取中的轉換模式**模式** 方塊中，SSMA 會套用下列設定：<br /><br />**預設開放式/全模式：** [是]|  
|**將 INSERT 陳述式中的 RETURNING 子句轉換成輸出**|Oracle 提供的 RETURNING 子句來立即取得插入的值。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]搭配 OUTPUT 子句中提供該功能。<br /><br />如果您選取**是**，SSMA 會將 INSERT 陳述式中的 RETURNING 子句轉換成輸出。 因為資料表上的觸發程序可以變更值，傳回的值可能會在不同[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]比它在 Oracle 中。<br /><br />如果您選取**否**，SSMA 插入，然後從參考資料表中選取值模擬 Oracle 功能。<br /><br />當您選取中的轉換模式**模式** 方塊中，SSMA 會套用下列設定：<br /><br />**預設開放式/全模式：** [是]|  
|**將 UPDATE 陳述式中的 RETURNING 子句轉換成輸出**|Oracle 提供的 RETURNING 子句來立即取得更新的值。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]搭配 OUTPUT 子句中提供該功能。<br /><br />如果您選取**是**，SSMA 會將 UPDATE 陳述式中的 RETURNING 子句轉換成的 OUTPUT 子句。 因為資料表上的觸發程序可以變更值，傳回的值可能會在不同[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]比它在 Oracle 中。<br /><br />如果您選取**否**，SSMA 會產生 SELECT 陳述式來擷取傳回值的 UPDATE 陳述式之後。<br /><br />當您選取中的轉換模式**模式** 方塊中，SSMA 會套用下列設定：<br /><br />**預設開放式/全模式：** [是]|  
  
## <a name="sequence-conversion"></a>順序轉換  
  
|||  
|-|-|  
|詞彙|定義|  
|**轉換順序產生器**|在 Oracle 中，您可以使用順序，產生唯一的識別碼。<br /><br />SSMA 可以轉換成以下的順序。<br /><br />使用 SQL Server 序列產生器 （此選項時才可用轉換為 SQL Server 2012 和 SQL Server 2014）。<br /><br />使用 SSMA 順序產生器。<br /><br />使用資料行的識別。<br /><br />轉換成 SQL Server 2012 或 SQL Server 2014 時的預設選項是使用 SQL Server 序列產生器。 不過，SQL Server 2012 和 SQL Server 2014 不支援取得目前的順序值 （例如，Oracle 序列 currval 方法）。 請參閱移轉 Oracle 序列 currval 方法上的指引 SSMA 團隊部落格網站。<br /><br />SSMA 還提供用以將 Oracle 序列轉換成 SSMA 順序模擬器選項。 這是預設選項，當您轉換成 SQL Server 2012 之前<br /><br />最後，您也可以轉換指派給 SQL Server 的識別值的資料表中的資料行的順序。 您必須指定 Oracle identity 資料行序列之間的對應**資料表** 索引標籤|  
|**轉換 CURRVAL 外部觸發程序**|設為轉換順序產生器時，才會顯示**使用資料行識別**。 Oracle 序列是與資料表不同的物件，因為使用順序的多個資料表使用觸發程序產生並插入新的序列值。 SSMA 註解化這些陳述式，或將其標示為錯誤，當超出註解會產生錯誤。<br /><br />如果您選取**是**，SSMA 會將標示為外部觸發程序上的轉換後排序 CURRVAL 警告的所有參考。<br /><br />如果您選取**否**，SSMA 會將標示為外部觸發程序上的轉換後排序 CURRVAL 並產生錯誤的所有參考。|  
  
## <a name="see-also"></a>另請參閱  
[使用者介面參考 &#40; OracleToSQL &#41;](../../ssma/oracle/user-interface-reference-oracletosql.md)  
  

