---
title: 跨版本相容性 |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- table-valued parameters (ODBC), cross-version compatibility
ms.assetid: 5f14850b-b85c-41e2-8116-6f5b3f5e0856
caps.latest.revision: 14
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: d256fe042562f902aeb3e6229b36f25308e3c138
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36031623"
---
# <a name="cross-version-compatibility"></a>跨版本相容性
  當早於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 用戶端或伺服器執行個體預期處理資料表值參數時，可能會發生跨版本衝突。  
  
 一般而言，資料表值參數功能僅適用於 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 用戶端 (使用 SQL Server Native Client 10.0)，或連接到 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] (或更新版本) 伺服器的更新版本。 目錄函數結果集中的新資料行才會顯示當連接到[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]（或更新版本） 伺服器。  
  
 如果利用舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 編譯的用戶端應用程式執行要求資料表值參數的陳述式，伺服器會透過資料轉換錯誤偵測到這個狀況，而且 ODBC 會將此狀況傳回為 SQLSTATE 07006 以及「限制的資料類型屬性違規」訊息。  
  
 如果用戶端應用程式的編譯[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client 10.0 或更新版本會嘗試使用資料表值參數，當連接到伺服器執行個體早於[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]原生用戶端會偵測到此，和 SQLBindCol，SQLBindParameter、 SQLSetDescFields 及 SQLSetDescRec 呼叫將會失敗含有 SQLSTATE 07006 和訊息 「 限制的資料類型屬性違規 （此連接的 SQL Server 版本不支援資料表值參數） 」。  
  
## <a name="see-also"></a>另請參閱  
 [資料表值參數&#40;ODBC&#41;](table-valued-parameters-odbc.md)  
  
  