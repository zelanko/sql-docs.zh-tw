---
title: SqlContext 物件 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: 223111874ca34ba4df4968c550e6cc47edf2b390
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62920048"
---
# <a name="sqlcontext-object"></a>SqlContext 物件
  當您呼叫程序或函數、在 Common Language Runtime (CLR) 使用者定義型別上呼叫方法，或您的動作引發以任何 [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework 語言定義的觸發程序時，會在伺服器中叫用 Managed 程式碼。 因為要求執行此程式碼做為使用者連接的一部分，所以需要從伺服器上執行的程式碼，存取呼叫端的內容。 此外，特定資料存取作業只有在呼叫端的內容下執行才會有效。 例如，對在觸發程序作業中使用之插入及刪除虛擬資料表的存取，只有在呼叫端的內容下才有效。  
  
 呼叫端的內容會在 `SqlContext` 物件中擷取。 如需有關 `SqlTriggerContext` 方法和屬性的詳細資訊，請參閱 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK 中的 `Microsoft.SqlServer.Server.SqlTriggerContext` 類別參考文件。  
  
 `SqlContext` 會提供下列元件的存取：  
  
-   `SqlPipe`:`SqlPipe`物件都代表 「 管道 」 透過結果藉以流向用戶端。 如需詳細資訊`SqlPipe`物件，請參閱 < [SqlPipe 物件](sqlpipe-object.md)。  
  
-   `SqlTriggerContext`:`SqlTriggerContext`物件只可從擷取 CLR 觸發程序內。 它提供造成引發觸發程序的作業及已更新資料行之對應的相關資訊。 如需詳細資訊`SqlTriggerContext`物件，請參閱 < [SqlTriggerContext 物件](sqltriggercontext-object.md)。  
  
-   `IsAvailable`:`IsAvailable`屬性用來判斷內容可用性。  
  
-   `WindowsIdentity`:`WindowsIdentity`屬性用來擷取呼叫端的 Windows 識別。  
  
## <a name="determining-context-availability"></a>決定內容可用性  
 查詢 `SqlContext` 類別，以查看目前執行的程式碼是否同處理序執行。 若要這樣做，請檢查 `IsAvailable` 物件的 `SqlContext` 屬性。 如果呼叫程式碼在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 內執行，且可存取其他 `IsAvailable` 成員，則 `True` 屬性是唯讀的，並會傳回 `SqlContext`。 如果 `IsAvailable` 屬性傳回 `False`，則使用的其他所有 `SqlContext` 成員會擲回 `InvalidOperationException`。 如果 `IsAvailable` 傳回 `False`，則開啟連接字串中包括 "context connection=true" 之連接物件的任何嘗試都會失敗。  
  
## <a name="retrieving-windows-identity"></a>擷取 Windows 識別  
 在處理序帳戶的內容中，永遠會叫用在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 內執行的 CLR 程式碼。 如果程式碼應使用呼叫使用者的識別 (而非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 處理序識別) 執行特定動作，則應透過 `WindowsIdentity` 物件的 `SqlContext` 屬性取得模擬 Token。 `WindowsIdentity` 屬性會傳回表示呼叫端之 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 識別的 `WindowsIdentity` 執行個體，或者，如果使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證來驗證用戶端，則會傳回 Null。 只有以 `EXTERNAL_ACCESS` 或 `UNSAFE` 使用權限標記的組件才能存取此屬性。  
  
 取得 `WindowsIdentity` 物件之後，呼叫端可以模擬用戶端帳戶，並代表它執行動作。  
  
 如果開始執行預存程序或函數的用戶端連接至使用 Windows 驗證的伺服器，則只能透過 `SqlContext.WindowsIdentity` 使用呼叫端的識別。 如果改用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證，則此屬性為 Null，而且程式碼無法模擬呼叫端。  
  
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
 [SqlPipe 物件](sqlpipe-object.md)   
 [SqlTriggerContext 物件](sqltriggercontext-object.md)   
 [CLR 觸發程序](../../database-engine/dev-guide/clr-triggers.md)   
 [ADO.NET 的 SQL Server 同處理序特定延伸模組](sql-server-in-process-specific-extensions-to-ado-net.md)  
  
  
