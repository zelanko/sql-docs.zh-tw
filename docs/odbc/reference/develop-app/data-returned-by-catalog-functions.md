---
title: 目錄函式所傳回的資料 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- catalog functions [ODBC], result sets
- functions [ODBC], catalog functions
ms.assetid: 399e1a64-8766-4c44-81ff-445399b7a1de
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 14499071bd180a7ea709fda3eb26aeae46f229c7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68077018"
---
# <a name="data-returned-by-catalog-functions"></a>目錄函式所傳回的資料
每個目錄函數都會以結果集的形式傳回資料。 這個結果集與其他任何結果集並無不同。 它通常是由在驅動程式中硬式編碼，或儲存在資料來源之程式中的預先定義參數化**SELECT**語句所產生。 如需如何從結果集取得資料的詳細資訊，請參閱[Was 是否已建立結果集？](../../../odbc/reference/develop-app/was-a-result-set-created.md)。  
  
 針對每個目錄函數的結果集，會在該函式的參考專案中描述。 除了列出的資料行之外，結果集可以包含最後一個預先定義的資料行之後的驅動程式特定資料行。 這些資料行（如果有的話）會在驅動程式檔中說明。  
  
 應用程式應該系結相對於結果集結尾的驅動程式特定資料行。 也就是說，它們應該將驅動程式特定資料行的數目，計算為最後一個資料行的數目（以**SQLNumResultCols** ），而不是在必要資料行之後發生的資料行數目。 當新的資料行加入至未來版本的 ODBC 或驅動程式中的結果集時，這可節省變更應用程式的時間。 若要讓此配置能夠正常執行，驅動程式必須在舊的驅動程式特定資料行之前加入新的驅動程式特定的資料行，如此一來，資料行編號就不會變更為結果集的結尾。  
  
 結果集中傳回的識別碼不會加上引號，即使它們包含特殊字元亦然。 例如，假設識別碼引號字元（它是驅動程式特有的，並透過**SQLGetInfo**傳回）是雙引號（"），而帳戶的應付資料表包含名為 Customer Name 的資料行。 在**SQLColumns**為此資料行所傳回的資料列中，[TABLE_NAME] 資料行的值是 [帳戶應付]，而不是 [應付帳款]，而 [COLUMN_NAME] 資料行的值是 [客戶名稱]，而不是 [客戶名稱]。 若要在帳戶的 [應付帳款] 資料表中抓取客戶的名稱，應用程式會將這些名稱括起來：  
  
```  
SELECT "Customer Name" FROM "Accounts Payable"  
```  
  
 如需詳細資訊，請參閱[引號識別碼](../../../odbc/reference/develop-app/quoted-identifiers.md)。  
  
 目錄函數是以類似 SQL 的授權模型為基礎，其中會根據使用者名稱和密碼來建立連線，而且只會傳回使用者具有許可權的資料。 不符合此模型的個別檔案的密碼保護是由驅動程式定義的。  
  
 目錄函式所傳回的結果集會幾乎無法更新，而且應用程式應該不會藉由變更這些結果集中的資料來變更資料庫的結構。
