---
description: 檢視篩選資訊 (Transact-SQL)
title: 檢視篩選資訊 (Transact-SQL) | Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- displaying filter information
- filters [SQL Server], viewing
- filters [SQL Server], traces
- traces [SQL Server], filters
- viewing filter information
ms.assetid: b7e52c13-8c83-47c2-8cd0-af7a49eceb5c
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 2876e99401b050e165713da583192fbc7fa0c4be
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88324972"
---
# <a name="view-filter-information-transact-sql"></a>檢視篩選資訊 (Transact-SQL)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  此主題描述如何使用內建函數來檢視追蹤篩選資訊。  
  
### <a name="to-view-filter-information"></a>若要檢視篩選資訊  
  
1.  藉由指定需要篩選資訊的追蹤識別碼，執行 **fn_trace_getfilterinfo** 。 此函數會傳回資料表，其中列出篩選、篩選套用的資料行及篩選套用的值。  
  
     以下列方式叫用函數：  
  
    ```  
    SELECT *  
    FROM ::fn_trace_getfilterinfo(trace_id)  
    ```  
  
## <a name="see-also"></a>另請參閱  
 [sys.fn_trace_getfilterinfo &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-trace-getfilterinfo-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [SQL Server Profiler 預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sql-server-profiler-stored-procedures-transact-sql.md)  
  
  
