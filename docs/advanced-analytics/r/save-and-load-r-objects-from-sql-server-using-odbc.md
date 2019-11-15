---
title: 使用 ODBC 儲存和載入 R 物件
description: RevoScaleR 套件包含序列化和還原序列化函式，可大幅改善效能，並更精簡地儲存物件。
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 98a14848db4854c0bcb19167e7fcf7d43eca5f2e
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/07/2019
ms.locfileid: "73727402"
---
# <a name="save-and-load-r-objects-from-sql-server-using-odbc"></a>從 SQL Server 使用 ODBC 儲存和載入 R 物件
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

SQL Server R Services 可以將序列化的 R 物件儲存到資料表中，並視需要從資料表載入物件；您不必重新執行 R 程式碼，或是重新定型模型。 這項可在資料庫中儲存 R 物件的功能，對下列案例來說至關重要：定型和儲存模型，以於稍後用來進行評分或分析等案例。

為了改善這項重要步驟的效能， **RevoScaleR** 套件現已包含新的序列化和還原序列化函式，可大幅改善效能，並更精簡地儲存物件。 本文將說明這些函式以及使用這些函式的方式。

## <a name="overview"></a>概觀

**RevoScaleR** 套件現已包含新的函式，可讓您更輕鬆地將 R 物件儲存到 SQL Server，然後從 SQL Server 資料表中讀取物件。 一般情況下，每個函式呼叫都會使用簡單的索引鍵值存放區，其中，索引鍵即為物件的名稱，而與索引鍵相關聯的值即為要移入或移出資料表的 varbinary R 物件。

若要直接從 R 環境中將 R 物件儲存到 SQL Server，您必須：

+ 使用 RxOdbcData  資料來源與 SQL Server 建立連線。
+ 透過 ODBC 連線呼叫新的函式
+ (選擇性) 您可以指定不要將物件序列化。 然後，選擇要使用的新壓縮演算法，而不是預設的壓縮演算法。

根據預設，您從 R 呼叫要移至 SQL Server 的任何物件，皆會受到序列化與壓縮處理。 反之，當您從 SQL Server 資料表載入物件以用於 R 程式碼時，即會將物件還原序列化與解壓縮。

## <a name="list-of-new-functions"></a>新函式清單

- `rxWriteObject` 可使用 ODBC 資料來源，將 R 物件寫入 SQL Server。

- `rxReadObject` 可使用 ODBC 資料來源，從 SQL Server 資料庫讀取 R 物件。

- `rxDeleteObject` 可將 ODBC 資料來源中指定的 R 物件，從 SQL Server 資料庫中刪除。 如果索引鍵/版本組合識別出多項物件，則會將其全部刪除。

- `rxListKeys` 會以索引鍵/值組的格式列出所有可用物件。 這可協助您決定 R 物件的名稱和版本。

如需每個函式語法的詳細說明，請參閱 R 說明。 [ScaleR 參考](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler)中也會提供詳細資料。

## <a name="how-to-store-r-objects-in-sql-server-using-odbc"></a>如何使用 ODBC 將 R 物件儲存到 SQL Server 中

此程序示範如何使用新的函式建立模型，並將它儲存到 SQL Server 中。

1. 設定 SQL Server 的連接字串。
   ```R
   conStr <- 'Driver={SQL Server};Server=localhost;Database=storedb;Trusted_Connection=true'
   ```
2. 使用連接字串，在 R 中建立 *rxOdbcData* 資料來源物件。
   ```R
   ds <- RxOdbcData(table="robjects", connectionString=conStr)
   ```

3. 如果該物件已存在，而且您不想要追蹤物件的舊版本，請刪除資料表。

   ```R
   if(rxSqlServerTableExists(ds@table, ds@connectionString)) {
       rxSqlServerDropTable(ds@table, ds@connectionString)
       }
   ```
   
4. 定義可用來儲存二進位物件的資料表。

   ```R
   ddl <- paste(" CREATE TABLE [", ds@table, "] 
      (","  [id] varchar(200) NOT NULL,
       "," [value] varbinary(max),
       "," CONSTRAINT unique_id UNIQUE (id))", 
       sep = "") 
   ```
5. 開啟 ODBC 連線以建立資料表，並在 DDL 陳述式完成時，關閉連線。

   ```R
    rxOpen(ds, "w") 
    rxExecuteSQLDDL(ds, ddl) 
    rxClose(ds)
    ```
6. 產生您想要儲存的 R 物件。

   ```R
   infertLogit <- rxLogit(case ~ age + parity + education + spontaneous + induced, 
     data = infert)
   ```
6. 使用稍早建立的 *RxOdbcData* 物件，將模型儲存至資料庫。

   ```R
   rxWriteObject(ds, "logit.model", infertLogit)
   ```

## <a name="how-to-read-r-objects-from-sql-server-using-odbc"></a>如何使用 ODBC 從 SQL Server 讀取 R 物件

此程序示範如何使用新的函式，從 SQL Server 載入模型。

1. 設定 SQL Server 的連接字串。

   ```R
   conStr2 <- 'Driver={SQL Server};Server=localhost;Database=storedb;Trusted_Connection=true'
   ```
2. 使用連接字串，在 R 中建立 *rxOdbcData* 資料來源物件。

   ```R
   ds <- RxOdbcData(table="robjects", connectionString=conStr2)
   ```
3. 指定模型的 R 物件名稱，以從資料表中讀取該模型。

   ```R
    infertLogit2 <- rxReadObject(ds, "logit.model")
   ```
