---
title: 指定連接屬性 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- connection properties [ADO]
- connections [ADO]
ms.assetid: 49456201-b085-4851-9686-e814136b07be
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5aee5946f3087956a0117b88f4044ef8a6c9bd9f
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "67924132"
---
# <a name="specifying-connection-properties"></a>指定連線屬性
您可以在開啟連接之前設定**連接**物件的屬性，藉以提供[連接字串](../../../ado/guide/data/creating-a-connection-string.md)所指定的許多資訊。 例如，您可以使用下列程式碼，達到與[建立連接字串](../../../ado/guide/data/creating-a-connection-string.md)中所討論的連接字串相同的效果。  
  
```  
With objConn  
.Provider = "SQLOLEDB"  
.Properties("Data Source") = "MySqlServer"  
   .Properties("Integrated Security") = "SSPI"  
.Open  
.DefaultDatabase = "Northwind"  
End With  
```  
  
 只有在您開啟連接之後，才會設定 DefaultDatabase。  
  
> [!NOTE]
>  在 ADO 中，除非密碼以單引號括住，否則您不得使用包含分號（";"）的密碼。
