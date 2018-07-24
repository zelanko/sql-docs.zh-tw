---
title: 已更新 - 關聯式資料庫文件 | Microsoft Docs
description: 針對關聯式資料庫，顯示文件最新變更之已更新內容的程式碼片段。
manager: craigg
author: MightyPen
ms.author: genemi
ms.topic: conceptual
ms.custom: UpdArt.exe
ms.suite: sql
ms.technology: release-landing
ms.prod: sql
ms.prod_service: sql-non-specified
ms.component: relational-databases
ms.date: 04/28/2018
ms.openlocfilehash: 4f962279eb30e15b395f96417cc5e03aa1dbcfad
ms.sourcegitcommit: c8f7e9f05043ac10af8a742153e81ab81aa6a3c3
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/17/2018
ms.locfileid: "39087770"
---
# <a name="new-and-recently-updated-relational-databases-docs"></a>新的與最近更新的文章： 關聯式資料庫文件



Microsoft 幾乎每天都會在其 [Docs.Microsoft.com](http://docs.microsoft.com/) 文件網站上更新一些現有文章。 本文會顯示最近更新文章的摘錄。 可能也會列出新文章的連結。

本文是透過定期重新執行的程式所產生。 摘錄中偶爾會出現示不完整的格式，或顯示為來自來源文章的 Markdown。 影像永遠不會顯示在這裡。

新的更新會報告下列日期範圍和主旨：



- *更新日期範圍：* &nbsp; **2018-02-03** &nbsp; 至 &nbsp; **2018-04-28**
- *主旨區域：* &nbsp; **關聯式資料庫**。




&nbsp;

## <a name="new-articles-created-recently"></a>最近建立的新文章

下列連結會跳至最近新增的新文章。


1. [聯結 (SQL Server)](performance/joins.md)
2. [子查詢 (SQL Server)](performance/subqueries.md)
3. [設定 Always On 可用性群組中的複寫散發資料庫](replication/configure-distribution-availability-group.md)
4. [SQL 資料探索與分類](security/sql-data-discovery-and-classification.md)
5. [交易鎖定與資料列版本設定指南](sql-server-transaction-locking-and-row-versioning-guide.md)
6. [sys.dm_os_job_object (Azure SQL Database)](system-dynamic-management-views/sys-dm-os-job-object-transact-sql.md)
7. [Filestream 和 FileTable 系統預存程序 (Transact-SQL)](system-stored-procedures/filestream-and-filetable-system-stored-procedures.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>更新文章與摘要

本節會顯示從最近發生大規模更新的文章所收集的更新摘錄。

此處顯示的摘錄不同於其適當語意內容。 此外，有時摘錄也與實際文件四周的重要 Markdown 語法不同。 因此，這些摘錄僅適用於一般指導方針。 摘錄只能讓您知道您感興趣的項目，是否值得花時間按一下並瀏覽實際文章。

由於這些和其他原因，請勿從這些摘錄中複製程式碼，而且不要將任何文字摘錄視為確切事實。 請改瀏覽實際文章。





&nbsp;

<a name="compactupdatedlist"/>

### <a name="compact-list-of-articles-updated-recently"></a>最近更新文章的壓縮清單

此壓縮清單提供＜摘要＞一節中所有更新文章的連結。

1. [使用格式檔案略過資料表資料行 (SQL Server)](#TitleNum_1)
2. [SQL Server 中的 JSON 資料](#TitleNum_2)
3. [查詢處理架構指南](#TitleNum_3)
4. [教學課程：準備 SQL Server 複寫 - 發行者、散發者、訂閱者](#TitleNum_4)
5. [教學課程：設定兩個完全連線的伺服器之間的複寫 (異動)](#TitleNum_5)
6. [教學課程：設定伺服器和行動用戶端之間的複寫 (合併)](#TitleNum_6)
7. [使用全文檢索搜尋查詢](#TitleNum_7)
8. [Azure SQL Database 和資料倉儲的透明資料加密與攜帶您自己的金鑰支援](#TitleNum_8)
9. [PowerShell 與 CLI：使用 Azure Key Vault 中您自己的金鑰來啟用透明資料加密](#TitleNum_9)
10. [關於異動資料擷取 (SQL Server)](#TitleNum_10)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-use-a-format-file-to-skip-a-table-column-sql-serverimport-exportuse-a-format-file-to-skip-a-table-column-sql-servermd"></a>1.&nbsp; [使用格式檔案略過資料表資料行 (SQL Server)](import-export/use-a-format-file-to-skip-a-table-column-sql-server.md)

*更新日期：2018-04-13* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([下一個](#TitleNum_2))

<!-- Source markdown line 221.  ms.author= "douglasl".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 167916d79c5de1e7f13990cb7acc41ceb541b9a7 cb92eb201292294e3397879c98f353fba45f1c1c  (PR=0  ,  Filename=use-a-format-file-to-skip-a-table-column-sql-server.md  ,  Dirpath=docs\relational-databases\import-export\  ,  MergeCommitSha40=f70f24bff1677b33c661abd13726f491ce32b305) -->



**使用 OPENROWSET(BULK...)**


若要透過使用 `OPENROWSET(BULK...)` 來使用 XML 格式檔案跳過資料表資料行，您必須在選取清單和目標資料表中提供明確的資料行清單，如下所示：

```
    INSERT ...<column_list> SELECT <column_list> FROM OPENROWSET(BULK...)
```

下列範例會使用 `OPENROWSET` 大量資料列集提供者和 `myTestSkipCol2.xml` 格式檔案。 此範例會將 `myTestSkipCol2.dat` 資料檔案大量匯入 `myTestSkipCol` 資料表。 此陳述式會依需要，在選取清單還有目標資料表中包含明確的資料行清單。

請在 SSMS 中執行下列程式碼。 更新您電腦上範例檔案位置的檔案系統路徑。

```
USE WideWorldImporters;
GO
INSERT INTO myTestSkipCol
  (Col1,Col3)
    SELECT Col1,Col3
      FROM  OPENROWSET(BULK  'C:\myTestSkipCol2.Dat',
      FORMATFILE='C:\myTestSkipCol2.Xml'
       ) as t1 ;
GO
```



&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-json-data-in-sql-serverjsonjson-data-sql-servermd"></a>2.&nbsp; [SQL Server 中的 JSON 資料](json/json-data-sql-server.md)

*更新日期：2018-04-13* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([上一個](#TitleNum_1) | [下一個](#TitleNum_3))

<!-- Source markdown line 145.  ms.author= "jovanpop".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 19e276637a463b412f2c29a84f9fb7d0b0f5fcc5 e2f2e8b4732779b3f24561cc0c4da3a958f4edbb  (PR=0  ,  Filename=json-data-sql-server.md  ,  Dirpath=docs\relational-databases\json\  ,  MergeCommitSha40=f70f24bff1677b33c661abd13726f491ce32b305) -->



JSON 文件可能會有不能直接對應到標準關聯式資料行的子項目和階層式資料。 在此情況下，您可以藉由聯結父實體和子陣列來壓平合併 JSON 階層。

在下列範例中，陣列中的第二個物件具有代表人員技能的子陣列。 每個子物件都可以使用其他 `OPENJSON` 函式呼叫加以剖析：

```
DECLARE @json NVARCHAR(MAX)
SET @json =
N'[
       { "id" : 2,"info": { "name": "John", "surname": "Smith" }, "age": 25 },
       { "id" : 5,"info": { "name": "Jane", "surname": "Smith", "skills": ["SQL", "C#", "Azure"] }, "dob": "2005-11-04T12:00:00" }
 ]'

SELECT *
FROM OPENJSON(@json)
  WITH (id int 'strict $.id',
        firstName nvarchar(50) '$.info.name', lastName nvarchar(50) '$.info.surname',
        age int, dateOfBirth datetime2 '$.dob',
    skills nvarchar(max) '$.skills' as json)
    outer apply openjson( a.skills )
                     with ( skill nvarchar(8) '$' ) as b
```
第一個 `OPENJSON` 傳回的 **skills** 陣列作為原始的 JSON 文字片段，並使用 `APPLY` 運算子傳遞給另一個 `OPENJSON` 函式。 第二個 `OPENJSON` 函式會剖析 JSON 陣列並傳回字串值作為單一資料行資料列集，與第一個 `OPENJSON` 的結果聯結。
下表顯示此查詢的結果：

**結果**

|id|firstName|lastName|age|dateOfBirth|skill|
|--------|---------------|--------------|---------|-----------------|----------|
|2|John|Smith|25|||
|5|Jane|Smith||2005-11-04T12:00:00|SQL|
|5|Jane|Smith||2005-11-04T12:00:00|C#|
|5|Jane|Smith||2005-11-04T12:00:00|Azure|

`OUTER APPLY OPENJSON` 會聯結第一個層級的實體和子陣列，並傳回壓平合併的結果集。 因為「聯結」的緣故，每個技能都會重複第二個資料列。




&nbsp;

&nbsp;

---

<a name="TitleNum_3"/>

### <a name="3-nbsp-query-processing-architecture-guidequery-processing-architecture-guidemd"></a>3.&nbsp; [查詢處理架構指南](query-processing-architecture-guide.md)

*更新日期：2018-04-13* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([上一個](#TitleNum_2) | [下一個](#TitleNum_4))

<!-- Source markdown line 34.  ms.author= "jroth".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 96d91b39acdb2f32aaff323e374e92d6f229d241 2c1d2f8585632ada174388399782dc3ed2721dba  (PR=0  ,  Filename=query-processing-architecture-guide.md  ,  Dirpath=docs\relational-databases\  ,  MergeCommitSha40=f70f24bff1677b33c661abd13726f491ce32b305) -->



**邏輯運算子優先順序**


當陳述式中使用一個以上的邏輯運算子，`NOT` 會第一個計算，接下來是 `AND`，最後才是 `OR`。 先處理算術以及位元運算子，接著才處理邏輯運算子。 如需詳細資訊，請參閱[運算子優先順序]。

在下列範例中，色彩條件與產品型號 21 相關，但不與產品型號 20 相關，原因是 `AND` 的優先順序高於 `OR`。

```
SELECT ProductID, ProductModelID
FROM Production.Product
WHERE ProductModelID = 20 OR ProductModelID = 21
  AND Color = 'Red';
GO
```

您可以加上括號，強迫陳述式先執行 `OR` 來變更查詢的意義。 下列查詢只會尋找型號 20 和 21 下的紅色產品。

```
SELECT ProductID, ProductModelID
FROM Production.Product
WHERE (ProductModelID = 20 OR ProductModelID = 21)
  AND Color = 'Red';
GO
```

即使非必要，也建議您使用括號，以改善查詢的可讀性，及減少因為運算子優先順序而不知不覺失誤的機會。 使用括號對效能不會有太大的負面影響。 下面的範例與原始範例雖然在句法上並無不同，但其可讀性更高。

```
SELECT ProductID, ProductModelID
FROM Production.Product
WHERE ProductModelID = 20 OR (ProductModelID = 21
  AND Color = 'Red');
GO
```




&nbsp;

&nbsp;

---

<a name="TitleNum_4"/>

### <a name="4-nbsp-tutorial-prepare-sql-server-for-replication---publisher-distributor-subscriberreplicationtutorial-preparing-the-server-for-replicationmd"></a>4.&nbsp; [教學課程：準備 SQL Server 複寫 - 發行者、散發者、訂閱者](replication/tutorial-preparing-the-server-for-replication.md)

*更新日期：2018-04-13* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([上一個](#TitleNum_3) | [下一個](#TitleNum_5))

<!-- Source markdown line 56.  ms.author= "mathoma".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 6e5caedacff193ce79bdd98708ae1b9dc91f0a8f 9f7af4d3f8b1cffd048db2a5b29fc9e6013f5ed2  (PR=0  ,  Filename=tutorial-preparing-the-server-for-replication.md  ,  Dirpath=docs\relational-databases\replication\  ,  MergeCommitSha40=f70f24bff1677b33c661abd13726f491ce32b305) -->



- 安裝 [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)。
- 安裝 [SQL Server 2017 Developer Edition](https://www.microsoft.com/sql-server/sql-server-downloads)。
- 下載 [AdventureWorks 範例資料庫](https://github.com/Microsoft/sql-server-samples/releases)。 如需在 SSMS 中還原資料庫的指示，請參閱[還原資料庫](https://docs.microsoft.com/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms)。

>[!NOTE]
> - 不支援版本相差兩個以上的 SQL Server 複寫。 如需詳細資訊，請參閱 [Supported SQL Versions in Repl Topology](https://blogs.msdn.microsoft.com/repltalk/2016/08/12/suppported-sql-server-versions-in-replication-topology/) (複寫技術支援的 SQL 版本)。
> - 在 *{Included-Content-Goes-Here}* 中，您必須使用 **sysadmin** 固定伺服器角色成員的登入，連線到發行者和訂閱者。 如需系統管理員角色的詳細資訊，請參閱[伺服器層級角色](https://docs.microsoft.com/sql/relational-databases/security/authentication-access/server-level-roles)。


**完成本教學課程的估計時間：30 分鐘**

**建立用於複寫的 Windows 帳戶**

在這一節中，您要建立 Windows 帳戶，以執行複寫代理程式。 您將在本機伺服器上，另外為下列代理程式建立 Windows 帳戶：

|Agent|位置|帳戶名稱|
|---------|------------|----------------|
|快照集代理程式|發行者|<*電腦名稱*>\repl_snapshot|



&nbsp;

&nbsp;

---

<a name="TitleNum_5"/>

### <a name="5-nbsp-tutorial-configure-replication-between-two-fully-connected-servers-transactionalreplicationtutorial-replicating-data-between-continuously-connected-serversmd"></a>5.&nbsp; [教學課程：設定兩個完全連線的伺服器之間的複寫 (交易式)](replication/tutorial-replicating-data-between-continuously-connected-servers.md)

*更新日期：2018-04-13* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([上一個](#TitleNum_4) | [下一個](#TitleNum_6))

<!-- Source markdown line 162.  ms.author= "mathoma".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 0d74f984d0ffc01cce0376837e6d94df3c5654d7 4ecf4d724286130927dd43687d6845059af6f9b7  (PR=0  ,  Filename=tutorial-replicating-data-between-continuously-connected-servers.md  ,  Dirpath=docs\relational-databases\replication\  ,  MergeCommitSha40=f70f24bff1677b33c661abd13726f491ce32b305) -->



**建立交易式發行集的訂閱**

在本節中，您要將訂閱者新增至之前建立的發行集。 本教學課程使用遠端訂閱者 (NODE2\SQL2016)，但也可以在本機將訂閱新增至發行者。

**建立訂閱**


1.  連線到 *{Included-Content-Goes-Here}* 中的發行者，展開伺服器節點，然後展開 [複寫] 資料夾。

2.  在 [本機發行集] 資料夾中，以滑鼠右鍵按一下 **AdvWorksProductTrans** 發行集，然後選取 [新增訂閱]。  [新增訂閱精靈]隨即啟動：

    [新增訂閱]

3.  在 [發行集] 頁面上，選取 [AdvWorksProductTrans]，然後選取 [下一步]：

    選取 Tran 發行者

4.  在 [散發代理程式位置] 頁面上，選取 [在散發者端執行所有代理程式]，然後選取 [下一步]。  如需提取和推送訂閱的詳細資訊，請參閱[訂閱發行集](https://docs.microsoft.com/sql/relational-databases/replication/subscribe-to-publications)：

    在 Dist 執行代理程式

5.  在 [訂閱者] 頁面上，如未顯示訂閱者執行個體的名稱，請選取 [新增訂閱者]，然後從下拉式清單選取 [新增 SQL Server 訂閱者]。 這會啟動 [連線到伺服器] 對話方塊。 輸入訂閱者執行個體的名稱，然後選取 [連線]。



&nbsp;

&nbsp;

---

<a name="TitleNum_6"/>

### <a name="6-nbsp-tutorial-configure-replication-between-a-server-and-mobile-clients-mergereplicationtutorial-replicating-data-with-mobile-clientsmd"></a>6.&nbsp; [教學課程：設定伺服器和行動用戶端之間的複寫 (合併)](replication/tutorial-replicating-data-with-mobile-clients.md)

*更新日期：2018-04-13* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([上一個](#TitleNum_5) | [下一個](#TitleNum_7))

<!-- Source markdown line 93.  ms.author= "mathoma".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 0eed78dfe83c88358c030539a2b25d11ef5ec2d3 79b2a3f32c940fede94b11ad2a3ef8a00b911a39  (PR=0  ,  Filename=tutorial-replicating-data-with-mobile-clients.md  ,  Dirpath=docs\relational-databases\replication\  ,  MergeCommitSha40=f70f24bff1677b33c661abd13726f491ce32b305) -->



Employee 資料表包含的資料行 (OrganizationNode) 具有 hierarchyid 資料類型，僅受 SQL 2017 中的複寫支援。 如果您使用的組建低於 SQL 2017，您會在畫面底部看到訊息，通知您在雙向複寫中使用此資料行可能會遺失資料。 為達到本教學課程的目的，此訊息可予以忽略。 不過，除非您使用的是受支援的組建，否則不應該在生產環境中複寫此資料類型。 如需複寫 hierarchyid 資料類型的詳細資訊，請參閱[在複寫中使用 Hierarchyid 資料行](https://docs.microsoft.com/sql/t-sql/data-types/hierarchyid-data-type-method-reference#using-hierarchyid-columns-in-replicated-tables)


-  在 [篩選資料表的資料列] 頁面上，選取 [新增]，然後選取 [新增篩選]。

-  在 [新增篩選] 對話方塊中，選取 [選取要篩選的資料表] 中的 [Employee (HumanResources)]。 選取 [LoginID] 資料行，再選取向右鍵將資料行新增至篩選查詢的 WHERE 子句中，並依照下列方式修改 WHERE 子句：

    ```
    WHERE [LoginID] = HOST_NAME()
    ```

    A. 選取 [這個資料表中的一個資料列只會提供給一個訂閱]，然後選取 [確定]：

    新增篩選



- 在 [篩選資料表的資料列] 頁面上，依序選取 [Employee (Human Resources)]、[新增] 和 [Add Join to Extend the Selected Filter] \(新增聯結以展開選取的篩選)。

    A. 在 [新增聯結] 對話方塊中，選取 [聯結的資料表] 下的 [Sales.SalesOrderHeader]。 選取 [手動寫入聯結陳述式] 並完成聯結陳述式，如下所示：



&nbsp;

&nbsp;

---

<a name="TitleNum_7"/>

### <a name="7-nbsp-query-with-full-text-searchsearchquery-with-full-text-searchmd"></a>7.&nbsp; [使用全文檢索搜尋進行查詢](search/query-with-full-text-search.md)

*更新日期：2018-04-13* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([上一個](#TitleNum_6) | [下一個](#TitleNum_8))

<!-- Source markdown line 247.  ms.author= "douglasl".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 5ec67b56aa0a6eadadbcfa8b73b6726e75eca2bb 4eb108b202d3dd035a312bac7872cf02bcf31cfa  (PR=0  ,  Filename=query-with-full-text-search.md  ,  Dirpath=docs\relational-databases\search\  ,  MergeCommitSha40=f70f24bff1677b33c661abd13726f491ce32b305) -->



**衍生詞彙搜尋的詳細資訊**


「字形變化」是指動詞的不同時態和變化或是名詞的單複數。

例如，搜尋 "drive" 單字的字形變化。 如果資料表的不同資料列中包括 "drive"、"drives"、"drove"、"driving" 及 "driven" 等字，因為這些單字全都從 "drive" 這個字變化而來，所以都會出現在結果集中。

[FREETEXT] 和 [FREETEXTTABLE] 預設會尋找所有指定單字的變化詞彙。 [CONTAINS] 和 [CONTAINSTABLE] 支援選擇性 `INFLECTIONAL` 引數。

**搜尋特定單字的同義字**


「同義字」會針對詞彙定義使用者指定的同義字。 如需同義字檔案的詳細資訊，請參閱[設定及管理全文檢索搜尋的同義字檔案]。

例如，如果 "{car, automobile, truck, van}" 項目新增到同義字中，您就可以搜尋 "car" 這個字的同義字變化。 由於 "automobile"、"truck"、"van" 或 "car" 這些字都是屬於內含 "car" 這個字的同義字擴充集，因此所查詢的資料表中，所有包含這些字的資料列都會出現在結果集。

[FREETEXT] 和 [FREETEXTTABLE] 預設會使用同義字。 [CONTAINS] 和 [CONTAINSTABLE] 支援選擇性 `THESAURUS` 引數。



&nbsp;

&nbsp;

---

<a name="TitleNum_8"/>

### <a name="8-nbsp-transparent-data-encryption-with-bring-your-own-key-support-for-azure-sql-database-and-data-warehousesecurityencryptiontransparent-data-encryption-byok-azure-sqlmd"></a>8.&nbsp; [Azure SQL Database 和資料倉儲的透明資料加密與攜帶您自己的金鑰支援](security/encryption/transparent-data-encryption-byok-azure-sql.md)

*更新日期：2018-04-24* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([上一個](#TitleNum_7) | [下一個](#TitleNum_9))

<!-- Source markdown line 110.  ms.author= "aliceku".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 9527658848d430bf0148be84474a75b232cbd112 70ed2a129c580962384f808e8526673957f00d2c  (PR=5662  ,  Filename=transparent-data-encryption-byok-azure-sql.md  ,  Dirpath=docs\relational-databases\security\encryption\  ,  MergeCommitSha40=91a9c812739a1c9a6ec9e7b8cda71ee1f5adae3d) -->



**如何使用 Azure Key Vault 設定 Geo-DR**


如需為加密的資料庫維護 TDE 保護裝置的高可用性，必須根據現有或所需的 SQL Database 容錯移轉群組或作用中的異地複寫執行個體，設定備援的 Azure Key Vault。  每個異地複寫的伺服器都需要個別的金鑰保存庫，其必須與伺服器共置於相同的 Azure 區域。 當主要資料庫因為某個區域發生中斷而無法存取，並觸發容錯移轉時，次要資料庫即可以使用次要金鑰保存庫來接管。

若是異地複寫的 Azure SQL 資料庫，將需要下列 Azure Key Vault 設定：
- 在區域中要有一個具有金鑰保存庫的主要資料庫以及一個具有金鑰保存庫的次要資料庫。
- 至少需要一個次要資料庫，最多可支援四個次要資料庫。
- 不支援次要資料庫的次要資料庫 (鏈結)。

下節將更詳細地介紹安裝及設定步驟。

**Azure Key Vault 設定步驟**


- 安裝 [PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-5.6.0)
- 使用 [PowerShell 在兩個不同的區域建立兩個 Azure Key Vault，以在金鑰保存庫上啟用「虛刪除」屬性](https://docs.microsoft.com/azure/key-vault/key-vault-soft-delete-powershell) (目前從 AKV 入口網站還無法使用此選項 - 但 SQL 需要它)。
- 這兩個 Azure Key Vault 必須位於相同 Azure 地理的兩個區域中，才能備份和還原金鑰。  如果您需要這兩個金鑰保存庫位於不同地理才能符合 SQL Geo-DR 需求，請遵循 [BYOK 程序](https://docs.microsoft.com/azure/key-vault/key-vault-hsm-protected-keys)，允許從內部部署 HSM 匯入金鑰。



&nbsp;

&nbsp;

---

<a name="TitleNum_9"/>

### <a name="9-nbsp-powershell-and-cli-enable-transparent-data-encryption-using-your-own-key-from-azure-key-vaultsecurityencryptiontransparent-data-encryption-byok-azure-sql-configuremd"></a>9.&nbsp; [PowerShell 與 CLI：使用 Azure Key Vault 中您自己的金鑰來啟用透明資料加密](security/encryption/transparent-data-encryption-byok-azure-sql-configure.md)

*更新日期：2018-04-24* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([上一個](#TitleNum_8) | [下一個](#TitleNum_10))

<!-- Source markdown line 196.  ms.author= "aliceku".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 a0e00f5701d9a493f503a477c69097ce65aba174 721e8fb856a55ee1e8e9e7fc06036a03adab647b  (PR=5662  ,  Filename=transparent-data-encryption-byok-azure-sql-configure.md  ,  Dirpath=docs\relational-databases\security\encryption\  ,  MergeCommitSha40=91a9c812739a1c9a6ec9e7b8cda71ee1f5adae3d) -->



**CLI 的必要條件**


- 您必須擁有 Azure 訂用帳戶，而且是該訂用帳戶的系統管理員。
- [建議但非必要] 備妥硬體安全性模組 (HSM) 或本機金鑰存放區，以建立 TDE 保護裝置金鑰內容的本機複本。
- 命令列介面 2.0 版或更新版本。 若要安裝最新版本並連線至您的 Azure 訂用帳戶，請參閱[安裝及設定 Azure 跨平台命令列介面 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest)。
- 建立 Azure Key Vault 和金鑰以用於 TDE。
   - [使用 CLI 2.0 管理 Key Vault](https://docs.microsoft.com/azure/key-vault/key-vault-manage-with-cli2)
   - [使用硬體安全性模組 (HSM) 與 Key Vault 的指示](https://docs.microsoft.com/azure/key-vault/key-vault-get-started#a-idhsmaif-you-want-to-use-a-hardware-security-module-hsm)
 - 金鑰保存庫必須具有以下屬性才能供 TDE 使用：
   - [虛刪除](https://docs.microsoft.com/azure/key-vault/key-vault-ovw-soft-delete)
   - [如何透過 CLI 使用金鑰保存庫虛刪除](https://docs.microsoft.com/azure/key-vault/key-vault-soft-delete-cli)
- 若要用於 TDE，金鑰必須具有下列屬性：
   - 無到期日
   - 未停用
   - 能夠執行「取得」、「包裝金鑰」和「解除包裝金鑰」作業

**步驟：建立伺服器並將 Azure AD 身分識別指派給您的伺服器**

      cli
      # create server (with identity) and database



&nbsp;

&nbsp;

---

<a name="TitleNum_10"/>

### <a name="10-nbsp-about-change-data-capture-sql-servertrack-changesabout-change-data-capture-sql-servermd"></a>10.&nbsp; [關於異動資料擷取 (SQL Server)](track-changes/about-change-data-capture-sql-server.md)

*更新日期：2018-04-17* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([上一個](#TitleNum_9))

<!-- Source markdown line 112.  ms.author= "jroth".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 588bff652adefd719e799e9777a416b70184c5f8 77ebdbb1b98b24054d5c5afbb3f1d40e94d1e6bc  (PR=5574  ,  Filename=about-change-data-capture-sql-server.md  ,  Dirpath=docs\relational-databases\track-changes\  ,  MergeCommitSha40=bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68) -->



**使用資料庫和資料表定序差異**


請務必注意，在資料庫與設定進行異動資料擷取的資料表資料行之間有不同的定序。 CDC 會使用暫時儲存體來填入側邊資料表。 如果資料表的 CHAR 或 VARCHAR 資料行具有與資料庫定序不同的定序，而且如果這些資料行儲存非 ASCII 字元 (例如雙位元組 DBCS 字元)，則 CDC 可能無法保存與基底資料表中資料一致的已變更資料。 原因是過度儲存體變數不能有與其建立關聯的定序。

請考慮下列其中一種方法來確保變更擷取資料已與基底資料表一致：

- 將 NCHAR 或 NVARCHAR 資料類型用於包含非 ASCII 資料的資料行。

- 或者，對於資料行和資料庫使用相同的定序。

例如，如果您有一個使用 SQL_Latin1_General_CP1_CI_AS 定序的資料庫，請考慮使用下表：

```
CREATE TABLE T1(
     C1 INT PRIMARY KEY,
     C2 VARCHAR(10) collate Chinese_PRC_CI_AI)
```

CDC 可能無法擷取資料行 C2 的二進位資料，因為其定序不同 (Chinese_PRC_CI_AI)。 使用 NVARCHAR 避免這個問題：

```
CREATE TABLE T1(
     C1 INT PRIMARY KEY,
     C2 NVARCHAR(10) collate Chinese_PRC_CI_AI --Unicode data type, CDC works well with this data type)
```







## <a name="similar-articles-about-new-or-updated-articles"></a>新文章或更新文章的類似文章

本節會在我們的公開 GitHub 存放庫中，列出與其他主題區中最近更新的文章十分相似的文章：[MicrosoftDocs/sql-docs](https://github.com/MicrosoftDocs/sql-docs/)。



#### <a name="subject-areas-that-do-have-new-or-recently-updated-articles"></a>具有新文章或最近更新文章的主題區

- [新文章 + 更新文章 (11+6)：&nbsp; &nbsp;**Advanced Analytics for SQL** 文件](../advanced-analytics/new-updated-advanced-analytics.md)
- [新文章 + 更新文章 (18+0)：&nbsp; &nbsp;**Analysis Services for SQL** 文件](../analysis-services/new-updated-analysis-services.md)
- [新文章 + 更新文章 (218+14)：**連線到 SQL** 文件](../connect/new-updated-connect.md)
- [新文章 + 更新文章 (14+0)：&nbsp; &nbsp;**SQL 資料庫引擎**文件](../database-engine/new-updated-database-engine.md)
- [新文章 + 更新文章 (3+2)：&nbsp; &nbsp; **Integration Services for SQL** 文件](../integration-services/new-updated-integration-services.md)
- [新文章 + 更新文章 (3+3)：&nbsp; &nbsp; **Linux for SQL** 文件](../linux/new-updated-linux.md)
- [新文章 + 更新文章 (7+10)：&nbsp; &nbsp;**SQL 的關聯式資料庫**文件](../relational-databases/new-updated-relational-databases.md)
- [新文章 + 更新文章 (0+2)：&nbsp; &nbsp; **Reporting Services for SQL** 文件](../reporting-services/new-updated-reporting-services.md)
- [新文章 + 更新文章 (1+3)：&nbsp; &nbsp; **SQL Operations Studio** 文件](../sql-operations-studio/new-updated-sql-operations-studio.md)
- [新文章 + 更新文章 (2+3)：&nbsp; &nbsp; **Microsoft SQL Server** 文件](../sql-server/new-updated-sql-server.md)
- [新文章 + 更新文章 (1+1)：&nbsp; &nbsp; **SQL Server Data Tools (SSDT)** 文件](../ssdt/new-updated-ssdt.md)
- [新文章 + 更新文章 (5+2)：&nbsp; &nbsp; **SQL Server Management Studio (SSMS)** 文件](../ssms/new-updated-ssms.md)
- [新文章 + 更新文章 (0+2)：&nbsp; &nbsp; **Transact-SQL** 文件](../t-sql/new-updated-t-sql.md)
- [新文章 + 更新文章 (1+1)：&nbsp; &nbsp; **SQL 工具**文件](../tools/new-updated-tools.md)



#### <a name="subject-areas-that-do-not-have-any-new-or-recently-updated-articles"></a>沒有新文章或最近更新文章的主題區

- [新文章 + 更新文章 (0+0)：**SQL 的分析平台系統**文件](../analytics-platform-system/new-updated-analytics-platform-system.md)
- [新文章 + 更新文章 (0+0)：**Data Quality Services for SQL** 文件](../data-quality-services/new-updated-data-quality-services.md)
- [新文章 + 更新文章 (0+0)：**SQL 資料採礦延伸模組 (DMX)** 文件](../dmx/new-updated-dmx.md)
- [新文章 + 更新文章 (0+0)：**SQL Master Data Services (MDS)** 文件](../master-data-services/new-updated-master-data-services.md)
- [新文章 + 更新文章 (0+0)：**SQL 多維度運算式 (MDX)** 文件](../mdx/new-updated-mdx.md)
- [新文章 + 更新文章 (0+0)：**SQL ODBC (開放式資料庫連接)** 文件](../odbc/new-updated-odbc.md)
- [新文章 + 更新文章 (0+0)：**PowerShell for SQL** 文件](../powershell/new-updated-powershell.md)
- [新文章 + 更新文章 (0+0)：**SQL 範例**文件](../samples/new-updated-samples.md)
- [新文章 + 更新文章 (0+0)：**SQL Server 移轉小幫手 (SSMA)** 文件](../ssma/new-updated-ssma.md)
- [新文章 + 更新文章 (0+0)：**XQuery for SQL** 文件](../xquery/new-updated-xquery.md)

