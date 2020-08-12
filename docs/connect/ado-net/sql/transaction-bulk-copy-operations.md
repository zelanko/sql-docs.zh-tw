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
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-kaywon
ms.openlocfilehash: 685bb349366ad955248a05e23ec030788dcbc63d
ms.sourcegitcommit: 6b3569977b034554883a94d73d1c4df6e2f74fe2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2020
ms.locfileid: "85106916"
---
# <a name="transaction-and-bulk-copy-operations"></a>交易和大量複製作業

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

大量複製作業可以做為隔離作業或做為多步驟交易的一部分執行。 這第二個選項可供執行相同交易內的多項大量複製作業，以及執行其他插入、更新和刪除等資料庫作業，同時仍然能夠認可或回復整個交易。  
  
根據預設，大量複製作業會作為隔離作業完成。 該複製作業會以非交易的方式進行，且沒有機會復原。 如果需要在發生錯誤時復原全部或部分大量複製，您可以：

 - 使用 <xref:Microsoft.Data.SqlClient.SqlBulkCopy> 管理的交易

 - 在現有交易中執行大量複製作業

 - 在 **System.Transactions** <xref:System.Transactions.Transaction> 中登錄。  
  
## <a name="performing-a-non-transacted-bulk-copy-operation"></a>執行非交易大量複製作業  
對於非交易大量複製作業在作業過程遭遇錯誤時的狀況，下列主控台應用程式顯示此時會發生什麼事。  
  
在範例中，來源資料表及目標資料表都包含名為 **ProductID** 的 `Identity` 資料行。 程式碼會先準備目的地資料表，方法是刪除所有資料列，然後插入單一資料列，且其 **ProductID** 已知存在於來源資料表中。 根據預設，在目的地資料表中，會針對每個新增的資料列產生 `Identity` 資料行的新值。 在此範例中，當此連接開啟時，且其強制大量載入處理序改為使用來源資料表中的 `Identity` 值時，就會設定某個選項。  
  
此大量複製作業執行時的 <xref:Microsoft.Data.SqlClient.SqlBulkCopy.BatchSize%2A> 屬性設定為 10。 當此作業遇到無效的資料列時，就會擲回例外狀況。 在第一個範例中，大量複製作業會為非交易作業。 所有出錯之前的複製批次都會被認可。 包含重複索引鍵的批次會回復，而大量複製作業會暫停，直到處理完任何剩餘的批次。  
  
> [!NOTE]
>  除非您已如[大量複製範例設定](bulk-copy-example-setup.md)中所述建立工作資料表，否則此範例不會執行。 這個程式碼僅是為了示範使用 **SqlBulkCopy** 的語法而提供。 如果來源和目的地資料表位於相同的 SQL Server 執行個體，則使用 Transact-SQL `INSERT … SELECT` 陳述式來複製資料會更方便且快速。  
  
[!code-csharp[DataWorks SqlBulkCopyOptions_Default#1](~/../sqlclient/doc/samples/SqlBulkCopyOptions_Default.cs#1)]
  
## <a name="performing-a-dedicated-bulk-copy-operation-in-a-transaction"></a>在交易中執行專用大量複製作業  
根據預設，大量複製作業為其自己的交易。 當要執行專用大量複製作業時，請建立具有連接字串的 <xref:Microsoft.Data.SqlClient.SqlBulkCopy> 執行個體，或使用不含使用中交易的現有 <xref:Microsoft.Data.SqlClient.SqlConnection> 物件。 大量複製作業會先在每個案例中建立交易，再認可或回復此交易。  
  
您可在 <xref:Microsoft.Data.SqlClient.SqlBulkCopy> 類別的建構函式中明確指定 <xref:Microsoft.Data.SqlClient.SqlBulkCopyOptions.UseInternalTransaction> 選項，以在其自己的交易中執行大量複製作業。 每個批次的作業會在個別交易內執行。  
  
> [!NOTE]
>  由於不同的批次在不同交易中執行，如果大量複製作業期間發生錯誤時，目前的批次中的所有資料列將會回復，但是先前批次的資料列將保留在資料庫中。  
  
在下方的主控台應用程式中，除了大量複製作業會自行管理本身的交易外，其餘部分均與前述範例類似。 所有出錯之前的複製批次都會被認可。 包含重複索引鍵的批次會回復，而大量複製作業會暫停，直到處理完任何剩餘的批次。 
  
> [!IMPORTANT]
>  除非您已如[大量複製範例設定](bulk-copy-example-setup.md)中所述建立工作資料表，否則此範例不會執行。 這個程式碼僅是為了示範使用 **SqlBulkCopy** 的語法而提供。 如果來源和目的地資料表位於相同的 SQL Server 執行個體，則使用 Transact-SQL `INSERT … SELECT` 陳述式來複製資料會更方便且快速。  
  
[!code-csharp[DataWorks SqlBulkCopyOptions_UseInternalTransaction#1](~/../sqlclient/doc/samples/SqlBulkCopyOptions_UseInternalTransaction.cs#1)]
  
## <a name="using-existing-transactions"></a>使用現有的交易  
您可以在 <xref:Microsoft.Data.SqlClient.SqlBulkCopy> 建構函式中，將現有的 <xref:Microsoft.Data.SqlClient.SqlTransaction> 物件指定為參數。 在此情況下，大量複製作業會在現有的交易中完成，且不會變更交易狀態，也就是其尚未認可或中止。 此方法可供應用程式在其他資料庫作業的交易中包含大量複製作業。 不過，如果您未指定 <xref:Microsoft.Data.SqlClient.SqlTransaction> 物件並傳遞了 Null 參考，而且連線具有使用中交易，則會擲回例外狀況。   
  
如果因為發生錯誤，或大量複製應該要以可復原之較大處理序的一部分來執行，而使得您需要復原整個大量複製作業，則您可以將 <xref:Microsoft.Data.SqlClient.SqlTransaction> 物件提供給 <xref:Microsoft.Data.SqlClient.SqlBulkCopy> 建構函式。  
  
下列主控台應用程式與第一個 (非交易) 範例類似，但有一項例外：在此範例中，大量複製作業包含在較大的外部交易中。 當發生主要索引鍵違規錯誤時，整個交易便會回復，並且沒有任何資料列會加入目的地資料表。  
  
> [!IMPORTANT]
>  除非您已如[大量複製範例設定](bulk-copy-example-setup.md)中所述建立工作資料表，否則此範例不會執行。 這個程式碼僅是為了示範使用 **SqlBulkCopy** 的語法而提供。 如果來源和目的地資料表位於相同的 SQL Server 執行個體，則使用 Transact-SQL `INSERT … SELECT` 陳述式來複製資料會更方便且快速。  
  
[!code-csharp[DataWorks SqlBulkCopy_ExternalTransaction#1](~/../sqlclient/doc/samples/SqlBulkCopy_ExternalTransaction.cs#1)]
  
## <a name="next-steps"></a>後續步驟
- [SQL Server 中的大量複製作業](bulk-copy-operations-sql-server.md)
