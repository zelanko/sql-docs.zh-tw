---
title: "指定連接屬性 |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- connection properties [ADO]
- connections [ADO]
ms.assetid: 49456201-b085-4851-9686-e814136b07be
caps.latest.revision: "15"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 87bcb0bed714e3fd2719405fbd1887a7943d219d
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
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
