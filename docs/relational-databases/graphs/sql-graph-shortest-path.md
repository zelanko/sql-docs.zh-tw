---
title: 最短的路徑 (SQL Graph) |Microsoft Docs
ms.custom: ''
ms.date: 06/26/2019
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
manager: craigg
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: ef8f38acbf621a9c73a0d85bca579c8b7c87aa13
ms.sourcegitcommit: 9d3ece500fa0e4a9f4fefc88df4af1db9431c619
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/28/2019
ms.locfileid: "67463547"
---
# <a name="shortestpath-transact-sql"></a>SHORTEST_PATH (Transact-SQL)
[!INCLUDE[tsql-appliesto-ssver2015-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

  指定搜尋條件圖形，也就是搜尋以遞迴方式或重複。 SHORTEST_PATH 可用在 MATCH 內使用 SELECT 陳述式中圖形節點和邊緣資料表。 
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="shortest-path"></a>最短的路徑
SHORTEST_PATH 函式可讓您尋找：    
* 兩個指定的節點/實體之間的最短路徑
* 單一來源的最短路徑。
* 最短到多個目標節點從多個來源節點路徑。

它會使用任意長度的模式，做為輸入，並傳回兩個節點之間的最短的路徑存在。 此函式僅適用於在 MATCH 內。 此函數會傳回任何兩個指定的節點之間只能有一個最短的路徑。 如果有，兩個或多個長度相同的來源和目的地節點，函式傳回只有一個路徑找到第一個周遊期間的任何一對之間的最短路徑。 請注意，使用任意長度的模式，只能指定在 SHORTEST_PATH 函式。 

請參閱[比對 (SQL Graph)](../../t-sql/queries/match-sql-graph.md)語法。 

## <a name="for-path"></a>路徑
路徑必須使用具有在 FROM 子句中，使用任意長度的模式，將會參與任何節點或邊緣資料表名稱。 路徑會告訴引擎節點或邊緣資料表將會傳回已排序的集合，表示節點或邊緣周遊的路徑中找到的清單。 從這些資料表的屬性不能直接在 SELECT 子句中投射。 專案屬性，這些資料表中的，圖形路徑彙總函式必須使用。  

## <a name="arbitrary-length-pattern"></a>任意長度的模式
此模式包含節點和邊緣，直到達到所需的節點，或直到此模式中所指定的反覆項目數上限必須重複周遊成立。 執行查詢時，每次執行此模式的結果會在節點與邊緣周遊的路徑從 [開始] 節點以結束節點的已排序的集合。 這是規則運算式樣式語法模式，並支援下列兩個模式數量詞：

* **‘+’** :重複的模式 1 或更多的時間。 終止只要找到最短的路徑。
* **{1，n}** :重複的 'n' 個的模式 1 次。 終止只要找到最短。

## <a name="lastnode"></a>LAST_NODE
LAST_NODE() 函式允許鏈結兩個任意長度的周遊模式。 用於案例其中：    
* 在查詢中使用多個最短的路徑模式，其中一個模式開始上一個模式的最後一個節點。
* 在相同的 LAST_NODE()，合併兩個最短的路徑模式。

## <a name="graph-path-order"></a>圖形的路徑順序
圖形的路徑順序參照此輸出路徑中的資料順序。 輸出路徑順序總是開始後面出現的遞迴部分節點/邊緣模式中非遞迴的一部分。 圖形周遊期間最佳化執行的查詢時的順序與列印輸出中的順序無關。 同樣地，在遞迴模式中的箭頭方向也不會影響圖形的路徑順序。 

## <a name="graph-path-aggregate-functions"></a>圖形路徑彙總函式
因為節點和邊緣涉及任意長度模式傳回 （節點和邊緣相隔周遊該路徑中） 的集合，則使用者無法專案直接使用傳統 tablename.attributename 語法的屬性。 查詢它需要所在專案屬性值從中繼節點或邊緣資料表，在周遊，路徑中使用下列圖形路徑彙總函式：STRING_AGG、 LAST_VALUE、 SUM、 AVG、 MIN、 MAX 和 COUNT。 SELECT 子句中使用這些彙總函式的一般語法是：

```
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

### <a name="stringagg"></a>STRING_AGG
STRING_AGG 函式採用的運算式和分隔符號，做為輸入，並傳回字串。 使用者可以使用此函式在 SELECT 子句中的專案屬性從中繼節點或邊緣周遊的路徑中。 

### <a name="lastvalue"></a>LAST_VALUE
從周遊，路徑 LAST_VALUE 彙總函式的最後一個節點的屬性可用的專案。 它是以邊緣資料表別名做為輸入，此函式，只有節點資料表名稱錯誤，或可以使用別名。

**最後一個節點**:最後一個節點是指會周遊，無論在符合述詞中的箭頭方向的路徑中最後一個出現的節點。 例如： `MATCH(SHORTEST_PATH(n(-(e)->p)+) )`＞。 在此路徑中的最後一個節點會瀏覽的最後一個 P 節點。 

而最後一個節點是在此模式的輸出圖形路徑中的最後一個第 n 個節點： `MATCH(SHORTEST_PATH((n<-(e)-)+p))`    

### <a name="sum"></a>SUM
此函數會傳回周遊的路徑中提供的節點/邊緣屬性值或運算式出現的總和。

### <a name="count"></a>COUNT
此函式會傳回路徑中的所需的節點/邊緣屬性的非 null 值的數目。 COUNT 函式支援 ' *' 運算子的節點或邊緣資料表別名。 沒有節點或邊緣資料表別名，使用 * 模稜兩可，而且會產生錯誤。

    {  COUNT( <expression> | <node_or_edge_alias>.* )  <order_clause>  }


### <a name="avg"></a>AVG
傳回提供的節點/邊緣屬性值或運算式出現的平均值中周遊的路徑。

### <a name="min"></a>MIN
從提供的節點/邊緣屬性值或運算式出現在周遊的路徑傳回最小值。

### <a name="max"></a>MAX
從提供的節點/邊緣屬性值或運算式出現在周遊的路徑傳回的最大值。

## <a name="remarks"></a>備註  
shortest_path 函式僅適用於在 MATCH 內。     
LAST_NODE 只有在 shortest_path 內執行。     
不支援尋找加權的最短路徑、 所有路徑或所有的最短路徑。         
在某些情況下，不正確的計劃可能會產生較高數目的躍點，會導致較高的查詢執行時間的查詢。 使用雜湊聯結提示可能會幫助。    


## <a name="examples"></a>範例 
在這裡顯示，我們要的範例查詢會使用節點和邊緣資料表建立在[SQL 圖形範例](./sql-graph-sample.md)

### <a name="a--find-shortest-path-between-2-people"></a>A.  尋找 2 人之間最短路徑
 在下列範例中，我們會發現 Jacob 和 Alice 之間最短路徑。 我們需要從圖形的範例指令碼建立的 FriendOf edge 與 /people/person 節點。 

 ```
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

 ### <a name="b--find-shortest-path-from-a-given-node-to-all-other-nodes-in-the-graph"></a>B.  尋找從給定的節點到所有其他節點的最短路徑圖表中。 
 下列範例會尋找 Jacob 連接到的所有人在下圖，並從 Jacob 所有人員的最短路徑。 

 ```
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

### <a name="c--count-the-number-of-hopslevels-traversed-to-go-from-one-person-to-another-in-the-graph"></a>C.  計算不同人員移至另一個圖形中周遊的躍點/層級的數目。
 下列範例會尋找 Jacob 與 Alice 之間最短的路徑，並印出 Jacob 前往 Alice 所花費的躍點數目。 

 ```
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

### <a name="d-find-people-1-3-hops-away-from-a-given-person"></a>D. 尋找指定的人員遠離 1-3 躍點的人員
下列範例會尋找在圖 1-3 躍點離開他 Jacob 和他已連線到的所有人員之間的最短路徑。 

```
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

### <a name="e-find-people-exactly-2-hops-away-from-a-given-person"></a>E. 尋找指定的人員遠離的 2 個躍點的人員
下列範例會尋找 Jacob 和 2 個的躍點離開他在圖形中的人之間最短的路徑。 

```
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
 [比對 (SQL Graph)](../../t-sql/queries/match-sql-graph.md)    
 [CREATE TABLE &#40;SQL Graph&#41;](../../t-sql/statements/create-table-sql-graph.md)   
 [INSERT (SQL Graph)](../../t-sql/statements/insert-sql-graph.md)]  
 [SQL Server 2017 的圖表處理](../../relational-databases/graphs/sql-graph-overview.md)     
 
