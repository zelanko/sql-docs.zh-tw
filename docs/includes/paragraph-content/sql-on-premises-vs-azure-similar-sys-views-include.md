
<!--
### Code examples for Azure cloud differ slightly from on-premises
  Or.....
### Code examples can differ for Azure SQL Database
-->

某些針對 SQL Server 內部部署所撰寫的 Transact-SQL 程式碼範例，需要進行小幅變更，才能在雲端的 Azure SQL Database 服務上執行。 這類程式碼範例的其中一個類別牽涉到系統檢視，而系統檢視的名稱前置詞在這兩個資料庫系統之間略有不同：

- **伺服器\_** &nbsp; - &nbsp; 內部部署的前置詞 
- **資料庫\_** &nbsp; - &nbsp; _Azure SQL Database 的前置詞_

為了示範，下表列出並比較兩個系統檢視子集。 為求簡潔，這些子集限制為同時包含字串 `_event` 的檢視名稱。 由於子集來自兩個不同資料庫系統，因此具有不同的名稱前置詞。

| 內部部署 2017 中的名稱 | 雲端服務中的名稱 |
| :------------------------- | :---------------------- |
| server_event_notifications<br />server_event_session_actions<br />server_event_session_events<br />server_event_session_fields<br />server_event_session_targets<br />server_event_sessions<br />server_events<br />server_trigger_events | database_event_session_actions<br />database_event_session_events<br />database_event_session_fields<br />database_event_session_targets<br />database_event_sessions |
| &nbsp; | &nbsp; |

上表中兩個清單截至 2019 年 6 月為止是準確的。 但這裡的資料表內容可能已經過時，因為其內容不會在此處進行維護。 如需準確的清單，請執行下列 T-SQL SELECT 陳述式。 執行 SELECT 兩次，在每個資料庫系統上各一次。

```sql
SELECT name
    FROM sys.all_objects
    WHERE
        (name LIKE 'database\_%' { ESCAPE '\' } OR
         name LIKE 'server\_%' { ESCAPE '\' })
        AND name LIKE '%\_event%' { ESCAPE '\' }
        AND type = 'V'
    ORDER BY name;
```

<!--
The creation of this docs/includes/ file was prompted by Issue 2211 (https://github.com/MicrosoftDocs/sql-docs/issues/2211).
Initial PR was PR 10427 (https://github.com/MicrosoftDocs/sql-docs-pr/pull/10427).
The complaint was that a specific T-SQL code block failed on Azure SQL Database.

GeneMi  ,  2019/05/28
-->
