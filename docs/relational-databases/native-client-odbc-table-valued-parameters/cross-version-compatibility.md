---
title: 跨版本相容性 |微軟文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- table-valued parameters (ODBC), cross-version compatibility
ms.assetid: 5f14850b-b85c-41e2-8116-6f5b3f5e0856
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 7990072ac539addf733720fd8c1eaba0652f5d70
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304502"
---
# <a name="cross-version-compatibility"></a>跨版本相容性
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  當早於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 用戶端或伺服器執行個體預期處理資料表值參數時，可能會發生跨版本衝突。  
  
 一般而言，資料表值參數功能僅適用於 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 用戶端 (使用 SQL Server Native Client 10.0)，或連接到 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] (或更新版本) 伺服器的更新版本。 目錄函數結果集中的新列僅在連接到[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)](或更高版本)伺服器時才會存在。  
  
 如果利用舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 編譯的用戶端應用程式執行要求資料表值參數的陳述式，伺服器會透過資料轉換錯誤偵測到這個狀況，而且 ODBC 會將此狀況傳回為 SQLSTATE 07006 以及「限制的資料類型屬性違規」訊息。  
  
 如果使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本機用戶端 10.0 或更高版本編譯的用戶端應用程序嘗試在[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]連接到早於的伺服器實例時使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]表值參數, 則本機客戶端將檢測到此參數,並且 SQLBindCol、SQLBind 參數、SQLSetDescFields 和 SQLSetScRec 調用將失敗,SQLSTATE 07006 和消息「受限數據類型屬性衝突(此連接的 SQL Server 版本不支援表值參數)。  
  
## <a name="see-also"></a>另請參閱  
 [&#40;ODBC&#41;的表值参数](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)  
  
  
