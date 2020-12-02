---
description: 計算資料行的索引
title: 計算資料行的索引 | Microsoft Docs
ms.custom: ''
ms.date: 11/19/2018
ms.prod: sql
ms.prod_service: table-view-index, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- computed columns, index creation
- index creation [SQL Server], computed columns
- imprecise columns
- persisted computed columns
- precise [SQL Server]
ms.assetid: 8d17ac9c-f3af-4bbb-9cc1-5cf647e994c4
author: MikeRayMSFT
ms.author: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: ea5366a8080ccbfb4d48c8bcfda8928ed54932d1
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "88408114"
---
# <a name="indexes-on-computed-columns"></a>計算資料行的索引
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

只要符合下列要求，您就可以在計算資料行上定義索引：  
  
-   擁有權需求  
-   決定性需求  
-   有效位數需求  
-   資料類型需求  
-   SET 選項需求  
  
#### <a name="ownership-requirements"></a>擁有權需求
  
計算資料行中的所有函數參考都必須與資料表具有相同的擁有者。  
  
## <a name="determinism-requirements"></a>決定性需求  

如果運算式一定會針對指定的輸入集傳回相同的結果，這些運算式就具有決定性。 **COLUMNPROPERTY** 函數的 [IsDeterministic](../../t-sql/functions/columnproperty-transact-sql.md) 屬性會報告 *computed_column_expression* 是否具決定性。  
*computed_column_expression* 必須具決定性。 若下列全部情況成立，*computed_column_expression* 就會具決定性：  
  
-   運算式所參考的所有函數都具有決定性而且是精確的。 這些函數包括使用者自訂函數與內建函數。 如需詳細資訊，請參閱 [決定性與非決定性函數](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md)。 如果計算的資料行是 PERSISTED，函數可能就不精確。 如需詳細資訊，請參閱本主題稍後的 [在保存的計算資料行上建立索引](#BKMK_persisted) 。  
  
-   運算式中參考的所有資料行都來自包含計算資料行的資料表。  
  
-   沒有資料行參考從多個資料列中提取資料。 例如，SUM 或 AVG 這類彙總函數將取決於來自多個資料列的資料，並使得 *computed_column_expression* 不具決定性。  
  
-   *computed_column_expression* 沒有系統資料存取或使用者資料存取。  
  
任何包含 Common Language Runtime (CLR) 運算式的計算資料行都必須具有決定性，而且必須在製作索引前標示為 PERSISTED。 在計算的資料行定義中允許 CLR 使用者自訂類型的運算式。 具有 CLR 使用者自訂類型的計算資料行，只要類型是可比較的就可製作索引。 如需詳細資訊，請參閱 [CLR 使用者定義型別](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)。  

#### <a name="cast-and-convert"></a>CAST 和 CONVERT

當您在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中參考索引計算資料行內的日期資料類型字串常值時，我們建議您使用具有決定性的日期格式樣式，將常值明確轉換成您想要的日期類型。 如需具決定性之日期格式樣式的清單，請參閱 [CAST 和 CONVERT](../../t-sql/functions/cast-and-convert-transact-sql.md)。 

如需詳細資訊，請參閱[將常值日期字串轉換成 DATE 值的非決定性轉換](../../t-sql/data-types/nondeterministic-convert-date-literals.md)。

#### <a name="compatibility-level"></a>相容性層級

除非相容性層級設定為 80 或以下；否則，定序之間非 Unicode 字元資料的隱含轉換會被視為不具決定性。  

當資料庫相容性層級設定為 90 時，您就不能在包含這些運算式的計算資料行上建立索引。 但是，包含這些來自升級資料庫之運算式的現有計算資料行是可以維護的。 如果您使用包含字串到日期之隱含轉換的索引計算資料行，請確定資料庫和應用程式中 LANGUAGE 和 DATEFORMAT 設定是一致的，以避免索引損毀。

相容性層級 90 對應至 SQL Server 2005。



## <a name="precision-requirements"></a>有效位數需求
  
 *computed_column_expression* 必須精確。 若下列一或多種情況成立， *computed_column_expression* 就會精確：  
  
-   它並非 **float** 或 **real** 資料類型的運算式。  
-   它的定義中並沒有使用 **float** 或 **real** 資料類型。 例如，在下列陳述式中， `y` 資料行是 **int** 且具決定性，但並不精確。  
  
    ```sql  
    CREATE TABLE t2 (a int, b int, c int, x float,   
       y AS CASE x   
             WHEN 0 THEN a   
             WHEN 1 THEN b   
             ELSE c   
          END);  
    ```  
  
> [!NOTE]  
> 任何 **float** 或 **real** 運算式都會視為不精確，並且不能作為索引的索引鍵； **float** 或 **real** 運算式可用於索引檢視中，但不能作為索引鍵。 對於計算資料行也是如此。 若任何函數、運算式、使用者定義函數包含任何 **float** 或 **real** 運算式，均會被視為不精確。 這包含邏輯運算式 (比較)。  
  
COLUMNPROPERTY 函數的 **IsPrecise** 屬性會報告 *computed_column_expression* 是否精確。  


## <a name="data-type-requirements"></a>資料類型需求
  
-   針對計算資料行所定義的 *computed_column_expression* 並不能評估為 **text**、 **ntext** 或 **image** 資料類型。  
-   從 **image**、 **ntext**、 **text**、 **varchar(max)**、 **nvarchar(max)**、 **varbinary(max)** 以及 **xml** 資料類型所衍生的計算資料行，只要其資料類型可作為索引鍵資料行，就可以製作成索引。  
-   從 **image**、 **ntext** 以及 **text** 資料類型所衍生的計算資料行，只要其資料類型可作為非索引鍵之索引資料行，就可作為非叢集索引中無索引鍵 (內含) 的資料行。  


## <a name="set-option-requirements"></a>SET 選項需求
  
-   執行定義計算資料行的 CREATE TABLE 或 ALTER TABLE 陳述式時，ANSI_NULLS 連接層級選項必須設定為 ON。 [OBJECTPROPERTY](../../t-sql/functions/objectproperty-transact-sql.md) 函數將透過 **IsAnsiNullsOn** 屬性，報告選項是否為開啟狀態。  
-   建立索引的連接，以及嘗試執行會變更索引值之 INSERT、UPDATE 或 DELETE 陳述式的所有連線，都必須有六個 SET 選項設成 ON，以及一個選項設成 OFF。 若有任何 SELECT 陳述式是由不具相同選項設定的連接所執行，最佳化工具將略過計算資料行上的索引。  
  
    -   NUMERIC_ROUNDABORT 選項必須設為 OFF，而且下列選項必須設為 ON：  
    -   ANSI_NULLS  
    -   ANSI_PADDING  
    -   ANSI_WARNINGS  
    -   ARITHABORT  
    -   CONCAT_NULL_YIELDS_NULL  
    -   QUOTED_IDENTIFIER  
  
> [!NOTE]
> 當資料庫的相容性層級設定為 90 或以上時，將 ANSI_WARNINGS 設定為 ON 也會將 ARITHABORT 隱含設定為 ON。  
  
## <a name="creating-indexes-on-persisted-computed-columns"></a><a name="BKMK_persisted"></a> 在保存的計算資料行上建立索引  

有時候您可以建立使用具決定性但不精確運算式定義的計算資料行。 您可以在資料行於 CREATE TABLE 或 ALTER TABLE 陳述式中標記為 PERSISTED 時執行此動作。

這表示 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 會將計算值儲存在資料表中，並在更新計算資料行所根據的任何其他資料行時更新這些計算值。 當 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 在資料行上建立某索引，且查詢中參考該索引時，它會使用這些保存值。

當 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 無法證明傳回計算資料行運算式的函數 (特別是在 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]中建立的 CLR 函數) 是否具有決定性和是否精確時，此選項可讓您在計算的資料行上建立索引。  


  
## <a name="related-content"></a>相關內容  
 [COLUMNPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/columnproperty-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)    
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)
  
  
