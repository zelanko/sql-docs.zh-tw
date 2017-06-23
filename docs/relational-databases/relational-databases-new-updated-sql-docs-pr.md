---
title: "已更新-關聯式資料庫文件 |Microsoft 文件"
description: "顯示更新的內容，如需關聯式資料庫的最近變更過的文件的程式碼片段。"
services: na
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: BYHAM
ms.service: na
ms.topic: updart-autogen
ms.technology: database-engine
ms.custom: UpdArt.exe
ms.workload: relational-databases
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 05/23/2017
ms.author: genemi
ms.translationtype: Human Translation
ms.sourcegitcommit: 96f6a7eeb03fdc222d0e5b42bcfbf05c25d11db6
ms.openlocfilehash: 3ab051a6fd00670139bb1089dcd3f4af76b9ecef
ms.contentlocale: zh-tw
ms.lasthandoff: 06/23/2017

---
# <a name="new-and-recently-updated-relational-databases-docs"></a>新的與最近的更新： 關聯式資料庫文件



幾乎每日 Microsoft 某些現有發行項上更新其[Docs.Microsoft.com](http://docs.microsoft.com/)文件網站。 這篇文章會顯示從最近已更新的發行項的摘錄。 可能也會列出新的文章連結。

這篇文章會定期重新執行程式所產生的。 偶爾摘錄會顯示具有完美的格式，或 markdown 從來源文件。 影像永遠不會顯示在這裡。

新的更新會報告下列日期範圍和主體：



- *日期範圍的更新：* &nbsp; **2017年-05-01** &nbsp; -到- &nbsp; **2017年-05-23**
- *主旨區域：* &nbsp; **關聯式資料庫**。




&nbsp;

## <a name="updated-articles-with-excerpts"></a>更新的發行項、 只有摘要

此區段會顯示更新從發行項的最近發生大規模的更新所收集的摘錄。

此處顯示的摘錄顯示分隔其適當語意的內容。 此外，有時摘錄分開四周實際文件中的重要的 markdown 語法。 因此，這些摘錄適用於一般指導方針。 摘錄只會讓您知道您的興趣是否值得花時間按一下，瀏覽實際的發行項。

如需這些和其他原因，不要複製程式碼從這些摘錄中，而且不採用確切真為任何文字摘錄。 相反地，請瀏覽實際的發行項。



&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-create-a-graph-database-and-run-some-pattern-matching-queries-using-t-sqlgraphssql-graph-samplemd"></a>1.&nbsp;[建立圖形資料庫並執行某些模式比對使用 T-SQL 查詢](graphs/sql-graph-sample.md)

*Updated: 2017-05-04* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([Next](#TitleNum_2))

<!-- Source markdown line 68.  ms.author= "shkale".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 ff467bf5fcf13592c796836def36e16e34f8cc31 99fcf0399006de16d0ac7cc9057564d307cb981b -->


```
INSERT INTO Person VALUES (1,'John');
INSERT INTO Person VALUES (2,'Mary');
INSERT INTO Person VALUES (3,'Alice');
INSERT INTO Person VALUES (4,'Jacob');
INSERT INTO Person VALUES (5,'Julie');

INSERT INTO Restaurant VALUES (1,'Taco Dell','Bellevue');
INSERT INTO Restaurant VALUES (2,'Ginger and Spice','Seattle');
INSERT INTO Restaurant VALUES (3,'Noodle Land', 'Redmond');

INSERT INTO City VALUES (1,'Bellevue','wa');
INSERT INTO City VALUES (2,'Seattle','wa');
INSERT INTO City VALUES (3,'Redmond','wa');

-- Insert into edge table. While inserting into an edge table, 
-- you need to provide the $node_id from $from_id and $to_id columns.
INSERT INTO likes VALUES ((SELECT $node_id FROM Person WHERE id = 1), 
       (SELECT $node_id FROM Restaurant WHERE id = 1),9);
INSERT INTO likes VALUES ((SELECT $node_id FROM Person WHERE id = 2), 
      (SELECT $node_id FROM Restaurant WHERE id = 2),9);
INSERT INTO likes VALUES ((SELECT $node_id FROM Person WHERE id = 3), 
      (SELECT $node_id FROM Restaurant WHERE id = 3),9);
INSERT INTO likes VALUES ((SELECT $node_id FROM Person WHERE id = 4), 
      (SELECT $node_id FROM Restaurant WHERE id = 3),9);
INSERT INTO likes VALUES ((SELECT $node_id FROM Person WHERE id = 5), 
      (SELECT $node_id FROM Restaurant WHERE id = 3),9);

INSERT INTO livesIn VALUES ((SELECT $node_id FROM Person WHERE id = 1),
      (SELECT $node_id FROM City WHERE id = 1));
INSERT INTO livesIn VALUES ((SELECT $node_id FROM Person WHERE id = 2),
      (SELECT $node_id FROM City WHERE id = 2));
INSERT INTO livesIn VALUES ((SELECT $node_id FROM Person WHERE id = 3),
      (SELECT $node_id FROM City WHERE id = 3));
INSERT INTO livesIn VALUES ((SELECT $node_id FROM Person WHERE id = 4),
      (SELECT $node_id FROM City WHERE id = 3));
INSERT INTO livesIn VALUES ((SELECT $node_id FROM Person WHERE id = 5),
      (SELECT $node_id FROM City WHERE id = 1));

INSERT INTO locatedIn VALUES ((SELECT $node_id FROM Restaurant WHERE id = 1),
      (SELECT $node_id FROM City WHERE id =1));
```



&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-sysfngetauditfile-transact-sqlsystem-functionssys-fn-get-audit-file-transact-sqlmd"></a>2. &nbsp; [sys.fn_get_audit_file (TRANSACT-SQL)](system-functions/sys-fn-get-audit-file-transact-sql.md)

*Updated: 2017-05-16* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([Previous](#TitleNum_1) | [Next](#TitleNum_3))

<!-- Source markdown line 145.  ms.author= "rickbyh".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 046fa92ad1b7e6bb7a956493ca06cf72d45b5285 fbf55361da90663835d7e107fda697c358e0e061 -->



- **Azure SQL Database**

  此範例會從名為 `ShiraServer/MayaDB/SqlDbAuditing_Audit/2017-07-14/10_45_22_173_1.xel` 的檔案進行讀取。  
  
  ```  
  SELECT * FROM sys.fn_get_audit_file sys.fn_get_audit_file ('https://mystorage.blob.core.windows.net/sqldbauditlogs/ShiraServer/MayaDB/SqlDbAuditing_Audit/2017-07-14/10_45_22_173_1.xel',default,default);
  GO  
  ```  

  這個範例會讀取所有稽核記錄檔開頭的伺服器從`Sh`。  
  
  ```  
  SELECT * FROM sys.fn_get_audit_file sys.fn_get_audit_file ('https://mystorage.blob.core.windows.net/sqldbauditlogs/Sh',default,default);
  GO  
  ```





&nbsp;

&nbsp;

---

<a name="TitleNum_3"/>

### <a name="3-nbsp-manage-retention-of-historical-data-in-system-versioned-temporal-tablestablesmanage-retention-of-historical-data-in-system-versioned-temporal-tablesmd"></a>3.&nbsp;[管理的系統版本設定時態表中的歷程記錄資料保留](tables/manage-retention-of-historical-data-in-system-versioned-temporal-tables.md)

*Updated: 2017-05-19* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([Previous](#TitleNum_2))

<!-- Source markdown line 425.  ms.author= "carlrab".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 ee69beb6a46913934d4a322f5d95343cc86f2ec4 94da98fec4ab16636a4581c16eb4456e2d1ff66b -->



**使用時態歷程記錄保留原則方法**

> **注意：**時態歷程記錄保留原則的方法適用於 [！包含 [sqldbesa../../includes/sqldbesa-md.md)] 和 SQL Server 2017 從 CTP 1.3 開始。  

可以是時態歷程記錄保留在個別的資料表層級的設定，可讓使用者建立彈性的過時原則。 套用暫時保留很簡單： 它只需要一個參數是在資料表建立或結構描述變更時設定。

定義保留原則之後，Azure SQL Database 會啟動定期檢查是否有資格可自動清除資料的歷程記錄資料列。 相符的資料列的識別和歷程記錄資料表中的移除它們發生背景工作，排程及執行系統中的透明的方式。 歷程記錄資料表資料列的存留期條件檢查會根據表示一端的 SYSTEM_TIME 期間資料行。 保留期限，例如，設定為六個月內，如果資料表有資格清除的資料列滿足下列條件：
```
ValidTo < DATEADD (MONTH, -6, SYSUTCDATETIME())
```
在上述範例中，我們假設 ValidTo 資料行對應至 SYSTEM_TIME 週期的結尾。
**如何設定保留原則？**

設定的時態表的保留原則之前，請先檢查是否啟用時態歷程記錄保留在資料庫層級：
```
SELECT is_temporal_history_retention_enabled, name
FROM sys.databases
```
資料庫旗標**is_temporal_history_retention_enabled**設為 ON，根據預設，但使用者可以變更利用 ALTER DATABASE 陳述式。 它也會自動設為 OFF 之後的時間還原作業中的點。 若要啟用時態歷程記錄保留為清除，為您的資料庫，請執行下列陳述式：
```
ALTER DATABASE <myDB>
SET TEMPORAL_HISTORY_RETENTION  ON
```
在資料表建立期間設定保留原則，藉由指定 HISTORY_RETENTION_PERIOD 參數值：
```
CREATE TABLE dbo.WebsiteUserInfo
```





&nbsp;

<a name="compactupdatedlist"/>

## <a name="compact-list-of-articles-updated-recently"></a>Compact 文件最近才更新清單

此壓縮清單所提供的所有更新發行項上一節中所列的連結。

1. [建立圖形資料庫並執行某些模式比對使用 T-SQL 查詢](#TitleNum_1)
2. [sys.fn_get_audit_file (TRANSACT-SQL)](#TitleNum_2)
3. [管理系統設定版本時態表中的歷程記錄資料保留](#TitleNum_3)


<a name="sisters2"/>

&nbsp;

## <a name="sister-articles"></a>姊文件

此區段會列出最近已更新的發行項相同的 GitHub 儲存機制中的其他主體區域中的相似的文件。


&nbsp;

[Microsoft /**sql-文件-pr** ](https://github.com/microsoftdocs/sql-docs-pr/) GitHub.com 上的儲存機制：

- [最近才更新：**關聯式資料庫和 Microsoft SQL Server**文件](/sql/relational-databases/relational-databases-new-updated-sql-docs-pr)
- [最近才更新： **Microsoft SQL Server**文件](/sql/sql-server/sql-server-new-updated-sql-docs-pr)
- [最近才更新： **SQL Server 中的 TRANSACT-SQL**文件](/sql/t-sql/t-sql-new-updated-sql-docs-pr)


&nbsp;

<!--
[Microsoft/**azure-docs**](https://github.com/microsoft/azure-docs/) repository on GitHub.com:

- [Sisters list for **azure-docs** repo](https://docs.microsoft.com/azure/sql-server-new-updated-azure-docs/#sisters2)
-->

&nbsp;



