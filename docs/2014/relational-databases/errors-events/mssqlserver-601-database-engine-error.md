---
title: MSSQLSERVER_601 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- "601"
helpviewer_keywords:
- 601 (Database Engine error)
ms.assetid: 2039cc0a-9a43-4369-a04a-935e384388b6
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 9aebe73ac73ee09ed2ba6de9162877d0e70bc7e6
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48176898"
---
# <a name="mssqlserver601"></a>MSSQLSERVER_601
    
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|[SQL Server]|  
|事件識別碼|601|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱||  
|訊息文字|由於資料移動而無法繼續用 NOLOCK 掃描。|  
  
## <a name="explanation"></a>說明  
 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 無法繼續執行查詢，因為另一項交易已更新或刪除它嘗試讀取的資料。 此查詢使用的是 NOLOCK 鎖定提示或 READ UNCOMMITTED 交易隔離等級。  
  
 一般都會拒絕存取其他交易正在變更的資料，原因是資料已加上鎖定。 不過，NOLOCK 鎖定提示和 READ UNCOMMITTED 交易隔離等級可以讓查詢讀取其他交易鎖定的資料。 這稱為中途讀取 (dirty read)，因為您可以讀取尚未認可且日後可能變更的值。  
  
## <a name="user-action"></a>使用者動作  
 這項錯誤會取消查詢。 請重新送出查詢或移除 NOLOCK 鎖定提示。  
  
## <a name="see-also"></a>另請參閱  
 [MSSQLSERVER_605](mssqlserver-605-database-engine-error.md)   
 [資料表提示 &#40;Transact-SQL&#41;](/sql/t-sql/queries/hints-transact-sql-table)   
 [SELECT &#40;Transact-SQL&#41;](/sql/t-sql/queries/select-transact-sql)   
 [SET TRANSACTION ISOLATION LEVEL &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-transaction-isolation-level-transact-sql)  
  
  
