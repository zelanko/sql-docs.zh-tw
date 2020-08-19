---
description: 目錄函式所傳回的資料
title: 目錄函數所傳回的資料 |Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4c42319520696060cd52c14c46f968badee27e20
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429360"
---
# <a name="data-returned-by-catalog-functions"></a>目錄函式所傳回的資料
每個目錄函數都會傳回資料做為結果集。 這個結果集會與其他任何結果集不同。 它通常是由在驅動程式中硬式編碼的預先定義參數化 **SELECT** 語句所產生，或是儲存在資料來源中的程式中。 如需如何從結果集取得資料的詳細資訊，請參閱 [Was 已建立結果集？](../../../odbc/reference/develop-app/was-a-result-set-created.md)。  
  
 在該函式的參考專案中，會描述每個目錄函數的結果集。 除了列出的資料行之外，結果集還可以在最後一個預先定義的資料行之後包含驅動程式專屬的資料行。 這些資料行 (有關驅動程式檔中所述的任何) 。  
  
 應用程式應該系結驅動程式特定的資料行（相對於結果集的結尾）。 也就是說，它們應該將驅動程式專屬的資料行數目計算為最後一次抓取資料行的數目，並以 **SQLNumResultCols** 減少在必要資料行之後發生的資料行數目。 如此一來，當新的資料行加入至未來版本的 ODBC 或驅動程式時，就必須變更應用程式。 若要讓此配置正常運作，驅動程式必須在舊的驅動程式專屬資料行之前加入新的驅動程式專用資料行，讓資料行編號不會隨著結果集的結尾而變更。  
  
 結果集中傳回的識別碼不會加上引號，即使它們包含特殊字元也是一樣。 例如，假設 (的識別碼引號字元，它是驅動程式特定的，而且透過 **SQLGetInfo**) 會以雙引號括住 ( ") 和 Accounts Accounts 資料表包含名為 Customer Name 的資料行。 在 **SQLColumns** 為此資料行傳回的資料列中，TABLE_NAME 資料行的值是應付的帳戶，而不是「應付的帳戶」，而 COLUMN_NAME 資料行的值是客戶名稱，而非「客戶名稱」。 若要在「帳戶應付」資料表中取出客戶的名稱，應用程式會將這些名稱加上引號：  
  
```  
SELECT "Customer Name" FROM "Accounts Payable"  
```  
  
 如需詳細資訊，請參閱 [加上引號的識別碼](../../../odbc/reference/develop-app/quoted-identifiers.md)。  
  
 目錄函式是以類似 SQL 的授權模型為基礎，在此模式中，會根據使用者名稱和密碼進行連接，而且只會傳回使用者具有許可權的資料。 不符合此模型的個別檔案的密碼保護是由驅動程式所定義。  
  
 目錄函式所傳回的結果集會幾乎無法更新，且應用程式應該不會藉由變更這些結果集中的資料來變更資料庫的結構。
