---
title: 使用 System.object |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- TransactionScope class
- Dispose method
- System.Transactions namespace
ms.assetid: 79656ce5-ce46-4c5e-9540-cf9869bd774b
author: rothja
ms.author: jroth
ms.openlocfilehash: a9b99842a92649a42e9a0a42e6732368dc5e06ec
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68081348"
---
# <a name="using-systemtransactions"></a>使用 System.Transactions
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [ **System.object** ] 命名空間提供與 ADO.NET 和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] COMMON language runtime （CLR）整合完全整合的交易架構。 在分散式交易中，會以隱含方式登記連接，使程式碼區塊成為**交易**式。 您必須在**TransactionScope**標記的程式碼區塊結尾呼叫**Complete**方法。 當程式執行離開程式碼區塊時，就會叫用**Dispose**方法，如果未呼叫**Complete**方法，則會導致交易中止。 如果已擲回造成程式碼離開範圍的例外狀況，則會將交易視為停止。  
  
 我們建議您在**使用**區塊結束時，使用**using**區塊來確保在**TransactionScope**物件上呼叫**Dispose**方法。 無法認可或回復暫止的交易可能會嚴重降低效能，因為**TransactionScope**的預設超時時間為一分鐘。 如果您未使用**using**語句，就必須在**Try**區塊中執行所有工作，並在**Finally**區塊中明確地呼叫**Dispose**方法。  
  
 如果在**TransactionScope**內發生例外狀況，則會將交易標記為不一致並放棄。 處置**TransactionScope**時，會將它復原。 如果沒有發生任何例外狀況，則會認可參與的交易。  
  
 只有在存取本機和遠端資料源或外部資源管理員時，才應該使用**TransactionScope** 。 這是因為**TransactionScope**一律會導致交易升級，即使它只在內容連接中使用也是如此。  
  
> [!NOTE]  
>  根據預設， **TransactionScope**類別會建立具有**IsolationLevel** **Serializable**的交易。 根據應用程式，您可能會考慮降低隔離等級，以避免應用程式中發生劇烈的競爭現象。  
  
> [!NOTE]  
>  建議您針對遠端伺服器，在分散式交易內僅執行更新、插入及刪除作業，因為它們會耗用大量的資料庫資源。 如果要在本機伺服器上執行作業，就不需要使用分散式交易，而且本機交易就已經足夠。 SELECT 陳述式可能會不必要地鎖定資料庫資源，而且在某些案例中，可能需要使用交易來進行選取。 除非涉及其他已交易的資源管理者，否則所有非資料庫工作都應在交易範圍外執行。 雖然交易範圍內的例外狀況會防止認可交易，但**TransactionScope**類別不會針對您的程式碼在交易本身範圍外所做的任何變更，提供回復。 如果您需要在回復交易時採取一些動作，則必須撰寫您自己的**IEnlistmentNotification**介面，並在交易中明確登記。  
  
## <a name="example"></a>範例  
 若要使用**system.object**，您必須擁有 system.string 檔案的參考。  
  
 下列程式碼示範如何針對兩個不同的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體，建立可以升級的交易。 這些實例會以兩個不同的**SqlClient**來表示，這些物件會包裝在**TransactionScope**區塊中。 程式碼會使用**using**語句建立**TransactionScope**區塊，並開啟第一個連接，它會自動在**transactionscope**中登記它。 一開始交易登記為輕量型交易，而不是完全分散式交易。 程式碼假設條件式邏輯存在 (已為了簡潔而省略該條件式邏輯)。 只有在需要時才會開啟第二個連接，並在**TransactionScope**中登記它。 開啟連接時，交易會自動提升為完全分散式交易。 然後，程式碼會叫用**TransactionScope. Complete**，這會認可交易。 當結束連接的**using**語句時，程式碼會處置兩個連接。 Transactionscope**的 transactionscope**方法會在**transactionscope**的**using**區塊**終止時自動**呼叫。 如果在**transactionscope**區塊中的任何一點擲回例外狀況，就不會呼叫**Complete** ，而且當**transactionscope**被處置時，分散式交易將會回復。  
  
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
 [CLR 整合和交易](../../relational-databases/clr-integration-data-access-transactions/clr-integration-and-transactions.md)  
  
  
