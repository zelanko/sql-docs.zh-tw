---
title: EXPLAIN (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 4846a576-57ea-4068-959c-81e69e39ddc1
author: shkale-msft
ms.author: shkale
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: a7b8a9ee85c7f3d04bc45c21d2605c839bdff01a
ms.sourcegitcommit: 05e18a1e80e61d9ffe28b14fb070728b67b98c7d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/04/2018
ms.locfileid: "37783579"
---
# <a name="explain-transact-sql"></a>EXPLAIN (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  傳回 [!INCLUDE[ssDW](../../includes/ssdw-md.md)] [!INCLUDE[DWsql](../../includes/dwsql-md.md)] 陳述式的查詢計劃，而不執行陳述式。 使用 **EXPLAIN** 預覽哪些作業需要移動資料，以及檢視查詢作業的估計成本。  
  
 如需查詢計劃的詳細資訊，請參閱 [!INCLUDE[pdw-product-documentation_md](../../includes/pdw-product-documentation-md.md)] 中的＜了解查詢計劃＞。  
  
## <a name="syntax"></a>語法  
  

```  
EXPLAIN SQL_statement  
[;]  
```  
  
## <a name="arguments"></a>引數  
 *SQL_statement*  
 **EXPLAIN** 將執行的 [!INCLUDE[DWsql](../../includes/dwsql-md.md)] 陳述式。 *SQL_statement* 可以是以下任何一個命令：**SELECT**、**INSERT**、**UPDATE**、**DELETE**、**CREATE TABLE AS SELECT**、**CREATE REMOTE TABLE**。  
  
## <a name="permissions"></a>Permissions  
 需要 **SHOWPLAN** 權限，以及執行 *SQL_statement* 的權限。 請參閱[權限：GRANT、DENY、REVOKE &#40;Azure SQL 資料倉儲、平行處理資料倉儲&#41;](../../t-sql/statements/permissions-grant-deny-revoke-azure-sql-data-warehouse-parallel-data-warehouse.md)。  
  
## <a name="return-value"></a>傳回值  
 從 **EXPLAIN** 命令的傳回值是具備以下結構的 XML 文件。 此 XML 文件會列出指定查詢之查詢計劃中的所有作業，每個作業都以 `<dsql_operation>` 標記括住。 傳回值為 **nvarchar(max)** 類型。  
  
 傳回的查詢計劃描述循序的 SQL 陳述式。當查詢執行時，可能包含平行化的作業，因此部分顯示的循序陳述式可能會同時執行。  
  
```  
\<?xml version="1.0" encoding="utf-8"?>  
<dsql_query>  
  <sql>. . .</sql>  
  <params />  
  <dsql_operations>  
    <dsql_operation>  
     . . .      
    </dsql_operation>  
    [ . . . n ]  
  <dsql_operations>  
</dsql_query>  
```  
  
 XML 標記包含這項資訊：  
  
|XML 標記|摘要、屬性和內容|  
|-------------|--------------------------------------|  
|\<dsql_query>|最上層/文件元素。|
|\<sql>|回應 *SQL_statement*。|  
|\<params>|目前不使用此標記。|  
|\<dsql_operations>|摘要說明和包含查詢步驟，並包含查詢的成本資訊。 也包含所有 `<dsql_operation>` 區塊。 此標記包含整個查詢的計數資訊：<br /><br /> `<dsql_operations total_cost=total_cost total_number_operations=total_number_operations>`<br /><br /> *total_cost* 是查詢執行的預估時間總計，以毫秒為單位。<br /><br /> *total_number_operations* 是查詢的作業總數。 將平行處理並在多個節點上執行的作業都會計算為單一作業。|  
|\<dsql_operation>|描述查詢計劃內的單一作業。 \<dsql_operation> 標記包含做為屬性的作業類型：<br /><br /> `<dsql_operation operation_type=operation_type>`<br /><br /> *operation_type* 是在[查詢資料 (SQL Server PDW)](http://msdn.microsoft.com/en-us/3f4f5643-012a-4c36-b5ec-691c4bbe668c) 中找到的其中一個值。<br /><br /> `\<dsql_operation>` 區塊中的內容取決於作業類型。<br /><br /> 請參閱下表。|  
  
|作業類型|內容|範例|  
|--------------------|-------------|-------------|  
|BROADCAST_MOVE、DISTRIBUTE_REPLICATED_TABLE_MOVE、MASTER_TABLE_MOVE、PARTITION_MOVE、SHUFFLE_MOVE 和 TRIM_MOVE|`<operation_cost>` 元素，具有這些屬性。 值只反映本機作業：<br /><br /> -   *cost* 是本機運算子成本，並顯示作業執行的預估時間，以毫秒為單位。<br />-   *accumulative_cost* 是計劃中包括平行作業加總值的所有所見作業總和，以毫秒為單位。<br />-   *average_rowsize* 是作業期間，擷取和傳遞之資料列的資料列預估平均大小 (以位元組為單位)。<br />-   *output_rows* 是輸出 (節點) 基數，並顯示輸出資料列的數目。<br /><br /> `<location>`：作業發生所在的節點或散發。 選項為：“Control”、“ComputeNode”、“AllComputeNodes”、“AllDistributions”、“SubsetDistributions”、“Distribution” 和 “SubsetNodes”。<br /><br /> `<source_statement>`：隨機移動的來源資料。<br /><br /> `<destination_table>`：資料將移入的內部暫存資料表。<br /><br /> `<shuffle_columns>`：(只適用於 SHUFFLE_MOVE 作業)。 一或多個將用於暫存資料表之散發資料行的資料行。|`<operation_cost cost="40" accumulative_cost="40" average_rowsize = "50" output_rows="100"/>`<br /><br /> `<location distribution="AllDistributions" />`<br /><br /> `<source_statement type="statement">SELECT [TableAlias_3b77ee1d8ccf4a94ba644118b355db9d].[dist_date] FROM [qatest].[dbo].[flyers] [TableAlias_3b77ee1d8ccf4a94ba644118b355db9d]       </source_statement>`<br /><br /> `<destination_table>Q_[TEMP_ID_259]_[PARTITION_ID]</destination_table>`<br /><br /> `<shuffle_columns>dist_date;</shuffle_columns>`|  
|CopyOperation|`<operation_cost>`：請參閱上面的 `<operation_cost>`。<br /><br /> `<DestinationCatalog>`：目的地節點。<br /><br /> `<DestinationSchema>`：DestinationCatalog 中的目的地結構描述。<br /><br /> `<DestinationTableName>`：目的地資料表或 “TableName” 的名稱。<br /><br /> `<DestinationDatasource>`：目的地資料來源的名稱或連線資訊。<br /><br /> `<Username>` 和 `<Password>`：這些欄位表示可能需要目的地的使用者名稱和密碼。<br /><br /> `<BatchSize>`：複製作業的批次大小。<br /><br /> `<SelectStatement>`：用來執行複製的 select 陳述式。<br /><br /> `<distribution>`：執行複製所在的散發。|`<operation_cost cost="0" accumulative_cost="0" average_rowsize="4" output_rows="1" />`<br /><br /> `<DestinationCatalog>master</DestinationCatalog>`<br /><br /> `<DestinationSchema>dbo</DestinationSchema>`<br /><br /> `<DestinationTableName>[TableName]</DestinationTableName>`<br /><br /> `<DestinationDatasource>localhost, 8080</DestinationDatasource>`<br /><br /> `<Username>...</Username>`<br /><br /> `<Password>...</Password>`<br /><br /> `<BatchSize>6000</BatchSize>`<br /><br /> `<SelectStatement>SELECT T1_1.c1 AS c1 FROM [qatest].[dbo].[gigs] AS T1_1</SelectStatement>`<br /><br /> `<distribution>ControlNode</distribution>`|  
|MetaDataCreate_Operation|`<source_table>`：作業的來源資料表。<br /><br /> `<destionation_table>`：作業的目的地資料表。|`<source_table>databases</source_table>`<br /><br /> `<destination_table>MetaDataCreateLandingTempTable</destination_table>`|  
|ON|`<location>`：請參閱上面的 `<location>`。<br /><br /> `<sql_operation>`：識別將在節點上執行的 SQL 命令。|`<location permanent="false" distribution="AllDistributions">Compute</location>`<br /><br /> `<sql_operation type="statement">CREATE TABLE [tempdb].[dbo]. [Q_[TEMP_ID_259]]_ [PARTITION_ID]]]([dist_date] DATE) WITH (DISTRIBUTION = HASH([dist_date]),) </sql_operation>`|  
|RemoteOnOperation|`<DestinationCatalog>`：目的地目錄。<br /><br /> `<DestinationSchema>`：DestinationCatalog 中的目的地結構描述。<br /><br /> `<DestinationTableName>`：目的地資料表或 “TableName” 的名稱。<br /><br /> `<DestinationDatasource>`：目的地資料來源的名稱。<br /><br /> `<Username>` 和 `<Password>`：這些欄位表示可能需要目的地的使用者名稱和密碼。<br /><br /> `<CreateStatement>`：目的地資料庫的資料表建立陳述式。|`<DestinationCatalog>master</DestinationCatalog>`<br /><br /> `<DestinationSchema>dbo</DestinationSchema>`<br /><br /> `<DestinationTableName>TableName</DestinationTableName>`<br /><br /> `<DestinationDatasource>DestDataSource</DestinationDatasource>`<br /><br /> `<Username>...</Username>`<br /><br /> `<Password>...</Password>`<br /><br /> `<CreateStatement>CREATE TABLE [master].[dbo].[TableName] ([col1] BIGINT) ON [PRIMARY] WITH(DATA_COMPRESSION=PAGE);</CreateStatement>`|  
|RETURN|`<resultset>`：結果集的識別碼。|`<resultset>RS_19</resultset>`|  
|RND_ID|`<identifier>`：建立之物件的識別碼。|`<identifier>TEMP_ID_260</identifier>`|  
  
## <a name="limitations-and-restrictions"></a>限制事項  
 **EXPLAIN** 只能套用至*可最佳化*的查詢，也就是可根據 **EXPLAIN** 命令的結果改善或修改的查詢。 支援的 **EXPLAIN** 命令列在上面。 嘗試使用 **EXPLAIN** 搭配不支援的查詢類型，將會傳回錯誤或回應查詢。  
  
 使用者交易中不支援 **EXPLAIN**。  
  
## <a name="examples"></a>範例  
 下列範例顯示在 **SELECT** 陳述式執行 **EXPLAIN** 命令，以及 XML 結果。  
  
 **提交 EXPLAIN 陳述式**  
  
 此範例中提交的命令為：  
  
```  
-- Uses AdventureWorks  
  
EXPLAIN   
    SELECT CAST (AVG(YearlyIncome) AS int) AS AverageIncome,   
        CAST(AVG(FIS.SalesAmount) AS int) AS AverageSales,   
        G.StateProvinceName, T.SalesTerritoryGroup  
    FROM dbo.DimGeography AS G  
    JOIN dbo.DimSalesTerritory AS T  
        ON G.SalesTerritoryKey = T.SalesTerritoryKey  
    JOIN dbo.DimCustomer AS C  
        ON G.GeographyKey = C.GeographyKey  
    JOIN dbo.FactInternetSales AS FIS  
        ON C.CustomerKey = FIS.CustomerKey  
    WHERE T.SalesTerritoryGroup IN ('North America', 'Pacific')  
        AND Gender = 'F'  
    GROUP BY G.StateProvinceName, T.SalesTerritoryGroup  
    ORDER BY AVG(YearlyIncome) DESC;  
GO  
```  
  
 使用 **EXPLAIN** 選項執行陳述式後，[訊息] 索引標籤會顯示一行標題 **explain**，並且以 XML 文字 `\<?xml version="1.0" encoding="utf-8"?>` 為開頭。按一下 XML 可在 XML 視窗中開啟整段文字。 若要進一步了解下列註解，您應該在 SSDT 中開啟行號的顯示。  
  
#### <a name="to-turn-on-line-numbers"></a>開啟行號  
  
1.  當 SSDT 的 [explain] 索引標籤出現輸出時，在 [工具] 功能表上，選取 [選項]。  
  
2.  展開 [文字編輯器] 區段，展開 [XML]，然後按一下 [一般]。  
  
3.  在 [顯示] 區域中，核取 [行號]。  
  
4.  按一下 [確定] 。  
  
 **範例 EXPLAIN 輸出**  
  
 **EXPLAIN** 命令開啟行號的 XML 結果為：  
  
```  
1  \<?xml version="1.0" encoding="utf-8"?>  
2  <dsql_query>  
3    <sql>SELECT CAST (AVG(YearlyIncome) AS int) AS AverageIncome,   
4          CAST(AVG(FIS.SalesAmount) AS int) AS AverageSales,   
5          G.StateProvinceName, T.SalesTerritoryGroup  
6      FROM dbo.DimGeography AS G  
7      JOIN dbo.DimSalesTerritory AS T  
8          ON G.SalesTerritoryKey = T.SalesTerritoryKey  
9      JOIN dbo.DimCustomer AS C  
10          ON G.GeographyKey = C.GeographyKey  
11      JOIN dbo.FactInternetSales AS FIS  
12          ON C.CustomerKey = FIS.CustomerKey  
13      WHERE T.SalesTerritoryGroup IN ('North America', 'Pacific')  
14          AND Gender = 'F'  
15      GROUP BY G.StateProvinceName, T.SalesTerritoryGroup  
16      ORDER BY AVG(YearlyIncome) DESC</sql>  
17    <dsql_operations total_cost="0.926237696" total_number_operations="9">  
18      <dsql_operation operation_type="RND_ID">  
19        <identifier>TEMP_ID_16893</identifier>  
20      </dsql_operation>  
21      <dsql_operation operation_type="ON">  
22        <location permanent="false" distribution="AllComputeNodes" />  
23        <sql_operations>  
24          <sql_operation type="statement">CREATE TABLE [tempdb].[dbo].[TEMP_ID_16893] ([CustomerKey] INT NOT NULL, [GeographyKey] INT, [YearlyIncome] MONEY ) WITH(DATA_COMPRESSION=PAGE);</sql_operation>  
25        </sql_operations>  
26      </dsql_operation>  
27      <dsql_operation operation_type="BROADCAST_MOVE">  
28        <operation_cost cost="0.121431552" accumulative_cost="0.121431552" average_rowsize="16" output_rows="31.6228" />  
29        <source_statement>SELECT [T1_1].[CustomerKey] AS [CustomerKey],  
30         [T1_1].[GeographyKey] AS [GeographyKey],  
31         [T1_1].[YearlyIncome] AS [YearlyIncome]  
32  FROM   (SELECT [T2_1].[CustomerKey] AS [CustomerKey],  
33                 [T2_1].[GeographyKey] AS [GeographyKey],  
34                 [T2_1].[YearlyIncome] AS [YearlyIncome]  
35          FROM   [AdventureWorksPDW2012].[dbo].[DimCustomer] AS T2_1  
36          WHERE  ([T2_1].[Gender] = CAST (N'F' COLLATE Latin1_General_100_CI_AS_KS_WS AS NVARCHAR (1)) COLLATE Latin1_General_100_CI_AS_KS_WS)) AS T1_1</source_statement>  
37        <destination_table>[TEMP_ID_16893]</destination_table>  
38      </dsql_operation>  
39      <dsql_operation operation_type="RND_ID">  
40        <identifier>TEMP_ID_16894</identifier>  
41      </dsql_operation>  
42      <dsql_operation operation_type="ON">  
43        <location permanent="false" distribution="AllDistributions" />  
44        <sql_operations>  
45          <sql_operation type="statement">CREATE TABLE [tempdb].[dbo].[TEMP_ID_16894] ([StateProvinceName] NVARCHAR(50) COLLATE Latin1_General_100_CI_AS_KS_WS, [SalesTerritoryGroup] NVARCHAR(50) COLLATE Latin1_General_100_CI_AS_KS_WS NOT NULL, [col] BIGINT, [col1] MONEY NOT NULL, [col2] BIGINT, [col3] MONEY NOT NULL ) WITH(DATA_COMPRESSION=PAGE);</sql_operation>  
46        </sql_operations>  
47      </dsql_operation>  
48      <dsql_operation operation_type="SHUFFLE_MOVE">  
49        <operation_cost cost="0.804806144" accumulative_cost="0.926237696" average_rowsize="232" output_rows="108.406" />  
50        <source_statement>SELECT [T1_1].[StateProvinceName] AS [StateProvinceName],  
51         [T1_1].[SalesTerritoryGroup] AS [SalesTerritoryGroup],  
52         [T1_1].[col2] AS [col],  
53         [T1_1].[col] AS [col1],  
54         [T1_1].[col3] AS [col2],  
55         [T1_1].[col1] AS [col3]  
56  FROM   (SELECT ISNULL([T2_1].[col1], CONVERT (MONEY, 0.00, 0)) AS [col],  
57                 ISNULL([T2_1].[col3], CONVERT (MONEY, 0.00, 0)) AS [col1],  
58                 [T2_1].[StateProvinceName] AS [StateProvinceName],  
59                 [T2_1].[SalesTerritoryGroup] AS [SalesTerritoryGroup],  
60                 [T2_1].[col] AS [col2],  
61                 [T2_1].[col2] AS [col3]  
62          FROM   (SELECT   COUNT_BIG([T3_2].[YearlyIncome]) AS [col],  
63                           SUM([T3_2].[YearlyIncome]) AS [col1],  
64                           COUNT_BIG(CAST ((0) AS INT)) AS [col2],  
65                           SUM([T3_2].[SalesAmount]) AS [col3],  
66                           [T3_2].[StateProvinceName] AS [StateProvinceName],  
67                           [T3_1].[SalesTerritoryGroup] AS [SalesTerritoryGroup]  
68                  FROM     (SELECT [T4_1].[SalesTerritoryKey] AS [SalesTerritoryKey],  
69                                   [T4_1].[SalesTerritoryGroup] AS [SalesTerritoryGroup]  
70                            FROM   [AdventureWorksPDW2012].[dbo].[DimSalesTerritory] AS T4_1  
71                            WHERE  (([T4_1].[SalesTerritoryGroup] = CAST (N'North America' COLLATE Latin1_General_100_CI_AS_KS_WS AS NVARCHAR (13)) COLLATE Latin1_General_100_CI_AS_KS_WS)  
72                                    OR ([T4_1].[SalesTerritoryGroup] = CAST (N'Pacific' COLLATE Latin1_General_100_CI_AS_KS_WS AS NVARCHAR (7)) COLLATE Latin1_General_100_CI_AS_KS_WS))) AS T3_1  
73                           INNER JOIN  
74                           (SELECT [T4_1].[SalesTerritoryKey] AS [SalesTerritoryKey],  
75                                   [T4_2].[YearlyIncome] AS [YearlyIncome],  
76                                   [T4_2].[SalesAmount] AS [SalesAmount],  
77                                   [T4_1].[StateProvinceName] AS [StateProvinceName]  
78                            FROM   [AdventureWorksPDW2012].[dbo].[DimGeography] AS T4_1  
79                                   INNER JOIN  
80                                   (SELECT [T5_2].[GeographyKey] AS [GeographyKey],  
81                                           [T5_2].[YearlyIncome] AS [YearlyIncome],  
82                                           [T5_1].[SalesAmount] AS [SalesAmount]  
83                                    FROM   [AdventureWorksPDW2012].[dbo].[FactInternetSales] AS T5_1  
84                                           INNER JOIN  
85                                           [tempdb].[dbo].[TEMP_ID_16893] AS T5_2  
86                                           ON ([T5_1].[CustomerKey] = [T5_2].[CustomerKey])) AS T4_2  
87                                   ON ([T4_2].[GeographyKey] = [T4_1].[GeographyKey])) AS T3_2  
88                           ON ([T3_1].[SalesTerritoryKey] = [T3_2].[SalesTerritoryKey])  
89                  GROUP BY [T3_2].[StateProvinceName], [T3_1].[SalesTerritoryGroup]) AS T2_1) AS T1_1</source_statement>  
90        <destination_table>[TEMP_ID_16894]</destination_table>  
91        <shuffle_columns>StateProvinceName;</shuffle_columns>  
92      </dsql_operation>  
93      <dsql_operation operation_type="ON">  
94        <location permanent="false" distribution="AllComputeNodes" />  
95        <sql_operations>  
96          <sql_operation type="statement">DROP TABLE [tempdb].[dbo].[TEMP_ID_16893]</sql_operation>  
97        </sql_operations>  
98      </dsql_operation>  
99      <dsql_operation operation_type="RETURN">  
100        <location distribution="AllDistributions" />  
101        <select>SELECT   [T1_1].[col] AS [col],  
102           [T1_1].[col1] AS [col1],  
103           [T1_1].[StateProvinceName] AS [StateProvinceName],  
104           [T1_1].[SalesTerritoryGroup] AS [SalesTerritoryGroup],  
105           [T1_1].[col2] AS [col2]  
106  FROM     (SELECT CONVERT (INT, [T2_1].[col], 0) AS [col],  
107                   CONVERT (INT, [T2_1].[col1], 0) AS [col1],  
108                   [T2_1].[StateProvinceName] AS [StateProvinceName],  
109                   [T2_1].[SalesTerritoryGroup] AS [SalesTerritoryGroup],  
110                   [T2_1].[col] AS [col2]  
111            FROM   (SELECT CASE  
112                            WHEN ([T3_1].[col] = CAST ((0) AS BIGINT)) THEN CAST (NULL AS MONEY)  
113                            ELSE ([T3_1].[col1] / CONVERT (MONEY, [T3_1].[col], 0))  
114                           END AS [col],  
115                           CASE  
116                            WHEN ([T3_1].[col2] = CAST ((0) AS BIGINT)) THEN CAST (NULL AS MONEY)  
117                            ELSE ([T3_1].[col3] / CONVERT (MONEY, [T3_1].[col2], 0))  
118                           END AS [col1],  
119                           [T3_1].[StateProvinceName] AS [StateProvinceName],  
120                           [T3_1].[SalesTerritoryGroup] AS [SalesTerritoryGroup]  
121                    FROM   (SELECT ISNULL([T4_1].[col], CONVERT (BIGINT, 0, 0)) AS [col],  
122                                   ISNULL([T4_1].[col1], CONVERT (MONEY, 0.00, 0)) AS [col1],  
123                                   ISNULL([T4_1].[col2], CONVERT (BIGINT, 0, 0)) AS [col2],  
124                                   ISNULL([T4_1].[col3], CONVERT (MONEY, 0.00, 0)) AS [col3],  
125                                   [T4_1].[StateProvinceName] AS [StateProvinceName],  
126                                   [T4_1].[SalesTerritoryGroup] AS [SalesTerritoryGroup]  
127                            FROM   (SELECT   SUM([T5_1].[col]) AS [col],  
128                                             SUM([T5_1].[col1]) AS [col1],  
129                                             SUM([T5_1].[col2]) AS [col2],  
130                                             SUM([T5_1].[col3]) AS [col3],  
131                                             [T5_1].[StateProvinceName] AS [StateProvinceName],  
132                                             [T5_1].[SalesTerritoryGroup] AS [SalesTerritoryGroup]  
133                                    FROM     [tempdb].[dbo].[TEMP_ID_16894] AS T5_1  
134                                    GROUP BY [T5_1].[StateProvinceName], [T5_1].[SalesTerritoryGroup]) AS T4_1) AS T3_1) AS T2_1) AS T1_1  
135  ORDER BY [T1_1].[col2] DESC</select>  
136      </dsql_operation>  
137      <dsql_operation operation_type="ON">  
138        <location permanent="false" distribution="AllDistributions" />  
139        <sql_operations>  
140          <sql_operation type="statement">DROP TABLE [tempdb].[dbo].[TEMP_ID_16894]</sql_operation>  
141        </sql_operations>  
142      </dsql_operation>  
143    </dsql_operations>  
144  </dsql_query>  
  
```  
  
 **EXPLAIN 輸出的意義**  
  
 上面的輸出包含 144 行。 您的查詢輸出可能稍有不同。 下列清單說明重要區段。  
  
-   第 3 到 16 行提供正在分析之查詢的描述。  
  
-   第 17 行指定作業的總數是 9。 您可以尋找單字 **dsql_operation** 找到每個作業的開始。  
  
-   第 18 行啟動第 1 個作業。 第 18 行和第 19 行表示 **RND_ID** 作業會建立一個用於物件描述的隨機識別碼號碼。 上面輸出中所描述的物件是 **TEMP_ID_16893**。 您的號碼將會不同。  
  
-   第 20 行啟動第 2 個作業。 第 21 到 25 行：在所有計算節點上，建立名為 **TEMP_ID_16893** 的暫存資料表。  
  
-   第 26 行啟動第 3 個作業。 第 27 到 37 行：使用廣播移動將資料移動至 **TEMP_ID_16893**。 提供傳送至每個計算節點的查詢。 第 37 行指定目的地資料表為 **TEMP_ID_16893**。  
  
-   第 38 行啟動第 4 個作業。 第 39 到 40 行：建立資料表的隨機識別碼。 **TEMP_ID_16894** 是上述範例中的識別碼號碼。 您的號碼將會不同。  
  
-   第 41 行啟動第 5 個作業。 第 42 到 46 行：在所有節點上，建立名為 **TEMP_ID_16894** 的暫存資料表。  
  
-   第 47 行啟動第 6 個作業。 第 48 到 91 行：使用隨機移動作業，從各個資料表 (包括**TEMP_ID_16893**) 移動資料到資料表 **TEMP_ID_16894**。 提供傳送至每個計算節點的查詢。 第 90 行指定目的地資料表為 **TEMP_ID_16894**。 第 91 行指定資料行。  
  
-   第 92 行啟動第 7 個作業。 第 93 到 97 行：在所有計算節點上，卸除名為 **TEMP_ID_16893** 的暫存資料表。  
  
-   第 98 行啟動第 8 個作業。 第 99 到 135 行：將結果傳回至用戶端。 使用提供的查詢取得結果。  
  
-   第 136 行啟動第 9 個作業。 第 137 到 140 行：在所有節點上，卸除名為 **TEMP_ID_16894** 的暫存資料表。  
  
  

