---
title: 使用 System.Transactions |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: clr
ms.tgt_pltfrm: ''
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- TransactionScope class
- Dispose method
- System.Transactions namespace
ms.assetid: 79656ce5-ce46-4c5e-9540-cf9869bd774b
caps.latest.revision: 16
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: cf0f57f84e4b1838b9fd2da9838891640782266b
ms.sourcegitcommit: 022d67cfbc4fdadaa65b499aa7a6a8a942bc502d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/03/2018
ms.locfileid: "37350060"
---
# <a name="using-systemtransactions"></a>使用 System.Transactions
  `System.Transactions` 命名空間會提供與 ADO.NET 和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Common Language Runtime (CLR) 整合完全整合的交易架構。 `System.Transactions.TransactionScope` 類別可藉由在分散式交易中隱含地編列連接，讓程式碼區塊可進行交易。 您必須呼叫 `Complete` 所標示之程式碼區塊結尾的 `TransactionScope` 方法。 當程式執行離開程式碼區塊時，會叫用 `Dispose` 方法，如果不呼叫 `Complete` 方法，則會讓交易停止。 如果已擲回造成程式碼離開範圍的例外狀況，則會將交易視為停止。  
  
 建議您使用 `using` 區塊，以確保結束 `Dispose` 區塊時，會在 `TransactionScope` 物件上呼叫 `using` 方法。 無法認可或復原暫止的交易可能會使效能嚴重下降，因為 `TransactionScope` 的預設逾時是一分鐘。 如果您不使用 `using` 陳述式，則必須在 `Try` 區塊中執行所有工作，並明確呼叫 `Dispose` 區塊中的 `Finally` 方法。  
  
 如果 `TransactionScope` 中發生例外狀況，則會將交易標記為不一致並放棄。 處置 `TransactionScope` 時，則會復原該交易。 如果沒有發生任何例外狀況，則會認可參與的交易。  
  
 只有在存取本機和遠端資料來源或外部資原管理員時，才應該使用 `TransactionScope`。 這是因為即使是在內容連接內使用 `TransactionScope`，還是永遠會使交易升級。  
  
> [!NOTE]  
>  `TransactionScope` 類別預設會以 `System.Transactions.Transaction.IsolationLevel` 的 `Serializable` 建立交易。 根據應用程式，您可能會考慮降低隔離等級，以避免應用程式中發生劇烈的競爭現象。  
  
> [!NOTE]  
>  建議您針對遠端伺服器，在分散式交易內僅執行更新、插入及刪除作業，因為它們會耗用大量的資料庫資源。 如果要在本機伺服器上執行作業，就不需要使用分散式交易，而且本機交易就已經足夠。 SELECT 陳述式可能會不必要地鎖定資料庫資源，而且在某些案例中，可能需要使用交易來進行選取。 除非涉及其他已交易的資源管理者，否則所有非資料庫工作都應在交易範圍外執行。 雖然交易範圍內的例外狀況會防止認可交易，但 `TransactionScope` 類別不支援針對在交易本身範圍外所做的任何程式碼變更，進行復原。 如果在復原交易時需要採取某些動作，則必須撰寫您自己的 `System.Transactions.IEnlistmentNotification` 介面實作，並在交易中明確編列。  
  
## <a name="example"></a>範例  
 若要使用 `System.Transactions`，您必須參考 System.Transactions.dll 檔。  
  
 下列程式碼示範如何針對兩個不同的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體，建立可以升級的交易。 這些執行個體會以兩個不同的 `System.Data.SqlClient.SqlConnection` 物件代表，並包裝在 `TransactionScope` 區塊中。 程式碼會使用 `TransactionScope` 陳述式來建立 `using` 區塊，並開啟第一個連接，這樣會自動在 `TransactionScope` 中編列它。 一開始交易登記為輕量型交易，而不是完全分散式交易。 程式碼假設條件式邏輯存在 (已為了簡潔而省略該條件式邏輯)。 僅當需要時，才會開啟第二個連接，並在 `TransactionScope` 中登記它。 開啟連接時，交易會自動提升為完全分散式交易。 然後，程式碼會叫用認可交易的 `TransactionScope.Complete`。 當結束連接的 `using` 陳述式時，程式碼會處置兩個連接。 結束 `TransactionScope.Dispose` 的 `TransactionScope` 區塊時，會自動呼叫 `using` 的 `TransactionScope` 方法。 如果在 `TransactionScope` 區塊中的任何一點擲回例外狀況，便不會呼叫 `Complete`，且分散式交易會在處置 `TransactionScope` 時復原。  
  
 Visual Basic  
  
```  
Using transScope As New TransactionScope()  
    Using connection1 As New SqlConnection(connectString1)  
        ' Opening connection1 automatically enlists it in the   
        ' TransactionScope as a lightweight transaction.  
        connection1.Open()  
  
        ' Do work in the first connection.  
  
        ' Assumes conditional logic in place where the second  
        ' connection will only be opened as needed.  
        Using connection2 As New SqlConnection(connectString2)  
            ' Open the second connection, which enlists the   
            ' second connection and promotes the transaction to  
            ' a full distributed transaction.  
            connection2.Open()  
  
            ' Do work in the second connection.  
  
        End Using  
    End Using  
  
    ' Commit the transaction.  
    transScope.Complete()  
End Using  
```  
  
 C#  
  
```  
using (TransactionScope transScope = new TransactionScope())  
{  
    using (SqlConnection connection1 = new   
       SqlConnection(connectString1))  
    {  
        // Opening connection1 automatically enlists it in the   
        // TransactionScope as a lightweight transaction.  
        connection1.Open();  
  
        // Do work in the first connection.  
  
        // Assumes conditional logic in place where the second  
        // connection will only be opened as needed.  
        using (SqlConnection connection2 = new   
            SqlConnection(connectString2))  
        {  
            // Open the second connection, which enlists the   
            // second connection and promotes the transaction to  
            // a full distributed transaction.   
            connection2.Open();  
  
            // Do work in the second connection.  
        }  
    }  
    //  The Complete method commits the transaction.  
    transScope.Complete();  
}  
```  
  
## <a name="see-also"></a>另請參閱  
 [CLR 整合和交易](../native-client-ole-db-transactions/transactions.md)  
  
  
