---
title: 使用 System.Transactions |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 8fd93c1efab0e589fc87ebe74ab5485fcb482caf
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63043263"
---
# <a name="using-systemtransactions"></a>使用 System.Transactions
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  **System.Transactions**命名空間提供與 ADO.NET 完全整合的交易架構和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]common language runtime (CLR) 整合。 **System.Transactions.TransactionScope**類別進行程式碼區塊交易式隱含地登記連接到分散式交易中的。 您必須呼叫**Complete**方法的程式碼區塊的結尾標記**TransactionScope**。 **處置**當程式執行離開程式碼區塊，而使交易如果終止時，會叫用方法**完成**不會呼叫方法。 如果已擲回造成程式碼離開範圍的例外狀況，則會將交易視為停止。  
  
 我們建議您採取**使用**區塊來確保**Dispose**上呼叫方法**TransactionScope**物件時**使用**區塊的結束方法。 無法認可或復原暫止的交易可能嚴重降低效能，因為的預設逾時值**TransactionScope**是一分鐘。 如果您不要使用**使用**陳述式中，您必須執行中的所有工作**嘗試**區塊，並明確呼叫**處置**中的方法**最後**區塊。  
  
 如果發生例外狀況內**TransactionScope**，將交易標示為不一致並放棄。 發行時**TransactionScope**處置。 如果沒有發生任何例外狀況，則會認可參與的交易。  
  
 **TransactionScope**正在存取本機和遠端資料來源或外部資原管理員時，才應該使用。 這是因為**TransactionScope**一律會導致交易升級，即使它在內容連接內使用。  
  
> [!NOTE]  
>  **TransactionScope**類別建立與交易**System.Transactions.Transaction.IsolationLevel**的**Serializable**預設。 根據應用程式，您可能會考慮降低隔離等級，以避免應用程式中發生劇烈的競爭現象。  
  
> [!NOTE]  
>  建議您針對遠端伺服器，在分散式交易內僅執行更新、插入及刪除作業，因為它們會耗用大量的資料庫資源。 如果要在本機伺服器上執行作業，就不需要使用分散式交易，而且本機交易就已經足夠。 SELECT 陳述式可能會不必要地鎖定資料庫資源，而且在某些案例中，可能需要使用交易來進行選取。 除非涉及其他已交易的資源管理者，否則所有非資料庫工作都應在交易範圍外執行。 雖然交易範圍內的例外狀況會防止認可交易，但**TransactionScope**類別具有不支援，如超出範圍的交易已回復任何變更您的程式碼它本身。 如果您需要回復交易時採取某個動作，您必須撰寫您自己實作**System.Transactions.IEnlistmentNotification**介面，並明確登記到交易中。  
  
## <a name="example"></a>範例  
 若要使用**System.Transactions**，您必須參考 System.Transactions.dll 檔。  
  
 下列程式碼示範如何針對兩個不同的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體，建立可以升級的交易。 這些執行個體都由兩個不同**System.Data.SqlClient.SqlConnection**物件，其中會包裝在**TransactionScope**區塊。 程式碼會建立**TransactionScope**含有區塊**使用**陳述式，並開啟第一個連接，自動登記在**TransactionScope**。 一開始交易登記為輕量型交易，而不是完全分散式交易。 程式碼假設條件式邏輯存在 (已為了簡潔而省略該條件式邏輯)。 它會開啟第二個連接，只有當有需要中登記它**TransactionScope**。 開啟連接時，交易會自動提升為完全分散式交易。 程式碼接著會叫用**TransactionScope.Complete**，這會認可交易。 程式碼會處置兩條連線，結束時**使用**連接的陳述式。 **TransactionScope.Dispose**方法**TransactionScope**在終止時，會自動呼叫**使用**封鎖**TransactionScope**。 如果有已擲回例外狀況在任何時間點**TransactionScope**區塊**完成**會被呼叫，且分散式的交易會向前復原時**TransactionScope**處置。  
  
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
  
  
