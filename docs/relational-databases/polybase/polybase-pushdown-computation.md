---
description: PolyBase 中的下推計算
title: PolyBase 中的下推計算 | Microsoft Docs
dexcription: Enable pushdown computation to improve performance of queries on your Hadoop cluster. You can select a subset of rows/columns in an external table for pushdown.
ms.date: 04/23/2019
ms.prod: sql
ms.technology: polybase
ms.topic: conceptual
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: ''
monikerRange: '>= sql-server-2016 || =sqlallproducts-allversions'
ms.openlocfilehash: 0b028d0476b55d17a7eca9a8cace18d9ca206bc3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88482501"
---
# <a name="pushdown-computations-in-polybase"></a>PolyBase 中的下推計算

## <a name="dmv"></a>DMV

[!INCLUDE [SQL Server Windows Only - ASDBMI ](../../includes/applies-to-version/sql-windows-only-asdbmi.md)]

下推計算可改善 Hadoop 叢集的查詢效能。

## <a name="enable-pushdown"></a>啟用下推

下文涵蓋啟用下推的步驟：

[在 Hadoop 中啟用下推計算](polybase-configure-hadoop.md#pushdown)

## <a name="select-a-subset-of-rows"></a>選取資料列的子集

使用述詞下推，來改善從外部資料表選取資料列子集之查詢的效能。

在此範例中，SQL Server 2016 會起始 map-reduce 工作，以擷取 Hadoop 上符合 `customer.account_balance < 200000` 述詞的資料列。 因為查詢可以順利完成，而不需要掃描資料表中的所有資料列，所以只會將符合述詞準則的資料列複製到 SQL Server。 這可以節省大量時間，而且相較於帳戶餘額 >= 200000 的客戶數目，客戶餘額數目 < 200000 需要較少的暫存儲存空間。

```sql
SELECT * FROM customer WHERE customer.account_balance < 200000
SELECT * FROM SensorData WHERE Speed > 65;  
```

### <a name="select-a-subset-of-columns"></a>選取資料行的子集

使用述詞下推，來改善從外部資料表選取資料行子集之查詢的效能。

在此查詢中，SQL Server 會起始 map-reduce 工作來前置處理 Hadoop 分隔符號文字檔，只將兩個資料行 (customer.name 和 customer.zip_code) 的資料複製至 SQL Server PDW。

```sql
SELECT customer.name, customer.zip_code FROM customer WHERE customer.account_balance < 200000
```

### <a name="pushdown-for-basic-expressions-and-operators"></a>基本運算式和運算子的下推

SQL Server 允許述詞下推的下列基本運算式和運算子。

+ 數值、日期和時間值的二進位比較運算子 (\<, >、=、!=、<>、>=、<=)。

+ 算術運算子 (+、-、*、/、% )。

+ 邏輯運算子 (AND、OR)。

+ 一元運算子 (NOT、IS NULL、IS NOT NULL)。

可能會下推 BETWEEN、NOT、IN 和 LIKE 運算子。 實際的行為取決於查詢最佳化工具如何將運算子運算式重新編寫為一系列使用基本關係運算子的陳述式。

此範例中的查詢有多個可下推到 Hadoop 的述詞。 SQL Server 可以將 map-reduce 工作推送到 Hadoop，以執行 `customer.account_balance <= 200000` 述詞。 `BETWEEN 92656 and 92677` 運算式也是由可推送到 Hadoop 的二進位和邏輯作業組成。 `customer.account_balance and customer.zipcode` 中的邏輯 **AND** 是最終運算式。

藉由這樣的述詞組合，map-reduce 工作就可以執行所有 WHERE 子句。 只有符合 SELECT 準則的資料會複製回 SQL Server PDW。

```sql
SELECT * FROM customer WHERE customer.account_balance <= 200000 AND customer.zipcode BETWEEN 92656 AND 92677
```

## <a name="force-pushdown"></a>強制下推

```sql
SELECT * FROM [dbo].[SensorData]
WHERE Speed > 65
OPTION (FORCE EXTERNALPUSHDOWN);
```

## <a name="disable-pushdown"></a>停用下推

```sql
SELECT * FROM [dbo].[SensorData]
WHERE Speed > 65
OPTION (DISABLE EXTERNALPUSHDOWN);
```

## <a name="next-steps"></a>後續步驟

如需 PolyBase 的詳細資訊，請參閱[什麼是 PolyBase？](polybase-guide.md)。
