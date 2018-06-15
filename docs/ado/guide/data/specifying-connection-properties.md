---
title: 指定連接屬性 |Microsoft 文件
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- connection properties [ADO]
- connections [ADO]
ms.assetid: 49456201-b085-4851-9686-e814136b07be
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c198eb4c8118328d68b40deed4ab0e57ff561f9c
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/11/2018
ms.locfileid: "35272658"
---
# <a name="specifying-connection-properties"></a>指定連接屬性
您可以提供許多所指定的資訊[連接字串](../../../ado/guide/data/creating-a-connection-string.md)設定屬性的屬性**連接**之前開啟連接物件。 例如，您可以達到相同的效果所述的連接字串[建立的連接字串](../../../ado/guide/data/creating-a-connection-string.md)使用下列程式碼。  
  
```  
With objConn  
.Provider = "SQLOLEDB"  
.Properties("Data Source") = "MySqlServer"  
   .Properties("Integrated Security") = "SSPI"  
.Open  
.DefaultDatabase = "Northwind"  
End With  
```  
  
 在開啟連接之後，才設定預設資料庫。  
  
> [!NOTE]
>  在 ADO 中您必須使用包含分號的密碼 （";"），除非密碼包含在單引號中。
