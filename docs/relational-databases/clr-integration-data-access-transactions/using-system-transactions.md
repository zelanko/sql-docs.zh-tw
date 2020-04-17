---
title: 使用系統.事務 |微軟文件
description: System.事務命名空間提供了一個與ADO.NET和 SQL Server CLR 整合完全整合的事務框架。
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
ms.openlocfilehash: 7fa98e9e13062d358a6a1810485d45c8d9d3e911
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2020
ms.locfileid: "81488489"
---
# <a name="using-systemtransactions"></a>使用 System.Transactions
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  **System.事務**命名空間提供了一個事務框架,該框架與ADO.NET[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]和 通用語言運行時 (CLR) 整合完全整合。 **系統.事務.事務範圍**類通過在分散式事務中隱式登記連接來創建代碼塊事務。 您必須在**事務作用域**標記的代碼塊的末尾調用**Complete**方法。 當程式執行離開代碼塊時調用**Dispose**方法,如果不調用**Complete**方法,則導致事務停止。 如果已擲回造成程式碼離開範圍的例外狀況，則會將交易視為停止。  
  
 我們建議您使用**using**塊,以確保在退出**使用**塊時在**事務範圍**物件上調用**Dispose**方法。 無法提交或回滾掛起的事務可能會嚴重降低性能,因為**事務範圍**的預設超時為一分鐘。 如果不使用**using**語句,則必須在**Try**塊中執行所有工作,並在**Finally**塊中顯式調用**Dispose**方法。  
  
 如果**事務範圍內**發生異常,則事務將標記為不一致並放棄。 釋放**事務範圍**時回滾它。 如果沒有發生任何例外狀況，則會認可參與的交易。  
  
 只使用本地碼與遠端資料來源或外部資源管理員時,才應使用**事務範圍**。 這是因為**事務範圍**總是導致事務升級,即使它僅在上下文連接中使用也是如此。  
  
> [!NOTE]  
>  **預設情況下,事務範圍**類別建立具有**System.事務.事務.隔離等級的****事務**。 根據應用程式，您可能會考慮降低隔離等級，以避免應用程式中發生劇烈的競爭現象。  
  
> [!NOTE]  
>  建議您針對遠端伺服器，在分散式交易內僅執行更新、插入及刪除作業，因為它們會耗用大量的資料庫資源。 如果要在本機伺服器上執行作業，就不需要使用分散式交易，而且本機交易就已經足夠。 SELECT 陳述式可能會不必要地鎖定資料庫資源，而且在某些案例中，可能需要使用交易來進行選取。 除非涉及其他已交易的資源管理者，否則所有非資料庫工作都應在交易範圍外執行。 儘管事務範圍內的異常阻止事務提交,但**事務範圍**類沒有用於回滾代碼在事務本身範圍之外所做的任何更改的規定。 如果在回滾事務時需要執行一些操作,則必須編寫自己的**System.事務.IEnlistment 通知**介面,並在事務中顯式登記。  
  
## <a name="example"></a>範例  
 要使用**System.事務**,您必須具有對 System.事務.dll 檔的引用。  
  
 下列程式碼示範如何針對兩個不同的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體，建立可以升級的交易。 這些實例由兩個不同的**System.Data.SqlClient.SqlConnect**物件表示,它們包在**事務範圍**塊中。 代碼使用**using**語句創建**事務範圍**塊,並打開第一個連接,該連接會自動在**事務作用域**中登記它。 一開始交易登記為輕量型交易，而不是完全分散式交易。 程式碼假設條件式邏輯存在 (已為了簡潔而省略該條件式邏輯)。 它僅在需要時才打開第二個連接,在**事務作用域**中登記它。 開啟連接時，交易會自動提升為完全分散式交易。 然後,代碼調用**事務範圍.Complete**,提交事務。 當退出連接的**using**語句時,程式碼會釋放兩個連接。 **事務範圍**的**事務範圍.Dispose**方法在**事務範圍****的 using**塊終止時自動調用。 如果在 **「事務範圍」** 塊中的任何點引發異常,則不會調用 **「完成」 ,** 並且分散式事務將在釋放**事務範圍**時回滾。  
  
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
  
  
