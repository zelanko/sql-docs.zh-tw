---
description: 指定連線屬性
title: 指定連接屬性 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- connection properties [ADO]
- connections [ADO]
ms.assetid: 49456201-b085-4851-9686-e814136b07be
author: rothja
ms.author: jroth
ms.openlocfilehash: 0c4d3a70388415402db3ecf8bdb21bd717a66aa6
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88979559"
---
# <a name="specifying-connection-properties"></a>指定連線屬性
您可以藉由在開啟連接之前設定**連接**物件的屬性，來提供[連接字串](../../../ado/guide/data/creating-a-connection-string.md)所指定的大部分資訊。 例如，您可以使用下列程式碼來 [建立連接字串](../../../ado/guide/data/creating-a-connection-string.md) 中所討論的連接字串，達到相同的效果。  
  
```  
With objConn  
.Provider = "SQLOLEDB"  
.Properties("Data Source") = "MySqlServer"  
   .Properties("Integrated Security") = "SSPI"  
.Open  
.DefaultDatabase = "Northwind"  
End With  
```  
  
 DefaultDatabase 只會在您開啟連接之後設定。  
  
> [!NOTE]
>  在 ADO 中，您不能使用包含分號 ( ";" 的密碼除非密碼以單引號括住，否則 ) 。
