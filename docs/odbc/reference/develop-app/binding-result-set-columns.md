---
description: 繫結結果集資料行
title: 系結結果集資料行 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- result sets [ODBC], binding columns
- binding columns [ODBC]
ms.assetid: 4bc9c30f-83ae-4766-a746-032953c187ad
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e6a228de81deb5cdfdaa62ee7940185b14bcaef8
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88499941"
---
# <a name="binding-result-set-columns"></a>繫結結果集資料行
應用程式可以在其選擇的情況下，系結任意數量或數量的結果集資料行，包括完全沒有系結的資料行。 提取資料列時，驅動程式會將系結資料行的資料傳回到應用程式。 應用程式是否系結結果集中的所有資料行，都取決於應用程式。 例如，產生報表的應用程式通常會有固定格式;這類應用程式會建立結果集，其中包含報表中使用的所有資料行，然後系結和取得所有這些資料行的資料。 顯示完整資料螢幕的應用程式有時可讓使用者決定要顯示的資料行;這類應用程式會建立一個結果集，其中包含使用者可能想要的所有資料行，但只系結和取得使用者所選資料行的資料。  
  
 您可以藉由呼叫 **SQLGetData**，從未系結的資料行中取出資料。 這通常是用來取出長資料（通常超過單一緩衝區的長度），而且必須在元件中取出。  
  
 您可以隨時系結資料行，即使是在提取資料列之後也一樣。 不過，在下一次提取資料列之前，新的系結不會生效;它們不會套用至已提取資料列中的資料。  
  
 變數會一直系結至資料行，直到不同的變數系結至資料行為止， **直到使用 null** 指標做為變數的位址來解除系結資料行，直到所有資料行都使用 SQL_UNBIND 選項來呼叫 **SQLFreeStmt** ，或直到語句釋放為止。 基於這個理由，應用程式必須確定所有系結的變數只要系結，就會保持有效。 如需詳細資訊，請參閱配置 [和釋放緩衝區](../../../odbc/reference/develop-app/allocating-and-freeing-buffers.md)。  
  
 由於資料行系結只是與語句結構相關聯的資訊，因此可以依任何順序進行設定。 它們也與結果集無關。 例如，假設應用程式系結下列 SQL 語句所產生之結果集的資料行：  
  
```  
SELECT * FROM Orders  
```  
  
 如果應用程式接著執行 SQL 語句  
  
```  
SELECT * FROM Lines  
```  
  
 在相同的語句控制碼上，第一個結果集的資料行系結仍會有效，因為它們是儲存在語句結構中的系結。 在大部分的情況下，這是不佳的程式設計實務，應予以避免。 相反地，應用程式應該使用 SQL_UNBIND 選項來呼叫 **SQLFreeStmt** ，以解除所有舊資料行的系結，然後系結新資料行。
