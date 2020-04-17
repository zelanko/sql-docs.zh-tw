---
title: SqlContext 物件 |微軟文件
description: 在使用者連接中調用 SQL Server 中的託管代碼時,對調用方上下文的訪問將抽象在 SqlContext 物件中。
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
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2020
ms.locfileid: "81487532"
---
# <a name="sqlcontext-object"></a>SqlContext 物件
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  當您呼叫程序或函數、在 Common Language Runtime (CLR) 使用者定義型別上呼叫方法，或您的動作引發以任何 [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework 語言定義的觸發程序時，會在伺服器中叫用 Managed 程式碼。 因為要求執行此程式碼做為使用者連接的一部分，所以需要從伺服器上執行的程式碼，存取呼叫端的內容。 此外，特定資料存取作業只有在呼叫端的內容下執行才會有效。 例如，對在觸發程序作業中使用之插入及刪除虛擬資料表的存取，只有在呼叫端的內容下才有效。  
  
 呼叫方的上下文在**SqlContext**物件中抽象。 有關**SqlTriggerContext**方法和屬性的詳細資訊,請[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]參閱 SDK 中的**Microsoft.SqlServer.Server.SqlTriggerContext**類引用文檔。  
  
 **SqlContext**提供對以下元件的存取:  
  
-   **SqlPipe**: **SqlPipe**物件表示結果流到用戶端的"管道"。 有關**SqlPipe**物件的詳細資訊,請參閱[SqlPipe 物件](../../relational-databases/clr-integration-data-access-in-process-ado-net/sqlpipe-object.md)。  
  
-   **SqlTriggerContext**: 只能從 CLR 觸發器中檢索**SqlTriggerContext**物件。 它提供造成引發觸發程序的作業及已更新資料行之對應的相關資訊。 有關**SqlTriggerContext**物件的詳細資訊,請參閱[SqlTriggerContext 物件](../../relational-databases/clr-integration-data-access-in-process-ado-net/sqltriggercontext-object.md)。  
  
-   **可用**: **Is 可用**屬性用於確定上下文可用性。  
  
-   **Windows 識別** **:Windows 識別**屬性用於檢索調用方的 Windows 標識。  
  
## <a name="determining-context-availability"></a>決定內容可用性  
 查詢**SqlContext**類以查看當前執行的代碼是否在行程中運行。 為此,請檢查**SqlContext**物件的**Is 可用**屬性。 **IsAccess**屬性是唯讀的,如果呼叫程式碼[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]在內部運行,並且可以存取其他**SqlContext**成員,則傳回**True。** 如果**Is 可用**屬性傳回**False,** 則所有其他**SqlContext**成員將引發**無效操作異常**,如果使用。 如果**Is 可用**傳回**False,** 則打開連接字串中具有「上下文連接_true」的連接物件的任何嘗試都失敗。  
  
## <a name="retrieving-windows-identity"></a>擷取 Windows 識別  
 在處理序帳戶的內容中，永遠會叫用在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 內執行的 CLR 程式碼。 如果代碼應使用調用使用者的身份執行某些操作,而不是[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]進程標識,則應通過**SqlContext**物件的**WindowsIdentity**屬性獲取類比權杖。 **Windows識別**屬性返回表示調用方[!INCLUDE[msCoName](../../includes/msconame-md.md)]的 Windows 標識的**Windows 識別**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]實例,如果用戶端使用 身份驗證進行身份驗證,則返回 null。 只有標有**EXTERNAL_ACCESS**或 UNSAFE 許可權**的**程式集才能存取此屬性。  
  
 獲取**Windows 標識**物件後,調用方可以類比用戶端帳戶並代表他們執行操作。  
  
 僅當啟動使用 Windows 身份驗證執行連接到伺服器的儲存過程或函數的用戶端時,調用方的標識只能透過**SqlContext.Windows 標識**獲得。 如果改用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證，則此屬性為 Null，而且程式碼無法模擬呼叫端。  
  
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
 [SqlTrigger上下文物件](../../relational-databases/clr-integration-data-access-in-process-ado-net/sqltriggercontext-object.md)   
 [CLR 觸發器](https://msdn.microsoft.com/library/302a4e4a-3172-42b6-9cc0-4a971ab49c1c)   
 [ADO.NET 的 SQL Server 同處理序特定擴充](../../relational-databases/clr-integration-data-access-in-process-ado-net/sql-server-in-process-specific-extensions-to-ado-net.md)  
  
  
