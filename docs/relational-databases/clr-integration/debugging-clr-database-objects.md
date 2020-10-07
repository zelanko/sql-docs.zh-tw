---
title: " (CLR) 資料庫物件的 Debug Common Language Runtime"
description: SQL Server 支援將 SQL Server 偵錯工具與 Microsoft Visual Studio 偵錯工具整合在資料庫中的 Transact-sql 和 CLR 物件。
ms.date: 10/06/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: how-to
helpviewer_keywords:
- database objects [CLR integration], debugging
- permissions [CLR integration]
- debugging [CLR integration]
- building database objects [CLR integration], debugging
- common language runtime [SQL Server], debugging
ms.assetid: 1332035c-d6ed-424d-8234-46ad21168319
author: rothja
ms.author: jroth
ms.openlocfilehash: 2a6e723c8ad5ff8c97a3b57edb554092211da4d7
ms.sourcegitcommit: 610e3ebe21ac6575850a29641a32f275e71557e3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/07/2020
ms.locfileid: "91785164"
---
# <a name="how-to-debug-clr-database-objects"></a>如何調試 CLR 資料庫物件

[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
 
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支援在資料庫中偵錯 [!INCLUDE[tsql](../../includes/tsql-md.md)] 和 Common Language Runtime (CLR) 物件。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中偵錯的關鍵層面是設定和使用的簡易性，以及 SQL Server 偵錯程式與 Microsoft Visual Studio 偵錯程式的整合。 此外，偵錯可跨語言運作。 使用者可以從 [!INCLUDE[tsql](../../includes/tsql-md.md)] 順利地逐步執行 CLR 物件，反之亦然。 SQL Server Management Studio 中的 Transact-SQL 偵錯工具無法用於偵錯 Managed 資料庫物件，但您可以使用 Visual Studio 中的偵錯工具來偵錯物件。 在 Visual Studio 中的 Managed 資料物件支援所有通用偵錯功能，例如伺服器上執行之常式內的「逐步執行」和「不進入函數」陳述式。 偵錯工具可在偵錯期間，設定中斷點、檢查呼叫堆疊，檢查變數，以及修改變數值。 

> [!NOTE]
> Visual Studio .NET 2003 無法用於 CLR 整合程式設計或偵錯工具。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 包含預先安裝的 .NET Framework，而且 Visual Studio .NET 2003 無法使用 .NET Framework 2.0 組件。  
  
## <a name="debugging-permissions-and-restrictions"></a>調試許可權和限制

偵錯工具是具有高度許可權的作業，因此只允許 **系統管理員（sysadmin** ）固定伺服器角色的成員在中執行此作業 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
偵錯時會套用下列限制：  
  
- 偵錯 CLR 常式一次只限於一個偵錯工具執行個體。 因為在叫用中斷點時，所有 CLR 程式碼執行都會凍結，在偵錯工具從中斷點繼續前進之前不會繼續執行，所以要套用此限制。 但是，您可以在其他連接中繼續偵錯 [!INCLUDE[tsql](../../includes/tsql-md.md)]。 雖然 [!INCLUDE[tsql](../../includes/tsql-md.md)] 偵錯不會凍結伺服器上的其他執行，但仍會因保留鎖定而讓其他連接等待。  
  
- 無法偵錯現有連接，只能偵錯新連接。這是因為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 需要用戶端及偵錯工具環境的詳細資訊，才能建立連接。  
  
由於上述限制，我們建議應在測試伺服器而不是生產伺服器上偵錯 [!INCLUDE[tsql](../../includes/tsql-md.md)] 和 CLR 程式碼。  
  
## <a name="overview"></a>概觀

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的偵錯遵循每個連接模型。 偵錯工具僅會偵測及偵錯其與用戶端之連接的活動。 因為偵錯工具的功能不受連接類型的限制，所以可以對表格式資料流 (TDS) 及 HTTP 連接進行偵錯。 不過，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不允許偵錯現有的連接。 偵錯支援在伺服器上執行的常式內的所有通用偵錯功能。 偵錯工具與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可透過分散式元件物件模式 (COM) 進行互動。  
  
如需有關調試 managed 預存程式、函數、觸發程式、使用者定義型別和匯總的詳細資訊和案例，請參閱 Visual Studio 檔中的 [SQL SERVER CLR Integration Database 的調試](https://go.microsoft.com/fwlink/?LinkId=120378) 程式。  
  
必須在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體上啟用 TCP/IP 網路通訊協定，才能針對遠端開發、偵錯和開發使用 Visual Studio。 如需在伺服器上啟用 TCP/IP 通訊協定的詳細資訊，請參閱 [設定用戶端通訊](../../database-engine/configure-windows/configure-client-protocols.md)協定。  
  
## <a name="debugging-steps"></a>調試步驟

使用下列步驟，在 Microsoft Visual Studio 中進行 CLR 資料庫物件的 debug 錯：

1. 開啟 Microsoft Visual Studio，然後建立新的 SQL Server 專案。 您可以使用 Visual Studio 隨附的 SQL LocalDB 實例。

2. 建立新的 SQL CLR 類型 (c # ) ：

   1. 在 **方案總管**中，以滑鼠右鍵按一下專案，然後選取 [ **加入**]、[ **新增專案 ...**]。 
   1. 從 [ **加入新專案** ] 視窗中，選取 [ **Sql Clr c # 預存**程式]、 **[Sql clr c # 使用者定義函式**]、[Sql clr c #] **使用者定義**型別、SQL Clr c # **觸發**程式、 **sql clr c # 匯總**或 **類別**。
   1. 指定新類型之來源檔案的名稱， **然後選取 [新增]**。

3. 將新類型的程式碼加入至文字編輯器。 如需範例預存程式的範例程式碼，請參閱本文中的下列範例一節。

4. 加入測試類型的腳本： 

   1. 在 **方案總管**中，以滑鼠右鍵按一下專案節點，然後選取 [ **加入**]、[ **腳本**]。 
   1. 在 [ **加入新專案** ] 視窗中，選取 [ **Script (Not in build) **]，然後指定名稱，例如 `Test.sql` 。 選取 [新增] 按鈕。
   1. 在 **方案總管**中，按兩下 `Test.sql` 節點以開啟預設的測試腳本來源檔案。
   1. 將測試腳本新增 (叫用程式碼) 至文字編輯器的測試腳本。 如需範例腳本，請參閱下一節中的範例。

5. 在原始程式碼中放置一或多個中斷點。 在您想要進行偵錯工具的函式或常式上，以滑鼠右鍵按一下文字編輯器中的程式程式碼。 選取 [ **中斷點**]、[ **插入中斷點**]。 中斷點隨即加入，程式碼行則以紅色反白顯示。

6. 在 [ **調試** ] 功能表中，選取 [ **開始調試** ] 以編譯、部署和測試專案。 中的測試腳本 `Test.sql` 會執行，並叫用 managed 資料庫物件。

7. 當黃色箭號 (指定指令指標) 出現在中斷點時，程式碼執行就會暫停。 然後，您可以將受控資料庫物件進行偵錯工具：

   1. 從 [**調試**程式] 功能表使用 [**逐步執行**]，將指令指標前進至下一行程式碼。
   1. 使用 [ **區域變數** ] 視窗來觀察指令指標目前反白顯示之物件的狀態。
   1. 將變數新增至 [ **監看** 式] 視窗。 您可以在整個偵錯工具中觀察監看的變數狀態，即使變數不在指令指標目前反白顯示的程式程式碼上也一樣。 
   1. 從 [**調試**程式] 功能表中選取 [**繼續**]，將指令指標前進至下一個中斷點，或在沒有其他中斷點時完成常式的執行。
  
## <a name="example-code"></a>程式碼範例

下列範例會將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本傳回給呼叫者。  
  
```csharp
using System.Data.SqlClient;
using Microsoft.SqlServer.Server;

public class StoredProcedures
{
    [Microsoft.SqlServer.Server.SqlProcedure]
    public static void GetVersion()
    {
        using (var connection = new SqlConnection("context connection=true"))
        {
            connection.Open();
            var command = new SqlCommand("select @@version", connection);
            SqlContext.Pipe.ExecuteAndSend(command);
        }
    }
}
```

## <a name="example-test-script"></a>範例測試腳本

下列測試腳本會示範如何叫 `GetVersion` 用前一個範例中定義的預存程式。  
  
```sql
EXEC GetVersion  
```  

## <a name="next-steps"></a>後續步驟
  
如需使用 Visual Studio 對 managed 程式碼進行偵錯工具的詳細資訊，請參閱 Visual Studio 檔中的 [managed 程式碼的調試](https://go.microsoft.com/fwlink/?LinkId=120377) 程式。  

如需詳細資訊，請參閱 [Common Language Runtime 整合程式設計概念](../../relational-databases/clr-integration/common-language-runtime-clr-integration-programming-concepts.md)  
