---
title: SQL Graph 架構 |Microsoft 文件
ms.custom: ''
ms.date: 04/19/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: graphs
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- SQL graph
- SQL graph, architecture
ms.assetid: ''
caps.latest.revision: 1
author: shkale-msft
ms.author: shkale
manager: craigg
ms.workload: On Demand
monikerRange: = azuresqldb-current || >= sql-server-2017 || = sqlallproducts-allversions
ms.openlocfilehash: 40a1cf05c5c17be3c11d25cd5e8792eb504c2fa4
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="sql-graph-architecture"></a>SQL Graph 架構  
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

了解如何 SQL 圖形的架構。 了解基本概念，將會進行更易於了解其他 SQL 圖形文件。
 
## <a name="sql-graph-database"></a>圖形的 SQL 資料庫
使用者可以建立一張圖表，每個資料庫。 圖形是節點和邊緣資料表的集合。 在資料庫中，任何結構描述下建立節點或邊緣資料表，但它們都屬於一個邏輯圖表。 節點資料表是類似的節點類型的集合。 例如，人員節點資料表保存屬於圖形的所有人員節點。 同樣地，邊緣資料表是邊緣的類似類型的集合。 例如，朋友邊緣資料表保留給其他人連線使用者的所有邊緣。 因為節點和邊緣儲存在資料表中，節點或邊緣資料表才支援大部分的一般資料表上支援的作業。 
 
 
![sql graph 架構](../../relational-databases/graphs/media/sql-graph-architecture.png "Sql 圖形 database 架構")   

圖 1: SQL 圖形 database 架構
 
## <a name="node-table"></a>節點資料表
節點資料表代表圖形結構描述中的實體。 每次節點建立的資料表，以及使用者定義資料行的隱含`$node_id`建立資料行，唯一識別資料庫中指定的節點。 中的值`$node_id`所自動產生，而且組合`object_id`該節點的資料表和內部產生的 bigint 值。 不過，當`$node_id`選取資料行時，會顯示計算的值的 JSON 字串形式。 此外，`$node_id`是虛擬資料行，對應至具有十六進位字串中的內部名稱。 當您選取`$node_id`從資料表中，資料行名稱會顯示為`$node_id_<hex_string>`。 在查詢中使用虛擬資料行名稱是建議的方法來查詢內部`$node_id`資料行和使用十六進位字串的內部名稱應予以避免。

建議使用者建立唯一條件約束或索引上`$node_id`建立節點的資料表，但如果沒有建立當時的資料行，唯一的非叢集索引會自動建立預設值。 不過，基礎的內部資料行上建立圖形虛擬資料行上的任何索引。 也就是上建立的索引`$node_id`資料行，將會出現在內部`graph_id_<hex_string>`資料行。   


## <a name="edge-table"></a>邊緣資料表
邊緣資料表代表圖形中的關聯性。 邊緣一律導向，並連接兩個節點。 邊緣資料表可讓使用者模型圖形中的多對多關聯性。 邊緣資料表可能會或可能沒有任何使用者定義屬性中。 每次建立邊緣資料表，以及使用者定義屬性中，邊緣資料表中建立三個隱含的資料行：

|資料行名稱    |Description  |
|---   |---  |
|`$edge_id`   |可唯一識別資料庫中的指定的邊緣。 它是產生的資料行，而且值是 object_id 邊緣資料表和內部產生的 bigint 值的組合。 不過，當`$edge_id`選取資料行時，會顯示計算的值的 JSON 字串形式。 `$edge_id` 是虛擬資料行對應至具有十六進位字串中的內部名稱。 當您選取`$edge_id`從資料表中，資料行名稱會顯示為`$edge_id_\<hex_string>`。 在查詢中使用虛擬資料行名稱是建議的方法來查詢內部`$edge_id`資料行和使用十六進位字串的內部名稱應予以避免。 |
|`$from_id`   |存放區`$node_id`的節點、 產生邊緣的位置。  |
|`$to_id`   |存放區`$node_id`的節點，並在其中邊緣會終止。 |

指定的邊緣可連接的節點由插入的資料`$from_id`和`$to_id`資料行。 在第一個版本中，不可以定義邊緣資料表，來限制從連接之節點的任何兩個類型條件約束。 也就是說，邊緣可以連接兩個節點在圖形中，不論它們的型別。

類似於`$node_id`資料行中，我們建議使用者上，建立唯一索引或條件約束`$edge_id`建立在邊緣資料表，但如果尚未建立時的資料行，預設值自動建立唯一、 非叢集索引此資料行。 不過，基礎的內部資料行上建立圖形虛擬資料行上的任何索引。 也就是上建立的索引`$edge_id`資料行，將會出現在內部`graph_id_<hex_string>`資料行。 也建議，針對使用者在建立索引的 OLTP 案例 (`$from_id`， `$to_id`) 的邊緣方向更快的查閱資料行。  

圖 2 顯示節點和邊緣資料表儲存在資料庫中的方式。 

![人員的朋友資料表](../../relational-databases/graphs/media/person-friends-tables.png "/people/person 節點與朋友邊緣資料表")   

圖 2： 節點與邊緣資料表表示法



## <a name="metadata"></a>中繼資料
您可以使用這些中繼資料檢視，查看節點或邊緣資料表的屬性。
 
### <a name="systables"></a>sys.tables
下列新的、 位元的類型，系統將會加入資料行。資料表。 如果`is_node`設為 1，表示資料表為節點資料表，而且如果`is_edge`設為 1，指出資料表是否使用邊緣資料表。
 
|資料行名稱 |資料類型 |Description |
|--- |---|--- |
|is_node |bit |1 = 這是節點的資料表 |
|is_edge |bit |1 = 這是使用邊緣資料表 |
 
### <a name="syscolumns"></a>sys.columns
`sys.columns`檢視包含其他資料行`graph_type`和`graph_type_desc`，表示節點和邊緣資料表中資料行的類型。
 
|資料行名稱 |資料類型 |Description |
|--- |---|--- |
|graph_type |int |有一組值的內部資料行。 值是介於 1-8 圖形資料行和其他項目為 NULL。  |
|graph_type_desc |nvarchar(60)  |有一組值的內部資料行 |
 
下表列出的有效值`graph_type`資料行

|資料行值  |Description  |
|---   |---   |
|1  |GRAPH_ID  |
|2  |GRAPH_ID_COMPUTED  |
|3  |GRAPH_FROM_ID  |
|4  |GRAPH_FROM_OBJ_ID  |
|5  |GRAPH_FROM_ID_COMPUTED  |
|6  |GRAPH_TO_ID  |
|7  |GRAPH_TO_OBJ_ID  |
|8  |GRAPH_TO_ID_COMPUTED  |


`sys.columns` 也會儲存在節點或邊緣資料表中建立的隱含資料行的相關資訊。 下列資訊可從擷取的 sys.columns，不過，使用者就無法選取這些資料行從節點或邊緣資料表。 

隱含節點資料表中的資料行  
|資料行名稱    |資料類型  |is_hidden  |註解  |
|---  |---|---|---  |
|graph_id_\<hex_string> |bigint |1  |內部 graph_id 資料行  |
|$node_id_\<hex_string> |NVARCHAR   |0  |外部的節點識別碼資料行  |

邊緣資料表中的隱含資料行  
|資料行名稱    |資料類型  |is_hidden  |註解  |
|---  |---|---|---  |
|graph_id_\<hex_string> |bigint |1  |內部 graph_id 資料行  |
|$edge_id_\<hex_string> |NVARCHAR   |0  |外部端 id 資料行  |
|from_obj_id_\<hex_string>  |INT    |1  |內部從節點物件識別碼  |
|from_id_\<hex_string>  |bigint |1  |從節點 graph_id 內部  |
|$from_id_\<hex_string> |NVARCHAR   |0  |節點識別碼從外部  |
|to_obj_id_\<hex_string>    |INT    |1  |內部節點物件識別碼  |
|to_id_\<hex_string>    |bigint |1  |內部節點 graph_id  |
|$to_id_\<hex_string>   |NVARCHAR   |0  |節點識別碼的外部  |
 
### <a name="system-functions"></a>系統函數
會加入下列的內建函數。 這些快速鍵可協助使用者從產生的資料行中擷取資訊。 請注意，這些方法將不會驗證使用者的輸入。 如果使用者指定了無效`sys.node_id`方法會擷取適當的組件，並將它傳回。 需要 OBJECT_ID_FROM_NODE_ID，例如`$node_id`做為輸入，並將傳回 object_id 這個節點所屬的資料表。 
 
|內建   |Description  |
|---  |---  |
|OBJECT_ID_FROM_NODE_ID |Object_id 擷取 node_id  |
|GRAPH_ID_FROM_NODE_ID  |Graph_id 擷取 node_id  |
|NODE_ID_FROM_PARTS |建構來自 object_id 和 graph_id node_id  |
|OBJECT_ID_FROM_EDGE_ID |擷取 edge_id object_id  |
|GRAPH_ID_FROM_EDGE_ID  |從 edge_id 擷取身分識別  |
|EDGE_ID_FROM_PARTS |建構 edge_id object_id 與身分識別  |



## <a name="transact-sql-reference"></a>TRANSACT-SQL 參考 
深入了解[!INCLUDE[tsql-md](../../includes/tsql-md.md)]導入了 SQL Server 和 Azure SQL Database 中的擴充功能，可讓建立和查詢圖表物件。 查詢語言擴充功能協助查詢，以及周遊使用 ASCII 封面語法圖表。
 
### <a name="data-definition-language-ddl-statements"></a>資料定義語言 (DDL) 陳述式
|工作   |相關主題  |注意
|---  |---  |---  |
|CREATE TABLE |[CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-sql-graph.md)|`CREATE TABLE ` 現在已延伸到支援建立 AS 節點或 AS 邊緣資料表。 請注意，邊緣資料表可能會或可能沒有任何使用者定義屬性。  |
|ALTER TABLE    |[ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)|節點與邊緣資料表可以更改關聯式資料表，使用的相同方式`ALTER TABLE`。 使用者可以新增或修改使用者定義資料行、 索引或條件約束。 不過，改變內部的圖表資料行，例如`$node_id`或`$edge_id`，將會產生錯誤。  |
|CREATE INDEX   |[CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)  |使用者可以在虛擬資料行和節點與邊緣資料表中的使用者定義資料行上建立索引。 支援所有的索引類型，包括叢集和非叢集資料行存放區索引。  |
|DROP TABLE |[卸除資料表&#40;Transact SQL&#41;](../../t-sql/statements/drop-table-transact-sql.md)  |節點與邊緣資料表可以卸除相同的方式，使用關聯式資料表`DROP TABLE`。 不過，在此版本中，有任何條件約束，以確保沒有邊緣指向已刪除的節點，並不支援重疊的邊緣、 刪除節點或節點資料表時刪除。 建議您，如果節點卸除資料表，使用者會中斷任何邊緣連接到該節點資料表中手動維護完整性圖形的節點。  |


### <a name="data-manipulation-language-dml-statements"></a>資料操作語言 (DML) 陳述式
|工作   |相關主題  |注意
|---  |---  |---  |
|INSERT |[INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-sql-graph.md)|插入節點的資料表並無不同關聯式資料表中插入。 值`$node_id`自動產生資料行。 嘗試插入的值`$node_id`或`$edge_id`欄將會產生錯誤。 使用者必須提供值`$from_id`和`$to_id`時邊緣資料表中插入的資料行。 `$from_id` 和`$to_id`是`$node_id`給定邊緣相連接節點的值。  |
|DELETE | [DELETE &#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)|來自關聯式資料表刪除之後，可以刪除節點或邊緣資料表中的資料相同的方式。 不過，在此版本中，有任何條件約束，以確保沒有邊緣指向已刪除的節點，並不支援重疊的邊緣、 刪除節點的後刪除。 建議，每當刪除節點，所有連接到該節點邊緣也會一併刪除為了維持圖表的完整性。  |
|UPDATE |[UPDATE &#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md)  |可以使用 UPDATE 陳述式來更新使用者定義資料行中的值。 更新內部的圖表資料行`$node_id`， `$edge_id`，`$from_id`和`$to_id`不允許。  |
|MERGE |[MERGE &#40;Transact-SQL&#41;](../../t-sql/statements/merge-transact-sql.md)  |`MERGE` 在節點或邊緣資料表不支援陳述式。  |


### <a name="query-statements"></a>查詢陳述式
|工作   |相關主題  |注意
|---  |---  |---  |
|SELECT |[SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)|節點和邊緣會儲存為資料表在內部，因此節點與邊緣資料表才支援大部分的 SQL Server 或 Azure SQL Database 的資料表上支援的作業  |
|MATCH  | [比對&#40;Transact SQL&#41;](../../t-sql/queries/match-sql-graph.md)|相符項目內建引進以支援模式比對和周遊圖表。  |



## <a name="limitations-and-known-issues"></a>限制與已知的問題  
有此版本中的節點和邊緣資料表的某些限制：
* 本機或全域暫存資料表不能節點或邊緣資料表。
* 資料表類型和資料表變數不能宣告為節點或邊緣資料表。 
* 無法建立節點和邊緣資料表為系統版本設定時態表。   
* 節點與邊緣資料表不可為記憶體最佳化的資料表。  
* 使用者無法更新 $from_id 和 $to_id 資料行的邊緣使用 UPDATE 陳述式。 若要更新的節點會以邊緣相連接，使用者必須插入新的 edge 指向新的節點，並刪除前一個。
* 跨資料庫圖表物件上的查詢不支援。 


## <a name="next-steps"></a>後續步驟
若要開始使用新語法，請參閱[SQL 圖形資料庫範例](./sql-graph-sample.md)
 

