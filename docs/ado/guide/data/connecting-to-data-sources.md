---
description: 連接到資料來源
title: 連接到資料來源 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- connections [ADO]
ms.assetid: 82770486-37bd-4c90-885f-6817a7c77ad7
author: rothja
ms.author: jroth
ms.openlocfilehash: 1de885a14dd2647df08ae6245f64a629d706796d
ms.sourcegitcommit: 33e774fbf48a432485c601541840905c21f613a0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/25/2020
ms.locfileid: "88806321"
---
# <a name="connecting-to-data-sources"></a>連接到資料來源
ADO **連接** 物件代表具有資料來源的唯一會話，包括 DBMS、檔案存放區或逗點分隔的文字檔。 在用戶端/伺服器資料庫系統的情況下，ADO 連接可以是與伺服器的實際網路連接。  
  
 **連接**物件支援各種[屬性和方法](../../reference/ado-api/connection-object-properties-methods-and-events.md)，以指定連接設定、開啟和關閉連接、針對資料來源建立和執行命令，以及提供架構資料列集的形式之基礎資料來源的設計相關資訊等。視提供者支援的功能而定，可能無法使用**連接**物件的某些集合、方法或屬性。  
  
 您可以使用 **連接** 物件或使用 **記錄集** 物件，連接到資料來源。  
  
 此章節包含下列主題。  
  
-   [使用 Connection 物件](./using-a-connection-object.md)  
  
-   [使用 Recordset 物件](./using-a-recordset-object.md)  
  
-   [建立連接字串](./creating-a-connection-string.md)  
  
-   [指定連線屬性](./specifying-connection-properties.md)  
  
-   [控制交易](./controlling-transactions-ado.md)