---
title: "連接到資料來源 |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: connections [ADO]
ms.assetid: 82770486-37bd-4c90-885f-6817a7c77ad7
caps.latest.revision: "12"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: dafec45c1acbe10277738f809c0804dc298be282
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="connecting-to-data-sources"></a>連接到資料來源
ADO**連接**物件都代表唯一的工作階段與資料來源，包括 DBMS、 檔案存放區中或以逗號分隔的文字檔。 在用戶端/伺服器資料庫系統，ADO 連接可以是實際的網路連線到伺服器。  
  
 **連接**物件支援各種[屬性和方法](../../../ado/reference/ado-api/connection-object-properties-methods-and-events.md)指定連線設定，開啟和關閉連接，建立和執行命令對資料來源並提供有關設計的基礎資料來源的結構描述資料列形式的資訊，等等。根據提供者、 某些集合、 方法或屬性所支援的功能**連接**物件可能無法使用。  
  
 您可以連接到資料來源使用**連接**物件，或使用**資料錄集**物件。  
  
 此章節包含下列主題。  
  
-   [使用 Connection 物件](../../../ado/guide/data/using-a-connection-object.md)  
  
-   [使用 Recordset 物件](../../../ado/guide/data/using-a-recordset-object.md)  
  
-   [建立連接字串](../../../ado/guide/data/creating-a-connection-string.md)  
  
-   [指定連接屬性](../../../ado/guide/data/specifying-connection-properties.md)  
  
-   [控制交易](../../../ado/guide/data/controlling-transactions-ado.md)
