---
title: SqlCoNtext 物件 |Microsoft Docs
description: 當您在使用者連接中叫用 SQL Server 中的 managed 程式碼時，存取呼叫端的內容會在 SqlCoNtext 物件中抽象化。
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
ms.openlocfilehash: c423b4d2b6296da5ce95e62bfc51a160beb956a5
ms.sourcegitcommit: 04cf7905fa32e0a9a44575a6f9641d9a2e5ac0f8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/07/2020
ms.locfileid: "91810716"
---
# <a name="sqlcontext-object"></a>SqlContext 物件
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  當您呼叫程序或函數、在 Common Language Runtime (CLR) 使用者定義型別上呼叫方法，或您的動作引發以任何 [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework 語言定義的觸發程序時，會在伺服器中叫用 Managed 程式碼。 因為要求執行此程式碼做為使用者連接的一部分，所以需要從伺服器上執行的程式碼，存取呼叫端的內容。 此外，特定資料存取作業只有在呼叫端的內容下執行才會有效。 例如，對在觸發程序作業中使用之插入及刪除虛擬資料表的存取，只有在呼叫端的內容下才有效。  
  
 呼叫端的內容是在 **SqlCoNtext** 物件中抽象化。 如需有關**SqlTriggerCoNtext**方法和屬性的詳細資訊，請參閱 SDK 中的**SqlTriggerCoNtext**類別參考檔。 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]  
  
 **SqlCoNtext** 提供下列元件的存取權：  
  
-   **SqlPipe**： **SqlPipe** 物件代表將結果流至用戶端的「管道」。 如需 **SqlPipe** 物件的詳細資訊，請參閱 [SqlPipe 物件](../../relational-databases/clr-integration-data-access-in-process-ado-net/sqlpipe-object.md)。  
  
-   **SqlTriggerCoNtext**：只能從 CLR 觸發程式內取出 **SqlTriggerCoNtext** 物件。 它提供造成引發觸發程序的作業及已更新資料行之對應的相關資訊。 如需 **SqlTriggerCoNtext** 物件的詳細資訊，請參閱 [SqlTriggerCoNtext 物件](../../relational-databases/clr-integration-data-access-in-process-ado-net/sqltriggercontext-object.md)。  
  
-   **IsAvailable**： **IsAvailable** 屬性可用來判斷內容可用性。  
  
-   **WindowsIdentity**： **WindowsIdentity** 屬性是用來取得呼叫端的 Windows 識別。  
  
## <a name="determining-context-availability"></a>決定內容可用性  
 查詢 **SqlCoNtext** 類別，以查看目前執行中的程式碼是否正在同進程中執行。 若要這樣做，請檢查**SqlCoNtext**物件的**IsAvailable**屬性。 **IsAvailable**屬性是唯讀的，如果呼叫程式碼正在內部執行， **True** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 而且可以存取其他**SqlCoNtext**成員，則會傳回 True。 如果 **IsAvailable** 屬性傳回 **False**，則所有其他 **SqlCoNtext** 成員都會擲回 **InvalidOperationException**（如果使用的話）。 如果 **IsAvailable** 傳回 **False**，則在連接字串中開啟具有 "coNtext connection = true" 之連線物件的任何嘗試都會失敗。  
  
## <a name="retrieving-windows-identity"></a>擷取 Windows 識別  
 在處理序帳戶的內容中，永遠會叫用在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 內執行的 CLR 程式碼。 如果程式碼應使用呼叫使用者的身分識別來執行某些動作，而不是使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 進程身分識別，則應該透過**SqlCoNtext**物件的**WindowsIdentity**屬性取得模擬權杖。 **WindowsIdentity**屬性會傳回代表**WindowsIdentity** [!INCLUDE[msCoName](../../includes/msconame-md.md)] 呼叫端之 Windows 身分識別的 WindowsIdentity 實例，如果用戶端是使用驗證進行驗證，則為 null [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 只有標記有 **EXTERNAL_ACCESS** 或 **UNSAFE** 許可權的元件可以存取這個屬性。  
  
 取得 **WindowsIdentity** 物件之後，呼叫端可以模擬用戶端帳戶，並代表他們執行動作。  
  
 呼叫端的身分識別只有在使用 Windows 驗證來初始化預存程式或函式的執行連接到伺服器的用戶端時，才能透過 **SqlCoNtext. WindowsIdentity** 使用。 如果改用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證，則此屬性為 Null，而且程式碼無法模擬呼叫端。  
  
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
 [CLR 觸發程式](/dotnet/framework/data/adonet/sql/clr-triggers)   
 [ADO.NET 的 SQL Server 同處理序特定擴充](../../relational-databases/clr-integration-data-access-in-process-ado-net/sql-server-in-process-specific-extensions-to-ado-net.md)  
  
