---
title: SQL Graph 架構 |Microsoft Docs
ms.custom: ''
ms.date: 09/24/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: language-reference
helpviewer_keywords:
- SQL graph
- SQL graph, architecture
ms.assetid: ''
author: shkale-msft
ms.author: shkale
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: ed234a487d5c382400b3a839820a4509c8b880f2
ms.sourcegitcommit: 8bc5d85bd157f9cfd52245d23062d150b76066ef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/07/2019
ms.locfileid: "57579348"
---
# <a name="sql-graph-architecture"></a>SQL Graph 架構  
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

了解 SQL Graph 架構的方式。 了解基本概念會讓您更輕鬆地了解其他 SQL Graph 文件。
 
## <a name="sql-graph-database"></a>SQL 圖形資料庫
使用者可以建立一張圖表，每個資料庫。 圖形是節點和邊緣資料表的集合。 可在資料庫中，任何結構描述下建立節點或邊緣資料表，但它們都屬於一個邏輯的圖表。 節點資料表是類似的節點類型的集合。 比方說，Person 節點資料表保留屬於圖形的所有人員節點。 同樣地，邊緣資料表是邊緣的類似類型的集合。 例如，朋友邊緣資料表會保存將人員連接到另一個人的所有邊緣。 因為節點和邊緣會儲存在資料表中，節點或邊緣資料表才支援大部分的一般資料表上支援的作業。 
 
 
![sql graph 架構](../../relational-databases/graphs/media/sql-graph-architecture.png "Sql 圖形資料庫架構")   

圖 1:SQL Graph 資料庫架構
 
## <a name="node-table"></a>節點資料表
節點資料表代表圖形的結構描述中的實體。 每次節點資料表建立時，使用者定義的資料行，以及隱含`$node_id`建立資料行，可唯一識別資料庫中指定的節點。 中的值`$node_id`會自動產生，而且是組合`object_id`的該節點資料表和內部產生的 bigint 值。 不過，當`$node_id`選取資料行時，會顯示計算的值的 JSON 字串的形式。 此外，`$node_id`是虛擬資料行，對應至十六進位字串中的內部名稱。 當您選取`$node_id`從資料表中，資料行名稱會顯示為`$node_id_<hex_string>`。 在查詢中使用虛擬資料行名稱是建議的方法來查詢內部`$node_id`資料行和使用十六進位字串中的內部名稱應予以避免。

建議使用者建立唯一條件約束或索引上`$node_id`建立當時的節點資料表，但如果尚未建立的資料行，會自動建立唯一、 非叢集索引的預設值。 不過，基礎的內部資料行上建立任何圖表虛擬資料行上的索引。 也就是上建立的索引`$node_id`資料行，會出現在內部`graph_id_<hex_string>`資料行。   


## <a name="edge-table"></a>邊緣資料表
邊緣資料表代表圖形中的關聯性。 邊緣會一律導向，並連接兩個節點。 邊緣資料表可讓使用者模型圖形中的多對多關聯性。 邊緣資料表可能會或可能沒有任何使用者定義的屬性中。 每次建立邊緣資料表時，使用者定義的屬性，以及在邊緣資料表建立三個隱含的資料行：

|資料行名稱    |描述  |
|---   |---  |
|`$edge_id`   |可唯一識別資料庫中的指定的邊緣。 它是產生的資料行和值是 object_id 邊緣資料表和內部產生的 bigint 值的組合。 不過，當`$edge_id`選取資料行時，會顯示計算的值的 JSON 字串的形式。 `$edge_id` 是虛擬資料行對應至十六進位字串中的內部名稱。 當您選取`$edge_id`從資料表中，資料行名稱會顯示為`$edge_id_\<hex_string>`。 在查詢中使用虛擬資料行名稱是建議的方法來查詢內部`$edge_id`資料行和使用十六進位字串中的內部名稱應予以避免。 |
|`$from_id`   |存放區`$node_id`從邊緣的來源位置 節點。  |
|`$to_id`   |存放區`$node_id`處結束邊緣 節點。 |

可以連接指定的邊緣節點中插入的資料受到`$from_id`和`$to_id`資料行。 在第一個版本中，不可以定義邊緣資料表，來限制從連接之節點的任何兩個類型條件約束。 也就是說，邊緣可以連接兩個節點在圖形中，不論其類型。

類似於`$node_id`資料行中，我們建議使用者上，建立唯一索引或條件約束`$edge_id`建立當時的邊緣資料表，但如果尚未建立的資料行，唯一的非叢集索引自動建立預設值此資料行。 不過，基礎的內部資料行上建立任何圖表虛擬資料行上的索引。 也就是上建立的索引`$edge_id`資料行，會出現在內部`graph_id_<hex_string>`資料行。 也建議，OLTP 案例中，使用者在建立索引 (`$from_id`， `$to_id`) 資料行、 查閱更快邊緣的方向。  

[圖 2] 顯示節點和邊緣資料表儲存在資料庫中的方式。 

![人員朋友表格](../../relational-databases/graphs/media/person-friends-tables.png "/people/person 節點和 friend 邊緣資料表")   

圖 2:節點和邊緣資料表表示法



## <a name="metadata"></a>中繼資料
您可以使用這些中繼資料檢視來查看節點或邊緣資料表的屬性。
 
### <a name="systables"></a>sys.tables
下列新功能、 位元的類型，系統將會加入資料行。資料表。 如果`is_node`設為 1，表示資料表是節點資料表時，才`is_edge`設為 1，表示資料表是邊緣資料表。
 
|資料行名稱 |資料類型 |描述 |
|--- |---|--- |
|is_node |bit |1 = 這是節點資料表 |
|is_edge |bit |1 = 這是邊緣資料表 |
 
### <a name="syscolumns"></a>sys.columns
`sys.columns`檢視包含額外的資料行`graph_type`和`graph_type_desc`，，表示節點和邊緣資料表中的資料行類型。
 
|資料行名稱 |資料類型 |描述 |
|--- |---|--- |
|graph_type |ssNoversion |具有一組值的內部資料行。 值是介於 1-8 圖形資料行和其他項目都是 NULL。  |
|graph_type_desc |nvarchar(60)  |具有一組值的內部資料行 |
 
下表列出有效的值，如`graph_type`資料行

|資料行值  |描述  |
|---   |---   |
|1  |GRAPH_ID  |
|2  |GRAPH_ID_COMPUTED  |
|3  |GRAPH_FROM_ID  |
|4  |GRAPH_FROM_OBJ_ID  |
|5  |GRAPH_FROM_ID_COMPUTED  |
|6  |GRAPH_TO_ID  |
|7  |GRAPH_TO_OBJ_ID  |
|8  |GRAPH_TO_ID_COMPUTED  |


`sys.columns` 也會儲存在節點或邊緣資料表中建立的隱含資料行的相關資訊。 下列資訊可從擷取 sys.columns，不過，使用者就無法選取這些資料行從節點或邊緣資料表。 

節點資料表中的隱含資料行

|資料行名稱    |資料類型  |is_hidden  |註解  |
|---  |---|---|---  |
|graph_id_\<hex_string> |bigint |1  |內部`graph_id`資料行  |
|$node_id_\<hex_string> |NVARCHAR   |0  |外部節點`node_id`資料行  |

邊緣資料表中的隱含資料行

|資料行名稱    |資料類型  |is_hidden  |註解  |
|---  |---|---|---  |
|graph_id_\<hex_string> |bigint |1  |內部`graph_id`資料行  |
|$edge_id_\<hex_string> |NVARCHAR   |0  |外部`edge_id`資料行  |
|from_obj_id_\<hex_string>  |INT    |1  |從節點內部 `object_id`  |
|from_id_\<hex_string>  |bigint |1  |從節點內部 `graph_id`  |
|$from_id_\<hex_string> |NVARCHAR   |0  |從節點的外部 `node_id`  |
|to_obj_id_\<hex_string>    |INT    |1  |內部節點 `object_id`  |
|to_id_\<hex_string>    |bigint |1  |內部節點 `graph_id`  |
|$to_id_\<hex_string>   |NVARCHAR   |0  |外部的節點 `node_id`  |
 
### <a name="system-functions"></a>系統函數
加入下列的內建函式。 這些功能會協助使用者產生的資料行中擷取資訊。 請注意，這些方法將不會驗證使用者的輸入。 如果使用者指定了無效`sys.node_id`方法會擷取適當的組件，並將它傳回。 比方說，需要 OBJECT_ID_FROM_NODE_ID`$node_id`做為輸入，並將傳回 object_id 這個節點所屬的資料表。 
 
|內建   |描述  |
|---  |---  |
|OBJECT_ID_FROM_NODE_ID |擷取從 object_id `node_id`  |
|GRAPH_ID_FROM_NODE_ID  |擷取從 graph_id `node_id`  |
|NODE_ID_FROM_PARTS |建構來自 node_id`object_id`和 `graph_id`  |
|OBJECT_ID_FROM_EDGE_ID |擷取`object_id`從 `edge_id`  |
|GRAPH_ID_FROM_EDGE_ID  |擷取從身分識別 `edge_id`  |
|EDGE_ID_FROM_PARTS |建構`edge_id`從`object_id`和身分識別  |



## <a name="transact-sql-reference"></a>Transact-SQL 參考 
了解[!INCLUDE[tsql-md](../../includes/tsql-md.md)]導入 SQL Server 和 Azure SQL Database 中的擴充功能，可讓建立和查詢圖表物件。 查詢語言擴充功能會協助查詢和周遊圖形，使用 ASCII 作品語法。
 
### <a name="data-definition-language-ddl-statements"></a>資料定義語言 (DDL) 陳述式

|工作   |相關的文章  |注意
|---  |---  |---  |
|CREATE TABLE |[CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-sql-graph.md)|`CREATE TABLE` 現在已擴充到支援建立 AS 節點或 AS 邊緣資料表。 請注意，邊緣資料表可能會或可能沒有任何使用者定義的屬性。  |
|ALTER TABLE    |[ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)|節點和邊緣資料表可以改變關聯式資料表，使用的相同方式`ALTER TABLE`。 使用者可以新增或修改使用者定義資料行、 索引或條件約束。 不過，改變內部圖形資料行，例如`$node_id`或`$edge_id`，將會產生錯誤。  |
|CREATE INDEX   |[CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)  |使用者可以在虛擬資料行和節點和邊緣資料表中的 使用者定義資料行上建立索引。 支援所有的索引類型，包括叢集和非叢集資料行存放區索引。  |
|建立邊緣條件約束    |[EDGE CONSTRAINTS &#40;Transact-SQL&#41;](../../relational-databases/tables/graph-edge-constraints.md)  |使用者可以現在建立邊緣條件約束，強制執行特定的語意的 edge 資料表上，同時又維持資料完整性  |
|DROP TABLE |[DROP TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-table-transact-sql.md)  |節點和邊緣資料表卸除相同的方式，使用關聯式資料表`DROP TABLE`。 不過，在此版本中，有任何條件約束，以確保沒有邊緣指向已刪除的節點，並不支援的邊緣節點或節點資料表的刪除時的串聯的刪除。 我們建議如果除節點資料表時，使用者會捨棄任何連接到該節點資料表，以手動方式來維護圖形的完整性中節點的邊緣。  |


### <a name="data-manipulation-language-dml-statements"></a>資料操作語言 (DML) 陳述式

|工作   |相關的文章  |注意
|---  |---  |---  |
|Insert |[INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-sql-graph.md)|插入節點資料表並無不同於關聯式資料表中插入就行了。 值`$node_id`自動產生資料行。 嘗試插入的值`$node_id`或`$edge_id`欄將會導致錯誤。 使用者必須提供值`$from_id`和`$to_id`插入至邊緣資料表時的資料行。 `$from_id` 並`$to_id`是`$node_id`指定的邊緣相連接節點的值。  |
|DELETE | [DELETE &#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)|從節點或邊緣資料表的資料可以刪除相同的方式，因為它會從關聯式資料表中刪除。 不過，在此版本中，有任何條件約束，以確保沒有邊緣指向已刪除的節點，並不支援的邊緣節點的刪除時的串聯的刪除。 建議是，每當刪除節點時，該節點的所有連接邊緣也會一併刪除，以維持圖表的完整性。  |
|UPDATE |[UPDATE &#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md)  |可以使用 UPDATE 陳述式來更新使用者定義的資料行中的值。 更新內部圖形資料行`$node_id`， `$edge_id`，`$from_id`和`$to_id`不允許。  |
|MERGE |[MERGE &#40;Transact-SQL&#41;](../../t-sql/statements/merge-transact-sql.md)  |`MERGE` 將節點或邊緣資料表支援陳述式。  |


### <a name="query-statements"></a>查詢陳述式

|工作   |相關的文章  |注意
|---  |---  |---  |
|SELECT |[SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)|節點和邊緣資料表為內部儲存，因此節點和邊緣資料表才支援大部分的 SQL Server 或 Azure SQL Database 中的資料表上支援的作業  |
|MATCH  | [MATCH &#40;Transact-SQL&#41;](../../t-sql/queries/match-sql-graph.md)|相符項目內建引進以支援模式比對和周遊圖形。  |



## <a name="limitations-and-known-issues"></a>限制與已知問題  
有某些限制，在此版本中的節點和邊緣資料表上：
* 本機或全域暫存資料表不可為節點或邊緣資料表。
* 資料表類型和資料表變數不可以宣告為節點或邊緣資料表。 
* 無法建立節點和邊緣資料表，為系統版本設定時態表。   
* 節點和邊緣資料表不可為記憶體最佳化資料表。  
* 無法更新使用者`$from_id`和`$to_id`鎏靮箵使用 UPDATE 陳述式的資料行。 若要更新以邊緣相連接的節點，使用者必須插入指向新節點的新邊緣和刪除前一個。
* 跨資料庫查詢圖形物件上的不支援。 


## <a name="next-steps"></a>後續步驟
若要開始使用新的語法，請參閱[SQL 圖形資料庫範例](./sql-graph-sample.md)
 

