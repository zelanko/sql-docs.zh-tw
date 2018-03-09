---
title: "說明 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 08/09/2017
ms.prod: sql-non-specified
ms.prod_service: sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|queries
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 4846a576-57ea-4068-959c-81e69e39ddc1
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 515c21cbf7874c0268eeedad0b67e0ce7cf3726d
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="explain-transact-sql"></a>說明 (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  傳回的查詢計畫[!INCLUDE[ssDW](../../includes/ssdw-md.md)][!INCLUDE[DWsql](../../includes/dwsql-md.md)]陳述式，而不需執行陳述式。 使用**解釋**哪些作業將需要移動資料的預覽，以及檢視查詢作業的估計的成本。  
  
 多個查詢計劃的詳細資訊，請參閱 「 了解查詢計劃 」，在[!INCLUDE[pdw-product-documentation_md](../../includes/pdw-product-documentation-md.md)]。  
  
## <a name="syntax"></a>語法  
  

```  
EXPLAIN SQL_statement  
[;]  
```  
  
## <a name="arguments"></a>引數  
 *SQL_statement*  
 [!INCLUDE[DWsql](../../includes/dwsql-md.md)]所在的陳述式**解釋**會執行。 *Q*可以是任何一種命令：**選取**，**插入**，**更新**，**刪除**， **CREATE TABLE AS SELECT**，**建立遠端資料表**。  
  
## <a name="permissions"></a>Permissions  
 需要**SHOWPLAN**權限與使用權限來執行*q*。 請參閱[權限： GRANT、 DENY、 REVOKE &#40;Azure SQL 資料倉儲、 Parallel Data Warehouse &#41;](../../t-sql/statements/permissions-grant-deny-revoke-azure-sql-data-warehouse-parallel-data-warehouse.md).  
  
## <a name="return-value"></a>傳回值  
 傳回的值從**解釋**命令是 XML 文件的結構如下所示。 此 XML 文件會列出所有作業中指定查詢的查詢計劃，每個括住`<dsql_operation>`標記。 傳回值是型別**nvarchar （max)**。  
  
 傳回的查詢計劃描述循序的 SQL 陳述式。執行查詢時它可能包含平行化的作業，因此部分顯示的循序陳述式可能會同時執行。  
  
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
  
|XML 標記|摘要、 屬性和內容|  
|-------------|--------------------------------------|  
|\<dsql_query>|最上層的層級/文件項目。|
|\<sql>|回應*q*。|  
|\<params>|在此階段不使用這個標記。|  
|\<dsql_operations>|摘要說明包含查詢的步驟，並包含查詢的成本資訊。 也包含所有`<dsql_operation>`區塊。 此標記包含整個查詢的計數資訊：<br /><br /> `<dsql_operations total_cost=total_cost total_number_operations=total_number_operations>`<br /><br /> *total_cost*是查詢執行，以毫秒的預估的時間總計。<br /><br /> *total_number_operations*是作業的查詢總數。 將平行處理，並在多個節點上執行的作業都會計算為單一作業。|  
|\<dsql_operation>|描述內的查詢計畫的單一作業。 \<Dsql_operation > 標記包含做為屬性的作業類型：<br /><br /> `<dsql_operation operation_type=operation_type>`<br /><br /> *operation_type*是中找到之值的其中一個[查詢資料 (SQL Server PDW)](http://msdn.microsoft.com/en-us/3f4f5643-012a-4c36-b5ec-691c4bbe668c)。<br /><br /> 中的內容`\<dsql_operation>`區塊是取決於作業類型。<br /><br /> 請參閱下表。|  
  
|作業類型|內容|範例|  
|--------------------|-------------|-------------|  
|BROADCAST_MOVE、 DISTRIBUTE_REPLICATED_TABLE_MOVE、 MASTER_TABLE_MOVE、 PARTITION_MOVE、 SHUFFLE_MOVE 和 TRIM_MOVE|`<operation_cost>`具有項目，這些屬性。 值反映的唯一本機作業：<br /><br /> -   *成本*本機運算子成本，並顯示作業執行，以毫秒的預估的時間。<br />-   *accumulative_cost*包括加總的平行作業中，以毫秒計劃中是所見的所有作業的總和。<br />-   *average_rowsize*是擷取和傳遞作業期間的資料列的估計平均資料列大小 （以位元組為單位）。<br />-   *output_rows*輸出 （節點） 基數而且顯示的輸出資料列數目。<br /><br /> `<location>`： 的節點或作業發生的分佈。 選項為: 「 控制項 」、 「 ComputeNode"、"AllComputeNodes"、"AllDistributions"、"SubsetDistributions 」、 「 分佈 」 和"SubsetNodes"。<br /><br /> `<source_statement>`： 隨機的來源資料移動。<br /><br /> `<destination_table>`: 內部暫存資料表資料會移入。<br /><br /> `<shuffle_columns>`只對 SHUFFLE_MOVE 作業: （適用)。 一或多個將用於視為散發資料行的暫存資料表的資料行。|`<operation_cost cost="40" accumulative_cost="40" average_rowsize = "50" output_rows="100"/>`<br /><br /> `<location distribution="AllDistributions" />`<br /><br /> `<source_statement type="statement">SELECT [TableAlias_3b77ee1d8ccf4a94ba644118b355db9d].[dist_date] FROM [qatest].[dbo].[flyers] [TableAlias_3b77ee1d8ccf4a94ba644118b355db9d]       </source_statement>`<br /><br /> `<destination_table>Q_[TEMP_ID_259]_[PARTITION_ID]</destination_table>`<br /><br /> `<shuffle_columns>dist_date;</shuffle_columns>`|  
|CopyOperation|`<operation_cost>`： 請參閱`<operation_cost>`上方。<br /><br /> `<DestinationCatalog>`： 目的地節點或節點。<br /><br /> `<DestinationSchema>`: 在 DestinationCatalog 目的結構描述。<br /><br /> `<DestinationTableName>`:"TableName"的目的地資料表的名稱。<br /><br /> `<DestinationDatasource>`： 目的地資料來源名稱或連接資訊。<br /><br /> `<Username>`和`<Password>`： 這些欄位表示使用者名稱和目的地的密碼可能會需要。<br /><br /> `<BatchSize>`： 複製作業批次大小。<br /><br /> `<SelectStatement>`: 用來執行複製的 select 陳述式。<br /><br /> `<distribution>`： 執行複製散發。|`<operation_cost cost="0" accumulative_cost="0" average_rowsize="4" output_rows="1" />`<br /><br /> `<DestinationCatalog>master</DestinationCatalog>`<br /><br /> `<DestinationSchema>dbo</DestinationSchema>`<br /><br /> `<DestinationTableName>[TableName]</DestinationTableName>`<br /><br /> `<DestinationDatasource>localhost, 8080</DestinationDatasource>`<br /><br /> `<Username>...</Username>`<br /><br /> `<Password>...</Password>`<br /><br /> `<BatchSize>6000</BatchSize>`<br /><br /> `<SelectStatement>SELECT T1_1.c1 AS c1 FROM [qatest].[dbo].[gigs] AS T1_1</SelectStatement>`<br /><br /> `<distribution>ControlNode</distribution>`|  
|MetaDataCreate_Operation|`<source_table>`： 作業來源資料表。<br /><br /> `<destionation_table>`： 作業的目的地資料表。|`<source_table>databases</source_table>`<br /><br /> `<destination_table>MetaDataCreateLandingTempTable</destination_table>`|  
|ON|`<location>`： 請參閱`<location>`上方。<br /><br /> `<sql_operation>`： 識別將會在節點執行的 SQL 命令。|`<location permanent="false" distribution="AllDistributions">Compute</location>`<br /><br /> `<sql_operation type="statement">CREATE TABLE [tempdb].[dbo]. [Q_[TEMP_ID_259]]_ [PARTITION_ID]]]([dist_date] DATE) WITH (DISTRIBUTION = HASH([dist_date]),) </sql_operation>`|  
|RemoteOnOperation|`<DestinationCatalog>`： 目的地目錄。<br /><br /> `<DestinationSchema>`: 在 DestinationCatalog 目的結構描述。<br /><br /> `<DestinationTableName>`:"TableName"的目的地資料表的名稱。<br /><br /> `<DestinationDatasource>`： 目的地資料來源名稱。<br /><br /> `<Username>`和`<Password>`： 這些欄位表示使用者名稱和目的地的密碼可能會需要。<br /><br /> `<CreateStatement>`： 目的地資料庫資料表建立陳述式。|`<DestinationCatalog>master</DestinationCatalog>`<br /><br /> `<DestinationSchema>dbo</DestinationSchema>`<br /><br /> `<DestinationTableName>TableName</DestinationTableName>`<br /><br /> `<DestinationDatasource>DestDataSource</DestinationDatasource>`<br /><br /> `<Username>...</Username>`<br /><br /> `<Password>...</Password>`<br /><br /> `<CreateStatement>CREATE TABLE [master].[dbo].[TableName] ([col1] BIGINT) ON [PRIMARY] WITH(DATA_COMPRESSION=PAGE);</CreateStatement>`|  
|RETURN|`<resultset>`： 結果集識別項。|`<resultset>RS_19</resultset>`|  
|RND_ID|`<identifier>`： 建立的物件識別項。|`<identifier>TEMP_ID_260</identifier>`|  
  
## <a name="limitations-and-restrictions"></a>限制事項  
 **說明**可以套用至*可最佳化*的結果為基礎的查詢，也就是查詢，可以改善或修改**說明**命令。 支援**解釋**以上所列的命令。 嘗試使用**解釋**與不支援的查詢類型將會傳回錯誤或回應查詢。  
  
 **說明**不支援使用者交易中。  
  
## <a name="examples"></a>範例  
 下列範例所示**解釋**上執行的命令**選取**陳述式和 XML 結果。  
  
 **正在提交解釋陳述式**  
  
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
  
 在執行陳述式使用之後**解釋**選項，[訊息] 索引標籤顯示標題為單行**說明**，和開始使用 XML 文字`\<?xml version="1.0" encoding="utf-8"?>`按一下以開啟中的整個文字 XMLXML 視窗。 若要進一步了解下列註解，您應該開啟在 SSDT 中的行號的顯示。  
  
#### <a name="to-turn-on-line-numbers"></a>若要開啟行號  
  
1.  使用中輸出出現**說明**SSDT 中，索引標籤上**工具**功能表上，選取**選項**。  
  
2.  展開**文字編輯器**區段中，展開**XML**，然後按一下 **一般**。  
  
3.  在**顯示**區域中，核取**行號**。  
  
4.  按一下 **[確定]**。  
  
 **解釋輸出範例**  
  
 在 XML 結果的**解釋**了命令開啟的資料列號碼：  
  
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
  
 **解釋輸出的意義**  
  
 上面的輸出包含 144 編號的行。 此查詢的輸出可能稍有不同。 下列清單說明重要區段。  
  
-   行 3 到 16 提供正在分析之查詢的描述。  
  
-   行 17，指定的作業總數都是 9。 您可以找到的每個作業，開始尋找的單字**dsql_operation**。  
  
-   行 18 啟動作業 1。 18 和 19 的線條表示， **RND_ID**作業將會建立將用於物件描述的隨機識別碼數字。 上面的輸出中所述的物件是**TEMP_ID_16893**。 您的號碼將會不同。  
  
-   第 20 行啟動作業 2。 行 21-25： 所有計算節點，請建立名為暫存資料表**TEMP_ID_16893**。  
  
-   行 26 啟動作業 3。 行 27 透過 37： 移動資料至**TEMP_ID_16893**使用廣播的移動。 提供傳送至每個計算節點的查詢。 一行 37 指定目的地資料表是**TEMP_ID_16893**。  
  
-   第 38 行啟動作業 4。 行到 40 39： 建立資料表的隨機識別碼。 **TEMP_ID_16894**上述範例中的識別碼。 您的號碼將會不同。  
  
-   行 41 啟動作業 5。 行透過 46 42： 所有節點上，建立名為的暫存資料表**TEMP_ID_16894**。  
  
-   行 47 啟動作業 6。 行 48 到 91： 移動資料，從各種不同的資料表 (包括**TEMP_ID_16893**) 到資料表**TEMP_ID_16894**，使用隨機移動作業。 提供傳送至每個計算節點的查詢。 一行 90 指定做為目的地資料表**TEMP_ID_16894**。 行 91年指定的資料行。  
  
-   行 92年啟動作業 7。 透過 97 行 93年： 所有計算節點、 卸除暫存資料表**TEMP_ID_16893**。  
  
-   行 98年啟動作業 8。 透過 135 行 99年： 結果傳回至用戶端。 會使用以取得結果所提供的查詢。  
  
-   行 136 啟動作業 9。 行 137 至 140： 所有節點上，卸除暫存資料表**TEMP_ID_16894**。  
  
  

