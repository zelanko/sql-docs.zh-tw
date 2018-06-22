---
title: 內容連接 |Microsoft 文件
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.suite: sql
ms.technology: reference
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
ms.openlocfilehash: 0ad8307d9423b25d01a802b65fbd66d0c20ac31c
ms.sourcegitcommit: a78fa85609a82e905de9db8b75d2e83257831ad9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2018
ms.locfileid: "35696019"
---
# <a name="context-connection"></a>內容連接
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  內部資料存取的問題是很常見的案例。 也就是說，您想要存取執行 Commn Language Runtime (CLR) 預存程序或函數所在的同一部伺服器。 其中一個選項是建立連接，使用**System.Data.SqlClient.SqlConnection**，指定連接字串指向本機伺服器，並開啟連接。 這需要指定認證以進行登入。 連接位於不同的資料庫工作階段的預存程序或函式，因此可能具有不同**設定**選項、 位於單獨交易中，不會看到您的暫存資料表，依此類推。 如果 Managed 預存程序或函數程式碼是在 SQL Server 處理序中執行的，則會是因為其他使用者已連接至該伺服器並執行 SQL 陳述式來叫用它。 您可能想要其交易，該連接的內容中執行函式的預存程序**設定**選項，等等。 這就稱為內容連接。  
  
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
 [一般與內容連接](../../../relational-databases/clr-integration/data-access/context-connections-vs-regular-connections.md)  
 描述正常連接及內容連接之間的差異。  
  
 [一般和內容連接的限制](../../../relational-databases/clr-integration/data-access/context-connections-and-regular-connections-restrictions.md)  
 描述正常連接及內容連接的限制。  
  
  
