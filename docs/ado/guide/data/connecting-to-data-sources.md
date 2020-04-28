---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 000302715e7ce7d3a8ae53f06d61f54e98cbd883
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "67925792"
---
# <a name="connecting-to-data-sources"></a>連接到資料來源
ADO **Connection**物件代表資料來源的唯一會話，包括 DBMS、檔案存放區或逗號分隔的文字檔。 在用戶端/伺服器資料庫系統的情況下，ADO 連接可以是與伺服器的實際網路連接。  
  
 **Connection**物件支援各種[屬性和方法](../../../ado/reference/ado-api/connection-object-properties-methods-and-events.md)來指定連接設定、開啟和關閉連接、針對資料來源建立和執行命令，以及以架構資料列集的形式提供基礎資料來源設計的相關資訊等等。視提供者支援的功能而定，可能無法使用**連接**物件的某些集合、方法或屬性。  
  
 您可以使用**連接**物件或使用**記錄集**物件，連接到資料來源。  
  
 此章節包含下列主題。  
  
-   [使用 Connection 物件](../../../ado/guide/data/using-a-connection-object.md)  
  
-   [使用 Recordset 物件](../../../ado/guide/data/using-a-recordset-object.md)  
  
-   [建立連接字串](../../../ado/guide/data/creating-a-connection-string.md)  
  
-   [指定連接屬性](../../../ado/guide/data/specifying-connection-properties.md)  
  
-   [控制交易](../../../ado/guide/data/controlling-transactions-ado.md)
