---
title: 透過 CLR UDT 來模擬記錄與集合
description: 涵蓋 Oracle 的 SQL Server 移轉小幫手（SSMA）如何使用 SQL Server Common Language Runtime （CLR）使用者定義資料類型（UDT）來模擬 Oracle 記錄和集合。
authors: nahk-ivanov
ms.service: ssma
ms.devlang: sql
ms.topic: article
ms.date: 1/22/2020
ms.author: alexiva
ms.openlocfilehash: 39a7e8d59425db7ce2d7e81083012321caac35ef
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "76762812"
---
# <a name="emulating-records-and-collections-via-clr-udt"></a>透過 CLR UDT 來模擬記錄與集合

本文涵蓋 Oracle 的 SQL Server 移轉小幫手（SSMA）如何使用 SQL Server Common Language Runtime （CLR）使用者定義資料類型（UDT）來模擬 Oracle 記錄和集合。

## <a name="declaring-record-or-collection-types-and-variables"></a>宣告記錄或集合類型和變數

SSMA 會建立三個以 CLR 為基礎的 Udt：

* `CollectionIndexInt`
* `CollectionIndexString`
* `Record`

此`CollectionIndexInt`類型適用于模擬以整數編制索引的集合，例如`VARRAY`s、嵌套資料表和以整數為基礎的關聯陣列。 `CollectionIndexString`型別用於以字元索引鍵編制索引的關聯陣列。 Oracle 記錄功能是由`Record`類型模擬。

記錄或集合類型的所有宣告都會轉換成此 Transact-sql 宣告：

```sql
declare @Collection$TYPE varchar(max) = '<type definition>'
```

以下`<type definition>`是可唯一識別來源 PL/SQL 類型的描述性文字。

請考慮下列範例：

```sql
DECLARE
    TYPE Manager IS RECORD
    (
        mgrid integer,
        mgrname varchar2(40),
        hiredate date
    );

    TYPE Manager_table is TABLE OF Manager INDEX BY PLS_INTEGER;

    Mgr_rec Manager;
    Mgr_table_rec Manager_table;
BEGIN
    mgr_rec.mgrid := 1;
    mgr_rec.mgrname := 'Mike';
    mgr_rec.hiredate := sysdate;

    select
        empno,
        ename,
        hiredate
    BULK COLLECT INTO
        mgr_table_rec
    FROM
        emp;
END;
```

使用 SSMA 進行轉換時，會變成下列 Transact-sql 程式碼：

```sql
BEGIN
    DECLARE
        @CollectionIndexInt$TYPE varchar(max) =
            ' TABLE INDEX BY INT OF ( RECORD ( MGRID INT , MGRNAME STRING , HIREDATE DATETIME ) )'

    DECLARE
        @Mgr_rec$mgrid int,
        @Mgr_rec$mgrname varchar(40),
        @Mgr_rec$hiredate datetime2(0),
        @Mgr_table_rec dbo.CollectionIndexInt =
            dbo.CollectionIndexInt::[Null].SetType(@CollectionIndexInt$TYPE)

    SET @mgr_rec$mgrid = 1
    SET @mgr_rec$mgrname = 'Mike'
    SET @mgr_rec$hiredate = sysdatetime()

    SET @mgr_table_rec = @mgr_table_rec.RemoveAll()
    SET @mgr_table_rec =
        @mgr_table_rec.AssignData(
            ssma_oracle.fn_bulk_collect2CollectionComplex((
                SELECT
                    CAST(EMP.EMPNO AS int) AS mgrid,
                    EMP.ENAME AS mgrname,
                    EMP.HIREDATE AS hiredate
                FROM dbo.EMP
                FOR XML PATH
            ))
        )
END
```

在這裡，由於`Manager`資料表與數值索引（`INDEX BY PLS_INTEGER`）相關聯，因此所使用的對應 t-sql 宣告的類型`@CollectionIndexInt$TYPE`為。 如果資料表與字元集索引相關聯（例如`VARCHAR2`），則對應的 t-sql 宣告會是下列類型： `@CollectionIndexString$TYPE`

```sql
-- Oracle
TYPE Manager_table is TABLE OF Manager INDEX BY VARCHAR2(40);

-- SQL Server
@CollectionIndexString$TYPE varchar(max) =
    ' TABLE INDEX BY STRING OF ( RECORD ( MGRID INT , MGRNAME STRING , HIREDATE DATETIME ) )'
```

Oracle 記錄功能僅由`Record`類型模擬。

、 `CollectionIndexInt`、和`CollectionIndexString` `Record`這兩種類型都有一個靜態屬性`[Null]` ，會傳回空的實例。 呼叫`SetType`方法來接收特定類型的空物件（如上述範例所示）。

## <a name="constructor-call-conversions"></a>函式呼叫轉換

函式標記法只能用於嵌套的資料表和`VARRAY`，因此所有的明確函式呼叫都會使用`CollectionIndexInt`類型進行轉換。 空白的函式呼叫會透過`SetType`在的 null 實例上叫`CollectionIndexInt`用的呼叫來轉換。 `[Null]`屬性會傳回 null 實例。 如果此函式包含專案清單，則會依序套用特殊方法呼叫，以將值新增至集合。

例如：

```sql
-- Oracle

DECLARE
    TYPE nested_type IS TABLE OF VARCHAR2(20);
    TYPE varray_type IS VARRAY(5) OF INTEGER;

    v1 nested_type;
    v2 varray_type;
BEGIN
   v1 := nested_type('Arbitrary','number','of','strings');
   v2 := varray_type(10, 20, 40, 80, 160);
END;

-- SQL Server

BEGIN
    DECLARE
        @CollectionIndexInt$TYPE varchar(max) = ' VARRAY OF INT',
        @CollectionIndexInt$TYPE$2 varchar(max) = ' TABLE OF STRING',
        @v1 dbo.CollectionIndexInt,
        @v2 dbo.CollectionIndexInt

    SET @v1 =
        dbo.CollectionIndexInt::[Null]
            .SetType(@CollectionIndexInt$TYPE$2)
            .AddString('Arbitrary')
            .AddString('number')
            .AddString('of')
            .AddString('strings')

   SET @v2 =
       dbo.CollectionIndexInt::[Null]
            .SetType(@CollectionIndexInt$TYPE)
            .AddInt(10)
            .AddInt(20)
            .AddInt(40)
            .AddInt(80)
            .AddInt(160)
END
```

## <a name="referencing-and-assigning-record-and-collection-elements"></a>參考和指派記錄和集合元素

每個 Udt 都有一組方法，可使用各種資料類型的元素。 例如， `SetDouble`方法會將`float(53)`值指派給 record 或 collection，而且`GetDouble`可以讀取此值。 以下是完整的方法清單：

```sql
GetCollectionIndexInt(@key <KeyType>) returns CollectionIndexInt;
SetCollectionIndexInt(@key <KeyType>, @value CollectionIndexInt) returns <UDT_type>;
GetCollectionIndexString(@key <KeyType>) returns CollectionIndexString;
SetCollectionIndexString(@key <KeyType>, @value CollectionIndexString) returns <UDT_type>;
Record GetRecord(@key <KeyType>) returns Record;
SetRecord(@key <KeyType>, @value Record) returns <UDT_type>;
GetString(@key <KeyType>) returns nvarchar(max);
SetString(@key <KeyType>, @value nvarchar(max)) returns nvarchar(max);
GetDouble(@key <KeyType>) returns float(53);
SetDouble(@key <KeyType>, @value float(53)) returns <UDT_type>;
GetDatetime(@key <KeyType>) returns datetime;
SetDatetime(@key <KeyType>, @value datetime) returns <UDT_type>;
GetVarbinary(@key <KeyType>) returns varbinary(max);
SetVarbinary(@key <KeyType>, @value varbinary(max)) returns <UDT_type>;
SqlDecimal GetDecimal(@key <KeyType>);
SetDecimal(@key <KeyType>, @value numeric) returns <UDT_type>;
GetXml(@key <KeyType>) returns xml;
SetXml(@key <KeyType>, @value xml) returns <UDT_type>;
GetInt(@key <KeyType>) returns bigint;
SetInt(@key <KeyType>, @value bigint) returns <UDT_type>;
```

這些方法會在參考或指派值給集合/記錄的元素時使用。

```sql
-- Oracle
a_collection(i) := 'VALUE';

-- SQL Server
SET @a_collection = @a_collection.SetString(@i, 'VALUE');
```

轉換具有 record 元素的多維度集合或集合的指派語句時，SSMA 會加入下列方法來參考 set 方法內的父項目：

```sql
GetOrCreateCollectionIndexInt(@key <KeyType>) returns CollectionIndexInt;
GetOrCreateCollectionIndexString(@key <KeyType>) returns CollectionIndexString;
GetOrCreateRecord(@key <KeyType>) returns Record;
```

例如，記錄元素的集合是以這種方式建立：

```sql
-- Oracle
DECLARE
    TYPE rec_details IS RECORD (id int, name varchar2(20));
    TYPE ntb1 IS TABLE of rec_details index BY binary_integer;
    c ntb1;
BEGIN
    c(1).id := 1;
END;

-- SQL Server
DECLARE
   @CollectionIndexInt$TYPE varchar(max) =
       ' TABLE INDEX BY INT OF ( RECORD ( ID INT , NAME STRING ) )',
   @c dbo.CollectionIndexInt =
       dbo.CollectionIndexInt::[Null].SetType(@CollectionIndexInt$TYPE)

SET @c = @c.SetRecord(1, @c.GetOrCreateRecord(1).SetInt(N'ID', 1))
```

## <a name="collection-built-in-methods"></a>集合內建方法

SSMA 會使用下列 UDT 方法來模擬 PL/SQL 集合的內建方法。

Oracle 收集方法 | `CollectionIndexInt`和`CollectionIndexString`對等
--- | ---
COUNT | `Count returns int`
刪除 | `RemoveAll() returns <UDT_type>`
刪除（n） | `Remove(@index int) returns <UDT_type>`
DELETE （m，n） | `RemoveRange(@indexFrom int, @indexTo int) returns <UDT_type>`
EXISTS | `ContainsElement(@index int) returns bit`
延遲 | `Extend() returns <UDT_type>`
擴充（n） | `Extend() returns <UDT_type>`
EXTEND （n，i） | `ExtendDefault(@count int, @def int) returns <UDT_type>`
FIRST | `First() returns int`
LAST | `Last() returns int`
LIMIT | N/A
PRIOR | `Prior(@current int) returns int`
NEXT | `Next(@current int) returns int`
TRIM | `Trim() returns <UDT_type>`
TRIM （n） | `TrimN(@count int) returns <UDT_type>`

## <a name="bulk-collect-operation"></a>大量收集作業

SSMA 會`BULK COLLECT INTO`將語句轉換`SELECT ... FOR XML PATH`成 SQL Server 語句，其結果會包裝成下列其中一個函數：

* `ssma_oracle.fn_bulk_collect2CollectionSimple`
* `ssma_oracle.fn_bulk_collect2CollectionComplex`

選擇取決於目標物件的類型。 這些函式會傳回可由`CollectionIndexInt`、 `CollectionIndexString`和`Record`類型剖析的 XML 值。 特殊`AssignData`函式會將以 XML 為基礎的集合指派給 UDT。

SSMA 會辨識三種`BULK COLLECT INTO`語句。

### <a name="the-collection-contains-elements-with-scalar-types-and-the-select-list-contains-one-column"></a>集合包含具有純量類型的元素，且`SELECT`清單包含一個資料行

```sql
-- Oracle
SELECT column_name_1
BULK COLLECT INTO <collection_name_1>
FROM <data_source>

-- SQL Server
SET @<collection_name_1> =
    @<collection_name_1>.AssignData(
        ssma_oracle.fn_bulk_collect2CollectionSimple(
            (SELECT column_name_1 FROM <data_source> FOR XML PATH)))
```

### <a name="the-collection-contains-elements-with-record-types-and-the-select-list-contains-one-column"></a>集合包含具有記錄類型的元素，且`SELECT`清單包含一個資料行

```sql
-- Oracle
SELECT
    column_name_1[, column_name_2...]
BULK COLLECT INTO
    <collection_name_1>
FROM
    <data_source>

-- SQL Server
SET @<collection_name_1> =
    @<collection_name_1>.AssignData(
        ssma_oracle.fn_bulk_collect2CollectionComplex(
            (SELECT
                column_name_1 as [collection_name_1_element_field_name_1],
                column_name_2 as [collection_name_1_element_field_name_2]
            FROM <data_source>
            FOR XML PATH)))
```

### <a name="the-collection-contains-elements-with-scalar-type-and-the-select-list-contains-multiple-columns"></a>集合包含具有純量類型的元素，且`SELECT`清單包含多個資料行

```sql
-- Oracle
SELECT
    column_name_1[, column_name_2 ...]
BULK COLLECT INTO
    <collection_name_1>[, <collection_name_2> ...]
FROM
    <data_source>

-- SQL Server
;WITH bulkC AS (
    SELECT
        column_name_1 [collection_name_1_element_field_name_1],
        column_name_2 [collection_name_1_element_field_name_2]
    FROM
        <data_source>
)
SELECT
    @<collection_name_1> =
        @<collection_name_1>.AssignData(
            ssma_oracle.fn_bulk_collect2CollectionSimple(
                (SELECT
                    [collection_name_1_element_field_name_1]
                FROM
                    bulkC
                FOR XML PATH))),
    @<collection_name_2> =
        @<collection_name_2>.AssignData(
            ssma_oracle.fn_bulk_collect2CollectionSimple(
                (SELECT
                    [collection_name_1_element_field_name_2]
                FROM bulkC
                FOR XML PATH)))
```

## <a name="select-into-record"></a>選取記錄

當 Oracle 查詢的結果儲存在 PL/SQL 記錄變數中時，您有兩個選項取決於 [轉換記錄] 的 [SSMA] 設定，**做為分隔變數清單**（可在 [**工具**] 功能表、[**專案設定**]、 **[一般** -> **轉換**] 底下取得）。 如果此設定的值為 **[是]** （預設值），則 SSMA 不會建立記錄類型的實例。 相反地，它會將記錄分割成構成欄位，方法是為每個記錄欄位建立個別的 Transact-sql 變數。 如果設定為 [**否**]，則會具現化記錄，並使用`Set`方法為每個欄位指派一個值。
