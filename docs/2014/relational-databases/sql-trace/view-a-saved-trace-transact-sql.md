---
title: 檢視已儲存的追蹤 (Transact-SQL) | Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- traces [SQL Server], viewing
- displaying traces
- viewing traces
ms.assetid: 3a95a816-aa89-4d5f-858c-968a9cb3ee87
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 16adeb7225df27d571e3c8ea30daa44151f3c19c
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "63285576"
---
# <a name="view-a-saved-trace-transact-sql"></a>檢視已儲存的追蹤 (Transact-SQL)
  此主題描述如何使用內建函數來檢視已儲存的追蹤。  
  
### <a name="to-view-a-specific-trace"></a>若要檢視特定追蹤  
  
1.  執行 **fn_trace_getinfo** ，並指定需要其資訊的追蹤識別碼。 此函數會傳回資料表，其中列出追蹤、追蹤屬性和屬性的相關資訊。  
  
     以下列方式叫用函數：  
  
    ```  
    SELECT *  
    FROM ::fn_trace_getinfo(trace_id)  
    ```  
  
### <a name="to-view-all-existing-traces"></a>若要檢視現有的所有追蹤  
  
1.  執行 **fn_trace_getinfo** ，並指定 `0` 或 `default`。 此函數會傳回資料表，其中列出所有追蹤、追蹤屬性和這些屬性的相關資訊。  
  
     以下列方式叫用函數：  
  
    ```  
    SELECT *  
    FROM ::fn_trace_getinfo(default)  
    ```  
  
## <a name="net-framework-security"></a>.NET Framework 安全性  
 若要執行內建函數 **fn_trace_getinfo**，使用者需要下列權限：  
  
 伺服器上的 ALTER TRACE。  
  
## <a name="see-also"></a>另請參閱  
 [sys.fn_trace_getinfo &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/sys-fn-trace-getinfo-transact-sql)   
 [使用 SQL Server Profiler 檢視和分析追蹤](../../tools/sql-server-profiler/view-and-analyze-traces-with-sql-server-profiler.md)  
  
  
