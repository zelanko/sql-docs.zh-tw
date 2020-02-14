---
title: 建立連結的伺服器提供者
ms.date: 07/01/2019
ms.prod: sql
ms.technology: ''
ms.prod_service: database-engine
ms.reviewer: MikeRayMSFT
ms.topic: conceptual
author: pmasl
ms.author: pelopes
manager: rothj
ms.custom: seo-dt-2019
ms.openlocfilehash: 933a37dd4ef627796b7688510bd235c80db417be
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2020
ms.locfileid: "74095997"
---
# <a name="microsoft-sql-server-distributed-queries-ole-db-connectivity"></a>Microsoft SQL Server 分散式查詢：OLE DB 連接

本文描述 Microsoft SQL Server 查詢處理器如何與 OLE DB 提供者互動，以啟用分散式查詢和異質性查詢。 主要適用於 OLE DB 提供者開發人員，並假設這些人員對 OLE DB 規格有深入了解。 重點在於 SQL Server 查詢處理器與 OLE DB 提供者之間的 OLE DB 介面，而不是在分散式查詢功能本身。 如需分散式查詢功能的完整說明，請參閱[連結的伺服器](../../relational-databases/linked-servers/linked-servers-database-engine.md)。

## <a name="overview-and-terminology"></a>概觀與術語

 在 Microsoft SQL Server 中，分散式查詢可讓 SQL Server 使用者存取 SQL Server 伺服器以外的資料，可能是在執行 SQL Server 的其他伺服器中，或是在公開 OLE DB 介面的其他資料來源中。 OLE DB 可讓您以一致的方式從異質資料來源存取表格式資料。

針對本文的目的，分散式查詢是參考一或多個外部 OLE DB 資料來源中資料表和資料列集的任何 `SELECT`、`INSERT`、`UPDATE` 或 `DELETE` 陳述式。

遠端資料表是儲存在 OLE DB 資料來源中的資料表，並來自執行 SQL Server 的伺服器 (執行查詢的伺服器) 外部。 分散式查詢會存取一或多個遠端資料表。

### <a name="ole-db-provider-categories"></a>OLE DB 提供者類別

下列從 SQL Server 分散式查詢觀點，根據 OLE DB 提供者的功能來分類這些提供者。 按照定義，這些類別可以同時存在；任何一個提供者可以屬於下列多個類別：

- SQL 命令提供者

- 索引提供者

- 簡單資料表提供者

- 非 SQL 命令提供者

#### <a name="sql-command-providers"></a>SQL 命令提供者

如果提供者所支援的 `Command` 物件具有 SQL Server 可辨識的 SQL 標準方言，則屬於此類別。 任何一個 OLE DB 提供者必須符合下列特定需求，SQL Server 才會將它視為 SQL 命令提供者：

- 提供者必須支援 `Command` 物件及其所有的必要 OLE DB 介面：`ICommand`、`ICommandText`、`IColumnsInfo`、`ICommandProperties` 和 `IAccessor`。

- 提供者支援的 SQL 方言必須至少為 SQL Subminimum。 提供者必須透過 `DBPROP_SQLSUPPORT` 屬性來報告方言。

SQL 命令提供者的範例為 Microsoft OLE DB Provider for SQL Server 和 Microsoft OLE DB Provider for ODBC。

#### <a name="index-providers"></a>索引提供者

索引提供者是指根據 OLE DB 支援和公開索引，並允許以索引方式查閱基底資料表的提供者。 任何一個 OLE DB 提供者必須符合下列特定需求，SQL Server 才會將它視為索引提供者：

- 提供者必須支援具有 TABLES、COLUMNS 與 INDEXES 結構描述資料列集的 `IDBSchemaRowset` 介面。

- 提供者必須支援可藉著指定索引名稱與對應的基底資料表名稱而透過 `IOpenRowset` 來開啟索引上的資料列集。

- `Index` 物件必須支援其所有的必要介面：`IRowset`、`IRowsetIndex`、`IAccessor`、`IColumnsInfo`、`IRowsetInfo` 和 `IConvertTypes`。

- 針對索引基底資料表開啟的資料列集 (透過 `IOpenRowset`) 必須支援 `IRowsetLocate` 介面，才能在以書籤為基礎的資料列上定位。

如果 OLE DB 提供者符合上述需求，使用者可設定 `Index As Access Path` 提供者選項，讓 SQL Server 能夠使用提供者的索引來評估查詢。 根據預設，除非已設定此選項，否則 SQL Server 不會嘗試使用提供者的索引。

>[!NOTE]
>SQL Server 支援影響 SQL Server 存取 OLE DB 提供者方式的各種選項。 SQL Server Enterprise Manager 中的 [`Linked Server Properties`] 對話方塊可用來設定這些選項。

#### <a name="simple-table-providers"></a>簡單資料表提供者

這些是指公開針對基底資料表透過 `IOpenRowset` 介面開啟資料列集方式的提供者。 這類提供者既不是 SQL 命令提供者，也不是索引提供者；相反地，它們是 SQL Server 分散式查詢可使用的最簡單提供者類別。

針對這類提供者，SQL Server 只能在分散式查詢評估期間執行資料表掃描。

#### <a name="non-sql-command-providers"></a>非 SQL 命令提供者

如果提供者支援 `Command` 物件及其必要介面，但不支援 SQL Server 可辨識的 SQL 標準方言，則屬於此類別。

非 SQL 命令提供者的兩個範例為 Microsoft OLE DB Provider for Indexing Service 和 [Microsoft OLE DB Provider for Microsoft Active Directory Service](../../ado/guide/appendixes/microsoft-ole-db-provider-for-microsoft-active-directory-service.md)。

### <a name="transact-sql-subset"></a>Transact-SQL 子集

如果提供者支援所需的 OLE DB 介面，則分散式查詢支援下列每個 Transact-SQL 陳述式類別。

- 除了 `SELECT` INTO 陳述式以外，所有 `SELECT` 陳述式都可使用遠端資料表作為目的地資料表。

- 如果提供者支援 INSERT 的必要介面，即可在遠端資料表上使用 `INSERT` 陳述式。 如需 INSERT 的 OLE DB 需求詳細資訊，請參閱本文稍後的 \"INSERT 陳述式\"。

- 如果提供者滿足指定資料表上的 OLE DB 介面需求，即可在遠端資料表上使用 `UPDATE` 和 DELETE 陳述式。 如需可更新或刪除遠端資料表的 OLE DB 介面需求和條件，請參閱本文稍後的 \"UPDATE 和 DELETE 陳述式\"。

### <a name="cursor-support"></a>資料指標支援

如果提供者支援必要的 OLE DB 函式，則支援對分散式查詢使用快照集和索引鍵集資料指標。 不支援對分散式查詢使用動態資料指標。 使用者對分散式查詢要求動態資料指標會降級為索引鍵集資料指標。

快照集資料指標會在資料指標開啟時填入，且結果集會保持不變；對基礎資料表所做的更新、插入和刪除並不會反映在資料指標中。

索引鍵集資料指標會在資料指標開啟時填入，且結果集會在整個資料指標存留期間保持不變。 不過，在瀏覽資料列之後，即會在資料指標中看見對基礎資料表所做的更新和刪除。 但如果對基礎資料表所做的插入可能影響資料指標成員資格，則看不見這些插入。

如果提供者符合遠端資料表上的更新和刪除條件，則可透過定義於分散式查詢並參考遠端資料表的資料指標來更新或刪除遠端資料表，例如資料表 `UPDATE` \| DELETE `<remote-table>` `WHERE` CURRENT OF `<cursor-name>`。 如需詳細資訊，請參閱本文稍後的 \"UPDATE 和 DELETE 陳述式\"。

#### <a name="keyset-cursor-support-requirements"></a>索引鍵集資料指標支援需求

如果符合所有的 Transact-SQL 語法需求，且存在下列任一項，則分散式查詢支援索引鍵集資料指標：

- OLE DB 提供者支援可在查詢中所有遠端資料表上重複使用的書籤。 可重複使用書籤可從指定資料表的資料列集使用，並用於相同資料表的不同資料列集。 您可以將 BOOKMARK_DURABILITY 資料行設定為 BMK_DURABILITY_INTRANSACTION 或更高持久性，透過 `IDBSchemaRowset` 的 TABLES_INFO 結構描述資料列集來指出支援可重複使用書籤。

- 所有遠端資料表都會透過 `IDBSchemaRowset` 介面的 INDEXES 資料列集來公開唯一索引鍵。 應該有一個索引項目，其中 UNIQUE 資料行設定為 VARIANT_TRUE。

不支援對涉及到 *OpenQuery* 函式的分散式查詢使用索引鍵集資料指標。

#### <a name="updatable-keyset-cursor-requirements"></a>可更新的索引鍵集資料指標需求

遠端資料表可透過定義於分散式查詢的索引鍵集資料指標來更新或刪除，例如 `UPDATE` \| DELETE `<remote-table>` `WHERE` CURRENT OF `<cursor-name>`。 必須符合下列條件，可更新的資料指標才允許用於分散式查詢：

- 如果提供者也符合遠端資料表上的更新和刪除條件，則允許可更新的資料指標。 如需詳細資訊，請參閱本文稍後的 \"UPDATE 和 DELETE 陳述式\"。

- 所有可更新索引鍵集資料指標作業都必須位於具有可重複讀取隔離等級或更高隔離等級的使用者定義交易之中。 此外，提供者必須使用 `ITransactionJoin` 介面來支援分散式交易。

## <a name="ole-db-provider-interaction-phases"></a>OLE DB 提供者互動階段

 所有分散式查詢執行案例有共通的六項作業：

- 連接建立和屬性擷取作業指出 SQL Server 如何連接到 OLE DB 提供者，以及使用了哪些提供者屬性。

- 資料表名稱解析和中繼資料擷取作業指出 SQL Server 如何將以兩種方式之一 (以連結伺服器為基礎的名稱或特定名稱) 指定的遠端資料表名稱解析為提供者中適當資料物件。 這也包括 SQL Server 為了進行分散式查詢編譯和最佳化，而從提供者擷取的資料表中繼資料。

- 交易管理作業指定與 OLE DB 提供者的所有交易相關互動。

- 資料類型處理作業指出 SQL Server 在處理分散式查詢期間從 OLE DB 提供者使用資料或將資料匯出到其中時，如何處理 OLE DB 資料類型。

- 錯誤處理作業指出 SQL Server 如何使用來自提供者的延伸錯誤資訊。

- 安全性作業指定 SQL Server 安全性如何與提供者的安全性互動。

### <a name="connection-establishment-and-property-retrieval"></a>連接建立和屬性擷取

SQL Server 支援兩種遠端資料物件命名慣例：以連結伺服器為基礎的四部分名稱，以及使用 `OPENROWSET` 函式的特定名稱。

#### <a name="linked-server-based-names"></a>以連結伺服器為基礎的名稱

連結的伺服器可作為 OLE DB 資料來源抽象層。 以連結伺服器為基礎的名稱是 `<linked-server>.<catalog>`. `<schema>.<object>` 形式的四部分名稱，其中 `<linked-server>` 是連結的伺服器名稱。 SQL Server 會解譯 `<linked-server>` 來衍生 OLE DB 提供者，以及識別提供者資料來源的連接屬性。 其他三個名稱部分則是由 OLE DB 資料來源解譯，以識別特定的遠端資料表。 :::

#### <a name="ad-hoc-names"></a>特定名稱

特定名稱是以 `OPENROWSET` 或 `OPENDATASOURCE` 函式為基礎的名稱。 其中包含每次在分散式查詢中參考遠端資料表時的所有連接資訊 (也就是所要使用的 OLE DB 提供者、識別資料來源所需的屬性、使用者識別碼和密碼)。

除了系統管理員 (sysadmin) 角色之外，預設不允許使用特定名稱。 若要對 OLE DB 提供者使用特定名稱，則應將提供者選項 `DisallowAdhocAccess` 設定為 `0`。

如果使用連結的伺服器名稱，SQL Server 會從連結的伺服器定義擷取 OLE DB 提供者名稱和提供者的初始化屬性。 如果使用特定名稱，SQL Server 會從 `OPENROWSET` 函式的引數擷取相同資訊。

如需使用四部分名稱來設定連結伺服器的詳細指示，以及特定名稱語法，請參閱[建立連結的伺服器](create-linked-servers-sql-server-database-engine.md)。

### <a name="connecting-to-an-ole-db-provider"></a>連接到 OLE DB 提供者

以下是當 SQL Server 連接到 OLE DB 提供者時所執行的高階步驟：

1. SQL Server 建立資料來源物件。

   SQL Server 會使用提供者的 `ProgID` 將其資料來源物件 (DSO) 具現化。 ProgID 會指定為所連結伺服器設定的 `provider_name` 參數，或指定為 `OPENROWSET` 函式的第一個引數 (在特定名稱案例中)。

   SQL Server 會透過 OLE DB 服務元件介面 `IDataInitialize` 將提供者的 DSO 具現化。 這可讓服務元件管理員在提供者的原生功能之上彙整其服務，例如捲動和更新支援。 此外，透過 `IDataInitialize` 將提供者具現化可讓 OLE DB 服務元件共用提供者的連接，藉此減少其中一些連接和初始化額外負荷。

   指定的提供者可以設定為在與 SQL Server 相同的處理序或在其本身的處理序中具現化。 在個別處理序中具現化可以保護 SQL Server 處理序不會受到提供者失敗的影響。 同時，在 SQL Server 的外部處理序中封送處理 OLE DB 呼叫會有與其建立關聯的效能負擔。 您可以透過設定 `Allow In Process` 提供者選項，將提供者設定為在相同的處理序或外部處理序中具現化。 如需詳細資訊，請參閱[設定提供者選項](../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md)。

   若要深入了解 OLE DB 服務元件和工作階段共用，請參閱提供者需求的相關 OLE DB 文件。

2. 資料來源經過初始化。

   建立 DSO 之後，如果伺服器設定選項 `remote login timeout` 大於 0，`IDBProperties` 介面會設定 DBPROP_INIT_TIMEOUT 初始化屬性；這是必要的屬性。

   如果已在連結的伺服器定義或 `OPENROWSET` 函式第二個引數中指定或隱含這些屬性，則會加以設定：

   - `DBPROP_INIT_PROVIDERSTRING`

   - `DBPROP_INIT_DATASOURCE`

   - `DBPROP_INIT_LOCATION`

   - `DBPROP_INIT_CATALOG`

   - `DBPROP_AUTH_USERID`

   - `DBPROP_AUTH_PASSWORD`

   設定這些屬性之後，系統會呼叫 `IDBInitialize::Initialize` 以使用指定的屬性將 DSO 初始化。

3. SQL Server 收集提供者特定的資訊。

   SQL Server 會收集要用於分散式查詢評估的數個提供者屬性；這些屬性是透過呼叫 `IDBProperties::GetProperties` 來擷取。 所有這些屬性都是選擇性的；不過，支援所有相關屬性可讓 SQL Server 充分利用提供者的功能。 例如，若要判斷 SQL Server 是否可以傳送查詢給提供者，則需要 `DBPROP_SQLSUPPORT`。 如果不支援此屬性，SQL Server 將不會使用遠端提供者作為 SQL 命令提供者，即使它是 SQL 命令提供者也一樣。 在下表中，[預設值] 欄指出提供者不支援屬性時，SQL Server 所假設的值。

屬性| 預設值| 使用 |
|:----|:----|:----|
|`DBPROP_DBMSNAME`|None|用於錯誤訊息。|
|`DBPROP_DBMSVER` |None|用於錯誤訊息。|
|`DBPROP_PROVIDERNAME`|None|用於錯誤訊息。|
|`DBPROP_PROVIDEROLEDBVER1`|1.5|用於判斷 2.0 功能的可用性。
|`DBPROP_CONCATNULLBEHAVIOR`|None|用於判斷提供者的 `NULL` 串連行為是否與 SQL Server 相同。|
|`DBPROP_NULLCOLLATION`|None|只有在 `NULLCOLLATION` 符合 SQL Server 執行個體的 Null 定序行為時，才允許用於排序/索引。|
|`DBPROP_OLEOBJECTS`|None|判斷提供者是否支援大型資料物件資料行的結構化儲存介面。|
|`DBPROP_STRUCTUREDSTORAGE`|None|判斷大型物件類型支援哪些結構化儲存介面 (`ILockBytes`、`Istream` 和 `ISequentialStream`)。|
|`DBPROP_MULTIPLESTORAGEOBJECTS`|False|判斷是否可以同時開啟多個大型物件資料行。|
|`DBPROP_SQLSUPPORT`|None|判斷是否可以將 SQL 查詢傳送給提供者。|
|`DBPROP_CATALOGLOCATION`|`DBPROPVAL_CL_START`|用於建構多部分資料表名稱。
|`SQLPROP_DYNAMICSQL`|False|SQL Server 特定屬性：如果它傳回 `VARIANT_TRUE`，則指出支援將 `?` 參數標記用於參數化查詢執行。
|`SQLPROP_NESTEDQUERIES`|False|SQL Server 特定屬性：如果它傳回 `VARIANT_TRUE`，則指出提供者支援 `FROM` 子句中的巢狀 `SELECT` 陳述式。
|`SQLPROP_GROUPBY`|False|SQL Server 特定屬性：如果它傳回 `VARIANT_TRUE`，則指出提供者支援 `SELECT` 陳述式中的 GROUP BY 子句 (如 SQL-92 標準所指定)。
|`SQLPROP_DATELITERALS `|False|SQL Server 特定屬性：如果它傳回 `VARIANT_TRUE`，則指出提供者支援日期時間常值 (根據 SQL Server Transact-SQL 語法)。
|`SQLPROP_ANSILIKE `|False|SQL Server 特定屬性：此屬性對於支援 SQL 最低層級的提供者很重要，且根據 SQL-92 入門層級支援 `LIKE` 運算子 (以 \'%\' 和 \'_\' 作為萬用字元)。
|`SQLPROP_SUBQUERIES `|False|SQL Server 屬性：此屬性對於支援 SQL 最低層級的提供者很重要。 此屬性指出提供者支援子查詢，如 SQL-92 入門層級所指定。 這包括 `SELECT` 清單和 `WHERE` 子句中的子查詢，並支援相互關聯子查詢的 `IN`、`EXISTS`、`ALL` 和 `ANY` 運算子。
|`SQLPROP_INNERJOIN`|False|SQL Server 特定屬性：此屬性對於支援 SQL 最低層級的提供者很重要。 此屬性指出支援在 `FROM` 子句中使用多個資料表進行聯結。 ------ ---

下列三個常值是從 `IDBInfo::GetLiteralInfo` 擷取而來：`DBLITERAL_CATALOG_SEPARATOR`、`DBLITERAL_SCHEMA_SEPARATOR` (以根據其目錄、結構描述和物件名稱部分建構完整物件名稱) 和 `DBLITERAL_QUOTE` (以在傳送給提供者的 SQL 查詢中括住識別項名稱)。

如果提供者不支援分隔符號常值，SQL Server 會使用句號 (.) 作為預設分隔符號字元。 如果提供者只支援目錄分隔符號字元，但不支援結構描述分隔符號字元，SQL Server 也會使用目錄分隔符號字元作為結構描述分隔符號字元。 如果提供者不支援 `DBLITERAL_QUOTE`，SQL Server 會使用單引號 (`'`) 作為引號字元。

>[!NOTE]
>如果提供者的名稱分隔符號常值不符合這些預設值，提供者必須透過 `IDBInfo` 將其公開，SQL Server 才能透過四部分名稱存取其資料表。 如果未公開這些常值，則只能對這類提供者使用傳遞查詢。

如需公開 `SQLPROP_DYNAMICSQL` 和 `SQLPROP_NESTEDQUERIES` 屬性的資訊，請參閱 [SQL Server 特定屬性](#appendixc)。

### <a name="table-name-resolution-and-meta-data-retrieval"></a>資料表名稱解析和中繼資料擷取

SQL Server 會將分散式查詢中的指定遠端資料表名稱，解析為 OLE DB 資料來源中的特定資料表或檢視表。 以連結伺服器為基礎的命名配置和特定命名配置都會產生三部分名稱供提供者解譯。 在以連結伺服器為基礎的名稱案例中，四部分名稱的最後三個部分是由目錄、結構描述和物件名稱組成。 在特定名稱案例中，`OPENROWSET` 函式第三個引數會指定描述目錄、結構描述和物件名稱的三部分名稱。 目錄名稱和結構描述名稱之一或兩者可為空白 (具有空白目錄名稱和結構描述名稱的四部分名稱看起來像是 `<server-name>...<object-name>`)。在此情況下，SQL Server 會使用 `NULL` 作為要在結構描述資料列集資料表中尋找的對應值。

SQL Server 所採用的名稱解析規則和中繼資料擷取步驟，取決於提供者是否在 `Session` 物件上支援 `IDBSchemaRowset` 介面。

如果支援 `IDBSchemaRowset`，則會從 `IDBSchemaRowset` 介面使用 `TABLES`、`COLUMNS`、`INDEXES` 和 `TABLES_INFO` 結構描述資料列集 (`TABLES_INFO` 結構描述資料列集是在 OLE DB 2.0 中定義)。SQL Server 會限制 `IDBSchemaRowset` 介面所傳回的結構描述資料列集，以尋找符合指定遠端資料表名稱部分的結構描述資料列。 下列是提供者在結構描述資料列集上支援的限制相關規則，以及 SQL Server 如何使用它們來擷取遠端資料表的中繼資料：

- 在 `TABLE_NAME` 和 `COLUMN_NAME` 資料行上一律需要限制。

- 如果提供者支援 `TABLE_CATALOG` (或 `TABLE_SCHEMA`) 上的限制，SQL Server 會在 `TABLE_CATALOG` (或 `TABLE_SCHEMA`) 上使用該限制。 如果沒有在遠端資料表名稱中指定目錄 (或結構描述) 名稱，則會使用 `NULL` 值作為對應的限制值。 如果指定了目錄 (或結構描述) 名稱，提供者必須支援 `TABLE_CATALOG` (或 `TABLE_SCHEMA`) 上的對應限制。

- 提供者必須同時支援 `TABLES` 和 `COLUMNS` 中 `TABLE_SCHEMA` 資料行上的限制，或兩者都不支援。 提供者必須同時支援 `TABLES` 和 `COLUMNS` 資料列集上的目錄名稱限制，或兩者都不支援。

- 如果支援 INDEXES 上的任何限制，提供者必須同時支援 `TABLES` 和 INDE`XES or support them on neither. The provider must either support catalog name restriction on both `TABLES` and `INDEXES` 資料列集上的目錄名稱限制，或兩者都不支援。

從 `TABLES` 結構描述資料列集，SQL Server 會根據上述規則設定限制，以擷取 `TABLE_CATALOG`、`TABLE_SCHEMA`、`TABLE_NAME`、`TABLE_TYPE`、`TABLE_GUID` 資料行。

從 `COLUMNS` 結構描述資料列集，SQL Server 會擷取 `TABLE_CATALOG`、`TABLE_SCHEMA`、`TABLE_NAME`、`COLUMN_NAME`、`COLUMN_GUID`、`ORDINAL_POSITION`、`COLUMN_FLAGS`、`IS_NULLABLE`、`DATA_TYPE`、`TYPE_GUID`、`CHARACTER_MAXIMUM_LENGTH`、`NUMERIC_PRECISION` 和 `NUMERIC_SCALE` 資料行。 `COLUMN_NAME`、`DATA_TYPE` 和 `ORDINAL_POSITION` 必須傳回有效的非 Null 值。 如果 `DATA_TYPE` 是 `DBTYPE_NUMERIC` 或 `DBTYPE_DECIMAL`，對應的 `NUMERIC_PRECISION` 和 `NUMERIC_SCALE` 必須是有效的非 Null 值。

從選擇性 `INDEXES` 結構描述資料列集，SQL Server 會根據上述規則設定限制，以在指定的遠端資料表上尋找索引。 從找到的相符索引項目，SQL Server 會擷取 `TABLE_CATALOG`、`TABLE_SCHEMA`、`TABLE_NAME`、`INDEX_CATALOG`、`INDEX_SCHEMA`、`INDEX_NAME`、`PRIMARY_KEY`、`UNIQUE`、`CLUSTERED`、`FILL_FACTOR`、`ORDINAL_POSITION`、`COLUMN_NAME`、`COLLATION`、`CARDINALITY` 和 `PAGES` 資料行。

從選擇性 `TABLES_INFO` 資料列集，SQL Server 會在指定的遠端資料表上尋找其他資訊，例如書籤支援、書籤類型和長度。 這會使用 `TABLES_INFO` 資料列集的 `DESCRIPTION` 資料行以外所有資料行。 `TABLES_INFO` 資料列集中的資訊使用方式如下：

- `BOOKMARK_DURABILITY` 資料行可用於實作更有效率的索引鍵集資料指標。 如果此資料行具有 `BMK_DURABILITY_INTRANSACTION` 的值或更高持久性值，SQL Server 會根據書籤擷取並更新遠端資料表資料列，以實作索引鍵集資料指標。

- `BOOKMARK_TYPE`、`BOOKMARK_DATA TYPE` 和 `BOOKMARK_MAXIMUM_LENGTH` 資料行可在查詢編譯期間用於判斷書籤中繼資料。 如果不支援這些資料行，SQL Server 會在編譯期間透過 `IOpenRowset` 開啟基底資料表資料列集來取得書籤資訊。

如果不支援 `IDBSchemaRowset` 且遠端資料表名稱包含目錄名稱或結構描述名稱，SQL Server 需要 `IDBSchemaRowset` 並會傳回錯誤。 不過，如果沒有提供目錄和結構描述名稱，SQL Server 會開啟對應到遠端資料表的資料列集，並從資料列集物件的必要 `IColumnsInfo` 介面擷取資料行中繼資料。

SQL Server 會透過呼叫 `IOpenRowset::OpenRowset` 來開啟對應到資料表的資料列集。 提供給 `OPENROWSET` 的資料表名稱是從目錄、結構描述和物件名稱部分建構而來。

- 每個名稱部分 (`catalog`、`schema`、`object name`) 都會以提供者的引號字元 (`DBLITERAL_QUOTE`) 括住，然後在其間內嵌 `DBLITERAL_CATALOG_SEPARATOR` 字元和 `DBLITERAL_SCHEMA_SEPARATOR` 字元來串連。 名稱建構會遵循 `IOpenRowset` 中的 OLE DB 規則。

- 開啟資料列集物件之後，即可透過 `IColumnsInfo::GetColumnInfo` 擷取資料表的資料行中繼資料。

如果 TABLES、COLUMNS 和 TABLES_INFO 資料列集不支援 `IDBSchemaRowset`，SQL Server 會在基底資料表上開啟資料列集兩次：一次在查詢編譯期間用於擷取中繼資料，一次在查詢執行期間。 如果提供者在開啟資料列集時會產生副作用 (例如執行改變即時裝置狀態的程式碼、傳送電子郵件、執行使用者提供的任意程式碼)，則必須注意此行為。

### <a name="statistics-retrieval"></a>統計資料擷取

如果提供者支援基底資料表的相關分佈統計資料，則 SQL Server 會使用這些統計資料。 SQL Server 查詢處理器有兩個重要的統計資料類型：

- **資料行 (或元組) 基數**。 這是資料表資料行 (或資料行組合) 中的唯一值數目。 這可用來估計資料行中述詞的選擇性。 支援分佈統計資料的提供者應該支援至少一種基數類型。

- **長條圖**。 如果值的分佈不均勻，則 唯一值的數目不足，無法準確地估計述詞的選擇性。 在此情況下，可以提供長條圖，讓您更鉅細靡遺地了解資料表中的資料行值分佈。

統計資料的可用性可讓 SQL Server 查詢最佳化工具更佳估計查詢的中繼操作基數，以為其產生更好的執行計畫。

OLE DB 提供者支援分佈統計資料的方式如下：

- **必要**。 支援下列屬性：(1) `DBPROP_TABLESTATISTICS`，指出是否支援資料行或元組基數，以及是否支援長條圖；(2) `DBPROP_OPENROWSETSUPPORT`，指出使用 `DBPROPVAL_ORS_HISTOGRAM` 位元，以及是否支援長條圖。

- **必要**。 `TABLE_STATISTICS` 結構描述資料列集。 `TABLE_STATISTICS` 結構描述資料列集會列出指定資料庫中可用的統計資料。 它也包含結構描述資料列集本身內部的資料行和元組基數，並指出特定資料行是否支援長條圖。 若要讓 SQL Server 使用統計資料，此結構描述資料列集中必須有資料行 `TABLE_NAME`、`STATISTICS_NAME`、`STATISTICS_TYPE`、`COLUMN_NAME` 和 `ORDINAL_POSITION`。 至少必須有 `COLUMN_CARDINALITY` 或 `TUPLE_CARDINALITY` 其中之一。 如果支援長條圖，也必須有 `NO_OF_RANGES`。

- **選擇性**。 (選擇性) 如果提供者支援長條圖，則應該支援 `IOpenRowset::OpenRowset` 方法的增強功能，以允許透過指定對應統計資料的 `DBID` 來開啟長條圖資料列集。

如需統計資料介面的完整資訊，請參閱 OLE DB 2.6 規格。

### <a name="constraints"></a>條件約束

如果 OLE DB 提供者支援 OLE DB 2.6 結構描述資料列集 `CHECK_CONSTRAINTS_BY_TABLE`，SQL Server 查詢最佳化工具也會使用定義於遠端資料來源中基底資料表的 `CHECK` 條件約束。 結構描述資料列集 `CHECK_CLAUSE` 資料行應該以符合 SQL-92 規範的語法傳回 `CHECK` 子句述詞。 查詢最佳化工具使用條件約束資訊以消除或簡化已知一律為 false 或一律為 true 的述詞，因為資料表上存在 check 條件約束。

### <a name="transaction-management"></a>交易管理

SQL Server 支援使用提供者的 `ITransactionLocal` (適用於本機交易) 與 `ITransactionJoin` (適用於分散式交易) OLE DB 介面，以交易方式存取分散式資料。 藉由對提供者啟動本機交易，SQL Server 保證不可部分完成的寫入作業。 藉由使用分散式交易，SQL Server 可確保涉及到多個節點的交易在所有節點中都有相同結果 (認可或中止)。 如果提供者不支援必要的 OLE DB 交易相關介面，則根據本機交易內容，不允許對該提供者執行更新作業。

下表描述當使用者根據提供者的功能和本機交易內容執行分散式查詢時所發生狀況。 對提供者的讀取作業是指 `SELECT` 陳述式，或當遠端資料表讀入 `SELECT INTO`、`INSERT`、`UPDATE` 或 `DELETE` 陳述式的輸入端時。 對提供者的寫入作業是指 `INSERT`、`UPDATE` 或 `DELETE` 陳述式，並使用遠端資料表作為目的地資料表。

根據提供者功能和交易內容，分散式查詢的結果如下：

|發生分散式查詢|提供者不支援 `ITransactionLocal`|提供者支援 `ITransactionLocal` 但不支援 `ITransactionJoin`|提供者同時支援 `ITransactionLocal` 和 `ITransactionJoin`|
|:-----|:-----|:-----|:-----|
| 在交易本身內部 (無使用者交易)。|根據預設，只允許讀取作業。 啟用提供者層級選項 `Nontransacted Updates` 時，允許寫入作業。 (啟用此選項時，SQL Server 無法保證提供者資料的不可部分完成性和一致性。 這可能會造成寫入作業的部分影響反映在遠端資料來源中，而無法復原。)| 允許對遠端資料執行所有陳述式。 索引鍵集資料指標是唯讀的。 本機交易是使用目前 SQL Server 工作階段的隔離等級在提供者上啟動，並在陳述式評估成功結束時認可。 (除非使用 `SET TRANSACTION ISOLATION LEVEL` 陳述式進行修改，否則 SQL Server 工作階段的預設隔離等級為 `READ COMMITTED`。 提供者必須支援要求的隔離等級。) | 允許所有陳述式。 索引鍵集資料指標是唯讀的。 本機交易是使用目前 SQL Server 工作階段的隔離等級在提供者上啟動，並在陳述式評估成功結束時認可。 |
| 在使用者交易中 (也就是在 `BEGIN TRAN` 或 `COMMIT` 與 `BEGIN DISTRIBUTED TRAN` 之間)。 | 如果交易的隔離等級為 `READ COMMITTED` (預設值) 或以下，則允許讀取作業。 如果隔離等級較高，則不允許任何分散式查詢。 | 只允許讀取作業。 新分散式交易是使用目前 SQL Server 工作階段的隔離等級在提供者上啟動。 |允許所有陳述式。 新分散式交易是使用目前 SQL Server 工作階段的隔離等級在提供者上啟動，並在使用者交易認可時認可。 針對資料修改陳述式，SQL Server 預設會在分散式交易下啟動巢狀交易，以便在特定錯誤狀況下能夠停止資料修改陳述式，而不需要停止周圍的交易。 如果開啟 `XACT_ABORT SET` 選項，則 SQL Server 不需要巢狀交易支援，並會在資料修改陳述式期間發生錯誤時停止周圍的交易。 |
|  |  |  |

### <a name="data-type-handling-in-distributed-queries"></a>分散式查詢中的資料類型處理

OLE DB 提供者以 OLE DB 定義的資料類型 (在 OLE DB 中以 `DBTYPE` 指出) 來公開其資料。 SQL Server 會將伺服器內的外部資料當作原生 SQL Server 類型來處理；這會導致在 SQL Server 使用資料時，將 OLE DB 資料類型對應到 SQL Server 原生類型，並在 SQL Server 匯出資料時，將 SQL Server 原生類型對應到 OLE DB 資料類型。 除非另有註明，否則會以隱含方式完成此對應。

您可以使用下列兩種對應方法之一來處理分散式查詢中的資料類型：

- 當遠端資料表出現在 `SELECT` 陳述式中以及 INSERT、UPDATE 和 DELETE 陳述式的輸入端時，使用端對應會將 OLE DB 資料類型的類型對應到使用端上 SQL Server 原生資料類型。

- 當遠端資料表似乎是 `INSERT` 或 `UPDATE` 陳述式的目的地資料表時，匯出端對應會將 SQL Server 資料類型中的類型對應到匯出端上 OLE DB 資料類型。

SQL Server 和 OLE DB 資料類型對應表。

| OLE DB 類型 | `DBCOLUMNFLAG` | SQL Server 資料類型 |
|-----|-----|-----|
|`DBTYPE_I1`*| |`numeric(3, 0)`|
|`DBTYPE_I2`| |`smallint`|
|`DBTYPE_I4`| |`int`|
|`DBTYPE_I8`| |`numeric(19,0)`|
|`DBTYPE_UI1`| |`tinyint`|
|`DBTYPE_UI2`*| |`numeric(5,0)`|
|`DBTYPE_UI4`*| |`numeric(10,0)`|
|`DBTYPE_UI8`*| |`numeric(20,0)`|
|`DBTYPE_R4`| |`float`|
|`DBTYPE_R8`| |`real`|
|`DBTYPE_NUMERIC`| |`numeric`|
|`DBTYPE_DECIMAL`| |`decimal`|
|`DBTYPE_CY`| |`money`|
|`DBTYPE_BSTR`| `DBCOLUMNFLAGS_ISFIXEDLENGTH=true`<br>或<br> 最大長度 > 4000 個字元|ntext|
|`DBTYPE_BSTR`| `DBCOLUMNFLAGS_ISFIXEDLENGTH=true`|NCHAR|
|`DBTYPE_BSTR`| `DBCOLUMNFLAGS_ISFIXEDLENGTH=false`|NVARCHAR|
|`DBTYPE_IDISPATCH`| |錯誤|
|`DBTYPE_ERROR`| |錯誤|
|`DBTYPE_BOOL`| |`bit`|
|`DBTYPE_VARIANT`*| |NVARCHAR|
|`DBTYPE_IUNKNOWN`| |錯誤|
|`DBTYPE_GUID`| |`uniqueidentifier`|
|`DBTYPE_BYTES`|`DBCOLUMNFLAGS_ISLONG=true` <br>或<br> 最大長度 > 8000|`image`|
|`DBTYPE_BYTES`|`DBCOLUMNFLAGS_ISROWVER=true`、`DBCOLUMNFLAGS_ISFIXEDLENGTH=true`、資料行大小 = 8 <br>或<br> 未回報最大長度。 | `timestamp` |
|`DBTYPE_BYTES`| `DBCOLUMNFLAGS_ISFIXEDLENGTH=true` | `binary` |
|`DBTYPE_BYTES`| `DBCOLUMNFLAGS_ISFIXEDLENGTH=true` | `varbinary`|
|`DBTYPE_STR`| `DBCOLUMNFLAGS_ISFIXEDLENGTH=true` | `char`|
|`DBTYPE_STR`| `DBCOLUMNFLAGS_ISFIXEDLENGTH=true` | `varchar` |
|`DBTYPE_STR`| `DBCOLUMNFLAGS_ISLONG=true` <br>或<br> 最大長度 > 8000 個字元 <br>或<br>   未回報最大長度。 | `text`|
|`DBTYPE_WSTR`| `DBCOLUMNFLAGS_ISFIXEDLENGTH=true` |`nchar`|
|`DBTYPE_WSTR` | `DBCOLUMNFLAGS_ISFIXEDLENGTH=false`|`nvarchar`|
|`DBTYPE_WSTR`| `DBCOLUMNFLAGS_ISLONG=true` <br>或<br> 最大長度 > 4000 個字元 <br>或<br>   未回報最大長度。 | `ntext`|
|`DBTYPE_UDT`| |錯誤|
|`DBTYPE_DATE`* | | `datetime` |
|`DBTYPE_DBDATE` | | `datetime` (需要明確轉換)|
|`DBTYPE_DBTIME`| | `datetime` (需要明確轉換)|
|`DBTYPE_DBTIMESTAMP`* | | `datetime`|
|`DBTYPE_ARRAY` | |錯誤|
|`DBTYPE_BYREF` | | 忽略 |
|`DBTYPE_VECTOR` | |錯誤|
|`DBTYPE_RESERVED`| |錯誤|

\* 指出因為 SQL Server 中沒有完全相等的資料類型，所以利用某種形式轉譯為 SQL Server 類型的代表。 這類轉換可能會導致遺失有效位數、溢位或反向溢位。 如果 SQL Server 未來版本支援對應的資料類型，則未來可以變更預設的隱含對應。

>[!NOTE]
>`numeric(p,s)` 指出 SQL Server 資料類型 `numeric`，有效位數是 `p`，小數位數是 `s`。 `DBTYPE_NUMERIC` 和 `DBTYPE_DECIMAL` 允許的最大有效位數為 38。 建立存取子時，提供者必須支援繫結至 `DBTYPE_BSTR` 資料行作為 `DBTYPE_WSTR`。 `DBTYPE_VARIANT` 資料行會當作 Unicode 字元字串 `nvarchar` 使用。 這需要提供者支援從 `DBTYPE_VARIANT` 轉換成 `DBTYPE_WSTR`。 提供者必須依照 OLE DB 中的定義來實作這項轉換。 如需詳細資訊，請參閱 [OLE DB 規格的資料類型](#appendixa)。

#### <a name="interpreting-data-type-mapping"></a>解譯資料類型對應

SQL Server 類型的對應取決於 OLE DB 資料類型，以及描述資料行或純量值的 DBCOLUMNFLAGS 值。 在 `COLUMNS` 結構描述資料列集案例中，會以 `DATA_TYPE` 和 `COLUMN_FLAGS` 資料行表示這些值。 在 `IColumnsInfo::GetColumnInfo` 介面案例中，會以 `DBCOLUMNINFO` 結構的 `wType` 和 `dwFlags` 成員表示這項資訊。

若要將使用端對應用於具有特定 `DBTYPE` 和 `DBCOLUMNFLAG` 值的指定資料行，請在資料表中尋找對應的 SQL Server 類型。 運算式中遠端資料表資料行的類型規則可以下列簡單規則來描述：

>在相同的內容中，若資料表中相對應的對應 SQL Server 類型正確，則 Transact-SQL 運算式中的指定遠端資料行值正確。

資料表和規則會定義：

- 比較和運算式。

一般而言，如果 `<op>` 是資料類型 `X` 及 `<remote-column>` 所對應資料類型的有效運算子，則 `X <op> <remote-column>` 是有效的運算式。

- 明確轉換。

如果 `<remote-column>` 的 `DBTYPE` 對應到原生資料類型 `Y` (如上表所示)，且允許從 `Y` 明確轉換成 `X`，則允許 `Convert(X, <remote-column>)`。

如果使用者想要將遠端資料轉換成非預設的原生資料類型，則必須使用明確轉換。

若要在對遠端資料表執行 `UPDATE` 和 `INSERT` 陳述式的案例中使用匯出端對應，請使用相同的資料表將原生 SQL Server 資料類型對應到 OLE DB 資料類型。 如果存在下列任一項，則允許從 SQL Server 類型 `S1` 對應到指定的 OLE DB 類型 `T`：

- 您可以直接在對應表中找到相對應的對應。

- 允許將 `S1` 隱含轉換成另一個 SQL Server 類型 `S2`，讓 `S2` 對應到對應表中的類型 `T`。

#### <a name="large-object-lob-handling"></a>大型物件 (LOB) 處理

如對應表中所示，如果 `DBTYPE_STR`、`DBTYPE_WSTR` 或 `DBTYPE_BSTR` 類型的資料行也回報 `DBCOLUMNFLAGS_ISLONG`，或如果其最大長度超過 4,000 個字元 (或未回報最大長度)，則 SQL Server 會適當地將其視為 `text` 或 `ntext` 資料行。 同樣地，針對 `DBTYPE_BYTES` 資料行，如果已設定 `DBCOLUMNFLAGS_ISLONG`，或如果最大長度超過 8,000 個位元組 (或未回報最大長度)，則會將資料行視為 `image` 資料行。 `Text`、`ntext` 和 `image` 資料行稱為 LOB 資料行。

SQL Server 不會從 OLE DB 提供者公開 LOB 的完整文字和影像功能。 OLE DB 提供者的大型物件上不支援 `TEXTPTRS`；因此，不支援任何相關功能，例如 `TEXTPTR` 系統函數以及 `READTEXT`、`WRITETEXT` 和 `UPDATETEXT` 陳述式。 支援使用 `SELECT` 陳述式來擷取整個 LOB 資料行，也支援針對遠端資料表中的整個大型物件資料行使用 `UPDATE` 和 `INSERT` 陳述式。

SQL Server 可以在 LOB 資料行上使用結構化儲存介面 (如果提供者支援的話)。 結構化儲存介面依優先順序和功能遞增排序如下：`ISequentialStream`、`Istream` 或 `ILockBytes`。 如果支援其中一或多個介面，當透過 `IDBProperties` 介面查詢時，提供者必須傳回 DBPROPVAL_OO_BLOB 作為 `DBPROP_OLEOBJECTS` 屬性的值。 此外，提供者應該指出支援它在 `DBPROP_STRUCTUREDSTORAGE` 屬性中支援的介面。

如果提供者不支援 LOB 資料行上的任何結構化儲存介面，SQL Server 會自行具體化此介面，並仍將其公開為 `text`、`ntext` 或 `image` 資料行。

#### <a name="accessing-lob-columns"></a>存取 LOB 資料行

如果提供者支援其中一個結構化儲存介面，SQL Server 會執行下列步驟，以在查詢執行期間擷取 LOB 資料行：

1. 在透過 `IOpenRowset::OpenRowset` 開啟資料列集之前，SQL Server 會先要求支援大型物件資料行上的一或多個結構化儲存介面 (`ISequentialStream`、`Istream` 和 `ILockBytes`)。 提供者支援的第一個介面為必要；其他介面則會以 \"set if cheap\" (若便宜即設定) 形式要求 (做法是將對應 DBPROP 結構的 *dwOptions* 元素設定為 DBPROPOPTIONS_SETIFCHEAP)。 例如，如果提供者同時支援 `ISequentialStream` 和 `ILockBytes`，則 `ISequentialStream` 是必要的，而 `ILockBytes` 會以 \"set if cheap\" (若便宜即設定) 形式來要求。

4. 在開啟資料列集之後，SQL Server 會使用 `IRowsetInfo::GetProperties` 來識別資料列集中可用的實際介面。 系統會使用提供者所傳回最後一個介面或優先順序最高的介面。 當 SQL Server 建立針對大型物件資料行的存取子時，資料行會繫結為 DBTYPE_IUNKNOWN，並將繫結中 DBOBJECT 結構的 *iid* 元素設定為介面。

#### <a name="reading-from-lob-columns"></a>從 LOB 資料行進行讀取

您可以使用所要求結構化儲存介面的介面指標 (透過 `IRowset::GetData` 在資料列緩衝區中傳回)，從大型物件資料行進行讀取。 如果提供者不支援同時開啟多個 LOB (也就是如果不支援 `DBPROP_MULTIPLE_STORAGEOBJECTS`)，且資料列具有多個大型物件資料行，則 SQL Server 會將 LOB 資料行複製到本機工作資料表。

#### <a name="update-and-insert-statements-on-lob-columns"></a>LOB 資料行上的 `UPDATE` 和 `INSERT` 陳述式

SQL Server 會將新儲存物件的指標傳遞給提供者，而不是使用提供者提供的介面來修改儲存物件。 針對每個 LOB 資料行，會使用所選結構化儲存介面來建立在儲存物件上更新或插入的值。 根據這是 `UPDATE` 或 `INSERT` 作業，會分別透過 `IRowsetChange::SetData` 或 `IRowsetChange::InsertRow` 將儲存物件的指標傳遞給提供者。

### <a name="error-handling"></a>錯誤處理

當針對 OLE DB 提供者的特定方法引動過程傳回錯誤碼時，SQL Server 會先尋找提供者的延伸錯誤資訊，再將錯誤狀況的相關資訊傳回給使用者。

SQL Server 會依照 OLE DB 所指定來使用 OLE DB 錯誤物件。 以下是其中一些高階步驟：

1. 當方法引動過程從提供者傳回錯誤碼時，SQL Server 會尋找 `ISupportErrorInfo` 介面。 如果支援此介面，SQL Server 會呼叫 `ISupportErrorInfo::InterfaceSupportsErrorInfo` 以確認產生錯誤碼的介面是否支援錯誤物件。

<!-- -->

5. 如果介面支援錯誤物件，SQL Server 會呼叫 `GetErrorInfo` 函式以取得目前錯誤物件上的 `IErrorInfo` 介面指標。

6. SQL Server 使用 `IErrorInfo` 介面來取得 `IErrorRecords` 介面的指標。

7. SQL Server 使用 `IErrorRecords` 來逐一查看物件中的所有錯誤記錄，並取得對應到每筆記錄的錯誤訊息文字。

如需如何使用提供者錯誤物件的詳細資訊，請參閱您的 OLE DB 文件。

### <a name="security"></a>安全性

當取用者連接到 OLE DB 提供者時，除非取用者想要以整合式安全性使用者身分進行驗證，否則提供者通常需要使用者識別碼和密碼。 在分散式查詢案例中，SQL Server 可作為 OLE DB 提供者的取用者，代替 SQL Server 登入執行分散式查詢。 SQL Server 會將目前的 SQL Server 登入對應到連結伺服器上使用者識別碼和密碼。

這些對應可由指定連結伺服器的使用者指定，並可透過系統預存程序 `sp_addlinkedsrvlogin` 和 `sp_droplinkedsrvlogin` 進行設定和管理。 藉由透過 `IDBProperties::SetProperties` 設定初始化群組屬性 DBPROP_AUTH_USERID 和 DBPROP_AUTH_PASSWORD，即可在連接建立期間，將由對應決定的使用者識別碼和密碼傳遞給提供者。

當用戶端透過 Windows 驗證連接到 SQL Server 時，如果登入已使用 `sp_addlinkedsrvlogin` 設定 `self` 對應，SQL Server 會在連接建立期間嘗試模擬用戶端的安全性內容，並在提供者上設定 `DBPROP_AUTH_INTEGRATED` 屬性。 此程序稱為「委派」  。

決定用於連接的安全性內容之後，此安全性內容的驗證，以及對資料來源中資料物件檢查該內容的權限，則完全取決於 OLE DB 提供者。

如需詳細資訊，請參閱 [`sp_addlinkedsrvlogin`](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md) 和 [`sp_droplinkedsrvlogin`](../../relational-databases/system-stored-procedures/sp-droplinkedsrvlogin-transact-sql.md)。

## <a name="query-execution-scenarios"></a>查詢執行案例

 評估分散式查詢時，SQL Server 會在下列一或多個案例中與 OLE DB 提供者互動：

- 遠端查詢

- 索引存取

- 純資料表掃描

- `UPDATE` 和 DELETE 陳述式

- `INSERT` 陳述式

- 傳遞查詢

### <a name="remote-query"></a>遠端查詢

SQL Server 會產生一個 SQL 查詢，其用來評估可完全由提供者評估的部分原始查詢。 此案例只能對 SQL 命令提供者進行。 SQL Server 藉由產生 SQL 查詢將作業推送給提供者的範圍，取決於提供者支援的 SQL 文法。 提供者應該透過下列方式指出其 SQL 支援層級：

1. 藉由透過 `DBPROP_SQLSUPPORT` 屬性表示 SQL 最低層級、ODBC 核心層級或 SQL-92 入門層級支援。 SQL 最低語法層級是 SQL Server 支援的新層級，可讓 SQL Server 將遠端查詢傳送給支援簡單 SQL 子集的簡單提供者。 此層級包含不包括子查詢的基本 `SELECT` 陳述式、`FROM` 子句中的多個資料表 (因此不含聯結) 和 GROUP BY。 如需 SQL Server 針對上述每個語法層級的提供者產生遠端查詢所使用 SQL 文法子集，請參閱[用於產生遠端查詢的 SQL 子集](#appendixb)。

1. 藉由支援各種 SQL Server 特定屬性來指出支援 DBPROP_SQLSUPPORT 所報告語法層級未包含的個別 SQL 功能。 本節稍後將提供屬性清單並描述 SQL Server 如何使用這些屬性。

SQL Server 使用參數化查詢執行，並以問號 (?) 作為 Transact-SQL 字串中的參數標記。 您可以針對 SQL Server、Microsoft Jet 和 Oracle OLE DB 提供者使用參數化查詢執行。 針對其他提供者，只有在提供者支援 `Command` 物件上的 `ICommandWithParameters`，並符合下列至少一個條件時，才能使用參數化查詢執行：

- 提供者透過 `DBPROP_SQLSUPPORT` 屬性指出 ODBC 核心層級的 SQL Server 支援。

- 提供者透過 `IDBPProperties` 支援 SQL Server 特定屬性 SQLPROP_DYNCMICSQL，來指出支援問號 (?) 參數標記。 如需詳細資訊，請參閱下一節的提供者屬性。

- 系統管理員在提供者上設定 `Dynamic Parameters` 提供者選項來讓 SQL Server 產生參數化查詢。

當 SQL Server 產生要從遠端執行的 SQL 文字時，會使用提供者的引號字元 (透過 `IDBInfo` 介面的 `DBLITERAL_QUOTE` 常值回報) 來括住資料表和資料行名稱。 如果不支援此常值，則不會括住資料表和資料行名稱。

如果提供者支援參數化查詢執行，SQL Server 可以考慮使用參數化查詢執行策略來評估遠端資料表與本機資料表的聯結。 您可以對從本機資料表中每個資料列產生的參數值來重複執行參數化查詢。 此策略可減少從提供者擷取的資料列數目，若將具有少量資料列之本機資料表與具有大量資料列的遠端資料表聯結，則可從中獲益。 此遠端聯結策略可透過 `REMOTE` 聯結最佳化工具提示來強制執行。 如需參數化查詢執行的詳細資訊，請參閱[如何：執行參數化查詢](../../connect/php/how-to-perform-parameterized-queries.md)。

下列是在遠端查詢案例中對提供者執行的更高階步驟。

1. SQL Server 使用 `IDBCreateCommand::CreateCommand` 從 `Session` 物件建立 `Command` 物件。

9. 如果 `Remote Query Timeout` 伺服器設定選項設定為值 > 0，則 SQL Server 會使用 `ICommandProperties::SetProperties` 將 `Command` 物件上的 `DBPROP_COMMANDTIMEOUT` 屬性設定為相同值；必須呼叫 `ICommand::SetCommandText`，才能將命令文字設定為產生的 Transact-SQL 字串。

10. SQL Server 呼叫 `ICommandPrepare::Prepare` 來準備命令。 如果提供者不支援此介面，SQL Server 會繼續執行步驟 4。

11. 如果產生的查詢已參數化，SQL Server 會使用 `ICommandWithParameters::SetParameterInfo` 來描述參數，並使用 `IAccessor::CreateAccessor` 為參數建立存取子。

12. SQL Server 呼叫 `ICommand::Execute` 來執行命令並建立資料列集。

13. SQL Server 使用 `IRowset` 介面來巡覽並使用資料表中的資料列。 您可以使用 `IRowset::GetNextRows` 來擷取資料列、使用 `IRowset::RestartPosition` 來重新置放到資料列集的開頭，並使用 `IRowset::ReleaseRows` 來釋放資料列。

#### <a name="provider-properties-of-interest-for-remote-query-execution"></a>遠端查詢執行的重要提供者屬性

如果提供者支援 DBPROP_SQLSUPPORT 所報告語法層級未涵蓋的 SQL 功能，則可以使用各種提供者特定屬性來指出這些支援。

- SQLPROP_GROUPBY。 此屬性對於支援 SQL 最低層級的提供者很重要。 此屬性指出提供者支援 `SELECT` 陳述式中的 GROUP BY 和 HAVING 子句。 此外，此屬性也指出提供者支援下列五個彙總函式 MIN、MAX、SUM、COUNT 和 AVG。 提供者可能不支援這些彙總函式引數上的 DISTINCT。

- SQLPROP_SUBQUERIES。 此屬性對於支援 SQL 最低層級的提供者很重要。 它指出提供者支援子查詢，如 SQL-92 入門層級所指定。 這包括 `SELECT` 清單和 `WHERE` 子句中的子查詢，並支援相互關聯子查詢的 `IN`、`EXISTS`、`ALL` 和 `ANY` 運算子。

- SQLPROP_DATELITERALS。 此屬性對於任何提供者 (包括支援 SQL-92 入門層級的提供者) 都很重要。 日期時間常值不是 SQL-92 入門層級支援的標準常值語法。 此 SQL Server 特定屬性指出提供者支援日期時間常值語法 (如 SQL-92 標準所指定)。

- SQLPROP_ANSILIKE。 對於支援 SQL 最低層級的提供者很重要。 此屬性指出提供者根據 SQL-92 入門層級支援 `LIKE` 運算子 (以 \'%\' 和 \'_\' 作為萬用字元)。 因為 SQL 最低層級不包含 `LIKE` 支援，所以這對於支援 SQL 最低層級的提供者很有用。

- SQLPROP_INNERJOIN。 此屬性對於支援 SQL 最低層級的提供者很重要。 它指出支援 `FROM` 子句中的多個資料表。 因為 SQL 最低層級不包含聯結支援，所以這對於只支援 SQL 最低層級的提供者很有用。 這不指出支援明確 JOIN 關鍵字，也不指出支援外部聯結。 它指出只支援透過 `FROM` 子句中的資料表清單進行隱含聯結。

- SQLPROP_DYNAMICSQL。 指出支援 `?` 作為參數標記。 `WHERE` 子句或 `SELECT` 清單中的純量項目位置應該支援參數標記。 `?` 參數標記支援可讓 SQL Server 將參數化查詢傳送給提供者。

- SQLPROP_NESTEDQUERIES。 指出支援 `FROM` 子句中的巢狀 SELECT (例如 `SELECT * FROM (SELECT * FROM T))`。 在許多情況下，當 SQL Server 產生要從遠端執行的查詢字串時，會在查詢的 `FROM` 子句中使用巢狀 `SELECT` 陳述式。 因為 SQL-92 入門層級不需要巢狀 `SELECT` 支援，所以除非提供者也設定此屬性，否則 SQL Server 不會將具有巢狀 `SELECT` 陳述式的查詢委派給提供者。 或者，系統管理員也可以為提供者設定 `Nested Queries` 提供者選項，讓 SQL Server 對提供者產生巢狀查詢。

提供者可以使用稱為 `SQLPROPSET_OPTHINTS` 的 SQL Server 特定屬性集來支援這些屬性，並具有定義的 `PROPID` 值。 使用下列常數來定義屬性集 `SQLPROPSET_OPTHINTS` 和兩個屬性：

```
extern const GUID `SQLPROPSET_OPTHINTS` = { 0x2344480c, 0x33a7, 0x11d1, { 0x9b, 0x1a, 0x0, 0x60, 0x8, 0x26, 0x8b, 0x9e } };
enum SQLPROPERTIES {
SQLPROP_NESTEDQUERIES = 0x4,
SQLPROP_DYNAMICSQL = 0x5,
SQLPROP_GROUPBY = 0x6,
SQLPROP_DATELITERALS = 0x7,
SQLPROP_ANSILIKE = 0x8,
SQLPROP_INNERJOIN = 0x9,
SQLPROP_SUBQUERIES = 0x10
};
```

#### <a name="character-set-and-sort-order-implications"></a>字元集和排序次序含意

SQL Server 支援在每個資料行層級指定字元資料的定序。 針對非 Unicode 字元資料 (`char` 和 `varchar` 資料行)，定序會包含字元集和排序次序規格。 針對 Unicode 資料 (`nchar` 和 `nvarchar` 資料行)，定序只會指定排序次序。

只有在連結伺服器所使用的字元集 (適用於非 Unicode 資料)、排序次序和字串比較語意與本機伺服器所使用的字元集相同時，SQL Server 才會將字串比較委派給提供者。

在 SQL Server 連結的伺服器案例中，SQL Server 會自動判斷定序相容性。 針對其他提供者，系統管理員必須向 SQL Server 指出字元資料定序來自指定的連結伺服器。 在 SQL Server 中，支援稱為 [`Collation Name`] 的新連結伺服器選項。 如果系統管理員判斷連結伺服器所採用的定序語意與其中一個 SQL Server 標準定序相同，則可以將 [`Collation Name`] 選項設定為該定序名稱。 您可以使用 `sp_serveroption` 系統預存程序設定 [`Collation Name`] 選項。 只有在同時符合下列兩個條件時，才應該設定此選項：

- 遠端排序次序和字元集與指定的 SQL Server 定序相同。

- OLE DB 提供者所使用的字串比較語意遵循 SQL-92 標準規格語意，或相當於 SQL Server 的比較語意。

為了回溯相容性，仍然支援 SQL Server 7.0 中支援的 [定序相容] 選項。 將它設定為 true 相當於將 [定序名稱] 選項設定為 SQL Server master 資料庫的預設定序。 新的應用程式應該使用 [定序名稱] 選項，而不是 [定序相容] 選項。

### <a name="indexed-access"></a>索引查詢

SQL Server 使用提供者所公開索引來評估分散式查詢的特定述詞。 此案例只能對索引提供者進行，且使用者必須設定 `Index as Access Path` 提供者選項。 下列是當 SQL Server 使用索引執行查詢時，對提供者所執行的主要高階步驟：

1. 使用完整資料表名稱和索引名稱，透過 `IOpenRowset::OpenRowset` 開啟索引資料列集。 系統已產生完整資料表和索引名稱，如遠端查詢案例稍早所述。

1. 使用完整資料表名稱，透過 `IOpenRowset::OpenRowset` 開啟基底資料表資料列集。

1. 根據查詢述詞，透過 `IRowsetIndex::SetRange` 設定索引資料列集上的範圍。

1. 在索引資料列集上，透過 `IRowset` 掃描超過索引資料列集的資料列。

1. 從擷取的索引資料列使用書籤資料行，透過 `IRowsetLocate::GetRowsByBookmark` 從基底資料表資料列集擷取對應的資料列。

針對基底資料表開啟的資料列集上需要資料列集屬性 `DBPROP_IRowsetLocate` 和 `DBPROP_BOOKMARKS`。

### <a name="pure-table-scans"></a>純資料表掃描

SQL Server 會從提供者掃描整個遠端資料表，並在本機執行所有查詢評估。 對應到資料表的資料列集是透過呼叫 `IOpenRowset::OpenRowset` 來開啟。 SQL Server 會從目錄、結構描述和物件名稱部分來建構提供給 `OPENROWSET` 的資料表名稱，如下所示：

1. 每個名稱部分都會以提供者的引號字元 (`DBLITERAL_QUOTE`) 括住，然後在其間內嵌 `DBLITERAL_CATALOG_SEPARATOR` 字元來串連。

1. 開啟資料列集物件之後，SQL Server 會使用 `IColumnsInfo` 介面來確認執行時間中繼資料與資料表的編譯時間中繼資料相同。

1. SQL Server 使用 `IRowset` 介面來巡覽並使用資料表中的資料列。 您可以使用 `IRowset::GetNextRows` 來擷取資料列、使用 `IRowset::RestartPosition` 來重新置放到資料列集的開頭，並使用 `IRowset::ReleaseRows` 來釋放資料列。

### <a name="update-and-delete-statements"></a>`UPDATE` 和 `DELETE` 陳述式

若要從 SQL Server 分散式查詢更新或刪除遠端資料表，必須滿足下列條件：

- 提供者必須支援書籤，才能更新或刪除資料表上透過 `IOpenRowset` 開啟的資料列集。

- 提供者必須在透過 `IRowsetLocate` 開啟的資料列集上支援 `IRowsetChange` 和 `IOpenRowset` 介面，才能更新或刪除資料表。

- `IRowsetChange` 介面必須支援更新 (`SetData`) 和刪除 (`DeleteRows`) 方法。

- 如果提供者不支援 `ITransactionLocal`，則只有在已為該提供者設定 `Non-transacted` 選項且陳述式不在使用者交易中時，才允許 `UPDATE` 和 `DELETE` 陳述式。

- 如果提供者不支援 `ITransactionJoin`，則只有在陳述式不在使用者交易中時，才允許 `UPDATE` 和 `DELETE` 陳述式。

針對已更新資料表開啟的資料列集上需要下列資料列集屬性：`DBPROP_IRowsetLocate`、`DBPROP_IRowsetChange` 和 `DBPROP_BOOKMARKS`。 根據執行的作業是 `UPDATE` 或 `DELETE`，`DBPROP_UPDATABILITY` 資料列集屬性會分別設定為 `DBPROPVAL_UP_CHANGE` 或 `DBPROPVAL_UP_DELETE`。

下列是為了處理 `UPDATE` 或 `DELETE` 作業，對提供者所執行的高階步驟：

1. SQL Server 透過 `IOpenRowset` 介面開啟基底資料表資料列集。 SQL Server 需要資料列集上的上述屬性。

1. SQL Server 決定要更新或刪除的合格資料列集。

1. SQL Server 使用書籤透過 `IRowsetLocate` 介面放置在合格資料列上。

1. 針對 `UPDATE` 作業使用 `IRowsetChange::SetData`，或針對 DELETE 作業使用 `IRowsetChange::DeleteRows`，以在合格資料列上執行所需的變更。

### <a name="insert-statement"></a>`INSERT` 陳述式

支援對遠端資料表使用 `INSERT` 陳述式的條件比 `UPDATE` 和 `DELETE` 陳述式寬鬆：

- 提供者必須在基底資料表上開啟的資料列集上支援 `IRowsetChange::InsertRow`，才能插入資料列集。

- 如果提供者不支援 `ITransactionLocal`，只有在已為該連結伺服器設定 `Non-transacted updates` 選項且陳述式不在使用者交易中時，才允許 `INSERT` 陳述式。

- 如果提供者不支援 `ITransactionJoin`，則只有在陳述式不在使用者交易中時，才允許 `INSERT` 陳述式。

SQL Server 使用 `IOpenRowset::OpenRowset` 在基底資料表上開啟資料列集，並呼叫 `IRowsetChange::InsertRow` 將新的資料列插入基底資料列集。

### <a name="pass-through-queries"></a>傳遞查詢

此案例類似於遠端查詢案例，不同之處在於提供給 `ICommand` 的命令文字是使用者所提交命令字串且無法由 SQL Server 解譯。 當 SQL Server 呼叫 `ICommandText::SetCommandText` 時，會使用 `DBGUID_DEFAULT` 作為方言識別碼。 `DBGUID_DEFAULT` 指出提供者應該使用其預設方言。 如果此命令文字傳回多個結果集 (例如，如果命令叫用傳回多個結果集的預存程序)，則 SQL Server 只會使用命令中的第一個結果集。

如需 SQL Server 使用的所有 OLE DB 介面清單，請參閱 [SQL Server 使用的 OLE DB 介面](#appendixa)。

### <a name="conclusion"></a>結論

Microsoft SQL Server 提供最強大的工具組，可從異質性資料來源存取資料。 藉由了解 SQL Server 所公開的 OLE-DB 介面，開發人員就可以在分散式查詢中進行高度的控制和複雜度。

## <a name="appendixa"></a> SQL Server 使用的 OLE DB 介面

下表列出 SQL Server 使用的所有 OLE DB 介面。 [必要] 欄指出介面是 SQL Server 所需最低 OLE DB 功能的一部分或其為選擇性。 如果指定的介面未標示為必要，則 SQL Server 仍然可以存取提供者，但無法對提供者執行某些特定的 SQL Server 功能或最佳化。

在選擇性介面案例中，[案例] 欄指出使用指定介面的六個案例其中一或多個案例。 例如，基底資料表資料列集上的 `IRowsetChange` 介面是選擇性介面，此介面可用於 `UPDATE` 和 DELETE 陳述式以及 `INSERT` 陳述式案例。 如果不支援此介面，就無法支援對該提供者使用 UPDATE、DELETE 和 `INSERT` 陳述式。 其他一些選擇性介面會在 [案例] 欄中標示為「效能」，表示此介面會產生更好的整體效能。 例如，如果不支援 `IDBSchemaRowset` 介面，則 SQL Server 必須開啟資料列集兩次：一次用於擷取其中繼資料，一次用於查詢執行。 藉由支援 `IDBSchemaRowset`，即可改善 SQL Server 效能。

|Object|介面|必要|註解|案例|
|:-----|:-----|:-----|:-----|:-----|
|Data Source 物件|`IDBInitialize`|是|初始化與設定資料和安全性內容。| |
| |`IDBCreateSession`|是|建立 DB Session 物件。| |
| |`IDBProperties`|是|取得提供者功能的相關資訊、設定初始化屬性，必要屬性：DBPROP_INIT_TIMEOUT。| |
| |`IDBInfo`|否|取得引號常值、目錄、名稱、部分、分隔符號、字元等。|遠端查詢。|
|DB Session 物件|`IDBSchemaRowset`|否|取得資料表/資料行中繼資料。 所需的資料列集：`TABLES`、`COLUMNS`、`PROVIDER_TYPES`；其他使用的資料列集 (如果可用)：`INDEXES`、`TABLE_STATISTICS`。|效能、索引存取。|
| |`IOpenRowset`|是|在資料表、索引或長條圖上開啟資料列集。| |
| |`IGetDataSource`|是|用於從 DB Session 物件回到 DSO。| |
| |`IDBCreateCommand`|否|用於為支援查詢的提供者建立 Command 物件 (查詢)。|遠端查詢、傳遞查詢。|
| |`ITransactionLocal`|否|用於交易更新。|`UPDATE` 和 `DELETE`、`INSERT` 陳述式。|
| |`ITransactionJoin`|否|用於分散式交易支援。|`UPDATE` 和 `DELETE`、`INSERT` 陳述式 (如果在使用者交易中)。|
|Rowset 物件|IRowset|是|掃描資料列。| |
| |`IAccessor`|是|繫結至資料列集的資料行。| |
| |`IColumnsInfo`|是|取得資料列集的資料行相關資訊。| |
| |`IRowsetInfo`|是|取得資料列集屬性的相關資訊。| |
| |`IRowsetLocate`|否|對於 `UPDATE`/`DELETE` 作業及以索引方式執行查閱是必要的；用於依書籤查閱資料列。|索引存取、`UPDATE` 和 `DELETE` 陳述式。|
| |`IRowsetChange`|否|對於在資料列集上執行 `INSERTS`/`UPDATES`/ `DELETES` 是必要的。 針對基底資料表的資料列集應該支援此介面，才能使用 `INSERT`、`UPDATE` 和 `DELETE` 陳述式。|`UPDATE` 和 `DELETE`、`INSERT` 陳述式。|
| |`IConvertType`|是|用於確認資料列集是否支援其資料行的特定資料類型轉換。| |
|索引|`IRowset`|是|掃描資料列。|索引存取、效能。|
| |`IAccessor`|是|繫結至資料列集的資料行。|索引存取、效能。|
| |`IColumnsInfo`|是|取得資料列集的資料行相關資訊。|索引存取、效能。|
| |`IRowsetInfo`|是|取得資料列集屬性的相關資訊。|索引存取、效能。|
| |`IRowsetIndex`|是|對於索引上的資料列集是必要的；用於索引功能 (設定範圍、搜尋)。|索引存取、效能。|
|Command|`ICommand`|是| |遠端查詢、傳遞查詢。|
| |`ICommandText`|是|用於定義查詢文字。|遠端查詢、傳遞查詢。|
| |`IColumnsInfo`|是|用於取得查詢結果的資料行中繼資料。|遠端查詢、傳遞查詢。|
| |`ICommandProperties`|是|用於指定命令所傳回資料列集的必要屬性。|遠端查詢、傳遞查詢。|
| |`ICommandWithParameters`|否|用於將查詢執行參數化。|遠端查詢、效能。|
| |`ICommandPrepare`|否|用於準備命令以取得中繼資料 (如果可用的話，用於傳遞查詢)。|遠端查詢、效能。|
|Error 物件|`IErrorRecords`|是|用於取得對應到單一錯誤記錄的 `IErrorInfo` 介面指標。| |
| |`IErrorInfo`|是|用於取得對應到單一錯誤記錄的 `IErrorInfo` 介面指標。| |
|Any 物件|`ISupportErrorInfo`|否|用於確認指定的介面是否支援錯誤物件。| |
|  |  |  |  |  |

>[!NOTE]
>`Index` 物件、`Command` 物件和 `Error` 物件非為必要。 不過，如果受到支援，則列出的介面會在 [必要] 欄中指定為必要。

## <a name="appendixb"></a>用於產生遠端查詢的 SQL 子集

SQL Server 查詢處理器針對 SQL 命令提供者產生的 SQL 子集，取決於提供者依照 `DBPROP_SQLSUPPORT` 屬性指定支援的語法層級。

支援 SQL 入門層級或 ODBC 核心層級的 SQL 命令提供者

SQL Server 會針對支援 SQL-92 入門層級或 ODBC 核心層級的 SQL 命令提供者所評估查詢，使用下列 SQL 語言子集：

1. `SELECT` 陳述式搭配 `SELECT`、`FROM`、`WHERE`、`GROUP BY`、`UNION`、`UNION ALL`、`ORDER BY DESC`、`ASC` 和 `HAVING` 子句。

1. `UNION` 和 `UNION ALL` 只會針對支援 SQL-92 入門層級的提供者產生，而不會針對支援 ODBC 核心層級的提供者產生。

1. `SELECT` 子句：

   - `SELECT` 清單中的純量子查詢。

   - 不含 `AS` 關鍵字的資料行別名。

1. `FROM` 子句：

   - 不會使用明確聯結關鍵字；使用以逗號分隔的資料表名稱來指定內部聯結，且不會在遠端查詢中指定外部聯結。

   - 表單的巢狀查詢 `FROM` ( `<nested query>` ) `<alias>`。

   - 不含 AS 關鍵字的資料表別名。

1. `WHERE` 子句搭配 `NOT`、`EXISTS`、`ANY`、`ALL` 使用子查詢。

1. 運算式：

   - 使用的彙總函式：`MIN([DISTINCT])`、`MAX([DISTINCT])`、`COUNT([DISTINCT])`、`SUM([DISTINCT])`、`AVG([DISTINCT])` 和 `COUNT(*)`。

   - 比較運算子：`<`、`=`、`<=`、`>`、`<>`、`>=`、`IS NULL` 和 `IS NOT NULL`。

   - 布林運算子：`AND`、`OR` 和 `NOT`。

 - 算術運算子：`+`、`-`、`*` 和 `/`。

1. 常數：

- 數值和貨幣常值一律會以 `( )` 括住。

- 字元常值會以 `' '` 括住。

支援 SQL 最低層級的 SQL 命令提供者

針對支援 SQL 最低層級的 SQL 命令提供者，SQL Server 會使用下列文法來產生 SQL。

此文法是使用 ODBC 3.0 中所述的 SQL 最低層級文法衍生而來。 此文法中的所有差異都會醒目提示。 以 `*bold italics`* 顯示的項目是 ODBC 3.0 中所述 SQL 最低層級文法中新增項目。 以綠色顯示已刪除項目是從此文法中移除的項目。

*select-statement* ::=

`SELECT [ALL | DISTINCT] *select-list* FROM *table-reference-list*[WHERE *search-condition*] [order-by-clause]`

`SELECT` 子句

select-list ::= `*` | `select-sublist [, select-sublist]...`

select-sublist ::= expression * [`alias`]*

`*alias ::= user-defined-name`*

`FROM clause`

table-reference-list ::= table-reference

table-identifier ::= user-defined-name

table-name ::= table-identifier

table-reference ::= table-name

`WHERE clause`

search-condition ::= boolean-term \[OR search-condition\]

boolean-term ::= boolean-factor \[AND boolean-term\]

boolean-factor ::= \[NOT\] boolean-primary

boolean-primary ::= comparison-predicate \| ( search-condition )

comparison-predicate ::= expression comparison-operator expression

*\| `expression IS \[NOT\] NULL`*

comparison-operator ::= `< \| >` \| `<= \| >`= \| = \| `<>`

`ORDER BY clause`

order-by-clause ::= ORDER BY sort-specification \[, sort-specification\]\..

sort-specification ::= { \| column-name } \[ASC \| DESC\]

`Common syntactic elements`

expression ::= term \| expression {+\|--} term

term ::= factor \| term {\*\|/} factor

factor ::= \[+\|--\] primary

primary ::= column-name

\| literal

\| ( expression )

column-name ::= \[table-name.\]column-identifier

literal ::= character-string-literal

*\| integer-literal*

*\| exact-numeric-literal*

character-string-literal ::= \'{character}...\'

(字元為驅動程式/資料來源的字元集中任意字元。 若要在 character-string-literal 中包含單一常值引號字元 (\')，請使用兩個常值引號字元 (\'\')。)

`*integer-literal ::=* \[*+ \| -*\] *unsigned-integer`*

`*exact-numeric-literal::=* \[*+ \| -*\] *unsigned-integer* \[*period unsigned-integer*\]`

`*\| period unsigned-integer`*

base-table-name ::= base-table-identifier

base-table-identifier ::= user-defined-name

column-identifier ::= user-defined-name

user-defined-name ::= letter\[digit \| letter \| _\]\..

unsigned-integer ::= {digit}...

digit ::= 0 \| 1 \| 2 \| 3 \| 4 \| 5 \| 6 \| 7 \| 8 \| 9

period ::= . 

## <a name="appendixc"></a>SQL Server 特定屬性

```
enum SQLPROPERTIES
       {
       SQLPROP_NOHPNEEDED = 0x1,
       SQLPROP_FREETHREADED = 0x2,
       SQLPROP_UMSENABLED = 0x3,
       SQLPROP_NESTEDQUERIES = 0x4,
       SQLPROP_DYNAMICSQL = 0x5,
       SQLPROP_GROUPBY = 0x6,
       SQLPROP_DATELITERALS = 0x7,
       SQLPROP_ANSILIKE = 0x8,
       SQLPROP_INNERJOIN = 0x9,
       SQLPROP_SUBQUERIES = 0x10, 
       SQLPROP_PARALLELSCAN = 0x11,
       SQLPROP_COLUMNCOLLATION = 0x12,
       SQLPROP_CARDINALITY = 0x13,
       SQLPROP_SIMPLEUPDATES = 0x14,
       SQLPROP_SQLLIKE = 0x15,
       SQLPROP_BITREMOTING = 0x16,
       SQLPROP_UNICODELITERALS = 0x17,
       SQLPROP_USELATESTCOLLATIONVERSION = 0x18
       };

```
