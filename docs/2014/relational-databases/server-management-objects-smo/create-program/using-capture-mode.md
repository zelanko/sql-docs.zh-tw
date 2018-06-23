---
title: 使用擷取模式 |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Management Objects, capture mode
- capture mode [SMO]
- SMO [SQL Server], capture mode
ms.assetid: ace29bf0-705a-434f-82e4-db99d01c5008
caps.latest.revision: 36
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 0585f571868c88b6fda1926b03f34f5e131bf6c4
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36037194"
---
# <a name="using-capture-mode"></a>使用擷取模式
  SMO 程式可以擷取與記錄程式所發出的相等 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 陳述式來取代程式所執行的陳述式，或是加上程式所執行的陳述式。 您可以使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 物件，或使用 <xref:Microsoft.SqlServer.Management.Smo.Server.ConnectionContext%2A> 物件的 <xref:Microsoft.SqlServer.Management.Smo.Server> 屬性來啟用擷取模式。  
  
## <a name="example"></a>範例  
 [!INCLUDE[ssChooseProgEnv](../../../includes/sschooseprogenv-md.md)]  
  
## <a name="enabling-capture-mode-in-visual-basic"></a>在 Visual Basic 中啟用擷取模式  
 此程式碼範例會啟用擷取模式，然後顯示擷取緩衝區中保留的 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 命令。  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBCapture1](SMO How to#SMO_VBCapture1)]  -->  
  
## <a name="enabling-capture-mode-in-visual-c"></a>在 Visual C# 中啟用擷取模式  
 此程式碼範例會啟用擷取模式，然後顯示擷取緩衝區中保留的 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 命令。  
  
```  
{   
// Connect to the local, default instance of SQL Server.   
Server srv;   
srv = new Server();   
// Set the execution mode to CaptureSql for the connection.   
srv.ConnectionContext.SqlExecutionModes = SqlExecutionModes.CaptureSql;   
// Make a modification to the server that is to be captured.   
srv.UserOptions.AnsiNulls = true;   
srv.Alter();   
// Iterate through the strings in the capture buffer and display the captured statements.   
string s;   
foreach ( String p_s in srv.ConnectionContext.CapturedSql.Text ) {   
   Console.WriteLine(p_s);   
}   
// Execute the captured statements.   
srv.ConnectionContext.ExecuteNonQuery(srv.ConnectionContext.CapturedSql.Text);   
// Revert to immediate execution mode.   
srv.ConnectionContext.SqlExecutionModes = SqlExecutionModes.ExecuteSql;   
}  
```  
  
  