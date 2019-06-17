---
title: 資料庫屬性 (選項頁面) | Microsoft 文件
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- sql12.swb.databaseproperties.options.f1
ms.assetid: a3447987-5507-4630-ac35-58821b72354d
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a4420aaf7b11eccecf0b04bb67a55386215f1fc9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62917080"
---
# <a name="database-properties-options-page"></a>資料庫屬性 (選項頁面)
  使用此頁面來檢視或修改選取之資料庫的選項。 在此頁面上的可用選項的相關資訊，請參閱[ALTER DATABASE SET 選項&#40;TRANSACT-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-set-options)。  
  
## <a name="page-header"></a>頁首  
 **定序**  
 從清單中選取以指定資料庫的定序。 如需詳細資訊，請參閱 [設定或變更資料庫定序](../collations/set-or-change-the-database-collation.md)。  
  
 **復原模式**  
 指定下列其中一個復原資料庫模式：[完整]  、[大量記錄]  或 [簡單]  。 如需復原模式的詳細資訊，請參閱[復原模式 &#40;SQL Server&#41;](../backup-restore/recovery-models-sql-server.md)。  
  
 **相容性層級**  
 指定資料庫所支援的最新 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本。 可能的值為  **SQL Server 2014 (120)** 、  **SQL Server 2012 (110)** 和 **SQL Server 2008 (100)** 。 當 SQL Server 2005 資料庫升級到 SQL Server 2014 時，該資料庫的相容性層級會從 90 變更為 100。  SQL Server 2014 不支援 90 相容性層級。 如需詳細資訊，請參閱 [ALTER DATABASE 相容性層級 &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-compatibility-level)。  
  
 **內含項目類型**  
 指定無或部分以指定其是否為自主資料庫。 如需自主資料庫的詳細資訊，請參閱[自主資料庫](contained-databases.md)。 必須先將伺服器屬性 [啟用自主資料庫]  設為 [TRUE]  ，才能將資料庫設為自主。  
  
> [!IMPORTANT]  
>  若啟用部分自主資料庫，會將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的存取控制權委派給資料庫擁有者。 如需詳細資訊，請參閱 [Security Best Practices with Contained Databases](security-best-practices-with-contained-databases.md)。  
  
## <a name="automatic"></a>Automatic  
 **自動關閉**  
 指定最後一個使用者結束後，資料庫是否正常關閉並釋出資源。 可能的值是 `True` 和 `False`。 當它是 `True` 時，資料庫會完整關機，最後一位使用者登出之後，便會將它的資源釋放出來。  
  
 自動建立累加統計資料  
 指定是否在每個分割區的統計資料建立時使用累加選項。 如需累加統計資料的資訊，請參閱 [CREATE STATISTICS &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-statistics-transact-sql)。  
  
 **自動建立統計資料**  
 指定資料庫是否自動建立遺漏的最佳化統計資料。 可能的值是 `True` 和 `False`。 當它是 `True` 時，在最佳化期間，會自動建置查詢最佳化所需要的任何遺漏的統計資料。 如需詳細資訊，請參閱 [CREATE STATISTICS &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-statistics-transact-sql)。  
  
 **自動壓縮**  
 指定資料庫檔案是否可用於定期壓縮。 可能的值是 `True` 和 `False`。 如需詳細資訊，請參閱 [壓縮資料庫](shrink-a-database.md)。  
  
 **自動更新統計資料**  
 指定資料庫是否自動更新過時的最佳化統計資料。 可能的值是 `True` 和 `False`。 當它是 `True` 時，在最佳化期間，會自動建置查詢最佳化所需要的任何過期統計資料。 如需詳細資訊，請參閱 [CREATE STATISTICS &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-statistics-transact-sql)。  
  
 **自動非同步更新統計資料**  
 當`True`，初始化自動更新過期統計資料的查詢將不會等待在編譯之前更新統計資料。 當有可用的更新統計資料時，後續的查詢會使用這些統計資料。  
  
 當`False`，初始化自動更新過期的統計資料的查詢等候，直到更新的統計資料可以用在查詢最佳化計畫中。  
  
 將此選項設定為`True`沒有任何作用，除非**自動 Update Statistics**也會設定為`True`。  
  
## <a name="containment"></a>Containment  
 在自主資料庫中，通常在伺服器層級設定的某些設定可在資料庫層級進行設定。  
  
 **預設全文檢索語言 LCID**  
 指定全文檢索索引資料行的預設語言。 全文檢索索引資料的語言分析相依於資料所用的語言。 這個選項的預設值是伺服器使用的語言。 如需所顯示設定的對應語言，請參閱 [sys.fulltext_languages &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql)。  
  
 **預設語言**  
 所有新自主資料庫使用者的預設語言，除非另有指定。  
  
 **巢狀觸發程序已啟用**  
 允許觸發程序引發其他觸發程序。 觸發程序的巢狀結構，最多可達 32 層。 如需詳細資訊，請參閱 [CREATE TRIGGER &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-trigger-transact-sql) 中的＜巢狀觸發程序＞一節。  
  
 **轉換非搜尋字**  
 如果非搜尋字 (即停用字詞) 導致全文檢索查詢的布林運算傳回零資料列，則會隱藏錯誤訊息。 如需詳細資訊，請參閱 [轉換非搜尋字伺服器組態選項](../../database-engine/configure-windows/transform-noise-words-server-configuration-option.md)。  
  
 **兩位數年份的截止**  
 指出可用兩位數年份格式輸入的最大年份數目。 列出的年份以及前 99 年均可用兩位數年份格式輸入。 所有其他的年份都必須用四位數年份輸入。  
  
 例如，2049 的預設設定指出用 '3/14/49' 格式輸入的日期會被解譯為 2049 年 3 月 14 日，而用 '3/14/50' 格式輸入的日期會被解譯為 1950 年 3 月 14 日。 如需詳細資訊，請參閱 [設定兩位數年份的截止伺服器組態選項](../../database-engine/configure-windows/configure-the-two-digit-year-cutoff-server-configuration-option.md)。  
  
## <a name="cursor"></a>資料指標  
 **認可時關閉資料指標已啟用**  
 指定在開啟此資料指標的交易已經認可之後是否關閉資料指標。 可能的值是 `True` 和 `False`。 當它是 `True` 時，會關閉認可或回復交易時在開啟狀態的任何資料指標。 當它是 `False` 時，在認可交易時，這類資料指標會維持開啟狀態。 當它是 `False` 時，回復交易會關閉任何資料指標，但定義為 INSENSITIVE 或 STATIC 的資料指標除外。 如需詳細資訊，請參閱 [SET CURSOR_CLOSE_ON_COMMIT &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-cursor-close-on-commit-transact-sql)。  
  
 **預設資料指標**  
 指定預設資料指標行為。 當它是 `True` 時，資料指標宣告預設為 LOCAL。 當`False`，[!INCLUDE[tsql](../../includes/tsql-md.md)]資料指標預設為 GLOBAL。  
  
## <a name="filestream"></a>FILESTREAM  
 **FILESTREAM 目錄名稱**  
 針對與選定資料庫相關的 FILESTREAM 資料指定目錄名稱。  
  
 **FILESTREAM 非交易存取**  
 指定下列其中一個選項，可進行透過檔案系統到 FileTable 中所儲存 FILESTREAM 資料的非交易存取：**OFF**、**READ_ONLY** 或 **FULL**。 如果伺服器上未啟用 FILESTREAM，這個值會設定為 OFF 而且會停用。 如需詳細資訊，請參閱 [FileTables &#40;SQL Server&#41;](../blob/filetables-sql-server.md)。  
  
## <a name="miscellaneous"></a>其他  
 **ANSI NULL 預設值**  
 針對在 `NOT NULL` 或 `CREATE TABLE` 陳述式期間，未明確定義為 `ALTER TABLE` 的所有使用者自訂的資料類型或資料行，允許 Null 值 (預設狀態)。 如需詳細資訊，請參閱 [SET ANSI_NULL_DFLT_ON &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-ansi-null-dflt-on-transact-sql) 和 [SET ANSI_NULL_DFLT_OFF &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-ansi-null-dflt-off-transact-sql)。  
  
 **ANSI NULLS 已啟用**  
 使用 Null 值時，指定等於 (`=`) 和不等於 (`<>`) 比較運算子的行為。 可能的值為`True`（開啟） 和`False`（關閉）。 當它是 `True` 時，所有對於 Null 值的比較都會得出 UNKNOWN。 當`False`，非 UNICODE 值與 null 值的比較都會得出`True`如果這兩個值都是 NULL。 如需詳細資訊，請參閱 [SET ANSI_NULLS &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-ansi-nulls-transact-sql)。  
  
 **ANSI 填補已啟用**  
 指定開啟或關閉 ANSI 填補。 允許的值為`True`（開啟） 和`False`（關閉）。 如需詳細資訊，請參閱 [SET ANSI_PADDING &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-ansi-padding-transact-sql)。  
  
 **ANSI 警告已啟用**  
 針對數個錯誤狀況指定 ISO 標準行為。 當`True`，如果 null 值出現在彙總函式 （例如總和、 AVG、 MAX、 MIN、 STDEV、 STDEVP、 VAR、 VARP 或計數），就會產生一則警告訊息。 當`False`，不會發出警告。 如需詳細資訊，請參閱 [SET ANSI_WARNINGS &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-ansi-warnings-transact-sql)。  
  
 **算術中止已啟用**  
 指定是否啟用資料庫選項算術中止。 可能的值是 `True` 和 `False`。 當它是 `True` 時，溢位或除以零的錯誤會終止查詢或批次。 如果交易發生這個錯誤，就會回復交易。 當它是 `False` 時，會顯示警告訊息，但查詢、批次或交易會繼續進行，如同未發生任何錯誤一樣。 如需詳細資訊，請參閱 [SET ARITHABORT &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-arithabort-transact-sql)。  
  
 **串連 Null 產生 Null**  
 指定串連 Null 值時的行為。 當屬性值是`True`， `string` + NULL 會傳回 NULL。 當`False`，結果是`string`。 如需詳細資訊，請參閱 [SET CONCAT_NULL_YIELDS_NULL &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-concat-null-yields-null-transact-sql)。  
  
 **已啟用跨資料庫擁有權鏈結**  
 這個唯讀值指出是否已啟用跨資料庫擁有權鏈結。 當`True`，資料庫可以是來源或目標的跨資料庫擁有權鏈結。 使用 ALTER DATABASE 陳述式設定這個屬性。  
  
 **已啟用日期相互關聯的最佳化**  
 當`True`，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]維護資料庫中 FOREIGN KEY 條件約束所連結且具有任何兩個資料表之間的相互關聯統計資料`datetime`資料行。  
  
 當`False`，不會維護交互關聯統計資料。  
  
 **數值捨入中止**  
 指定資料庫如何處理捨入錯誤。 可能的值是 `True` 和 `False`。 當它是 `True` 時，在運算式中遺失有效位數時，會產生錯誤。 當`False`、 遺失有效位數並不會產生錯誤訊息，並將結果四捨五入成的資料行或變數儲存結果的精確度。 如需詳細資訊，請參閱 [SET NUMERIC_ROUNDABORT &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-numeric-roundabort-transact-sql)。  
  
 **參數化**  
 若為 [SIMPLE]  ，將會根據資料庫的預設行為將查詢參數化。 若為 [FORCED]  ，則 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會將資料庫中的所有查詢都參數化。  
  
 **引號識別碼已啟用**  
 指定如果以引號括住，是否可以使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 關鍵字做為識別碼 (物件或變數名稱)。 可能的值是 `True` 和 `False`。 如需詳細資訊，請參閱 [SET QUOTED_IDENTIFIER &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-quoted-identifier-transact-sql)。  
  
 **遞迴觸發程序已啟用**  
 指定其他觸發程序是否可以引發觸發程序。 可能的值是 `True` 和 `False`。 當設定為`True`，就會啟用觸發程序的遞迴引發。 當設定為`False`，則只會避免直接遞迴。 若要停用間接遞迴，請使用 sp_configure 將巢狀觸發程序伺服器選項設定為 0。 如需相關資訊，請參閱 [建立巢狀觸發程序](../triggers/create-nested-triggers.md)。  
  
 `Trustworthy`  
 顯示時`True`，這個唯讀選項指出[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]可讓您存取資料庫外部的資源在資料庫內建立模擬內容。 在資料庫模組上使用 EXECUTE AS 使用者陳述式或 EXECUTE AS 子句，即可在資料庫內建立模擬內容。  
  
 若要擁有存取權，資料庫的擁有者也需要具有伺服器層級的 AUTHENTICATE SERVER 權限。  
  
 這個屬性也允許在資料庫內建立和執行不安全及外部存取組件。 除了將這個屬性設定為 `True` 之外，資料庫的擁有者也必須具有伺服器層級的 EXTERNAL ACCESS ASSEMBLY 或 UNSAFE ASSEMBLY 權限。  
  
 根據預設，所有使用者資料庫和所有系統資料庫 (除了**MSDB**) 將此屬性設定為`False`。 **model** 和 **tempdb** 資料庫的這個值不可變更。  
  
 只要資料庫是附加至伺服器，就會將 TRUSTWORTHY 設定為 `False`。  
  
 建議在附加 `Trustworthy` 選項時使用憑證和簽章，存取具有模擬內容之資料庫外部的資源。  
  
 若要設定此屬性，請使用 ALTER DATABASE 陳述式。  
  
 **VarDecimal 儲存格式已啟用**  
 此選項是唯讀的開頭為[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]及更新版本中，所有資料庫都會啟用 vardecimal 儲存格式。 這個選項會使用 [sp_db_vardecimal_storage_format](/sql/relational-databases/system-stored-procedures/sp-db-vardecimal-storage-format-transact-sql)。  
  
## <a name="recovery"></a>復原  
 **頁面確認**  
 指定用來探索和報告磁碟 I/O 錯誤所引起之不完整 I/O 交易的選項。 可能的值為 [無]  、[TornPageDetection]  及 [總和檢查碼]  。 如需詳細資訊，請參閱 [管理 suspect_pages 資料表 &#40;SQL Server&#41;](../backup-restore/manage-the-suspect-pages-table-sql-server.md)，在  中還原頁面。  
  
 **目標復原時間 (秒)**  
 指定發生損毀時，復原指定之資料庫的時間上限 (以秒鐘表示)。 如需詳細資訊，請參閱[資料庫檢查點 &#40;SQL Server&#41;](../logs/database-checkpoints-sql-server.md)。  
  
## <a name="state"></a>State  
 **資料庫唯讀**  
 指定資料庫是否為唯讀。 可能的值是 `True` 和 `False`。 當它是 `True` 時，使用者只能讀取資料庫中的資料。 使用者無法修改資料或資料庫物件，但可以使用 DROP DATABASE 陳述式刪除該資料庫。 在指定 [資料庫唯讀]  選項的新值時，資料庫不可在使用中。 master 資料庫為例外，只有系統管理員可以在設定此選項時使用 master。  
  
 **資料庫狀態**  
 檢視資料庫的目前狀態。 它是不可編輯的。 如需 [資料庫狀態]  的詳細資訊，請參閱[資料庫狀態](database-states.md)。  
  
 **限制存取**  
 指定哪些使用者可以存取資料庫。 可能的值為：  
  
-   **多重**  
  
     生產資料庫的一般狀態，允許多位使用者同時存取資料庫。  
  
-   **Single**  
  
     用於維護動作，每次只允許一位使用者存取資料庫。  
  
-   **Restricted**  
  
     只有 db_owner、dbcreator 或 sysadmin 角色的成員可以使用資料庫。  
  
 **加密已啟用**  
 當`True`，此資料庫已啟用資料庫加密。 「資料庫加密金鑰」都需要加密。 如需詳細資訊，請參閱[透明資料加密 &#40;TDE&#41;](../security/encryption/transparent-data-encryption.md)。  
  
## <a name="see-also"></a>另請參閱  
 [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)   
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](/sql/t-sql/statements/create-database-sql-server-transact-sql)  
  
  
