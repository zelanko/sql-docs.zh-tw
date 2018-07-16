---
title: 內容連接 |Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: clr
ms.tgt_pltfrm: ''
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- context connections [CLR integration]
- database objects [CLR integration], connections
- connections [CLR integration]
- context [CLR integration]
ms.assetid: 67dd1925-d672-4986-a85f-bce4fe832ef7
caps.latest.revision: 13
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: a75e69d8f455baaac1efb860a074727a829f5cd9
ms.sourcegitcommit: 022d67cfbc4fdadaa65b499aa7a6a8a942bc502d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/03/2018
ms.locfileid: "37349656"
---
# <a name="context-connection"></a>內容連接
  內部資料存取的問題是很常見的案例。 也就是說，您想要存取執行 Commn Language Runtime (CLR) 預存程序或函數所在的同一部伺服器。 有一個選擇是使用 `System.Data.SqlClient.SqlConnection` 建立連接，指定指向本機伺服器的連接字串，並開啟連接。 這需要指定認證以進行登入。 連接與預存程序或函數位於不同的資料庫工作階段中，因此可能會具有不同的 `SET` 選項、位於單獨交易中，或是找不到暫存資料表等。 如果 Managed 預存程序或函數程式碼是在 SQL Server 處理序中執行的，則會是因為其他使用者已連接至該伺服器並執行 SQL 陳述式來叫用它。 您可能會想讓預存程序或函數在該連接的內容及其交易、`SET` 選項等條件中執行。 這就稱為內容連接。  
  
 內容連接可讓您在第一次叫用程式碼的同一內容中執行 Transact-SQL 陳述式。 為了取得內容連接，必須使用 "context connection" 連接字串關鍵字，如下列範例所示：  
  
 [C#]  
  
```  
using(SqlConnection connection = new SqlConnection("context connection=true"))   
{  
    connection.Open();  
    // Use the connection  
}  
```  
  
 [Visual Basic]  
  
```  
Using connection as new SqlConnection("context connection=true")  
    connection.Open()  
    ' Use the connection  
End Using  
  
```  
  
## <a name="in-this-section"></a>本節內容  
 [一般連線與內容連線的比較](context-connections-vs-regular-connections.md)  
 描述正常連接及內容連接之間的差異。  
  
 [一般和內容連線的限制](context-connections-and-regular-connections-restrictions.md)  
 描述正常連接及內容連接的限制。  
  
  
