---
title: 命令物件總覽 |Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 0048765d3a5f5cb57419f9dbd755790c9931e218
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82761194"
---
# <a name="command-object-overview"></a>Command 物件概觀
使用**Command**物件，您可以執行下列動作：  
  
-   使用**CommandText**屬性定義命令的可執行文字（例如，SQL 語句或預存程式）。  
  
-   使用**參數**物件和**Parameters**集合，定義參數化查詢或預存程式引數。  
  
-   執行命令，並使用**execute**方法傳回**記錄集**物件（如果適用的話）。  
  
-   在執行之前使用**CommandType**屬性指定命令的類型，以優化效能。  
  
-   使用**command**物件的**方言**屬性，指定有關命令文字的特定資訊。  
  
-   控制提供者是否會在執行之前，使用**備**妥的屬性來儲存已備妥（或已編譯）的命令版本。  
  
-   使用**CommandTimeout**屬性，設定提供者將等候命令執行的秒數。  
  
-   藉由設定其**ActiveConnection**屬性，讓開啟的連接與**命令**物件產生關聯。  
  
-   設定 [**名稱**] 屬性，將**命令**物件識別為相關聯**連接**物件上的方法。  
  
-   將**命令**物件傳遞至**記錄集**的**Source**屬性，以便取得資料。  
  
-   將包含命令的**資料流程**物件（例如 XML 命令）傳遞給支援它的提供者。
