---
title: 最短路徑（SQL Graph） |Microsoft Docs
ms.custom: ''
ms.date: 07/01/2020
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: language-reference
f1_keywords:
- SHORTEST PATH
- SHORTEST_PATH
dev_langs:
- TSQL
helpviewer_keywords:
- MATCH statement [SQL Server], SQL graph
- SQL graph, MATCH statement
author: shkale-msft
ms.author: shkale
monikerRange: =azuresqldb-current||>=sql-server-ver15||=sqlallproducts-allversions||=azuresqldb-mi-current
ms.openlocfilehash: 334b4ee83df73284abe7d20cdff66675d42039d5
ms.sourcegitcommit: e6c260a139326f5a400a57ece812d39ef8b820bd
ms.contentlocale: zh-TW
ms.lasthandoff: 07/07/2020
ms.locfileid: "86032560"
---
# <a name="shortest_path-transact-sql"></a>SHORTEST_PATH （Transact-sql）
[!INCLUDE[tsql-appliesto-SQL 19-SQL DB-SQL MI](../../includes/applies-to-version/sqlserver2019-asdb-asdbmi.md)]

  指定以遞迴或重複方式搜尋之圖形的搜尋條件。 在 SELECT 語句中，可以在與圖形節點和邊緣資料表相符的 SHORTEST_PATH 中使用。 
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="shortest-path"></a>最短路徑
SHORTEST_PATH 函數可讓您尋找：    
* 兩個指定節點/實體之間的最短路徑
* 單一來源最短路徑。
* 從多個來源節點到多個目標節點的最短路徑。

它接受任意長度模式做為輸入，並傳回兩個節點之間存在的最短路徑。 此函式只能用在 MATCH 內部。 此函式只會傳回兩個指定節點之間的一個最短路徑。 如果有兩個或多個相同長度的最短路徑在任何一組來源與目的地節點之間存在，此函式只會傳回在遍歷期間第一個找到的路徑。 請注意，任意長度模式只能在 SHORTEST_PATH 函式內指定。 

如需語法，請參閱[MATCH （SQL Graph）](../../t-sql/queries/match-sql-graph.md) 。 

## <a name="for-path"></a>針對 PATH
針對 PATH，必須搭配 FROM 子句中的任何節點或邊緣資料表名稱使用，這將會參與任意長度模式。 針對 [路徑]，告訴引擎節點或邊緣資料表將傳回已排序的集合，代表沿著所遍歷路徑中找到的節點或邊緣的清單。 這些資料表中的屬性無法直接投射在 SELECT 子句中。 若要從這些資料表投影屬性，必須使用圖形路徑彙總函式。  

## <a name="arbitrary-length-pattern"></a>任意長度模式
此模式包含節點和邊緣，必須重複地進行迴圈，直到達到所需的節點，或在符合模式中所指定的反覆運算次數上限為止。 每次執行查詢時，執行此模式的結果會是已排序的節點集合，以及從開始節點到結束節點的路徑所進行的邊緣。 這是正則運算式樣式語法模式，而且支援下列兩種模式數量詞：

* **' + '**：重複模式1或多次。 在找到最短路徑後立即終止。
* **{1，n}**：重複模式1到 ' n ' 次。 一旦找到最短的，就終止。

## <a name="last_node"></a>LAST_NODE
LAST_NODE （）函數可允許兩個任意長度的遍歷模式的連結。 它可以用於下列情況：    
* 查詢中使用一個以上的最短路徑模式，而一個模式從上一個模式的最後一個節點開始。
* 以相同的 LAST_NODE （）合併兩個最短的路徑模式。

## <a name="graph-path-order"></a>圖形路徑順序
圖形路徑順序指的是輸出路徑中的資料順序。 輸出路徑順序一律會在模式的非遞迴部分啟動，後面接著出現在遞迴部分中的節點/邊緣。 在查詢優化/執行期間，圖表的執行順序與輸出中列印的順序無關。 同樣地，遞迴模式中的箭號方向也不會影響圖形路徑順序。 

## <a name="graph-path-aggregate-functions"></a>圖形路徑彙總函式
由於與任意長度模式相關的節點和邊緣會傳回集合（在該路徑中所進行的節點和邊緣），因此使用者無法直接使用傳統的 attributename 語法來投影屬性。 針對需要從中繼節點或邊緣資料表投影屬性值的查詢，在所進行的路徑中，請使用下列圖形路徑彙總函式： STRING_AGG、LAST_VALUE、SUM、AVG、MIN、MAX 和 COUNT。 在 SELECT 子句中使用這些彙總函式的一般語法為：

```syntaxsql
<GRAPH_PATH_AGGREGATE_FUNCTION>(<expression> , <separator>)  <order_clause>

    <order_clause> ::=
        { WITHIN GROUP (GRAPH PATH) }

    <GRAPH_PATH_AGGREGATE_FUNCTION> ::=
          STRING_AGG
        | LAST_VALUE
        | SUM
        | COUNT
        | AVG
        | MIN
        | MAX

```

### <a name="string_agg"></a>STRING_AGG
STRING_AGG 函式會採用運算式和分隔符號做為輸入，並傳回字串。 使用者可以在 SELECT 子句中使用此函式，從所遍歷之路徑中的中繼節點或邊緣投影屬性。 

### <a name="last_value"></a>LAST_VALUE
若要從已進行路徑的最後一個節點來投影屬性，可以使用 LAST_VALUE 彙總函式。 提供邊緣資料表別名做為此函式的輸入是錯誤的，只可以使用節點資料表名稱或別名。

**最後一個節點**：最後一個節點會參考出現在路徑中的最後一個節點，而不考慮 MATCH 述詞中箭號的方向。 例如： `MATCH(SHORTEST_PATH(n(-(e)->p)+) )` 。 在這裡，路徑中的最後一個節點會是最後一次造訪的 P 節點。 

不過，最後一個節點是此模式輸出圖形路徑中的最後 n 個節點：`MATCH(SHORTEST_PATH((n<-(e)-)+p))`    

### <a name="sum"></a>SUM
此函式會傳回所提供節點/邊緣屬性值的總和，或出現在所遍歷路徑中的運算式。

### <a name="count"></a>COUNT
此函式會傳回路徑中所需節點/邊緣屬性的非 null 值數目。 COUNT 函數支援 \* 具有節點或邊緣資料表別名的 ' ' 運算子。 如果沒有節點或邊緣資料表別名，的使用方式 \* 就不明確，而且會導致錯誤。

```syntaxsql
{  COUNT( <expression> | <node_or_edge_alias>.* )  <order_clause>  }
```

### <a name="avg"></a>平均
傳回所提供節點/邊緣屬性值的平均值，或出現在所遍歷路徑中的運算式。

### <a name="min"></a>最小值
從所提供的節點/邊緣屬性值或在已進行的路徑中出現的運算式，傳回最小值。

### <a name="max"></a>最大值
從所提供的節點/邊緣屬性值或在已進行的路徑中出現的運算式，傳回最大值。

## <a name="remarks"></a>備註  
shortest_path 函式只能用在 MATCH 內部。     
只有 shortest_path 內才支援 LAST_NODE。     
若要尋找加權最短路徑，則不支援所有路徑或所有最短路徑。         
在某些情況下，可能會針對具有較高躍點數目的查詢產生不良的計畫，因而產生較高的查詢執行時間。 使用雜湊聯結提示可能會有説明。    


## <a name="examples"></a>範例 
針對此處顯示的範例查詢，我們將使用在[SQL Graph](./sql-graph-sample.md)中建立的節點和邊緣資料表範例

### <a name="a--find-shortest-path-between-2-people"></a>A.  尋找2人之間最短的路徑
 在下列範例中，我們會找到 Jacob 與 Alice 之間的最短路徑。 我們將需要從 graph 範例腳本建立的 Person 節點和 FriendOf edge。 

```sql
SELECT PersonName, Friends
FROM (  
    SELECT
        Person1.name AS PersonName, 
        STRING_AGG(Person2.name, '->') WITHIN GROUP (GRAPH PATH) AS Friends,
        LAST_VALUE(Person2.name) WITHIN GROUP (GRAPH PATH) AS LastNode
    FROM
        Person AS Person1,
        friendOf FOR PATH AS fo,
        Person FOR PATH  AS Person2
    WHERE MATCH(SHORTEST_PATH(Person1(-(fo)->Person2)+))
    AND Person1.name = 'Jacob'
) AS Q
WHERE Q.LastNode = 'Alice'
```

 ### <a name="b--find-shortest-path-from-a-given-node-to-all-other-nodes-in-the-graph"></a>B.  尋找從指定節點到圖形中所有其他節點的最短路徑。 
 下列範例會尋找 Jacob 在圖形中連接的所有人員，以及從 Jacob 開始到所有這些人員的最短路徑。 

```sql
SELECT
    Person1.name AS PersonName, 
    STRING_AGG(Person2.name, '->') WITHIN GROUP (GRAPH PATH) AS Friends
FROM
    Person AS Person1,
    friendOf FOR PATH AS fo,
    Person FOR PATH  AS Person2
WHERE MATCH(SHORTEST_PATH(Person1(-(fo)->Person2)+))
AND Person1.name = 'Jacob'
```

### <a name="c--count-the-number-of-hopslevels-traversed-to-go-from-one-person-to-another-in-the-graph"></a>C.  計算從某個人員到圖形中另一個人所往返的躍點/層級數目。
 下列範例會尋找 Jacob 與 Alice 之間的最短路徑，並列印從 Jacob 到 Alice 所需的躍點數目。 

```sql
 SELECT PersonName, Friends, levels
FROM (  
    SELECT
        Person1.name AS PersonName, 
        STRING_AGG(Person2.name, '->') WITHIN GROUP (GRAPH PATH) AS Friends,
        LAST_VALUE(Person2.name) WITHIN GROUP (GRAPH PATH) AS LastNode,
        COUNT(Person2.name) WITHIN GROUP (GRAPH PATH) AS levels
    FROM
        Person AS Person1,
        friendOf FOR PATH AS fo,
        Person FOR PATH  AS Person2
    WHERE MATCH(SHORTEST_PATH(Person1(-(fo)->Person2)+))
    AND Person1.name = 'Jacob'
) AS Q
WHERE Q.LastNode = 'Alice'
```

### <a name="d-find-people-1-3-hops-away-from-a-given-person"></a>D. 尋找特定人員的1-3 躍點
下列範例會尋找 Jacob 與他在 graph 1-3 躍點中連線的所有人員之間的最短路徑。 

```sql
SELECT
    Person1.name AS PersonName, 
    STRING_AGG(Person2.name, '->') WITHIN GROUP (GRAPH PATH) AS Friends
FROM
    Person AS Person1,
    friendOf FOR PATH AS fo,
    Person FOR PATH  AS Person2
WHERE MATCH(SHORTEST_PATH(Person1(-(fo)->Person2){1,3}))
AND Person1.name = 'Jacob'
```

### <a name="e-find-people-exactly-2-hops-away-from-a-given-person"></a>E. 從特定人員找出剛好2個躍點的使用者
下列範例會尋找 Jacob 之間的最短路徑，以及與他在圖形中剛好2個躍點的人。 

```sql
SELECT PersonName, Friends
FROM (
    SELECT
        Person1.name AS PersonName, 
        STRING_AGG(Person2.name, '->') WITHIN GROUP (GRAPH PATH) AS Friends,
        COUNT(Person2.name) WITHIN GROUP (GRAPH PATH) AS levels
    FROM
        Person AS Person1,
        friendOf FOR PATH AS fo,
        Person FOR PATH  AS Person2
    WHERE MATCH(SHORTEST_PATH(Person1(-(fo)->Person2){1,3}))
    AND Person1.name = 'Jacob'
) Q
WHERE Q.levels = 2
```

## <a name="see-also"></a>另請參閱  
 [MATCH （SQL Graph）](../../t-sql/queries/match-sql-graph.md)    
 [CREATE TABLE &#40;SQL Graph&#41;](../../t-sql/statements/create-table-sql-graph.md)   
 [插入（SQL Graph）](../../t-sql/statements/insert-sql-graph.md)]  
 [SQL Server 2017 的圖表處理](../../relational-databases/graphs/sql-graph-overview.md)     
 
