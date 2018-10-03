---
title: 繫結結果集資料行 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b92f317d72410a5dff56652dd9de1e3b2ba5c9cb
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47725906"
---
# <a name="binding-result-set-columns"></a>繫結結果集資料行
應用程式可以為多或較少的資料行，結果集，當他們選擇，包括完全沒有資料行繫結的繫結。 當擷取的資料列時，驅動程式可以傳回應用程式的繫結的資料行的資料。 不論應用程式繫結所有資料行在結果集中，則應用程式而定。 比方說，通常是產生報表的應用程式有固定的格式;這類應用程式建立結果集包含所有在報表中使用的資料行然後再繫結和擷取所有這些資料行的資料。 有時候顯示完整的資料畫面的應用程式可讓使用者決定要顯示; 的資料行這類應用程式會建立包含使用者可能會想，但繫結，並只為這些使用者所選擇的資料行擷取資料的所有資料行的結果集。  
  
 可以從繫結的資料行擷取資料，藉由呼叫**SQLGetData**。 這通常稱為擷取 long 資料，這通常超過單一緩衝區的長度，而且必須在組件中擷取。  
  
 資料行都可以在任何時間，即使已經提取的資料列繫結。 不過，新的繫結才會生效之前擷取的資料列; 在下一次不會套用至資料的已擷取的資料列。  
  
 變數在不同的變數繫結至資料行，直到資料行藉由呼叫未繫結直到繫結至資料行**SQLBindCol**做為變數的位址，直到所有資料行藉由呼叫未繫結以null指標**SQLFreeStmt**使用 SQL_UNBIND 選項時，或直到釋放陳述式。 基於這個理由，應用程式必須確定所有繫結的變數維持有效的只要它們所繫結。 如需詳細資訊，請參閱 < [Allocating 及釋放緩衝區](../../../odbc/reference/develop-app/allocating-and-freeing-buffers.md)。  
  
 因為資料行繫結只是陳述式的結構與相關聯的資訊，他們可以依任何順序設定。 它們也是獨立的結果集。 例如，假設應用程式繫結的下列 SQL 陳述式所產生的結果集資料行：  
  
```  
SELECT * FROM Orders  
```  
  
 如果應用程式接著會執行 SQL 陳述式  
  
```  
SELECT * FROM Lines  
```  
  
 在相同的陳述式控制代碼，第一個結果集的資料行繫結是仍在作用中因為這些是儲存在陳述式結構中的繫結。 在大部分情況下，這是不良的程式設計做法，而且應該予以避免。 相反地，應用程式應該呼叫**SQLFreeStmt**所有舊的資料行解除繫結，然後將新的繫結的 SQL_UNBIND 選項。
