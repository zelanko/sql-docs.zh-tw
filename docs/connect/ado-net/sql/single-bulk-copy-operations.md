---
title: 單一大量複製作業
description: 描述如何使用 SqlBulkCopy 類別，在 SQL Server 的執行個體中單一大量複製資料，以及如何使用 Transact-SQL 陳述式和 SqlCommand 類別來執行大量複製作業。
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: 5e7ff0be-3f23-4996-a92c-bd54d65c3836
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: 1029d9a0121b23963ccfc12582bd9d9cc7fd6cd6
ms.sourcegitcommit: 610e49c3e1fa97056611a85e31e06ab30fd866b1
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/07/2020
ms.locfileid: "78896592"
---
# <a name="single-bulk-copy-operations"></a>單一大量複製作業

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

執行 SQL Server 大量複製作業最簡單的方式為執行對資料庫的單一作業。 根據預設，大量複製作業會做為隔離作業執行：該複製作業會以非交易的方式進行，且沒有機會復原。  
  
> [!NOTE]
>  當錯誤發生時，如果您需要復原全部或部分大量複製，您可以使用 <xref:Microsoft.Data.SqlClient.SqlBulkCopy> 受管理的交易，或執行現有交易中的大量複製作業。 如果將連線 (以隱含或明確的方式) 登記到 **System.Transactions** 交易中，則 **SqlBulkCopy** 也會使用 <xref:System.Transactions>。  
>   
>  如需詳細資訊，請參閱[交易和大量複製作業](transaction-bulk-copy-operations.md)。  
  
執行大量複製作業的一般步驟如下：  
  
1. 連接到來源伺服器，並取得要複製的資料。 如果可以從 <xref:System.Data.IDataReader> 或 <xref:System.Data.DataTable> 物件中擷取資料，則資料也可來自其他來源。  
  
2. 連線至目的伺服器 (除非您要讓 **SqlBulkCopy** 建立連線)。  
  
3. 建立 <xref:Microsoft.Data.SqlClient.SqlBulkCopy> 物件，並設定任何必要的屬性。  
  
4. 設定 **DestinationTableName** 屬性，以表示用於大量插入作業的目標資料表。  
  
5. 呼叫其中一種 **WriteToServer** 方法。  
  
6. 視需要，選擇性地更新屬性，並重新呼叫 **WriteToServer**。  
  
7. 呼叫 <xref:Microsoft.Data.SqlClient.SqlBulkCopy.Close%2A>，或將大量複製作業包裝在 `Using` 陳述式內。  
  
> [!CAUTION]
>  我們建議來源和目標資料行的資料類型必須相符。 如果資料類型不相符，則 **SqlBulkCopy** 會嘗試使用 <xref:Microsoft.Data.SqlClient.SqlParameter.Value%2A> 所使用的規則，將每個來源值轉換為目標資料類型。 轉換可能會影響效能，並也可能會導致未預期的錯誤。 例如，`Double` 資料類型大多可以轉換成 `Decimal` 資料類型，但並非總是如此。  
  
## <a name="example"></a>範例  
下列主控台應用程式示範如何使用 <xref:Microsoft.Data.SqlClient.SqlBulkCopy> 類別載入資料。 在這個範例中，<xref:Microsoft.Data.SqlClient.SqlDataReader> 用於從 SQL Server **AdventureWorks** 資料庫的 **Production.Product** 資料表，將資料複製到同一資料庫中的類似資料表中。  
  
> [!IMPORTANT]
>  除非您已如[大量複製範例設定](bulk-copy-example-setup.md)中所述建立工作資料表，否則此範例不會執行。 這個程式碼僅是為了示範使用 **SqlBulkCopy** 的語法而提供。 如果來源和目的地資料表位於相同的 SQL Server 執行個體，則使用 Transact-SQL `INSERT … SELECT` 陳述式來複製資料會更方便且快速。  
  
[!code-csharp[DataWorks SqlBulkCopy_WriteToServer#1](~/../sqlclient/doc/samples/SqlBulkCopy_WriteToServer.cs#1)]
  
## <a name="performing-a-bulk-copy-operation-using-transact-sql-and-the-command-class"></a>使用 Transact-SQL 和命令類別執行大量複製作業  
以下範例將示範如何使用 <xref:Microsoft.Data.SqlClient.SqlCommand.ExecuteNonQuery%2A> 方法來執行 BULK INSERT 陳述式。  
  
> [!NOTE]
>  資料來源的檔案路徑是與伺服器相對的。 伺服器處理序必須存取該路徑，藉此順利完成大量複製作業。  
  
```csharp  
using (SqlConnection connection = New SqlConnection(connectionString))  
{  
string queryString =  "BULK INSERT Northwind.dbo.[Order Details] " +  
    "FROM 'f:\mydata\data.tbl' " +  
    "WITH ( FORMATFILE='f:\mydata\data.fmt' )";  
connection.Open();  
SqlCommand command = new SqlCommand(queryString, connection);  
  
command.ExecuteNonQuery();  
}  
```  
  
## <a name="next-steps"></a>後續步驟
- [SQL Server 中的大量複製作業](bulk-copy-operations-sql-server.md)
