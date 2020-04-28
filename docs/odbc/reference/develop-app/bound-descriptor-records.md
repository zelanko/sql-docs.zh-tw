---
title: 系結描述項記錄 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- bound descriptor records [ODBC]
- descriptors [ODBC], bound descriptor records
ms.assetid: 55d09344-6682-40f6-b634-036b134ff650
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 155ef4951abddc7a73d9d4abfbc45248f33d653c
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81306305"
---
# <a name="bound-descriptor-records"></a>繫結描述項記錄
當應用程式設定描述項記錄的 SQL_DESC_DATA_PTR 欄位，使其不再包含 null 值時，*就會將*該記錄稱為「系結」。  
  
 如果描述項是 APD，則每個系結記錄都會構成系結參數。 對於輸入參數，應用程式必須在執行語句之前，先系結 SQL 語句中每個動態參數標記的參數。 針對輸出參數，應用程式不需要系結參數。  
  
 如果描述元是一個 ARD，其中描述資料庫資料的一列，則每個系結記錄都會構成系結的資料行。
