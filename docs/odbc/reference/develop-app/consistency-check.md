---
title: "一致性檢查 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- descriptors [ODBC], consistency checks
- consistency checks [ODBC]
ms.assetid: deb80efa-ad1f-4ea5-b334-9817cd279e5c
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 81ecac0249bc5e981c95b319f64768d45b792b96
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="consistency-check"></a>一致性檢查
一致性檢查驅動程式自動執行應用程式在設定 SQL_DESC_DATA_PTR 欄位 APD、 ARD，或 IPD 時。 每當設定此欄位時，驅動程式會檢查 SQL_DESC_TYPE 欄位的值以及適用於同一筆記錄中的 SQL_DESC_TYPE 欄位的值有效，而且一致。  
  
 通常未設定 SQL_DESC_DATA_PTR 欄位的 IPD;不過，應用程式可以進行強制 IPD 欄位的一致性檢查。 IPD 的 SQL_DESC_DATA_PTR 欄位設定為值實際上不會儲存且無法擷取由呼叫**SQLGetDescField**或**SQLGetDescRec**; 只以強制進行設定一致性檢查。 無法在 IRD 上執行一致性檢查。  
  
 如需有關一致性檢查的詳細資訊，請參閱[SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md)。

