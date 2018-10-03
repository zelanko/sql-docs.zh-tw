---
title: 預設 C 資料類型 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], pseudo-type identifiers
- pseudo-type identifiers [ODBC], about pseudo-type identifiers
- pseudo-type identifiers [ODBC]
ms.assetid: 229140ae-af8f-4ec8-9ccf-1e92360e0bac
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9c4147b1bfa5ffb1e379c3aa8be2c9ea2a9d2775
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47854106"
---
# <a name="default-c-data-types"></a>預設 C 資料類型
如果應用程式指定在 SQL_C_DEFAULT **SQLBindCol**， **SQLGetData**，或**SQLBindParameter**，驅動程式會假設 C 資料類型的輸出或輸入的緩衝區對應至 SQL 資料類型的資料行或參數繫結至緩衝區。  
  
> [!IMPORTANT]  
>  互通的應用程式不應使用 SQL_C_DEFAULT。 相反地，它們應該一律指定他們所使用之緩衝區的 C 類型。 這是因為驅動程式一定能夠正確無法判斷預設的 C 類型，原因如下：  
  
-   如果 DBMS 升級的資料行或參數的 SQL 資料類型，驅動程式無法判斷原始的 SQL 資料類型的資料行或參數。 因此，它無法判斷對應的預設 C 資料類型。  
  
-   如果驅動程式無法判斷是否已簽署的特定資料行或參數，因為通常是這個步驟時由 DBMS，驅動程式無法判斷對應的預設 C 資料類型是否應該簽署或不帶正負號。  
  
     因為程式設計的便利性只提供 SQL_C_DEFAULT，應用程式不會遺失任何功能時，它會指定實際的 C 資料類型。  
  
 顯示每個 SQL 資料類型的預設 C 資料類型的資料表包含在[轉換將資料從 SQL 到 C 資料類型](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)稍後在本附錄中。
