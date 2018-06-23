---
title: 計算資料行的索引 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-indexes
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- computed columns, index creation
- index creation [SQL Server], computed columns
- imprecise columns
- persisted computed columns
- precise [SQL Server]
ms.assetid: 8d17ac9c-f3af-4bbb-9cc1-5cf647e994c4
caps.latest.revision: 41
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 9b7d9b25ccb9404011c459ba0275f2ba0c63746a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36032770"
---
# <a name="indexes-on-computed-columns"></a>計算資料行的索引
  只要符合下列要求，您就可以在計算資料行上定義索引：  
  
-   擁有權需求  
  
-   決定性需求  
  
-   有效位數需求  
  
-   資料類型需求  
  
-   SET 選項需求  
  
 **Ownership Requirements**  
  
 計算資料行中的所有函數參考都必須與資料表具有相同的擁有者。  
  
 **Determinism Requirements**  
  
> [!IMPORTANT]  
>  如果運算式一定會針對指定的輸入集傳回相同的結果，這些運算式就具有決定性。 **COLUMNPROPERTY** 函數的 [IsDeterministic](/sql/t-sql/functions/columnproperty-transact-sql) 屬性會報告 *computed_column_expression* 是否具決定性。  
  
 *computed_column_expression* 必須具決定性。 若下列一或多種情況成立， *computed_column_expression* 就會具決定性：  
  
-   運算式所參考的所有函數都具有決定性而且是精確的。 這些函數包括使用者自訂函數與內建函數。 如需詳細資訊，請參閱 [決定性與非決定性函數](../user-defined-functions/deterministic-and-nondeterministic-functions.md)。 如果計算的資料行是 PERSISTED，函數可能就不精確。 如需詳細資訊，請參閱本主題稍後的 [在保存的計算資料行上建立索引](#BKMK_persisted) 。  
  
-   運算式中參考的所有資料行都來自包含計算資料行的資料表。  
  
-   沒有資料行參考從多個資料列中提取資料。 例如，SUM 或 AVG 這類彙總函數將取決於來自多個資料列的資料，並使得 *computed_column_expression* 不具決定性。  
  
-   *computed_column_expression* 沒有系統資料存取或使用者資料存取。  
  
 任何包含 Common Language Runtime (CLR) 運算式的計算資料行都必須具有決定性，而且必須在製作索引前標示為 PERSISTED。 在計算的資料行定義中允許 CLR 使用者自訂類型的運算式。 具有 CLR 使用者自訂類型的計算資料行，只要類型是可比較的就可製作索引。 如需詳細資訊，請參閱 [CLR 使用者定義型別](../clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)。  
  
> [!NOTE]  
>  當您在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中參考索引計算資料行內的日期資料類型字串常值時，我們建議您使用具有決定性的日期格式樣式，將常值明確轉換成您想要的日期類型。 如需具決定性之日期格式樣式的清單，請參閱 [CAST 和 CONVERT](/sql/t-sql/functions/cast-and-convert-transact-sql)。 除非資料庫相容性層級設定為 80 或以下，否則牽涉到將字元字串隱含轉換成日期資料類型的運算式都會視為不具決定性。 這是因為結果需視伺服器工作階段的 [LANGUAGE](/sql/t-sql/statements/set-language-transact-sql) 和 [DATEFORMAT](/sql/t-sql/statements/set-dateformat-transact-sql) 設定而定。 例如，運算式 `CONVERT (datetime, '30 listopad 1996', 113)` 的結果需視 LANGUAGE 設定而定，因為字串 '`30 listopad 1996`' 在不同的語言中表示不同的月份。 同樣地，在運算式 `DATEADD(mm,3,'2000-12-01')`中，「 [!INCLUDE[ssDE](../../../includes/ssde-md.md)] 」會根據 DATEFORMAT 設定來解譯 `'2000-12-01'` 字串。  
>   
>  除非相容性層級設定為 80 或以下，否則，定序之間的非 Unicode 字元資料的隱含轉換被視為不具決定性。  
>   
>  當資料庫相容性層級設定為 90 時，您就不能在包含這些運算式的計算資料行上建立索引。 但是，包含這些來自升級資料庫之運算式的現有計算資料行是可以維護的。 如果您使用包含字串到日期之隱含轉換的索引計算資料行，請確定資料庫和應用程式中 LANGUAGE 和 DATEFORMAT 設定是一致的，以避免索引損毀。  
  
 **Precision Requirements**  
  
 *computed_column_expression* 必須精確。 若下列一或多種情況成立， *computed_column_expression* 就會精確：  
  
-   它並非 `float` 或 `real` 資料類型的運算式。  
  
-   它不會使用`float`或`real`其定義中的資料類型。 例如，下列陳述式，在資料行`y`是`int`且具決定性，但不是精確。  
  
    ```  
    CREATE TABLE t2 (a int, b int, c int, x float,   
       y AS CASE x   
             WHEN 0 THEN a   
             WHEN 1 THEN b   
             ELSE c   
          END);  
    ```  
  
> [!NOTE]  
>  任何`float`或`real`運算式被視為不精確，並且不能的索引鍵;`float`或`real`運算式可用於索引檢視中，但不是做為索引鍵。 對於計算資料行也是如此。 任何函式、 運算式或使用者定義函式會被視為不精確，如果它包含任何`float`或`real`運算式。 這包含邏輯運算式 (比較)。  
  
 COLUMNPROPERTY 函數的 **IsPrecise** 屬性會報告 *computed_column_expression* 是否精確。  
  
 **Data Type Requirements**  
  
-   *Computed_column_expression*中定義的計算資料行不能評估為`text`， `ntext`，或`image`資料型別。  
  
-   計算資料行，衍生自`image`， `ntext`， `text`， `varchar(max)`， `nvarchar(max)`， `varbinary(max)`，和`xml`，只要計算資料行資料類型時，才允許做為索引鍵資料行，可以進行索引的資料類型。  
  
-   計算資料行，衍生自`image`， `ntext`，和`text`資料類型可以是在非叢集索引的非索引鍵 （內含） 資料行，只要計算資料行資料類型時，才允許非索引鍵索引資料行。  
  
 **SET Option Requirements**  
  
-   執行定義計算資料行的 CREATE TABLE 或 ALTER TABLE 陳述式時，ANSI_NULLS 連接層級選項必須設定為 ON。 [OBJECTPROPERTY](/sql/t-sql/functions/objectpropertyex-transact-sql) 函數將透過 **IsAnsiNullsOn** 屬性，報告選項是否為開啟狀態。  
  
-   建立索引的連接，以及嘗試執行會變更索引值之 INSERT、UPDATE 或 DELETE 陳述式的所有連線，都必須有六個 SET 選項設成 ON，以及一個選項設成 OFF。 若有任何 SELECT 陳述式是由不具相同選項設定的連接所執行，最佳化工具將略過計算資料行上的索引。  
  
    -   NUMERIC_ROUNDABORT 選項必須設為 OFF，而且下列選項必須設為 ON：  
  
    -   ANSI_NULLS  
  
    -   ANSI_PADDING  
  
    -   ANSI_WARNINGS  
  
    -   ARITHABORT  
  
    -   CONCAT_NULL_YIELDS_NULL  
  
    -   QUOTED_IDENTIFIER  
  
     當資料庫的相容性層級設定為 90 或以上時，將 ANSI_WARNINGS 設定為 ON 也會將 ARITHABORT 隱含設定為 ON。  
  
##  <a name="BKMK_persisted"></a> 在保存的計算資料行上建立索引  
 如果計算的資料行在 CREATE TABLE 或 ALTER TABLE 陳述式中是標示成 PERSISTED，就可在以具有決定性但不精確的運算式所定義的計算資料行上建立索引。 這表示[!INCLUDE[ssDE](../../../includes/ssde-md.md)]且在查詢中參考該索引資料行上建立索引時，使用這些保存的值。 此選項可讓您在計算資料行上建立索引時[!INCLUDE[ssDE](../../../includes/dnprdnshort-md.md)]，是具決定性且精確。  
  
## <a name="related-content"></a>相關內容  
 [COLUMNPROPERTY &#40;Transact-SQL&#41;](/sql/t-sql/functions/columnproperty-transact-sql)  
  
  
