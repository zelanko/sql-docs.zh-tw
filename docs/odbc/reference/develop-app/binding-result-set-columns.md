---
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
ms.openlocfilehash: 558ceb79d42d82477b70a028395de82cc023c170
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81306359"
---
# <a name="binding-result-set-columns"></a>繫結結果集資料行
應用程式可以在選擇時系結結果集的多個或最少資料行，包括完全不系結任何資料行。 提取資料列時，驅動程式會將系結資料行的資料傳回到應用程式。 應用程式是否系結結果集中的所有資料行都取決於應用程式。 例如，產生報表的應用程式通常會有固定格式;這類應用程式會建立結果集，其中包含報表中使用的所有資料行，然後系結和抓取所有這些資料行的資料。 顯示完整資料畫面的應用程式有時可讓使用者決定要顯示的欄;這類應用程式會建立包含使用者可能想要的所有資料行的結果集，但只會針對使用者所選擇的資料行，系結和取出資料。  
  
 藉由呼叫**SQLGetData**，可以從未系結的資料行中取出資料。 這通常會被呼叫來抓取長資料，這通常會超過單一緩衝區的長度，而且必須在部分中取得。  
  
 資料行可以隨時系結，即使在提取資料列之後也一樣。 不過，新的系結在下一次提取資料列之前不會生效;它們不會套用至已經提取的資料列中。  
  
 變數會繼續系結至資料行，直到有不同的變數系結至資料行為止，直到資料行解除系結為止，方法是呼叫具有 null 指標的**SQLBindCol**做為變數的位址，直到所有資料行都已解除系結，方法是使用 SQL_UNBIND 選項呼叫**SQLFreeStmt** ，或直到語句釋放為止。 基於這個理由，應用程式必須確定所有系結的變數只要系結，就會保持有效。 如需詳細資訊，請參閱配置[和釋放緩衝區](../../../odbc/reference/develop-app/allocating-and-freeing-buffers.md)。  
  
 因為資料行系結只是與語句結構相關聯的資訊，所以可以依任何順序設定。 它們也與結果集無關。 例如，假設應用程式系結下列 SQL 語句所產生之結果集的資料行：  
  
```  
SELECT * FROM Orders  
```  
  
 如果應用程式接著執行 SQL 語句  
  
```  
SELECT * FROM Lines  
```  
  
 在相同的語句控制碼上，第一個結果集的資料行系結仍然有效，因為這些系結是儲存在語句結構中的系結。 在大部分情況下，這是不佳的程式設計實務，應予以避免。 相反地，應用程式應該使用 SQL_UNBIND 選項來呼叫**SQLFreeStmt** ，以解除系結所有舊的資料行，然後再系結新的資料行。
