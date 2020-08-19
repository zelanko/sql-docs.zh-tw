---
title: 調試 CLR 資料庫物件 |Microsoft Docs
description: SQL Server 支援將 SQL Server 偵錯工具與 Microsoft Visual Studio 偵錯工具整合在資料庫中的 Transact-sql 和 CLR 物件。
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- database objects [CLR integration], debugging
- permissions [CLR integration]
- debugging [CLR integration]
- building database objects [CLR integration], debugging
- common language runtime [SQL Server], debugging
ms.assetid: 1332035c-d6ed-424d-8234-46ad21168319
author: rothja
ms.author: jroth
ms.openlocfilehash: 7af58a109a658a4af60ca49ad6eea401284782ac
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85756318"
---
# <a name="debugging-clr-database-objects"></a>偵錯 CLR 資料庫物件
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支援在資料庫中偵錯 [!INCLUDE[tsql](../../includes/tsql-md.md)] 和 Common Language Runtime (CLR) 物件。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中偵錯的關鍵層面是設定和使用的簡易性，以及 SQL Server 偵錯程式與 Microsoft Visual Studio 偵錯程式的整合。 此外，偵錯可跨語言運作。 使用者可以從 [!INCLUDE[tsql](../../includes/tsql-md.md)] 順利地逐步執行 CLR 物件，反之亦然。 SQL Server Management Studio 中的 Transact-SQL 偵錯工具無法用於偵錯 Managed 資料庫物件，但您可以使用 Visual Studio 中的偵錯工具來偵錯物件。 在 Visual Studio 中的 Managed 資料物件支援所有通用偵錯功能，例如伺服器上執行之常式內的「逐步執行」和「不進入函數」陳述式。 偵錯工具可在偵錯期間，設定中斷點、檢查呼叫堆疊，檢查變數，以及修改變數值。 請注意，Visual Studio .NET 2003 無法用於 CLR 整合程式設計或偵錯。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 包含預先安裝的 .NET Framework，而且 Visual Studio .NET 2003 無法使用 .NET Framework 2.0 組件。  
  
 如需使用 Visual Studio 來對 managed 程式碼進行偵錯工具的詳細資訊，請參閱 Visual Studio 檔中的「將[managed 程式碼調試](https://go.microsoft.com/fwlink/?LinkId=120377)程式」主題。  
  
## <a name="debugging-permissions-and-restrictions"></a>偵錯使用權限及限制  
 偵錯工具是具有高度許可權的作業，因此只允許 **系統管理員（sysadmin** ）固定伺服器角色的成員在中執行此作業 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
 偵錯時會套用下列限制：  
  
-   偵錯 CLR 常式一次只限於一個偵錯工具執行個體。 因為在叫用中斷點時，所有 CLR 程式碼執行都會凍結，在偵錯工具從中斷點繼續前進之前不會繼續執行，所以要套用此限制。 但是，您可以在其他連接中繼續偵錯 [!INCLUDE[tsql](../../includes/tsql-md.md)]。 雖然 [!INCLUDE[tsql](../../includes/tsql-md.md)] 偵錯不會凍結伺服器上的其他執行，但仍會因保留鎖定而讓其他連接等待。  
  
-   無法偵錯現有連接，只能偵錯新連接。這是因為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 需要用戶端及偵錯工具環境的詳細資訊，才能建立連接。  
  
 由於上述限制，我們建議應在測試伺服器而不是生產伺服器上偵錯 [!INCLUDE[tsql](../../includes/tsql-md.md)] 和 CLR 程式碼。  
  
## <a name="overview-of-debugging-managed-database-objects"></a>偵錯 Managed 資料庫物件的概觀  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的偵錯遵循每個連接模型。 偵錯工具僅會偵測及偵錯其與用戶端之連接的活動。 因為偵錯工具的功能不受連接類型的限制，所以可以對表格式資料流 (TDS) 及 HTTP 連接進行偵錯。 不過，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不允許偵錯現有的連接。 偵錯支援在伺服器上執行的常式內的所有通用偵錯功能。 偵錯工具與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可透過分散式元件物件模式 (COM) 進行互動。  
  
 如需有關調試 managed 預存程式、函數、觸發程式、使用者定義型別和匯總的詳細資訊和案例，請參閱 Visual Studio 檔中的「[SQL SERVER CLR 整合資料庫的調試](https://go.microsoft.com/fwlink/?LinkId=120378)程式」主題。  
  
 必須在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體上啟用 TCP/IP 網路通訊協定，才能針對遠端開發、偵錯和開發使用 Visual Studio。 如需在伺服器上啟用 TCP/IP 通訊協定的詳細資訊，請參閱 [設定用戶端通訊](../../database-engine/configure-windows/configure-client-protocols.md)協定。  
  
#### <a name="to-debug-a-managed-database-object"></a>偵錯 Managed 資料庫物件  
  
1.  開啟 Microsoft Visual Studio、建立新的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 專案，然後在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體上建立資料庫連接。  
  
2.  建立新類型。 在 **方案總管**中，以滑鼠右鍵按一下專案，然後選取 [ **加入** ] 和 [ **新增專案** ]。從 [ **加入新專案** ] 視窗中，選取 [ **預存**程式]、[ **使用者定義函數**]、[ **使用者定義類型**]、[ **觸發**程式]、[ **匯總**] 或 [ **類別**] 指定新類型之來源檔案的名稱，然後按一下 [ **新增**]。  
  
3.  將新類型的程式碼加入至文字編輯器。 如需範例預存程序的範例程式碼，請參閱本主題稍後的章節。  
  
4.  加入測試類型的指令碼。 在 **方案總管**中，展開 [ **TestScripts** ] 目錄按兩下 [ **test** ] 以開啟預設測試腳本來源檔案。 將叫用要偵錯之程式碼的測試指令碼加入至文字編輯器。 如需範例指令碼，請參閱下文。  
  
5.  在原始程式碼中放置一或多個中斷點。 以滑鼠右鍵按一下文字編輯器中您要進行調試的函式或常式內的一行程式碼，然後選取 [ **中斷點** ] 和 [ **插入中斷點**]。 中斷點隨即加入，程式碼行則以紅色反白顯示。  
  
6.  在 [ **調試** ] 功能表中，選取 [ **開始調試** ] 以編譯、部署和測試專案。 Test.sql 中的測試指令碼將會執行，並會叫用 Managed 資料庫物件。  
  
7.  當中斷點出現表示指令指標的黃色箭頭時，程式碼執行會暫停，而您可以開始針錯 Managed 資料庫物件。 您可以從 [**調試**程式] 功能表**逐步執行**，將指令指標前進至下一行程式碼。 [ **區域變數** ] 視窗是用來觀察指令指標目前反白顯示之物件的狀態。 變數可以加入至 [ **監看** 式] 視窗。 在整個偵錯工作階段中都可以觀察受監看變數的狀態，而不只是變數在程式碼行中由指令指標反白顯示時。 從 [偵錯] 功能表選取 [繼續]，將指令指標前進至下一個中斷點，或者如果沒有中斷點了，就完成常式的執行。  
  
### <a name="example"></a>範例  
 下列範例會將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本傳回給呼叫者。  
  
 C#  
  
```  
using System;  
using System.Data;  
using System.Data.SqlTypes;  
using System.Data.SqlClient;  
using Microsoft.SqlServer.Server;   
  
public class StoredProcedures   
{  
   [Microsoft.SqlServer.Server.SqlProcedure]  
   public static void GetVersion()  
   {  
   using(SqlConnection connection = new SqlConnection("context connection=true"))   
   {  
      connection.Open();  
      SqlCommand command = new SqlCommand("select @@version",  
                                           connection);  
      SqlContext.Pipe.ExecuteAndSend(command);  
      }  
   }  
}  
```  
  
 Visual Basic  
  
```  
Imports System  
Imports System.Data  
Imports System.Data.Sql  
Imports System.Data.SqlTypes  
Imports Microsoft.SqlServer.Server  
Imports System.Data.SqlClient  
  
Partial Public Class StoredProcedures   
    <Microsoft.SqlServer.Server.SqlProcedure> _  
    Public Shared Sub GetVersion()  
        Using connection As New SqlConnection("context connection=true")  
            connection.Open()  
            Dim command As New SqlCommand("SELECT @@VERSION", connection)  
            SqlContext.Pipe.ExecuteAndSend(command)  
        End Using  
    End Sub  
End Class  
```  
  
 下列的測試指令碼會叫用以上定義的 GetVersion 預存程序。  
  
```  
EXEC GetVersion  
```  
  
## <a name="see-also"></a>另請參閱  
 [Common Language Runtime &#40;CLR&#41; 整合程式設計概念](../../relational-databases/clr-integration/common-language-runtime-clr-integration-programming-concepts.md)  
  
  
