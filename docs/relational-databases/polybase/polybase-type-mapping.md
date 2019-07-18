---
title: 使用 PolyBase 進行類型對應 | Microsoft Docs
ms.date: 09/24/2018
ms.prod: sql
ms.technology: polybase
ms.topic: conceptual
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: aboke
manager: craigg
ms.openlocfilehash: 67ecc3a75da04849d6b23d0b07f6e650c2825b0b
ms.sourcegitcommit: e0c55d919ff9cec233a7a14e72ba16799f4505b2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/10/2019
ms.locfileid: "67731798"
---
# <a name="type-mapping-with-polybase"></a>使用 PolyBase 進行類型對應

[!INCLUDE[appliesto-ss-xxxx-asdw-pdw-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文描述 PolyBase 外部資料來源和 SQL Server 間的對應。 您可以使用此資訊，搭配 [CREATE EXTERNAL TABLE](../../t-sql/statements/create-external-table-transact-sql.md) Transact-SQL 命令正確定義外部資料表。

## <a name="overview"></a>概觀

當使用 PolyBase 建立外部資料表時，資料行定義 (包括資料類型及資料行數目) 必須符合外部檔案中的資料。 若有不相符的情形，系統在查詢實際資料時將會拒絕檔案資料列。  
  
針對會參考位於外部資料來源中之檔案的外部資料表，資料行和類型定義必須對應至外部檔案中的確切結構描述。 定義會參考儲存於 Hadoop/Hive 中資料的資料類型時，請在 SQL 和 Hive 資料類型之間使用下列對應，並在從類型進行選取時將該類型轉換成 SQL 資料類型。 除非另行指定，否則這些類型都包含 Hive 的所有版本。

> [!NOTE]  
> SQL Server 在任何轉換中皆不支援 Hive 的 *infinity* 資料值。 PolyBase 將會搭配資料類型轉換錯誤而失敗。

## <a name="hadoop-type-mapping-reference"></a>Hadoop 類型對應參考

| SQL 資料類型 | .NET 資料類型            | Hive 資料類型 | Hadoop/Java 資料類型 | 註解                       |
| ------------- | ------------------------- | -------------- | --------------------- | ------------------------------ |
| TINYINT       | Byte                      | TINYINT        | ByteWritable          | 僅適用於不帶正負號的數字。     |
| SMALLINT      | Int16                     | SMALLINT       | ShortWritable         |
| INT           | Int32                     | INT            | IntWritable           |
| BIGINT        | Int64                     | BIGINT         | LongWritable          |
| bit           | 布林                   | boolean        | BooleanWritable       |
| FLOAT         | Double                    | double         | DoubleWritable        |
| REAL          | Single                    | FLOAT          | FloatWritable         |
| money         | Decimal                   | double         | DoubleWritable        |
| SMALLMONEY    | Decimal                   | double         | DoubleWritable        |
| NCHAR         | String<br /><br /> Char[] | string         | Varchar               |
| NVARCHAR      | String<br /><br /> Char[] | string         | Varchar               |
| char          | String<br /><br /> Char[] | string         | Varchar               |
| varchar       | String<br /><br /> Char[] | string         | Varchar               |
| BINARY        | Byte[]                    | BINARY         | BytesWritable         | 適用於 Hive 0.8 及更新版本。 |
| varbinary     | Byte[]                    | BINARY         | BytesWritable         | 適用於 Hive 0.8 及更新版本。 |
| 日期          | DateTime                  | TIMESTAMP      | TimestampWritable     |
| smalldatetime | DateTime                  | TIMESTAMP      | TimestampWritable     |
| datetime2     | DateTime                  | TIMESTAMP      | TimestampWritable     |
| DATETIME      | DateTime                  | TIMESTAMP      | TimestampWritable     |
| time          | TimeSpan                  | TIMESTAMP      | TimestampWritable     |
| Decimal       | Decimal                   | Decimal        | BigDecimalWritable    | 適用於 Hive 0.11 及更新版本。 |

<!--SQL Server 2019-->
::: moniker range=">= sql-server-ver15 || =sqlallproducts-allversions"

## <a name="oracle-type-mapping-reference"></a>Oracle 類型對應參考

| Oracle 資料類型 | SQL Server 類型 | 
| -------------    | --------------- |
|float             |float            |
|NUMBER            |Decimal          |
|LONG              |nvarchar         |
|BINARY_FLOAT      |Real             | 
|BINARY_DOUBLE     |float            | 
|CHAR              |Char             |
|VARCHAR2          |Varchar          | 
|NVARCHAR2         |nvarchar         | 
|RAW               |Varbinary        |
|LONG RAW          |Varbinary        | 
|BLOB              |Varbinary        |
|CLOB              |Varchar          |
|NCLOB             | nvarchar        | 
|ROWID             |Varchar          |
|UROWID            |Varchar          | 
|DATE              |Datetime2        |
|timestamp         |Datetime2        | 

**類型不符** 

**Float：** Oracle 支援 126 浮點數精確度，低於 SQL Server 支援的程度 (53)。 因此，**Float (1-53)** 可以直接對應，但在超出這個範圍之後，便會因截斷而發生資料遺失。

**Timestamp：** Oracle 中的 Timestamp 和 Timestamp with local timezone 支援 9 毫秒精確度，但 SQL Server DateTime2 只支援 7 毫秒精確度。 




## <a name="mongodb-type-mapping"></a>MongoDB 類型對應

| BSON 資料類型     | SQL Server 類型 |
| ------------------ | --------------- |
| Double             | float           |
| String             | nvarchar        |
| 二進位資料        | nvarchar        |
| 物件識別碼          | nvarchar        |
| 布林            | bit             |
| date               | Datetime2       |
| 32 位元整數     | int             |
| 時間戳記          | nvarchar        |
| 64 位元整數     | BigInt          |
|Decimal 128         | Decimal         | 
| DBPointer          | nvarchar        |
| Javascript         | nvarchar        |
| 最大索引鍵            | nvarchar        |
| 最小索引鍵            | nvarchar        |
| 符號             | nvarchar        |
| 規則運算式 | nvarchar        |
| 未定義/NULL     | nvarchar        |


MongoDB 會使用 BSON 文件來儲存資料記錄。 不同於先前的案例，BSON 為無結構描述，並支援內嵌文件和其他文件內的陣列。 這可為使用者提供彈性。 


## <a name="teradata-type-mapping-reference"></a>Teradata 類型對應參考

| Teradata 資料類型 | SQL Server 類型 | 
| -------------      | -------------   |
|INTEGER             |int              |
|SMALLINT            |SmallInt         |
|bigint              |BigInt           |
|BYTEINT             |SmallInt         |
|DECIMAL             |Decimal          |
|FLOAT               |Decimal          |
|BYTE                |二進位           |
|VARBYTE             |Varbinary        |
|BLOB                |varbinary        |
|CHAR                |Nchar            |
|CLOB                |nvarchar         |
|VARCHAR             |nvarchar         |
|Graphic             |Nchar            |
|JSON                |nvarchar         |
|VARGRAPHIC          |nvarchar         |
|DATE                |date             |
|timestamp           |Datetime2        |
|TIME                |Time             |
|TIME WITH TIME ZONE |Time             |
|TIMESTAMP WITH TIME ZONE|Time         |

::: moniker-end

## <a name="next-steps"></a>後續步驟

如需使用此項目方式的詳細資訊，請參閱 [CREATE EXTERNAL TABLE](../../t-sql/statements/create-external-table-transact-sql.md) 的 Transact-SQL 參考文章。
