---
title: 專案設定（轉換）（OracleToSQL） |Microsoft Docs
description: 瞭解如何使用 [專案設定] 對話方塊的 [轉換] 頁面，自訂 SSMA 如何將 Oracle 語法轉換成 SQL Server 語法。
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: a98a5e07-eb5e-47b9-a6f2-e2cb3a18309c
author: Shamikg
ms.author: Shamikg
manager: shamikg
ms.openlocfilehash: 86cc0909140190ca7731ddc647fc979a6cd21c7a
ms.sourcegitcommit: 59cda5a481cfdb4268b2744edc341172e53dede4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/02/2020
ms.locfileid: "84293618"
---
# <a name="project-settings-conversion-oracletosql"></a>專案設定 (轉換) (OracleToSQL)
[**專案設定**] 對話方塊的 [轉換] 頁面包含自訂 SSMA 如何將 Oracle 語法轉換成語法的設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
[轉換] 窗格可在 [**專案設定**] 和 [**預設專案設定**] 對話方塊中使用：  
  
-   若要指定所有 SSMA 專案的設定，請在 [**工具**] 功能表上，按一下 [**預設專案設定**]，從 [**遷移目標版本**] 下拉式下選取 [需要查看或變更設定] 的 [遷移專案類型]，然後按一下左窗格底部的 **[一般**]，再按一下 [**轉換**]。  
  
-   若要指定目前專案的設定，請在 [**工具**] 功能表上按一下 [**專案設定**]，然後按一下左窗格底部的 **[一般**]，再按一下 [**轉換**]。  
  
## <a name="conversion-messages"></a>轉換訊息  
  
|||  
|-|-|  
|詞彙|定義|  
|**產生已套用問題的相關訊息**|指定 SSMA 是否會在轉換期間產生參考用訊息，並在 [輸出] 窗格中顯示它們，並將它們加入轉換後的程式碼中。<br /><br />當您在 [**模式]** 方塊中選取轉換模式時，SSMA 會套用下列設定：<br /><br />**預設/開放式模式：** 不<br /><br />**完整模式：** 不|  
  
## <a name="miscellaneous-options"></a>其他選項  
  
|||  
|-|-|  
|詞彙|定義|  
|**將 ROWNUM 運算式轉換成整數**|當 SSMA 轉換 ROWNUM 運算式時，它會將運算式轉換成 TOP 子句，後面接著運算式。 下列範例顯示 Oracle DELETE 子句中的 ROWNUM：<br /><br />`DELETE FROM Table1`<br /><br />`WHERE ROWNUM < expression and Field1 >= 2`<br /><br />下列範例會顯示所產生的 [!INCLUDE[tsql](../../includes/tsql-md.md)] ：<br /><br />`DELETE TOP (expression-1)`<br /><br />`FROM Table1`<br /><br />`WHERE Field1>=2`<br /><br />TOP 子句運算式必須評估為整數。 如果整數是負數，語句將會產生錯誤。<br /><br />如果您選取 **[是]**，SSMA 會將運算式轉換成整數。<br /><br />如果您選取 [**否**]，SSMA 會在轉換後的程式碼中，將所有非整數運算式標示為錯誤。<br /><br />當您在 [**模式]** 方塊中選取轉換模式時，SSMA 會套用下列設定：<br /><br />**預設/完整模式：** 不<br /><br />**開放式模式：** 是的|  
|**預設架構對應**|此設定會指定如何將 Oracle 架構對應至 SQL Server 架構。 此設定中提供兩個選項：<br /><br />**架構到資料庫：** 在此模式中，Oracle 架構 ' sch1 ' 預設會對應到 SQL Server 資料庫 ' sch1 ' 中的 ' dbo ' SQL Server 架構。<br /><br />架構**到架構：** 在此模式中，Oracle 架構 ' sch1 ' 預設會對應至 [連接] 對話方塊中所提供之預設 SQL Server 資料庫中的 ' sch1 ' SQL Server 架構。<br /><br />當您在 [**模式]** 方塊中選取轉換模式時，SSMA 會套用下列設定：<br /><br />**預設/開放式/完整模式：** 架構到資料庫|  
|**MERGE 語句的轉換方式**|如果您選取 [**使用 INSERT]、[update]、[delete] 語句**，SSMA 會將合併語句轉換成 INSERT、UPDATE、delete 語句。<br /><br />如果您選取 [**使用 MERGE 語句**]，SSMA 就會將合併語句轉換成中的 MERGE 語句 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。<br /><br />**注意：** 這個專案設定選項僅適用于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014。<br /><br />當您在 [**模式]** 方塊中選取轉換模式時，SSMA 會套用下列設定：<br /><br />**預設/開放式/完整模式：** 使用 MERGE 語句|  
|**將呼叫轉換為使用預設引數的 subprograms**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]函數不支援省略函式呼叫中的參數。 此外， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 函數和程式不支援運算式做為預設參數值。<br /><br />如果您選取 **[是]** ，而函式呼叫省略了參數，SSMA 就會將關鍵字**default**插入函式中，並在正確的位置呼叫。 然後，它會將呼叫標示為警告。<br /><br />如果您選取 [**否**]，SSMA 會將函數呼叫標示為錯誤。<br /><br />當您在 [**模式]** 方塊中選取轉換模式時，SSMA 會套用下列設定：<br /><br />**預設/開放式/完整模式：** 是的|  
|**將 COUNT 函數轉換成 COUNT_BIG**|如果您的 COUNT 函數可能傳回大於2147483647的值，也就是 2<sup>31</sup>-1，您應該將函數轉換成 COUNT_BIG。<br /><br />如果您選取 **[是]**，SSMA 會將 COUNT 的所有使用轉換成 COUNT_BIG。<br /><br />如果您選取 [**否**]，函式會維持為 [計數]。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]如果函數傳回大於 2<sup>31</sup>-1 的值，將會傳回錯誤。<br /><br />當您在 [**模式]** 方塊中選取轉換模式時，SSMA 會套用下列設定：<br /><br />**預設/完整模式：** 是的<br /><br />**開放式模式：** 不|  
|**將 FORALL 語句轉換成 WHILE 語句**|定義 SSMA 將如何處理 PL/SQL 集合元素上的 FORALL 迴圈。<br /><br />如果您選取 **[是]**，SSMA 會建立一個 WHILE 迴圈，其中逐一抓取集合元素。<br /><br />如果您選取 [**否**]，SSMA 會使用節點（）方法從集合產生資料列集，並使用它做為單一資料表。 這會更有效率，但會使輸出程式碼較不容易閱讀。<br /><br />當您在 [**模式]** 方塊中選取轉換模式時，SSMA 會套用下列設定：<br /><br />**預設/開放式模式：** 不<br /><br />**完整模式：** 是的|  
|**在非 Null 的資料行上，轉換具有 SET Null 引用動作的外鍵**|Oracle 允許建立外鍵條件約束，其中無法執行 SET Null 動作，因為參考的資料行中不允許 Null。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]不允許這種外鍵設定。<br /><br />如果您選取 **[是]**，SSMA 將會產生 Oracle 中的參考動作，但是您必須先進行手動變更，然後再將條件約束載入至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 例如，您可以選擇 [沒有動作]，而不是 [設定 Null]。<br /><br />如果您選取 [**否**]，條件約束將會標示為錯誤。<br /><br />當您在 [**模式]** 方塊中選取轉換模式時，SSMA 會套用下列設定：<br /><br />**預設/開放式/完整模式：** 不|  
|**將函式呼叫轉換為程序呼叫**|有些 Oracle 函式定義為自發交易，或包含在中不正確語句 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 在這些情況下，SSMA 會建立程式和函式，這是程式的包裝函式。 轉換的函式會呼叫執行程式。<br /><br />SSMA 可以將包裝函式的呼叫轉換成對程式的呼叫。 這會建立更容易閱讀的程式碼，並可改善效能。 不過，內容並不一定會允許它;例如，您無法以程序呼叫取代 SELECT 清單中的函式呼叫。 SSMA 有幾個選項可涵蓋常見的案例：<br /><br />如果您選取 [**永遠**]，SSMA 會嘗試將包裝函式呼叫轉換為程序呼叫。 如果目前的內容不允許這種轉換，則會產生錯誤訊息。 如此一來，產生的程式碼中就不會有任何函式呼叫。<br /><br />如果您選取 [**可能的話**]，只有在函式具有輸出參數時，SSMA 才會進行 move to procedure 呼叫。 不可能移動時，會移除參數的 output 屬性。 在所有其他情況下，SSMA 會離開函式呼叫。<br /><br />如果您選取 [**永不**]，SSMA 會將所有函式呼叫保留為函式呼叫。 有時候，這項選擇可能會因為效能的緣故而無法接受。<br /><br />當您在 [**模式]** 方塊中選取轉換模式時，SSMA 會套用下列設定：<br /><br />**預設/開放式/完整模式：** 可能的話|  
|**Convert 鎖定資料表語句**|SSMA 可以將許多鎖定資料表語句轉換成資料表提示。 SSMA 無法轉換包含 PARTITION、SUBPARTITION、和 NOWAIT 子句的任何鎖定資料表語句 @dblink ，而且會將這類語句標記為轉換錯誤訊息。<br /><br />如果您選取 **[是]**，SSMA 會將支援的鎖定資料表語句轉換成資料表提示。<br /><br />如果您選取 [**否**]，SSMA 會將所有鎖定資料表語句標記為轉換錯誤訊息。<br /><br />下表顯示 SSMA 如何轉換 Oracle 鎖定模式：<br /><br />**Oracle 鎖定模式**<br /><br />資料列共用<br /><br />獨佔資料列<br /><br />共用更新 = 資料列共用<br /><br />共用<br /><br />共用<br /><br />獲得<br /><br />**SQL Server 資料表提示**<br /><br />ROWLOCK、HOLDLOCK<br /><br />ROWLOCK、XLOCK、HOLDLOCK<br /><br />ROWLOCK、HOLDLOCK<br /><br />TABLOCK、HOLDLOCK<br /><br />TABLOCK、XLOCK、HOLDLOCK<br /><br />TABLOCKX、HOLDLOCK<br /><br />當您在 [**模式]** 方塊中選取轉換模式時，SSMA 會套用下列設定：<br /><br />**預設/開放式/完整模式：** 是的|  
|**針對 REF CURSOR OUT 參數轉換 OPEN FOR 語句**|在 Oracle 中，可以使用 OPEN-FOR 語句，將結果集傳回給 REF 資料指標類型的 subprogram OUT 參數。 在中 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，預存程式會直接傳回 SELECT 語句的結果。<br /><br />SSMA 可以將許多開啟的語句轉換成 SELECT 語句。<br /><br />如果您選取 **[是]**，SSMA 會將 OPEN-FOR 語句轉換成 select 語句，以將結果集傳回用戶端。<br /><br />如果您選取 [**否**]，SSMA 會在轉換後的程式碼和輸出窗格中產生錯誤訊息。<br /><br />當您在 [**模式]** 方塊中選取轉換模式時，SSMA 會套用下列設定：<br /><br />**預設/開放式/完整模式：** 是的|  
|**將記錄轉換為分隔變數清單**|SSMA 可以將 Oracle 記錄轉換成以特定結構分隔變數和 XML 變數。<br /><br />如果您選取 **[是]**，SSMA 會將記錄轉換成分隔變數的清單（如果可能的話）。<br /><br />如果您選取 [**否**]，SSMA 會將記錄轉換成具有特定結構的 XML 變數。<br /><br />當您在 [**模式]** 方塊中選取轉換模式時，SSMA 會套用下列設定：<br /><br />**預設/開放式/完整模式：** 是的|  
|**將 SUBSTR 函式呼叫轉換成 SUBSTRING 函式呼叫**|SSMA 可以將 Oracle SUBSTR 函式呼叫轉換成 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **substring**函式呼叫，視參數數目而定。 如果 SSMA 無法轉換 SUBSTR 函式呼叫，或不支援參數數目，則 SSMA 會將 SUBSTR 函式呼叫轉換為自訂的 SSMA 函式呼叫。<br /><br />如果您選取 **[是]**，SSMA 會將使用三個參數的 SUBSTR 函式呼叫轉換成 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **子字串**。 其他 SUBSTR 函式將會轉換以呼叫自訂 SSMA 函數。<br /><br />如果您選取 [**否**]，SSMA 會將 SUBSTR 函式呼叫轉換為自訂 SSMA 函式呼叫。<br /><br />當您在 [**模式]** 方塊中選取轉換模式時，SSMA 會套用下列設定：<br /><br />**預設/開放式模式：** 是的<br /><br />**完整模式：** 不|  
|**轉換子類型**|SSMA 可以透過兩種方式來轉換 PL/SQL 子類型：<br /><br />如果您選取 **[是]**，SSMA 會 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 從子類型建立使用者定義型別，並將它用於這個子型別的每個變數。<br /><br />如果您選取 [**否**]，SSMA 將會以基礎類型取代子類型的所有來源宣告，並照常轉換結果。 在此情況下，不會在中建立其他類型[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]<br /><br />當您在 [**模式]** 方塊中選取轉換模式時，SSMA 會套用下列設定：<br /><br />**預設/開放式/完整模式：** 不|  
|**轉換同義字**|下列 Oracle 物件的同義字可以遷移至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ：<br /><br />資料表和物件資料表<br /><br />視圖和物件檢視<br /><br />預存程式和函數<br /><br />具體化檢視<br /><br />**下列的同義字**Oracle 物件可由物件的直接參考取代：<br /><br />序列<br /><br />套件<br /><br />JAVA 類別架構物件<br /><br />使用者定義物件類型<br /><br />其他同義字則無法遷移。 SSMA 會產生同義字的錯誤訊息，以及使用同義字的所有參考。<br /><br />如果您選取 **[是]**，SSMA 會 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 根據先前的清單建立同義字和直接物件參考。<br /><br />如果您選取 [**否**]，SSMA 會針對此處所列的所有同義字建立直接的物件參考。<br /><br />當您在 [**模式]** 方塊中選取轉換模式時，SSMA 會套用下列設定：<br /><br />**預設/開放式/完整模式：** 是的|  
|**轉換 TO_CHAR （日期、格式）**|SSMA 可以將 Oracle TO_CHAR （日期、格式）轉換成 sysdb 資料庫的程式。<br /><br />如果您選取 [**使用 TO_CHAR_DATE**函式]，SSMA 會將 TO_CHAR （日期、格式）轉換為使用英文語言進行轉換的 TO_CHAR_DATE 函數。<br /><br />如果您選取 **[使用 TO_CHAR_DATE_LS 函式（NLS 護理）**]，SSMA 會使用轉換的會話語言，將 TO_CHAR （日期、格式）轉換成 TO_CHAR_DATE_LS 函數<br /><br />當您在 [**模式]** 方塊中選取轉換模式時，SSMA 會套用下列設定：<br /><br />**預設/開放式模式：** 使用 TO_CHAR_DATE 函數<br /><br />**完整模式：** 使用 TO_CHAR_DATE_LS 函數（NLS 護理）|  
|**轉換交易處理語句**|SSMA 可以轉換 Oracle 交易處理語句：<br /><br />如果您選取 **[是**]，SSMA 會將 Oracle 交易處理語句轉換成 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 語句。<br /><br />如果您選取 [**否**]，SSMA 會將交易處理語句標示為轉換錯誤。<br /><br />**注意：** Oracle 會隱含開啟交易。 若要在上模擬這種行為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，您必須在想要開始交易的位置手動加入 BEGIN TRANSACTION 語句。 或者，您也可以在會話的開頭執行 SET IMPLICIT_TRANSACTIONS ON 命令。 SSMA 會在使用自發交易轉換副程式時，自動將 SET IMPLICIT_TRANSACTIONS 新增至。<br /><br />當您在 [**模式]** 方塊中選取轉換模式時，SSMA 會套用下列設定：<br /><br />**預設/開放式/完整模式：** 是的|  
|**模擬 ORDER BY 子句中的 Oracle null 行為**|Null 值在和 Oracle 中的排序方式不同 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ：<br /><br />在中 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，Null 值是已排序清單中的最低值。 在遞增清單中，會先出現 Null 值。<br /><br />在 Oracle 中，Null 值是已排序清單中的最高值。 根據預設，Null 值會出現在 [遞增順序] 清單中的最後一個。<br /><br />Oracle 具有 Null FIRST 和 Null LAST 子句，可讓您變更 Oracle 排序 Null 的方式。<br /><br />SSMA 可以藉由檢查是否有 Null 值來模擬 Oracle ORDER BY 行為。 接著，它會先依指定順序的 Null 值排序，然後再依其他值排序。<br /><br />如果您選取 **[是]**，SSMA 會以模擬 ORACLE ORDER BY 行為的方式來轉換 oracle 語句。<br /><br />如果您選取 [**否**]，SSMA 會忽略 Oracle 規則，並在遇到 null FIRST 和 null LAST 子句時產生錯誤訊息。<br /><br />當您在 [**模式]** 方塊中選取轉換模式時，SSMA 會套用下列設定：<br /><br />**預設/開放式模式：** 不<br /><br />**完整模式：** 是的|  
|**模擬 SELECT 中的資料列計數例外狀況**|如果含有 INTO 子句的 SELECT 語句不會傳回任何資料列，Oracle 就會引發 NO_DATA_FOUND 例外狀況。 如果語句傳回兩個或多個資料列，就會引發 TOO_MANY_ROWS 例外狀況。 如果資料列計數不同，中已轉換的語句不 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會引發任何例外狀況。<br /><br />如果您選取 **[是]**，SSMA 會在每個 select 語句之後 db_error_exact_one_row_check 新增對 sysdb 程式的呼叫。 此程式會模擬 NO_DATA_FOUND 並 TOO_MANY_ROWS 例外狀況。 這是預設值，它可讓您盡可能接近地重現 Oracle 行為。 如果原始程式碼有處理這些錯誤的例外狀況處理常式，您應該一律選擇 [**是]** 。 請注意，如果 SELECT 語句出現在使用者自訂函數中，此模組將會轉換成預存程式，因為執行預存程式和引發例外狀況與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 函數內容不相容。<br /><br />如果您選取 [**否**]，則不會產生任何例外狀況。 當 SSMA 轉換使用者定義的函式，而您想要讓它保持在中時，這項功能會很有用。[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]<br /><br />當您在 [**模式]** 方塊中選取轉換模式時，SSMA 會套用下列設定：<br /><br />**預設/開放式/完整模式：** 是的|  
|**產生 DBMS_SQL 的錯誤。分析**|如果您選取 [**錯誤**]，SSMA 會在轉換 DBMS_SQL 產生錯誤。分析.<br /><br />如果您選取 [**警告**]，SSMA 會在轉換 DBMS_SQL 產生警告。分析.<br /><br />當您在 [**模式]** 方塊中選取轉換模式時，SSMA 會套用下列設定：<br /><br />**預設/開放式/完整模式：** 糾錯|  
|**產生 ROWID 資料行**|當 SSMA 在中建立資料表時 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，它可以建立 ROWID 資料行。 遷移資料時，每個資料列都會取得 newid （）函數所產生的新 UNIQUEIDENTIFIER 值。<br /><br />如果您選取 **[是]**，則會在所有資料表上建立 [ROWID] 資料行，並在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 您插入值時產生 guid。 如果您打算使用 SSMA 測試人員，請一律選擇 [**是]** 。<br /><br />如果您選取 [**否**]，則不會將 ROWID 資料行加入資料表中。<br /><br />針對包含觸發程式的資料表加入 ROWID 資料**行（含觸發**程式的資料表）。<br /><br />**注意：** 如果是 SQL Server 2005，SQL Server 2008 和 SQL Server 2012 和2014的預設設定，就是為**具有觸發程式的資料表新增 [ROWID] 資料行**。<br /><br />當您在 [**模式]** 方塊中選取轉換模式時，SSMA 會套用下列設定：<br /><br />**預設/開放式模式：** 針對具有觸發程式的資料表加入 ROWID 資料行<br /><br />**完整模式：** 是的|  
|**在 ROWID 資料行上產生唯一索引**|指定 SSMA 是否會在 ROWID 產生的資料行上產生唯一的索引資料行。 如果選項設定為 [是]，則會產生唯一索引，如果設定為 [否]，則不會在 [ROWID] 資料行上產生唯一索引。<br /><br />當您在 [**模式]** 方塊中選取轉換模式時，SSMA 會套用下列設定：<br /><br />**預設/開放式/完整模式：** 是的|  
|**本機模組轉換**|定義 oracle nested subprogram （在獨立預存程式或函數中宣告）轉換的類型。<br /><br />如果您選取 [**內嵌**]，則會將嵌套的 subprogram 呼叫取代為其主體。<br /><br />如果您選取 [**預存程式**]，則會將嵌套的 subprogram 轉換成 SQL Server 預存程式，而在此程序呼叫中，將會取代它的呼叫。<br /><br />當您在 [**模式]** 方塊中選取轉換模式時，SSMA 會套用下列設定：<br /><br />**預設/開放式/完整模式：** 隨|  
|**在字串串連中使用 ISNull**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]當字串串連包含 Null 值時，Oracle 和會傳回不同的結果。 Oracle 會將 Null 值視為空的字元集。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]傳回 Null。<br /><br />如果您選取 **[是]**，SSMA 會以 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 串連字號（+）取代 Oracle 串連字號（&#124;&#124;）。 SSMA 也會檢查串連兩端的運算式是否有 Null 值。<br /><br />如果您選取 [**否**]，SSMA 會取代串連字號，但不會檢查是否有 Null 值。<br /><br />當您在 [**模式]** 方塊中選取轉換模式時，SSMA 會套用下列設定：<br /><br />**預設/開放式/完整模式：** 是的|  
|**在 REPLACE 函式呼叫中使用 ISNull**|ISNull 語句是用來取代函式呼叫，以模擬 Oracle 行為。 此設定有下列選項：<br /><br />YES<br /><br />否<br /><br />當您在 [**模式]** 方塊中選取轉換模式時，SSMA 會套用下列設定：<br /><br />**預設/開放式模式：** 不<br /><br />**完整模式：** 是的|  
|**在 CONCAT 函式呼叫中使用 ISNull**|ISNull 語句會用於 CONCAT 函式呼叫中，以模擬 Oracle 行為。 此設定有下列選項：<br /><br />YES<br /><br />否<br /><br />當您在 [**模式]** 方塊中選取轉換模式時，SSMA 會套用下列設定：<br /><br />**預設/開放式模式：** 不<br /><br />**完整模式：** 是的|  
|**可能的話，請使用原生轉換函數**|如果您選取 **[是]**，SSMA 會盡可能將 TO_CHAR （日期、格式）轉換成原生 convert 函數。<br /><br />如果您選取 [**否**]，SSMA 會將 TO_CHAR （日期、格式）轉換成 TO_CHAR_DATE 或 TO_CHAR_DATE_LS （它是由 [轉換 TO_CHAR （日期、格式）] 選項所定義）。<br /><br />當您在 [**模式]** 方塊中選取轉換模式時，SSMA 會套用下列設定：<br /><br />**預設/開放式模式：** 是的<br /><br />**完整模式：** 不|  
|**使用 SELECT .。。轉換 SELECT 時的 FOR XML .。。INTO 記錄變數**|指定當您選取至記錄變數時，是否要產生 XML 結果集。<br /><br />如果您選取 **[是]**，select 語句會傳回 XML。<br /><br />如果您選取 [**否**]，select 語句會傳回結果集。<br /><br />當您在 [**模式]** 方塊中選取轉換模式時，SSMA 會套用下列設定：<br /><br />**預設/開放式/完整模式：** 不|  
  
## <a name="returning-clause-conversion"></a>傳回子句轉換  
  
|||  
|-|-|  
|詞彙|定義|  
|**將 DELETE 子句中的傳回子句轉換成輸出**|Oracle 提供傳回子句做為立即取得已刪除值的方式。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]提供具有 OUTPUT 子句的功能。<br /><br />如果您選取 **[是]**，SSMA 會將 DELETE 子句中的傳回子句轉換成 OUTPUT 子句。 因為資料表上的觸發程式可以變更值，所以傳回的值可能會 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 與 Oracle 中的不同。<br /><br />如果您選取 [**否**]，SSMA 會在 DELETE 子句之前產生 select 語句，以抓取傳回的值。<br /><br />當您在 [**模式]** 方塊中選取轉換模式時，SSMA 會套用下列設定：<br /><br />**預設/開放式/完整模式：** 是的|  
|**將 INSERT 語句中的傳回子句轉換成輸出**|Oracle 提供傳回子句做為立即取得插入值的方式。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]提供具有 OUTPUT 子句的功能。<br /><br />如果您選取 **[是]**，SSMA 會將 INSERT 語句中的傳回子句轉換成輸出。 因為資料表上的觸發程式可以變更值，所以傳回的值可能會 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 與 Oracle 中的不同。<br /><br />如果您選取 [**否**]，SSMA 會藉由插入並選取參考資料表中的值來模擬 Oracle 功能。<br /><br />當您在 [**模式]** 方塊中選取轉換模式時，SSMA 會套用下列設定：<br /><br />**預設/開放式/完整模式：** 是的|  
|**將 UPDATE 語句中的傳回子句轉換成輸出**|Oracle 提供傳回子句做為立即取得更新值的方式。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]提供具有 OUTPUT 子句的功能。<br /><br />如果您選取 **[是]**，SSMA 會將 UPDATE 語句中的傳回子句轉換成 OUTPUT 子句。 因為資料表上的觸發程式可以變更值，所以傳回的值可能會 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 與 Oracle 中的不同。<br /><br />如果您選取 [**否**]，SSMA 會在 UPDATE 語句之後產生 select 語句，以取得傳回值。<br /><br />當您在 [**模式]** 方塊中選取轉換模式時，SSMA 會套用下列設定：<br /><br />**預設/開放式/完整模式：** 是的|  
  
## <a name="sequence-conversion"></a>序列轉換  
  
|||  
|-|-|  
|詞彙|定義|  
|**轉換序列產生器**|在 Oracle 中，您可以使用序列來產生唯一的識別碼。<br /><br />SSMA 可以將序列轉換成下列各項。<br /><br />使用 SQL Server 順序產生器（只有在轉換成 SQL Server 2012 和 SQL Server 2014 時，才可使用此選項）。<br /><br />使用 SSMA 序列產生器。<br /><br />使用資料行識別。<br /><br />轉換成 SQL Server 2012 或 SQL Server 2014 時的預設選項是使用 SQL Server 順序產生器。 不過，SQL Server 2012 和 SQL Server 2014 不支援取得目前的順序值（例如 Oracle sequence currval 方法的值）。 如需遷移 Oracle sequence currval 方法的指引，請參閱 SSMA team blog 網站。<br /><br />SSMA 也提供將 Oracle 序列轉換成 SSMA 序列模擬器的選項。 當您轉換成2012之前的 SQL Server 時，這是預設選項<br /><br />最後，您也可以將指派給資料表中資料行的序列轉換成 SQL Server 識別值。 您必須在 [Oracle**資料表**] 索引標籤上，指定序列與識別資料行之間的對應|  
|**轉換 CURRVAL 外部觸發程式**|只有在 Convert 序列產生器設定為使用資料**行識別**時才會顯示。 因為 Oracle 序列是不同于資料表的物件，所以許多使用順序的資料表會使用觸發程式來產生並插入新的序列值。 將這些語句 SSMA 批註，或在批註 out 會產生錯誤時，將其標示為錯誤。<br /><br />如果您選取 **[是]**，SSMA 會在轉換後的序列 CURRVAL 上，將所有對外部觸發程式的參考標記為警告。<br /><br />如果您選取 [**否**]，SSMA 會在轉換後的序列 CURRVAL 上，將所有對外部觸發程式的參考標記為錯誤。|  
  
## <a name="see-also"></a>另請參閱  
[&#40;OracleToSQL&#41;的使用者介面參考](../../ssma/oracle/user-interface-reference-oracletosql.md)  
  
