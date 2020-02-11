---
title: 延後欄位 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- descriptors [ODBC], deferred fields
- deferred fields [ODBC]
ms.assetid: 5abeb9cc-4070-4f43-a80d-ad6a2004e5f3
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c2c229d31941d5cef0da253545cecd7d1496ee4a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68076818"
---
# <a name="deferred-fields"></a>延遲的欄位
當延遲的*欄位*設定時，不會使用這些值，但是驅動程式會儲存延遲效果的變數位址。 針對應用程式參數描述元，驅動程式會在呼叫**SQLExecDirect**或**SQLExecute**時，使用變數的內容。 針對應用程式資料列描述元，驅動程式會在提取時使用變數的內容。  
  
 延遲的欄位如下：  
  
-   描述項記錄的 SQL_DESC_DATA_PTR 和 SQL_DESC_INDICATOR_PTR 欄位。  
  
-   應用程式描述項記錄的 SQL_DESC_OCTET_LENGTH_PTR 欄位。  
  
-   在多資料列提取的案例中，描述項標頭的 SQL_DESC_ARRAY_STATUS_PTR 和 SQL_DESC_ROWS_PROCESSED_PTR 欄位。  
  
 配置描述元時，每個描述項記錄的延後欄位一開始會有 null 值。 Null 值的意義如下：  
  
-   如果 SQL_DESC_ARRAY_STATUS_PTR 具有 null 值，多資料列提取就無法傳回每個資料列之診斷資訊的這個元件。  
  
-   如果 SQL_DESC_DATA_PTR 具有 null 值，則記錄為未系結。  
  
-   如果 ARD 的 SQL_DESC_OCTET_LENGTH_PTR 欄位具有 null 值，則驅動程式不會傳回該資料行的長度資訊。  
  
-   如果 APD 的 SQL_DESC_OCTET_LENGTH_PTR 欄位具有 null 值，且參數是字元字串，則驅動程式會假設字串是以 null 結束。 針對輸出動態參數，此欄位中的 null 值會防止驅動程式傳回長度資訊。 （如果 [SQL_DESC_TYPE] 欄位未指出字元字串參數，則會忽略 [SQL_DESC_OCTET_LENGTH_PTR] 欄位）。  
  
 應用程式不能解除配置或捨棄延遲欄位在其與欄位相關聯的時間和驅動程式讀取或寫入的時間之間所使用的變數。
