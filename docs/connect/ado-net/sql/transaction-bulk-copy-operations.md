---
title: 交易和大量複製作業
description: 描述如何在交易內執行大量複製作業，包括如何認可或復原交易。
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: f6f0cbc9-f7bf-4d6e-875f-ad1ba0b4aa62
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: 465870aa05b97b841a23c0ca1843e3de395a0b8b
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "75233804"
---
# <a name="transaction-and-bulk-copy-operations"></a>交易和大量複製作業

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[下載 ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

大量複製作業可以做為隔離作業或做為多步驟交易的一部分執行。 這第二個選項可讓您執行相同交易內的多項大量複製作業，以及執行其他資料庫作業 (例如插入、更新和刪除)，同時仍然能夠認可或回復整個交易。  
  
根據預設，大量複製作業會做為隔離作業執行。 該複製作業會以非交易的方式進行，且沒有機會復原。 如果需要在發生錯誤時，復原全部或部分大量複製，您可以使用 <xref:Microsoft.Data.SqlClient.SqlBulkCopy> 管理的交易，在現有交易內執行大量複製作業，或在 **System.Transactions**<xref:System.Transactions.Transaction> 中登記。  
  
## <a name="performing-a-non-transacted-bulk-copy-operation"></a>執行非交易大量複製作業  
對於非交易大量複製作業在作業過程遭遇錯誤時的狀況，下列主控台應用程式顯示此時會發生什麼事。  
  
在範例中，來源資料表及目標資料表都包含名為 **ProductID** 的 `Identity` 資料行。 程式碼會先準備目的地資料表，方法是刪除所有資料列，然後插入單一資料列，且其 **ProductID** 已知存在於來源資料表中。 根據預設，在目的地資料表中，會針對每個新增的資料列產生 `Identity` 資料行的新值。 在此範例中，當此連接開啟時，且其強制大量載入處理序改為使用來源資料表中的 `Identity` 值時，就會設定某個選項。  
  
此大量複製作業執行時的 <xref:Microsoft.Data.SqlClient.SqlBulkCopy.BatchSize%2A> 屬性設定為 10。 當此作業遇到無效的資料列時，就會擲回例外狀況。 在第一個範例中，大量複製作業會為非交易作業。 發生錯誤前複製的所有批次均已認可；包含重複索引鍵的批次已回復，而且大量複製作業會在處理任何其他批次之前暫止。  
  
> [!NOTE]
>  除非您已如[大量複製範例設定](bulk-copy-example-setup.md)中所述建立工作資料表，否則此範例不會執行。 這個程式碼僅是為了示範使用 **SqlBulkCopy** 的語法而提供。 如果來源和目的地資料表位於相同的 SQL Server 執行個體，則使用 Transact-SQL `INSERT … SELECT` 陳述式來複製資料會更方便且快速。  
  
[!code-csharp[DataWorks SqlBulkCopyOpeions_Default#1](~/../sqlclient/doc/samples/SqlBulkCopyOptions_Default.cs#1)]
  
## <a name="performing-a-dedicated-bulk-copy-operation-in-a-transaction"></a>在交易中執行專用大量複製作業  
根據預設，大量複製作業為其自己的交易。 當您要執行專用大量複製作業時，請建立具有連接字串的新 <xref:Microsoft.Data.SqlClient.SqlBulkCopy> 執行個體，或使用不含使用中交易的現有 <xref:Microsoft.Data.SqlClient.SqlConnection> 物件。 在每個案例中，大量複製作業會先建立，然後再認可或回復此交易。  
  
您可以明確指定 <xref:Microsoft.Data.SqlClient.SqlBulkCopy> 類別建構函式中的 <xref:Microsoft.Data.SqlClient.SqlBulkCopyOptions.UseInternalTransaction> 選項，以便明確地讓大量複製作業在自己的交易中執行，使得大量複製作業的每個批次在個別的交易內執行。  
  
> [!NOTE]
>  由於不同的批次在不同交易中執行，如果大量複製作業期間發生錯誤時，目前的批次中的所有資料列將會回復，但是先前批次的資料列將保留在資料庫中。  
  
下列主控台應用程式類似於前一個範例，但有一個例外狀況：在此範例中，大量複製作業會管理自己的交易。 發生錯誤前複製的所有批次均已認可；包含重複索引鍵的批次已回復，而且大量複製作業會在處理任何其他批次之前暫止。  
  
> [!IMPORTANT]
>  除非您已如[大量複製範例設定](bulk-copy-example-setup.md)中所述建立工作資料表，否則此範例不會執行。 這個程式碼僅是為了示範使用 **SqlBulkCopy** 的語法而提供。 如果來源和目的地資料表位於相同的 SQL Server 執行個體，則使用 Transact-SQL `INSERT … SELECT` 陳述式來複製資料會更方便且快速。  
  
[!code-csharp[DataWorks SqlBulkCopyOptions_UseInternalTransaction#1](~/../sqlclient/doc/samples/SqlBulkCopyOptions_UseInternalTransaction.cs#1)]
  
## <a name="using-existing-transactions"></a>使用現有的交易  
您可以在 <xref:Microsoft.Data.SqlClient.SqlBulkCopy> 建構函式中，將現有的 <xref:Microsoft.Data.SqlClient.SqlTransaction> 物件指定為參數。 在此情況下，大量複製作業會在現有的交易中執行，而且不會變更交易狀態 (也就是其尚未認可或中止)。 這可讓應用程式在其他資料庫作業的交易中包含大量複製作業。 不過，如果您未指定 <xref:Microsoft.Data.SqlClient.SqlTransaction> 物件並傳遞了 Null 參考，而且連線具有使用中交易，則會擲回例外狀況。  
  
如果因為發生錯誤，或大量複製應該要以可復原之較大處理序的一部分來執行，而使得您需要復原整個大量複製作業，則您可以將 <xref:Microsoft.Data.SqlClient.SqlTransaction> 物件提供給 <xref:Microsoft.Data.SqlClient.SqlBulkCopy> 建構函式。  
  
下列主控台應用程式與第一個 (非交易) 範例類似，但有一項例外：在此範例中，大量複製作業包含在較大的外部交易中。 當發生主要索引鍵違規錯誤時，整個交易便會回復，並且沒有任何資料列會加入目的地資料表。  
  
> [!IMPORTANT]
>  除非您已如[大量複製範例設定](bulk-copy-example-setup.md)中所述建立工作資料表，否則此範例不會執行。 這個程式碼僅是為了示範使用 **SqlBulkCopy** 的語法而提供。 如果來源和目的地資料表位於相同的 SQL Server 執行個體，則使用 Transact-SQL `INSERT … SELECT` 陳述式來複製資料會更方便且快速。  
  
[!code-csharp[DataWorks SqlBulkCopy_ExternalTransaction#1](~/../sqlclient/doc/samples/SqlBulkCopy_ExternalTransaction.cs#1)]
  
## <a name="next-steps"></a>後續步驟
- [SQL Server 中的大量複製作業](bulk-copy-operations-sql-server.md)
