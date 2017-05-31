---
title: MSSQLSERVER_2596 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 2596 (Database Engine error)
ms.assetid: 49ab892f-8ba3-4ba1-b562-ddf205019802
caps.latest.revision: 18
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 669ad8fa565b39b8a589bf2940b91059d6355bb0
ms.contentlocale: zh-tw
ms.lasthandoff: 04/11/2017

---
# <a name="mssqlserver2596"></a>MSSQLSERVER_2596
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|2596|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|DBCC_DATABASE_IN_READ_ONLY_MODE|  
|訊息文字|未處理修復陳述式。 資料庫不可以是唯讀模式。|  
  
## <a name="explanation"></a>說明  
此訊息指出資料庫為唯讀模式。 當資料庫處於唯讀模式時，便無法進行修復。  
  
## <a name="user-action"></a>使用者動作  
使用 ALTER DATABASE 將資料庫設定成讀取/寫入，然後重新執行 DBCC 命令。  
  
## <a name="see-also"></a>另請參閱  
[ALTER DATABASE &#40;Transact-SQL&#41;](~/t-sql/statements/alter-database-transact-sql-set-options.md)  
  

