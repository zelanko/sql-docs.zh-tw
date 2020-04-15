---
title: 繫結符紀錄 :微軟文件
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306305"
---
# <a name="bound-descriptor-records"></a>繫結描述項記錄
當應用程式設定描述符紀錄的SQL_DESC_DATA_PTR欄位,使其不再包含 null 值時,該紀錄即表示為 *「 綁定*」 。  
  
 如果描述符是 APD,則每個綁定記錄構成綁定參數。 對於輸入參數,應用程式在執行語句之前必須為 SQL 語句中的每個動態參數標記綁定參數。 對於輸出參數,應用程式不需要綁定該參數。  
  
 如果描述符是描述一行資料庫數據的 ARD,則每個綁定記錄構成一個綁定列。
