---
title: SqlCoNtext 物件 |Microsoft Docs
description: 當您在使用者連接的 SQL Server 中叫用 managed 程式碼時，會在 SqlCoNtext 物件中抽象化對呼叫端內容的存取。
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- Windows identity [CLR integration]
- SqlContext object
- context [CLR integration]
ms.assetid: 67437853-8a55-44d9-9337-90689ebba730
author: rothja
ms.author: jroth
ms.openlocfilehash: cd6d3091b155ae829e368bdd182b3da8286c7194
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81487532"
---
# <a name="sqlcontext-object"></a>SqlContext 物件
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  當您呼叫程序或函數、在 Common Language Runtime (CLR) 使用者定義型別上呼叫方法，或您的動作引發以任何 [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework 語言定義的觸發程序時，會在伺服器中叫用 Managed 程式碼。 因為要求執行此程式碼做為使用者連接的一部分，所以需要從伺服器上執行的程式碼，存取呼叫端的內容。 此外，特定資料存取作業只有在呼叫端的內容下執行才會有效。 例如，對在觸發程序作業中使用之插入及刪除虛擬資料表的存取，只有在呼叫端的內容下才有效。  
  
 呼叫端的內容會在**SqlCoNtext**物件中抽象化。 如需有關**SqlTriggerCoNtext**方法和屬性的詳細資訊，請**Microsoft.SqlServer.Server.SqlTriggerContext**參閱[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK 中的 SqlTriggerCoNtext 類別參考檔。  
  
 **SqlCoNtext**提供下列元件的存取權：  
  
-   **SqlPipe**： **SqlPipe**物件代表將結果流向用戶端的「管道」。 如需**SqlPipe**物件的詳細資訊，請參閱[SqlPipe 物件](../../relational-databases/clr-integration-data-access-in-process-ado-net/sqlpipe-object.md)。  
  
-   **SqlTriggerCoNtext**： **SqlTriggerCoNtext**物件只能從 CLR 觸發程式內抓取。 它提供造成引發觸發程序的作業及已更新資料行之對應的相關資訊。 如需**SqlTriggerCoNtext**物件的詳細資訊，請參閱[SqlTriggerCoNtext 物件](../../relational-databases/clr-integration-data-access-in-process-ado-net/sqltriggercontext-object.md)。  
  
-   **IsAvailable**： **IsAvailable**屬性是用來判斷內容可用性。  
  
-   **WindowsIdentity**： **WindowsIdentity**屬性是用來抓取呼叫端的 Windows 識別。  
  
## <a name="determining-context-availability"></a>決定內容可用性  
 查詢**SqlCoNtext**類別，以查看目前執行中的程式碼是否正在同進程執行。 若要這麼做，請檢查**SqlCoNtext**物件的**IsAvailable**屬性。 **IsAvailable**屬性是唯讀的，如果呼叫程式碼**True**在內部[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行，而且可以存取其他**SqlCoNtext**成員，則會傳回 True。 如果**IsAvailable**屬性傳回**False**，則所有其他**SqlCoNtext**成員都會擲回**InvalidOperationException**（如果有使用的話）。 如果**IsAvailable**傳回**False**，則在連接字串中開啟具有 "coNtext connection = true" 之連線物件的任何嘗試都會失敗。  
  
## <a name="retrieving-windows-identity"></a>擷取 Windows 識別  
 在處理序帳戶的內容中，永遠會叫用在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 內執行的 CLR 程式碼。 如果程式碼應使用呼叫使用者的身分識別來執行特定動作，而不是[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]處理常式身分識別，則應該透過**SqlCoNtext**物件的**WindowsIdentity**屬性來取得模擬 token。 **WindowsIdentity**屬性會傳回代表**WindowsIdentity**呼叫者之[!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 識別的 WindowsIdentity 實例，如果用戶端是使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]驗證進行驗證，則會傳回 null。 只有以**EXTERNAL_ACCESS**或**UNSAFE**許可權標記的元件才能存取此屬性。  
  
 取得**WindowsIdentity**物件之後，呼叫者可以模擬用戶端帳戶，並代表他們執行動作。  
  
 只有當使用 Windows 驗證來起始執行預存程式或函式的用戶端連接到伺服器時，才可以透過**SqlCoNtext**取得呼叫者的身分識別。 如果改用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證，則此屬性為 Null，而且程式碼無法模擬呼叫端。  
  
### <a name="example"></a>範例  
 下列範例示範如何取得呼叫用戶端的 Windows 識別以及模擬該用戶端。  
  
 C#  
  
```  
[Microsoft.SqlServer.Server.SqlProcedure]  
public static void WindowsIDTestProc()  
{  
    WindowsIdentity clientId = null;  
    WindowsImpersonationContext impersonatedUser = null;  
  
    // Get the client ID.  
    clientId = SqlContext.WindowsIdentity;  
  
    // This outer try block is used to thwart exception filter   
    // attacks which would prevent the inner finally   
    // block from executing and resetting the impersonation.  
    try  
    {  
        try  
        {  
            impersonatedUser = clientId.Impersonate();  
            if (impersonatedUser != null)  
            {  
                // Perform some action using impersonation.  
            }  
        }  
        finally  
        {  
            // Undo impersonation.  
            if (impersonatedUser != null)  
                impersonatedUser.Undo();  
        }  
    }  
    catch  
    {  
        throw;  
    }  
}  
```  
  
 Visual Basic  
  
```  
<Microsoft.SqlServer.Server.SqlProcedure()> _  
Public Shared Sub  WindowsIDTestProcVB ()  
    Dim clientId As WindowsIdentity  
    Dim impersonatedUser As WindowsImpersonationContext  
  
    ' Get the client ID.  
    clientId = SqlContext.WindowsIdentity  
  
    ' This outer try block is used to thwart exception filter   
    ' attacks which would prevent the inner finally   
    ' block from executing and resetting the impersonation.  
  
    Try  
        Try  
  
            impersonatedUser = clientId.Impersonate()  
  
            If impersonatedUser IsNot Nothing Then  
                ' Perform some action using impersonation.  
            End If  
  
        Finally  
            ' Undo impersonation.  
            If impersonatedUser IsNot Nothing Then  
                impersonatedUser.Undo()  
            End If  
        End Try  
  
    Catch e As Exception  
  
        Throw e  
  
    End Try  
End Sub  
```  
  
## <a name="see-also"></a>另請參閱  
 [SqlPipe 物件](../../relational-databases/clr-integration-data-access-in-process-ado-net/sqlpipe-object.md)   
 [SqlTriggerCoNtext 物件](../../relational-databases/clr-integration-data-access-in-process-ado-net/sqltriggercontext-object.md)   
 [CLR 觸發程式](https://msdn.microsoft.com/library/302a4e4a-3172-42b6-9cc0-4a971ab49c1c)   
 [ADO.NET 的 SQL Server 同處理序特定擴充](../../relational-databases/clr-integration-data-access-in-process-ado-net/sql-server-in-process-specific-extensions-to-ado-net.md)  
  
  
