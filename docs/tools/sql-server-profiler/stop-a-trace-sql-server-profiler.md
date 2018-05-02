---
title: 停止追蹤 (SQL Server Profiler) |Microsoft 文件
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: sql-server-profiler
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- traces [SQL Server], stopping
- stopping traces
ms.assetid: 47c4f33d-63e0-4444-bec8-4c1c91f8e25c
caps.latest.revision: 22
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2a25d344bb188b457b70baebffcfe70678000007
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/17/2018
---
# <a name="stop-a-trace-sql-server-profiler"></a>停止追蹤 (SQL Server Profiler)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] 本主題描述如何使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 來停止執行中的追蹤。  
  
 停止追蹤便會停止擷取資料。 追蹤一旦停止，重新啟動之後將會遺失先前所擷取的資料，除非已經將資料擷取到追蹤檔或追蹤資料表。 您也可以在停止追蹤之後，將收集的資料儲存至資料表或檔案。 追蹤停止時，先前所選取的所有追蹤屬性將會保留。 此時您可以變更名稱、事件、欄位及篩選條件。  
  
### <a name="to-stop-a-trace"></a>若要停止追蹤  
  
1.  選擇執行中的追蹤。  
  
2.  在 **[檔案]** 功能表上，按一下 **[停止追蹤]**。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
