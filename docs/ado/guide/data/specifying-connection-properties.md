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
manager: craigg
ms.openlocfilehash: 885d201736adb3cd16efbea4f3907cd0aa324128
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47622756"
---
# <a name="specifying-connection-properties"></a>指定連線屬性
您可以提供所指定的資訊的大部分[連接字串](../../../ado/guide/data/creating-a-connection-string.md)藉由設定屬性**連線**之前開啟連接的物件。 例如，您可以達到相同的效果中的連接字串所述[建立的連接字串](../../../ado/guide/data/creating-a-connection-string.md)使用下列程式碼。  
  
```  
With objConn  
.Provider = "SQLOLEDB"  
.Properties("Data Source") = "MySqlServer"  
   .Properties("Integrated Security") = "SSPI"  
.Open  
.DefaultDatabase = "Northwind"  
End With  
```  
  
 只有在您開啟連接之後，才設定 DefaultDatabase。  
  
> [!NOTE]
>  在 ADO 中您必須使用包含分號的密碼 （";"），除非密碼包含在單引號中。
