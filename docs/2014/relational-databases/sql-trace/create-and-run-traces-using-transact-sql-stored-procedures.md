---
title: 使用 Transact-SQL 預存程序來建立和執行追蹤 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 80347417-338d-4bea-8885-91fae5181cfe
caps.latest.revision: 7
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 92d4cc3a62f6e9c5f180b6263bd36918fe0d9d87
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37329468"
---
# <a name="create-and-run-traces-using-transact-sql-stored-procedures"></a>使用 Transact-SQL 預存程序來建立和執行追蹤
  SQL 追蹤的追蹤處理，會因您使用 Microsoft [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 或使用系統預存程序來建立和執行追蹤，而有所不同。  
  
 您可以使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]系統預存程序代替 [!INCLUDE[tsql](../../includes/tsql-md.md)] ，來建立和執行追蹤。 使用系統預存程序的追蹤處理如下：  
  
1.  使用 **sp_trace_create**建立追蹤。  
  
2.  使用 **sp_trace_setevent**加入事件。  
  
3.  (選擇性) 使用 **sp_trace_setfilter**設定篩選。  
  
4.  使用 **sp_trace_setstatus**啟動追蹤。  
  
5.  使用 **sp_trace_setstatus**停止追蹤。  
  
6.  使用 **sp_trace_setstatus**關閉追蹤。  
  
    > [!NOTE]  
    >  使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 系統預存程序會建立伺服器端的追蹤，其保證只要磁碟上有空間且未發生寫入錯誤，就不會遺失事件。 如果磁碟已滿或磁碟錯誤，則 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體會繼續執行，但追蹤會停止。 如果已設定 **c2 audit mode** ，並且發生寫入失敗，則追蹤會停止且 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體會關閉。 如需 **c2 稽核模式** 設定的詳細資訊，請參閱 [c2 稽核模式伺服器組態選項](../../database-engine/configure-windows/c2-audit-mode-server-configuration-option.md)。  
  
## <a name="in-this-section"></a>本節內容  
  
|主題|描述|  
|-----------|-----------------|  
|[最佳化 SQL 追蹤](sql-trace.md)|包含如何降低追蹤對於系統效能之影響的相關資訊。|  
|[篩選追蹤](filter-a-trace.md)|包含使用篩選進行追蹤的相關資訊。|  
|[限制追蹤檔案和資料表的大小](limit-trace-file-and-table-sizes.md)|包含如何限制追蹤資料所寫入之檔案和資料表大小的相關資訊。 請注意，只有 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 可以將追蹤資訊寫入資料表。|  
|[排程追蹤](schedule-traces.md)|包含如何設定追蹤的開始時間和結束時間之相關資訊。|  
  
## <a name="see-also"></a>另請參閱  
 [sp_trace_create &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-create-transact-sql)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)   
 [sp_trace_setfilter &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setfilter-transact-sql)   
 [sp_trace_setstatus &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setstatus-transact-sql)  
  
  
