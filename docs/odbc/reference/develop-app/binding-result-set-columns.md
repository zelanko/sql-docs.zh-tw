---
title: 繫結結果集資料行 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- result sets [ODBC], binding columns
- binding columns [ODBC]
ms.assetid: 4bc9c30f-83ae-4766-a746-032953c187ad
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0377442c56b02ab9a93f5737a7f1f42275aba205
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32910823"
---
# <a name="binding-result-set-columns"></a>繫結結果集資料行
應用程式可以做為多或較少的資料行結果集選擇，包括完全沒有資料行繫結的繫結。 時擷取資料的資料列，驅動程式會傳回至應用程式的繫結的資料行的資料。 是否應用程式中的繫結的所有資料行的結果集取決於應用程式。 比方說，通常是產生報告的應用程式有固定的格式。這類應用程式建立結果集包含所有在報表中使用的資料行和再繫結，以及擷取所有這些資料行的資料。 有時候顯示螢幕的資料完整的應用程式可讓使用者決定要顯示的資料行這類應用程式會建立包含使用者可能會想，但繫結，並只為這些使用者選擇的資料行擷取資料的所有資料行的結果集。  
  
 可以從繫結的資料行擷取資料，藉由呼叫**SQLGetData**。 這通常稱為擷取通常超過單一緩衝區的長度，且必須擷取部分的 long 資料。  
  
 資料行可以在任何時間，即使已經提取的資料列繫結。 不過，新的繫結才會生效之前擷取的資料列; 在下一次不會套用至資料從已經提取的資料列。  
  
 變數維持繫結至資料行，直到不同的變數繫結至資料行，直到資料行藉由呼叫未繫結**SQLBindCol**以 null 指標做為變數的位址，直到所有資料行藉由呼叫未繫結**SQLFreeStmt** SQL_UNBIND 選項時，或釋放陳述式之前。 基於這個理由，應用程式必須確定所有的繫結的變數維持有效，只要它們繫結。 如需詳細資訊，請參閱[Allocating 和釋放緩衝區](../../../odbc/reference/develop-app/allocating-and-freeing-buffers.md)。  
  
 因為資料行繫結就與陳述式結構相關聯的資訊，您可以依照任何順序設定。 它們也是獨立的結果集。 例如，假設應用程式繫結的下列 SQL 陳述式所產生的結果集資料行：  
  
```  
SELECT * FROM Orders  
```  
  
 如果應用程式接著會執行 SQL 陳述式  
  
```  
SELECT * FROM Lines  
```  
  
 在相同的陳述式控制代碼，第一個結果集的資料行繫結是仍在作用中因為這些是儲存在陳述式結構中的繫結。 在大部分情況下，這是不佳的程式設計作法，而且應該避免。 相反地，應用程式應該呼叫**SQLFreeStmt**解除繫結所有舊的資料行，並接著將新的繫結的 SQL_UNBIND 選項。
