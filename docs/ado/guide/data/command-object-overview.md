---
title: 命令物件概觀 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- command object [ADO]
ms.assetid: e84a14b1-3c2a-4f7d-a966-9e08a93948df
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: d9dd8315945d07aa4c6e99dc8661c26c7d92fb95
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/05/2019
ms.locfileid: "66718463"
---
# <a name="command-object-overview"></a>Command 物件概觀
具有**命令**物件時，您可以執行下列動作：  
  
-   定義所使用的命令 （例如，SQL 陳述式或預存程序） 的可執行檔的文字**CommandText**屬性。  
  
-   使用來定義參數化的查詢或預存程序引數**參數**物件並**參數**集合。  
  
-   執行命令，並傳回**Recordset**物件，如果適當的話，利用**Execute**方法。  
  
-   使用指定的命令類型**CommandType**來最佳化效能的執行前的屬性。  
  
-   使用指定的命令文字的特定資訊**方言**屬性**命令**物件。  
  
-   控制提供者是否會儲存已備妥 （或已編譯的） 版本之前執行命令，使用**已準備**屬性。  
  
-   設定提供者會等候命令執行所使用的秒數**CommandTimeout**屬性。  
  
-   將與開啟的連接產生關聯**命令**物件，藉由設定其**ActiveConnection**屬性。  
  
-   設定**名稱**屬性來識別**命令**物件上相關聯的方法作為**連接**物件。  
  
-   傳遞**命令**物件**來源**屬性**資料錄集**為了取得資料。  
  
-   傳遞**Stream**包含命令 （例如，XML 命令），來支援它的提供者的物件。
