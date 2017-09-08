---
title: "轉換 DB2 結構描述 (DB2ToSQL) |Microsoft 文件"
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
- Azure SQL Database
- SQL Server
ms.assetid: 7947efc3-ca86-4ec5-87ce-7603059c75a0
caps.latest.revision: 9
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: a1463d2f715bb957c28064840dcf0ce33e3a0f1e
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="converting-db2-schemas-db2tosql"></a>轉換 DB2 結構描述 (DB2ToSQL)
您已經連接到 DB2 之後，連接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，設定專案和對應的資料選項，您可以將轉換至 DB2 資料庫物件和[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]資料庫物件。  
  
## <a name="the-conversion-process"></a>轉換程序  
轉換的資料庫物件從 DB2 接受物件定義、 將它們轉換成類似[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]物件，然後再將這項資訊載入至 SSMA 中繼資料。 不會載入到的執行個體資訊[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。 您接著可以使用檢視物件和其屬性[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]中繼資料總管。  
  
在轉換期間，SSMA 會列印至輸出窗格的輸出訊息和錯誤訊息 [錯誤清單] 窗格。 若要判斷您是否需要修改您的 DB2 資料庫或您要取得所需的轉換結果的轉換程序使用的輸出和錯誤的資訊。  
  
## <a name="setting-conversion-options"></a>設定轉換選項  
在轉換前的物件，請檢閱中的專案轉換選項**專案設定** 對話方塊。 藉由使用此對話方塊中，您可以設定 SSMA 如何將轉換函式和全域變數。 如需詳細資訊，請參閱[專案設定 &#40;轉換 &#41;&#40; DB2ToSQL &#41;](../../ssma/db2/project-settings-conversion-db2tosql.md).  
  
## <a name="conversion-results"></a>轉換結果  
下表顯示 DB2 的物件轉換，並產生[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]物件：  
  
|DB2 物件|產生 SQL Server 物件|  
|-----------|----------------------------|  
|資料型別|**SSMA 會將對應下列下面所列以外的每個類型：**<br /><br />CLOB： 這個類型的某些原生函式不支援 (例如 CLOB_EMPTY())<br /><br />BLOB： 這個類型的某些原生函式不支援 (例如 BLOB_EMPTY())<br /><br />DBLOB： 這個類型的某些原生函式不支援 (例如 DBLOB_EMPTY())|  
|使用者定義類型|**SSMA 會將對應下列使用者定義：**<br /><br />不同類型<br /><br />結構化型別<br /><br />SQL PL 資料型別 – 附註： 不支援弱式資料指標類型。|  
|特殊暫存器|**SSMA 只會將下面所列的暫存器對應：**<br /><br />目前的時間戳記<br /><br />目前的日期<br /><br />目前的時間<br /><br />目前的時區<br /><br />目前的使用者<br /><br />SESSION_USER 和使用者<br /><br />SYSTEM_USER<br /><br />目前 CLIENT_APPLNAME<br /><br />目前 CLIENT_WRKSTNNAME<br /><br />目前鎖定逾時。<br /><br />目前的結構描述<br /><br />目前的伺服器<br /><br />目前的隔離<br /><br />其他特殊的註冊不被對應到 SQL server 的語意。|  
|CREATE TABLE|**SSMA 會將 CREATE TABLE 對應但有下列例外狀況：**<br /><br />多維度的叢集 (MDC) 資料表<br /><br />範圍叢集資料表 (RCT)<br /><br />資料分割資料表<br /><br />中斷連結的資料表<br /><br />資料擷取子句<br /><br />IMPLICITLY 隱藏選項<br /><br />動態選項|  
|CREATE VIEW|SSMA 會將對應建立的檢視，以 ' WITH 本機 CHECK OPTION'，但其他選項不對應到 SQL server 的語意|  
|CREATE INDEX|**SSMA 對應建立索引，但有下列例外狀況：**<br /><br />XML 索引<br /><br />BUSINESS_TIME 不重疊的選項<br /><br />資料分割的子句<br /><br />只有規格選項<br /><br />使用擴充選項<br /><br />MINPCTUSED 選項<br /><br />頁面分割選項|  
|觸發程序|**SSMA 會將對應下列觸發程序語意：**<br /><br />之後/EACH 資料列觸發程序<br /><br />/FOR 之後觸發每個陳述式<br /><br />之前 / EACH 資料列，而不是 / EACH 資料列觸發程序|  
|序列|對應。|  
|SELECT 陳述式|**SSMA 對應選取有下列例外：**<br /><br />資料變更的資料表參考子句 – 部分對應，但最後的資料表並不支援<br /><br />資料表參考子句 – 部分對應，僅限-資料表的參考、 外部資料表參考、 analyze_table 運算式，但集合衍生資料表、 資料運算式不對應到 SQL server 的語意<br /><br />期間規格子句 – 未對應。<br /><br />繼續處理常式子句 – 未對應。<br /><br />輸入的相互關聯子句 – 未對應。<br /><br />並行存取解析子句 – 未對應。|  
|VALUES 陳述式|對應。|  
|INSERT 陳述式|對應。|  
|UPDATE 陳述式|S**SMA 對應更新，但有下列例外狀況：**<br /><br />資料表參考子句 – 僅限-資料表的參考不會對應到 SQL server 的語意<br /><br />週期子句 – 未對應。|  
|MERGE 陳述式|**SSMA 對應合併，但有下列例外狀況：**<br /><br />單一和多個出現的每個子句-對應到每個子句的有限次數的 SQL server 語意<br /><br />訊號子句 – 不會對應到 SQL Server 的語意<br /><br />混合的更新和刪除子句 – 不會對應到 SQL Server 的語意<br /><br />期間子句 – 不會對應到 SQL Server 的語意|  
|DELETE 陳述式|**SSMA 對應刪除，但有下列例外狀況：**<br /><br />資料表參考子句 – 僅限-資料表的參考不會對應到 SQL server 的語意<br /><br />週期子句 – 不會對應到 SQL Server 的語意|  
|隔離等級，且鎖定類型|對應。|  
|程序 (SQL)|對應。|  
|程序 （外部）|需要手動更新。|  
|（來源） 的程序|未對應至 SQL Server 的語意。|  
|指派陳述式|對應。|  
|如需程序的 CALL 陳述式|對應。|  
|CASE 陳述式|對應。|  
|陳述式|對應。|  
|GOTO 陳述式|對應。|  
|IF 陳述式|對應。|  
|反覆運算陳述式|對應。|  
|保留陳述式|對應。|  
|迴圈陳述式|對應。|  
|重複執行陳述式|對應。|  
|RESIGNAL 陳述式|不支援條件。 訊息可以是選擇性的。|  
|RETURN 陳述式|對應。|  
|訊號陳述式|不支援條件。 訊息可以是選擇性的。|  
|WHILE 陳述式|對應。|  
|取得診斷陳述式|**SSMA 對應取得診斷，但有下列例外狀況：**<br /><br />對應 ROW_COUNT –。<br /><br />對應 DB2_RETURN_STATUS –。<br /><br />對應 MESSAGE_TEXT –。<br /><br />DB2_SQL_NESTING_LEVEL-不會對應到 SQL Server 的語意<br /><br />DB2_TOKEN_STRING-不會對應到 SQL Server 的語意|  
|資料指標|**SSMA 會將資料指標對應但有下列例外狀況：**<br /><br />配置資料指標陳述式-不會對應到 SQL Server 的語意<br /><br />建立關聯的定位器陳述式-不會對應到 SQL Server 的語意<br /><br />DECLARE CURSOR 陳述式-Returnability 子句未對應到 SQL server 的語意<br /><br />FETCH 陳述式 – 部分對應。 僅支援做為目標的變數。 Sqlda 裡的描述元未對應到 SQL server 的語意|  
|變數|對應。|  
|例外狀況、 處理常式和條件|**SSMA 對應 」 例外狀況處理 」，但有下列例外狀況：**<br /><br />結束處理常式 – 對應。<br /><br />復原處理常式 – 對應。<br /><br />繼續處理常式 – 未對應。<br /><br />條件-它不會對應到 SQL server 的語意。|  
|動態 SQL|未對應。|  
|Aliases|對應。|  
|別名|部分的對應。 手動處理都需要基礎物件|  
|同義字|對應。|  
|DB2 中的標準函式|使用 SQL Server 中相等的函式時，SSMA 對應 DB2 標準函式：|  
|授權|未對應。|  
|述詞|對應。|  
|SELECT INTO 陳述式|未對應。|  
|值 INTO 陳述式|未對應。|  
|交易控制|未對應。|  
  
## <a name="converting-db2-database-objects"></a>轉換 DB2 資料庫物件  
轉換 DB2 資料庫物件，您必須先選取您想要轉換，該物件並則有 SSMA 執行轉換。 若要進行轉換時，檢視輸出訊息上**檢視**功能表上，選取**輸出**。  
  
**若要將 DB2 物件轉換成 SQL Server 語法**  
  
1.  在 DB2 中繼資料總管，展開 DB2 伺服器，然後再展開**結構描述**。  
  
2.  選取要轉換的物件：  
  
    -   若要轉換的所有結構描述，選取核取方塊旁的 **結構描述**。  
  
    -   若要轉換或省略資料庫，選取結構描述名稱旁邊的核取方塊。  
  
    -   轉換或省略物件的類別，結構描述中，依序展開，然後選取或清除類別旁的核取方塊。  
  
    -   轉換或省略個別物件，展開類別目錄資料夾，然後選取或清除物件旁的核取方塊。  
  
3.  若要將所有選取的物件，以滑鼠右鍵按一下**結構描述**選取**轉換結構描述**。  
  
    您也可以轉換個別物件或類別目錄的物件，該物件或其父資料夾上按一下滑鼠右鍵，然後選取**轉換結構描述**。  
  
## <a name="viewing-conversion-problems"></a>檢視轉換問題  
DB2 的某些物件可能不會轉換。 您可以檢視摘要轉換報表來判斷轉換成功率。  
  
**若要檢視摘要報表**  
  
1.  在 DB2 中繼資料總管，選取**結構描述**。  
  
2.  在右窗格中，選取**報表** 索引標籤。  
  
    此報告會顯示摘要評估報表中的所有資料庫物件評估或轉換。 您也可以檢視個別物件的摘要報告：  
  
    -   若要檢視報表中的個別結構描述，請在 DB2 中繼資料總管 選取的結構描述。  
  
    -   若要檢視報表中的個別物件，請在 DB2 中繼資料總管 選取的物件。 已轉換問題的物件具有紅色錯誤圖示。  
  
無法轉換的物件，您可以檢視導致轉換失敗的語法。  
  
**若要檢視個別轉換問題**  
  
1.  在 DB2 中繼資料總管，依序展開**結構描述**。  
  
2.  展開結構描述會顯示紅色錯誤圖示。  
  
3.  在結構描述中，展開一個資料夾具有紅色錯誤圖示。  
  
4.  選取具有紅色錯誤圖示的物件。  
  
5.  在右窗格中，按一下 [**報表**] 索引標籤。  
  
6.  在頂端**報表** 索引標籤是下拉式清單。 如果此清單會顯示**統計資料**，變更選取範圍到**來源**。  
  
    SSMA 會顯示與原始程式碼和數個程式碼正上方的按鈕。  
  
7.  按一下**下一個問題** 按鈕。 這是指向右側的箭號紅色錯誤圖示。  
  
    SSMA 會反白顯示在目前的物件中找到的第一個有問題的原始碼。  
  
針對無法轉換每個項目，您必須決定您想要使用該物件：  
  
-   您可以修改程序的程式碼上**SQL**  索引標籤。  
  
-   您可以修改以移除或修改程式碼有問題的 DB2 資料庫中的物件。 若要更新的程式碼載入 SSMA，您必須更新的中繼資料。 如需詳細資訊，請參閱[連接到 DB2 資料庫 &#40; DB2ToSQL &#41;](../../ssma/db2/connecting-to-db2-database-db2tosql.md)。  
  
-   您可以從移轉排除的物件。 在[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]中繼資料總管和 DB2 中繼資料總管，清除項目旁邊的核取方塊，然後再載入物件到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]和從 DB2 移轉資料。  
  
## <a name="next-step"></a>下一個步驟  
移轉程序的下一個步驟是[已轉換的物件載入 SQL Server](http://msdn.microsoft.com/en-us/f4ea1ced-9f9f-4a9d-88ab-81dbab64adc3)。  
  
## <a name="see-also"></a>另請參閱  
[將 DB2 資料移轉到 SQL Server &#40; DB2ToSQL &#41;](../../ssma/db2/migrating-db2-data-into-sql-server-db2tosql.md)  
  

