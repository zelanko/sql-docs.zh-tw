---
description: " (DB2ToSQL) 轉換 DB2 架構"
title: 轉換 DB2 架構 (DB2ToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 7947efc3-ca86-4ec5-87ce-7603059c75a0
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: b506f7ae063964bc1667b4425028cd35fbc9c91e
ms.sourcegitcommit: a41e1f4199785a2b8019a419a1f3dcdc15571044
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/13/2020
ms.locfileid: "91985096"
---
# <a name="converting-db2-schemas-db2tosql"></a> (DB2ToSQL) 轉換 DB2 架構
當您連接到 DB2、連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，並設定專案和資料對應選項之後，您可以將 DB2 資料庫物件轉換成 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫物件。  
  
## <a name="the-conversion-process"></a>轉換程式  
轉換資料庫物件會從 DB2 取得物件定義、將它們轉換成類似 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的物件，然後將此資訊載入至 SSMA 中繼資料。 它不會將資訊載入至的實例 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 然後，您可以使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中繼資料瀏覽器來查看物件和其屬性。  
  
在轉換期間，SSMA 會將輸出訊息列印至 [輸出] 窗格，並將錯誤訊息列印至 [錯誤清單] 窗格。 使用輸出和錯誤資訊來判斷您是否需要修改 DB2 資料庫或轉換程式，以取得所需的轉換結果。  
  
## <a name="setting-conversion-options"></a>設定轉換選項  
轉換物件之前，請在 [ **專案設定** ] 對話方塊中檢查項目轉換選項。 您可以使用這個對話方塊來設定 SSMA 轉換函式和全域變數的方式。 如需詳細資訊，請參閱 [&#40;轉換&#41; &#40;DB2ToSQL&#41;的專案設定 ](../../ssma/db2/project-settings-conversion-db2tosql.md)。  
  
## <a name="conversion-results"></a>轉換結果  
下表顯示轉換的 DB2 物件和產生的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 物件：  
  
|DB2 物件|產生的 SQL Server 物件|  
|-----------|----------------------------|  
|資料類型|**SSMA 會對應每種類型，如下所示：**<br /><br />CLOB：不支援使用此類型的某些原生函式 (例如 CLOB_EMPTY ( # A2 # A3<br /><br />BLOB：不支援使用此類型的某些原生函式 (例如 BLOB_EMPTY ( # A2 # A3<br /><br />DBLOB：不支援使用此類型的某些原生函式 (例如 DBLOB_EMPTY ( # A2 # A3|  
|使用者定義類型|**SSMA 對應下列使用者定義：**<br /><br />Distinct 類型<br /><br />結構化類型<br /><br />SQL PL 資料類型-注意：不支援弱式資料指標類型。|  
|特殊暫存器|**SSMA 只會列出下列對應暫存器：**<br /><br />目前的時間戳記<br /><br />目前日期<br /><br />目前時間<br /><br />目前的時區<br /><br />目前的使用者<br /><br />SESSION_USER 和使用者<br /><br />SYSTEM_USER<br /><br />目前的 CLIENT_APPLNAME<br /><br />目前的 CLIENT_WRKSTNNAME<br /><br />目前的鎖定超時<br /><br />目前的架構<br /><br />目前的伺服器<br /><br />目前的隔離<br /><br />其他特殊暫存器未對應到 SQL server 語義。|  
|CREATE TABLE|**SSMA maps CREATE TABLE 但有下列例外狀況：**<br /><br />多維度叢集 (MDC) 資料表<br /><br />範圍叢集資料表 (.RCT) <br /><br />資料分割資料表<br /><br />卸離資料表<br /><br />DATA CAPTURE 子句<br /><br />隱含隱藏的選項<br /><br />VOLATILE 選項|  
|CREATE VIEW|SSMA maps CREATE VIEW with ' WITH LOCAL CHECK OPTION '，但其他選項未對應至 SQL server 語義|  
|CREATE INDEX|**SSMA maps CREATE INDEX 具有下列例外狀況：**<br /><br />XML 索引<br /><br />沒有重迭選項的 BUSINESS_TIME<br /><br />分割的子句<br /><br />僅規格選項<br /><br />擴充 USING 選項<br /><br />MINPCTUSED 選項<br /><br />頁面分割選項|  
|觸發程序|**SSMA 會對應下列觸發程式語義：**<br /><br />AFTER/FOR EACH ROW 觸發程式<br /><br />/FOR 每個語句觸發程式之後<br /><br />在每個資料列之前/之前，而不是每個資料列觸發程式|  
|序列|對應。|  
|SELECT 陳述式|**SSMA maps SELECT 具有下列例外狀況：**<br /><br />資料-變更-資料表參考子句-部分對應，但不支援最終資料表<br /><br />資料表參考子句-部分對應，但僅限資料表參考、外部資料表參考、analyze_table 運算式、集合衍生資料表、xmltable 運算式未對應到 SQL server 語義<br /><br />句號-規格子句-未對應。<br /><br />Continue-處理常式子句-未對應。<br /><br />具類型的相互關聯子句-未對應。<br /><br />平行存取解析子句-未對應。|  
|VALUES 語句|已對應。|  
|INSERT 語句|已對應。|  
|UPDATE 語句|**具有下列例外狀況的 SMA MAPS 更新：**<br /><br />僅限資料表參考子句-資料表參考未對應到 SQL server 語義<br /><br />Period 子句-未對應。|  
|MERGE 陳述式|**SSMA maps MERGE 與下列例外狀況：**<br /><br />每個子句的單一與多個出現專案-會對應到 SQL server 語義，以取得每個子句的有限出現次數<br /><br />信號子句-不會對應至 SQL Server 的語義<br /><br />混合的 UPDATE 和 DELETE 子句-不會對應至 SQL Server 的語義<br /><br />Period-子句-不會對應至 SQL Server 的語義|  
|DELETE 子句|**SSMA maps DELETE 具有下列例外狀況：**<br /><br />僅限資料表參考子句-資料表參考未對應到 SQL server 語義<br /><br />Period 子句-不會對應至 SQL Server 的語義|  
|隔離等級和鎖定類型|已對應。|  
|SQL) 程式 (|對應。|  
|外部) 程式 (|需要手動更新。|  
| (來源的程式) |請勿對應至 SQL Server 的語法。|  
|指派語句|已對應。|  
|Procedure 的 CALL 語句|已對應。|  
|CASE 陳述式|已對應。|  
|FOR 語句|已對應。|  
|GOTO 陳述式|已對應。|  
|IF 陳述式|已對應。|  
|反覆運算語句|已對應。|  
|LEAVE 語句|已對應。|  
|LOOP 語句|已對應。|  
|REPEAT 語句|已對應。|  
|RESIGNAL 語句|不支援條件。 訊息可以是選擇性的。|  
|RETURN 語句|已對應。|  
|信號語句|不支援條件。 訊息可以是選擇性的。|  
|WHILE 語句|已對應。|  
|取得診斷聲明|**SSMA maps 會取得診斷，但有下列例外狀況：**<br /><br />ROW_COUNT-已對應。<br /><br />DB2_RETURN_STATUS-已對應。<br /><br />MESSAGE_TEXT-已對應。<br /><br />DB2_SQL_NESTING_LEVEL-不會對應至 SQL Server 的語義<br /><br />DB2_TOKEN_STRING-不會對應至 SQL Server 的語義|  
|資料指標|**SSMA 會對應資料指標，但有下列例外狀況：**<br /><br />配置資料指標語句-未對應至 SQL Server 的語義<br /><br />建立定位器語句的關聯-不會對應至 SQL Server 的語義<br /><br />DECLARE CURSOR 語句-Returnability 子句未對應到 SQL server 語義<br /><br />FETCH 語句-部分對應。 僅支援做為目標的變數。 SQLDA 描述元未對應到 SQL server 語義|  
|變數|對應。|  
|例外狀況、處理常式和條件|**SSMA 會對應「例外狀況處理」，但有下列例外狀況：**<br /><br />EXIT 處理常式-已對應。<br /><br />復原處理常式-已對應。<br /><br />繼續處理常式-未對應。<br /><br />條件-不會對應至 SQL server 語義。|  
|動態 SQL|未對應。|  
|別名|對應。|  
|昵稱|部分對應。 基礎物件需要手動處理|  
|同義字|對應。|  
|DB2 中的標準函式|當 SQL Server 中有對等的函式時，SSMA 會對應 DB2 標準函式：|  
|授權|未對應。|  
|述詞|對應。|  
|SELECT INTO 陳述式|未對應。|  
|值 INTO 語句|未對應。|  
|交易控制|未對應。|  
  
## <a name="converting-db2-database-objects"></a>轉換 DB2 資料庫物件  
若要轉換 DB2 資料庫物件，您必須先選取要轉換的物件，然後讓 SSMA 執行轉換。 若要在轉換期間查看輸出訊息，請在 [ **view** ] 功能表上選取 [ **輸出**]。  
  
**將 DB2 物件轉換成 SQL Server 語法**  
  
1.  在 [DB2 中繼資料瀏覽器] 中，展開 DB2 伺服器，然後展開 [ **架構**]。  
  
2.  選取要轉換的物件：  
  
    -   若要轉換所有架構，請選取 [ **架構**] 旁的核取方塊。  
  
    -   若要轉換或省略資料庫，請選取架構名稱旁邊的核取方塊。  
  
    -   若要轉換或省略物件的類別目錄，請展開架構，然後選取或清除類別旁的核取方塊。  
  
    -   若要轉換或省略個別物件，請展開類別目錄資料夾，然後選取或清除物件旁的核取方塊。  
  
3.  若要轉換所有選取的物件，以滑鼠右鍵按一下 [ **架構** ]，然後選取 [ **轉換架構**]。  
  
    您也可以用滑鼠右鍵按一下物件或其父資料夾，然後選取 [ **轉換架構**]，以轉換物件的個別物件或類別。  
  
## <a name="viewing-conversion-problems"></a>查看轉換問題  
某些 DB2 物件可能不會轉換。 您可以藉由查看摘要轉換報告來判斷轉換成功率。  
  
**若要查看摘要報表**  
  
1.  在 [DB2 中繼資料瀏覽器] 中，選取 [ **架構**]。  
  
2.  在右窗格中，選取 [ **報表** ] 索引標籤。  
  
    此報表會顯示所有已評估或已轉換之資料庫物件的摘要評量報告。 您也可以查看個別物件的摘要報表：  
  
    -   若要查看個別架構的報表，請在 [DB2 中繼資料瀏覽器] 中選取架構。  
  
    -   若要查看個別物件的報表，請在 [DB2 中繼資料瀏覽器] 中選取物件。 具有轉換問題的物件有紅色的錯誤圖示。  
  
針對轉換失敗的物件，您可以查看導致轉換失敗的語法。  
  
**若要查看個別轉換問題**  
  
1.  在 [DB2 中繼資料瀏覽器] 中，展開 [ **架構**]。  
  
2.  展開顯示紅色錯誤圖示的架構。  
  
3.  在 [架構] 底下，展開有紅色錯誤圖示的資料夾。  
  
4.  選取具有紅色錯誤圖示的物件。  
  
5.  在右窗格中，按一下 [ **報表** ] 索引標籤。  
  
6.  [ **報表** ] 索引標籤頂端有一個下拉式清單。 如果清單顯示 **統計資料**，請將選取範圍變更為 [ **來源**]。  
  
    SSMA 會在程式碼的正上方顯示原始程式碼和數個按鈕。  
  
7.  按一下 [ **下一個問題]** 按鈕。 這是紅色的錯誤圖示，其中有指向右邊的箭號。  
  
    SSMA 會反白顯示在目前物件中找到的第一個有問題的原始碼。  
  
針對每個無法轉換的專案，您必須決定要如何使用該物件：  
  
-   您可以在 [ **SQL** ] 索引標籤上修改程式的原始程式碼。  
  
-   您可以修改 DB2 資料庫中的物件，以移除或修改有問題的程式碼。 若要將更新的程式碼載入至 SSMA，您必須更新中繼資料。 如需詳細資訊，請參閱 [連接到 DB2 資料庫 &#40;DB2ToSQL&#41;](../../ssma/db2/connecting-to-db2-database-db2tosql.md)。  
  
-   您可以從遷移中排除物件。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [中繼資料瀏覽器] 和 [Db2 中繼資料瀏覽器] 中，清除專案旁的核取方塊，然後將物件載入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 並從 DB2 遷移資料。  
  
## <a name="next-step"></a>後續步驟  
遷移程式的下一個步驟是將已 [轉換的物件載入 SQL Server](./loading-converted-database-objects-into-sql-server-db2tosql.md)中。  
  
## <a name="see-also"></a>另請參閱  
[將 DB2 資料移轉至 SQL Server &#40;DB2ToSQL&#41;](../../ssma/db2/migrating-db2-data-into-sql-server-db2tosql.md)  
