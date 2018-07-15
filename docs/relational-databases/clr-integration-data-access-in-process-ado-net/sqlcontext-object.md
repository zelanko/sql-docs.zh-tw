---
title: SqlContext 物件 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.suite: sql
ms.technology: clr
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- Windows identity [CLR integration]
- SqlContext object
- context [CLR integration]
ms.assetid: 67437853-8a55-44d9-9337-90689ebba730
caps.latest.revision: 54
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: fd8bcd270794394bcb576c42657c2d9cd831fc98
ms.sourcegitcommit: 022d67cfbc4fdadaa65b499aa7a6a8a942bc502d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/03/2018
ms.locfileid: "37359540"
---
# <a name="sqlcontext-object"></a>SqlContext 物件
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  當您呼叫程序或函數、在 Common Language Runtime (CLR) 使用者定義型別上呼叫方法，或您的動作引發以任何 [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework 語言定義的觸發程序時，會在伺服器中叫用 Managed 程式碼。 因為要求執行此程式碼做為使用者連接的一部分，所以需要從伺服器上執行的程式碼，存取呼叫端的內容。 此外，特定資料存取作業只有在呼叫端的內容下執行才會有效。 例如，對在觸發程序作業中使用之插入及刪除虛擬資料表的存取，只有在呼叫端的內容下才有效。  
  
 呼叫端的內容中抽離**SqlContext**物件。 如需詳細資訊**SqlTriggerContext**方法和屬性，請參閱**Microsoft.SqlServer.Server.SqlTriggerContext**類別中的參考文件[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]SDK。  
  
 **SqlContext**可讓您存取下列元件：  
  
-   **SqlPipe**: **SqlPipe**物件都代表 「 管道 」 透過結果藉以流向用戶端。 如需詳細資訊**SqlPipe**物件，請參閱[SqlPipe 物件](../../relational-databases/clr-integration-data-access-in-process-ado-net/sqlpipe-object.md)。  
  
-   **SqlTriggerContext**: **SqlTriggerContext**物件只可從擷取 CLR 觸發程序內。 它提供造成引發觸發程序的作業及已更新資料行之對應的相關資訊。 如需詳細資訊**SqlTriggerContext**物件，請參閱[SqlTriggerContext 物件](../../relational-databases/clr-integration-data-access-in-process-ado-net/sqltriggercontext-object.md)。  
  
-   **IsAvailable**: **IsAvailable**屬性用來判斷內容可用性。  
  
-   **WindowsIdentity**: **WindowsIdentity**屬性用來擷取呼叫端的 Windows 識別。  
  
## <a name="determining-context-availability"></a>決定內容可用性  
 查詢**SqlContext**類別，以查看同處理序時，是否要執行的目前執行的程式碼。 若要這樣做，請**IsAvailable**屬性**SqlContext**物件。 **IsAvailable**屬性是唯讀的並且傳回 **，則為 True**如果呼叫程式碼執行內[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]如果有其他**SqlContext**成員可以存取。 如果**IsAvailable**屬性會傳回**False**，所有其他**SqlContext**成員會擲回**InvalidOperationException**，如果使用. 如果**IsAvailable**會傳回**False**，任何嘗試開啟連接物件的 「 內容連接 = true"的連接字串中就會失敗。  
  
## <a name="retrieving-windows-identity"></a>擷取 Windows 識別  
 在處理序帳戶的內容中，永遠會叫用在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 內執行的 CLR 程式碼。 如果程式碼應該執行特定動作，而不使用呼叫使用者的身分識別[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]處理身分識別，則應該透過取得模擬語彙基元**WindowsIdentity** 屬性**SqlContext**物件。 **WindowsIdentity**屬性會傳回**WindowsIdentity**執行個體，代表[!INCLUDE[msCoName](../../includes/msconame-md.md)]呼叫端，則為 null，如果用戶端的驗證使用的 Windows 身分識別[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]驗證。 只有組件標示**EXTERNAL_ACCESS**或是**UNSAFE**權限可以存取這個屬性。  
  
 取得之後**WindowsIdentity**物件，呼叫端可以模擬用戶端帳戶，並代表他們執行動作。  
  
 呼叫端的身分識別才可透過**SqlContext.WindowsIdentity**如果開始執行預存程序或函式的用戶端連接至使用 Windows 驗證的伺服器。 如果改用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證，則此屬性為 Null，而且程式碼無法模擬呼叫端。  
  
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
 [SqlTriggerContext 物件](../../relational-databases/clr-integration-data-access-in-process-ado-net/sqltriggercontext-object.md)   
 [CLR 觸發程序](http://msdn.microsoft.com/library/302a4e4a-3172-42b6-9cc0-4a971ab49c1c)   
 [ADO.NET 的 SQL Server 同處理序特定延伸模組](../../relational-databases/clr-integration-data-access-in-process-ado-net/sql-server-in-process-specific-extensions-to-ado-net.md)  
  
  
