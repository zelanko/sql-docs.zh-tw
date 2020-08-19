---
description: 延遲的欄位
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f8b313f2d77270e95830de1a524706aa7fe36e33
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424690"
---
# <a name="deferred-fields"></a>延遲的欄位
當您設定 *延遲欄位* 的值時，不會使用這些值，但驅動程式會儲存變數的位址以獲得延遲效果。 針對應用程式參數描述項，驅動程式會在呼叫 **SQLExecDirect** 或 **SQLExecute**時，使用變數的內容。 針對應用程式資料列描述項，驅動程式會在提取時使用變數的內容。  
  
 以下是延後欄位：  
  
-   描述項記錄的 SQL_DESC_DATA_PTR 和 SQL_DESC_INDICATOR_PTR 欄位。  
  
-   應用程式描述項記錄的 SQL_DESC_OCTET_LENGTH_PTR 欄位。  
  
-   在多資料列提取的案例中，描述項標頭的 SQL_DESC_ARRAY_STATUS_PTR 和 SQL_DESC_ROWS_PROCESSED_PTR 欄位。  
  
 配置描述項之後，每個描述項記錄的延遲欄位一開始會有 null 值。 Null 值的意義如下：  
  
-   如果 SQL_DESC_ARRAY_STATUS_PTR 有 null 值，多資料列提取將無法傳回每個資料列診斷資訊的這個元件。  
  
-   如果 SQL_DESC_DATA_PTR 有 null 值，則記錄會解除系結。  
  
-   如果 ARD 的 SQL_DESC_OCTET_LENGTH_PTR 欄位有 null 值，驅動程式就不會傳回該資料行的長度資訊。  
  
-   如果 APD 的 SQL_DESC_OCTET_LENGTH_PTR 欄位有 null 值，而參數是字元字串，則驅動程式會假設字串是以 null 結束。 針對輸出動態參數，此欄位中的 null 值會防止驅動程式傳回長度資訊。  (如果 SQL_DESC_TYPE 欄位未指出字元字串參數，則會忽略 SQL_DESC_OCTET_LENGTH_PTR 欄位。 )   
  
 應用程式不能在將延遲欄位與欄位相關聯的時間以及驅動程式讀取或寫入它們的時間之間，解除配置或捨棄這些變數所使用的變數。
