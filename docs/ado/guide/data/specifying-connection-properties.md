---
description: 指定連線屬性
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 2e1f7a26e66eae550bc740f2f9be5a3606650dcb
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88452830"
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
