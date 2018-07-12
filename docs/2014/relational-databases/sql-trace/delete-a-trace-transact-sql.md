---
title: 刪除追蹤 (Transact-SQL) | Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- traces [SQL Server], deleting
- removing traces
- deleting traces
ms.assetid: a5502814-b281-42dd-b885-5c9368025ae6
caps.latest.revision: 21
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e255ab5d72c8d7d0cfd935ba971b7f1c409ee38a
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37157999"
---
# <a name="delete-a-trace-transact-sql"></a>刪除追蹤 (Transact-SQL)
  本主題說明如何使用預存程序來刪除追蹤。  
  
 如需使用追蹤預存程序的範例，請參閱[建立追蹤 &#40;Transact-SQL&#41;](create-a-trace-transact-sql.md)。  
  
### <a name="to-delete-a-trace"></a>若要刪除追蹤  
  
1.  指定 **@status = 0**，執行 **sp_trace_setstatus** 以停止追蹤。  
  
2.  指定 **@status = 2**，執行 **sp_trace_setstatus** 以關閉追蹤，並將其資訊從伺服器中刪除。  
  
> [!NOTE]  
>  您必須先關閉追蹤，才能將它刪除。  
  
## <a name="see-also"></a>另請參閱  
 [sp_trace_setstatus &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setstatus-transact-sql)   
 [系統預存程序 &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/system-stored-procedures-transact-sql)   
 [SQL Server Profiler 預存程序 &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sql-server-profiler-stored-procedures-transact-sql)  
  
  
