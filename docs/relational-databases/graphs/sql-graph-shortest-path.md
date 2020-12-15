---
description: 'SHORTEST_PATH (Transact-sql) '
title: SQL Graph) 的最短路徑 (|Microsoft Docs
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
monikerRange: =azuresqldb-current||>=sql-server-ver15||=azuresqldb-mi-current
ms.openlocfilehash: c916466f6a105a2b10508e23f1739bba0d192970
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97480179"
---
# <a name="shortest_path-transact-sql"></a>SHORTEST_PATH (Transact-sql) 
[!INCLUDE[tsql-appliesto-SQL 19-SQL DB-SQL MI](../../includes/applies-to-version/sqlserver2019-asdb-asdbmi.md)]

  指定以遞迴或重複方式搜尋的圖表搜尋條件。 SHORTEST_PATH 可以用在 SELECT 語句中，與圖形節點和邊緣資料表相符。 
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="shortest-path"></a>最短路徑
SHORTEST_PATH 函數可讓您尋找：    
* 兩個指定節點/實體之間的最短路徑
* 單一來源最短路徑 (s) 。
* 從多個來源節點到多個目標節點的最短路徑。

它接受任意長度的模式作為輸入，並傳回存在於兩個節點之間的最短路徑。 這個函式只能用在 MATCH 內。 函數只會傳回兩個指定節點之間的一個最短路徑。 如果有兩個或多個相同長度的最短路徑在) 的任何一組來源和目的地 (節點之間存在，則此函式只會傳回在遍歷期間最先找到的一個路徑。 請注意，您只能在 SHORTEST_PATH 函數中指定任意長度的模式。 

如需語法，請參閱 [MATCH (SQL Graph) ](../../t-sql/queries/match-sql-graph.md) 。 

## <a name="for-path"></a>針對路徑
FOR PATH 必須與 FROM 子句中的任何節點或邊緣資料表名稱一起使用，這將會參與任意長度的模式。 針對 PATH，會告知引擎節點或邊緣資料表將會傳回已排序的集合，該集合代表沿著路徑所找到的節點或邊緣清單。 這些資料表中的屬性不能直接投射在 SELECT 子句中。 若要投影這些資料表中的屬性，必須使用圖形路徑彙總函式。  

## <a name="arbitrary-length-pattern"></a>任意長度模式
這種模式包括必須重複進行的節點和邊緣，直到到達所需的節點，或直到符合模式指定的最大反覆運算數目為止。 每次執行查詢時，執行這個模式的結果將會是節點的已排序集合，以及從開始節點到結束節點的路徑。 這是正則運算式樣式語法模式，並支援下列兩個模式數量詞：

* **' + '**：重複模式1次或多次。 在找到最短路徑後立即終止。
* **{1,n}** ：重複模式 1 至 'n' 次。 一旦找到最短，就會終止。

## <a name="last_node"></a>LAST_NODE
LAST_NODE ( # A1 函數可讓兩個任意長度的遍歷模式連結。 它可以用於下列情況：    
* 在查詢中使用一個以上的最短路徑模式，而一個模式從上一個模式的最後一個節點開始。
* 兩個最短路徑模式會合並在相同的 LAST_NODE ( # A1。

## <a name="graph-path-order"></a>圖形路徑順序
圖形路徑順序指的是輸出路徑中的資料順序。 輸出路徑順序一律會從模式的非遞迴部分開始，後面接著遞迴部分中出現的節點/邊緣。 在查詢優化/執行期間，圖形的往返順序與輸出中列印的順序無關。 同樣地，遞迴模式中的箭號方向也不會影響圖形路徑順序。 

## <a name="graph-path-aggregate-functions"></a>圖形路徑彙總函式
由於與任意長度模式相關的節點和邊緣會傳回 (節點 () s 的集合，而) 在該路徑) 中 (，所以使用者無法直接使用傳統的 attributename 語法來投影屬性。 針對需要從中繼節點或邊緣資料表投射屬性值的查詢，在經過的路徑中，請使用下列圖形路徑彙總函式： STRING_AGG、LAST_VALUE、SUM、AVG、MIN、MAX 和 COUNT。 在 SELECT 子句中使用這些彙總函式的一般語法如下：

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
STRING_AGG 函式會採用運算式和分隔符號做為輸入，並傳回字串。 使用者可以在 SELECT 子句中使用這個函數，從中繼節點或所進行的路徑中的邊緣投射屬性。 

### <a name="last_value"></a>LAST_VALUE
若要從路徑的最後一個節點投射屬性，可以使用 LAST_VALUE 彙總函式。 提供 edge 資料表別名做為此函數的輸入是錯誤的，只能使用節點資料表名稱或別名。

**最後一個節點**：最後一個節點指的是在路徑中最後出現的節點，不論 MATCH 述詞中的箭號方向如何。 例如： `MATCH(SHORTEST_PATH(n(-(e)->p)+) )` 。 在此，路徑中的最後一個節點將會是最後一個造訪的 P 節點。 

但是，最後一個節點是此模式之輸出圖形路徑中的最後 n 個節點： `MATCH(SHORTEST_PATH((n<-(e)-)+p))`    

### <a name="sum"></a>SUM
此函式會傳回所提供之節點/邊緣屬性值的總和，或出現在已進行路徑中的運算式。

### <a name="count"></a>COUNT
此函數會傳回路徑中所需節點/邊緣屬性的非 null 值數目。 COUNT 函數支援 \* 具有 node 或 edge 資料表別名的 ' ' 運算子。 如果沒有 node 或 edge 資料表別名，的使用方式 \* 就不明確，而且會產生錯誤。

```syntaxsql
{  COUNT( <expression> | <node_or_edge_alias>.* )  <order_clause>  }
```

### <a name="avg"></a>平均
傳回所提供之節點/邊緣屬性值的平均值，或出現在已被遍歷路徑中的運算式。

### <a name="min"></a>最小值
從提供的節點/邊緣屬性值或出現在已進行路徑中的運算式傳回最小值。

### <a name="max"></a>最大值
從提供的節點/邊緣屬性值或出現在已進行路徑中的運算式傳回最大值。

## <a name="remarks"></a>備註  
shortest_path 函式只能用在相符的內部。     
LAST_NODE 僅在 shortest_path 內支援。     
尋找加權的最短路徑，不支援所有路徑或所有最短路徑。         
在某些情況下，可能會針對具有較高躍點數目的查詢產生不良的計畫，因而產生較高的查詢執行時間。 使用雜湊聯結提示可能會有所説明。    


## <a name="examples"></a>範例 
在這裡顯示的範例查詢中，我們會使用在[SQL Graph](./sql-graph-sample.md)中建立的節點和邊緣資料表範例

### <a name="a--find-shortest-path-between-2-people"></a>A.  尋找2個人之間的最短路徑
 在下列範例中，我們會尋找 Jacob 與 Alice 之間的最短路徑。 我們將需要從圖形範例腳本建立的 Person 節點和 FriendOf edge。 

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

 ### <a name="b--find-shortest-path-from-a-given-node-to-all-other-nodes-in-the-graph"></a>B.  從指定的節點尋找圖形中所有其他節點的最短路徑。 
 下列範例會尋找在圖形中 Jacob 連接的所有人員，以及從 Jacob 開始到所有人員的最短路徑。 

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

### <a name="c--count-the-number-of-hopslevels-traversed-to-go-from-one-person-to-another-in-the-graph"></a>C.  計算在圖形中移至另一個人的躍點/層級數目。
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

### <a name="d-find-people-1-3-hops-away-from-a-given-person"></a>D. 從指定的人員尋找人員1-3 的躍點
下列範例會尋找 Jacob 之間的最短路徑，以及他在圖形1-3 躍點與他之間連接的所有人員之間的最短路徑。 

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

### <a name="e-find-people-exactly-2-hops-away-from-a-given-person"></a>E. 從指定的人員確切找出2個躍點
下列範例會尋找 Jacob 之間的最短路徑，以及在圖形中剛好等於2個躍點的人員之間的最短路徑。 

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
 [ (SQL Graph) 相符 ](../../t-sql/queries/match-sql-graph.md)    
 [CREATE TABLE &#40;SQL Graph&#41;](../../t-sql/statements/create-table-sql-graph.md)   
 [INSERT (SQL Graph)](../../t-sql/statements/insert-sql-graph.md)]  
 [SQL Server 2017 的圖表處理](../../relational-databases/graphs/sql-graph-overview.md)     
 
