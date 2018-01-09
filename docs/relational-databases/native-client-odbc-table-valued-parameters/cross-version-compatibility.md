---
title: "跨版本相容性 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-table-valued-parameters
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords: table-valued parameters (ODBC), cross-version compatibility
ms.assetid: 5f14850b-b85c-41e2-8116-6f5b3f5e0856
caps.latest.revision: "14"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 38f2a11a0926b53dad729137d602281cc17bf64a
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="cross-version-compatibility"></a>跨版本相容性
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  當早於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 用戶端或伺服器執行個體預期處理資料表值參數時，可能會發生跨版本衝突。  
  
 一般而言，資料表值參數功能僅適用於 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 用戶端 (使用 SQL Server Native Client 10.0)，或連接到 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] (或更新版本) 伺服器的更新版本。 目錄函數結果集中的新資料行才會顯示當連接到[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]（或更新版本） 伺服器。  
  
 如果利用舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 編譯的用戶端應用程式執行要求資料表值參數的陳述式，伺服器會透過資料轉換錯誤偵測到這個狀況，而且 ODBC 會將此狀況傳回為 SQLSTATE 07006 以及「限制的資料類型屬性違規」訊息。  
  
 如果用戶端應用程式的編譯[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client 10.0 或更新版本會嘗試使用資料表值參數，當連接到伺服器執行個體早於[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]原生用戶端會偵測到此，和 SQLBindCol，SQLBindParameter、 SQLSetDescFields 及 SQLSetDescRec 呼叫將會失敗含有 SQLSTATE 07006 和訊息 「 限制的資料類型屬性違規 （此連接的 SQL Server 版本不支援資料表值參數） 」。  
  
## <a name="see-also"></a>請參閱  
 [資料表值參數 &#40; ODBC &#41;](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)  
  
  
