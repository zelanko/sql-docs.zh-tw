---
title: Filestream 和 FileTable 的系統預存程序 (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- FileTables [SQL Server], catalog views
ms.assetid: 2c83a4a7-720b-4435-a3b5-788c29f56949
caps.latest.revision: 7
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: d60b802e0f55b6b597baf2450ba97fd00cbdb381
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2018
---
# <a name="filestream-and-filetable-system-stored-procedures-transact-sql"></a>Filestream 和 FileTable 的系統預存程序 (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  本章節描述與 FileTable 和 Filestream 功能的系統預存程序。  

## <a name="filestream-and-filetable-system-stored-procedures"></a>Filestream 和 Filetable 的系統預存程序
  [s (TRANSACT-SQL)](filestream-and-filetable-sp-filestream-force-garbage-collection.md)

   強制執行 FILESTREAM 記憶體回收行程，刪除任何不必要的 FILESTREAM 檔案。

  [sp_kill_filestream_non_transacted_handles (TRANSACT-SQL)](filestream-and-filetable-sp-kill-filestream-non-transacted-handles.md)

  關閉 FileTable 資料的非交易式檔案控制代碼。


## <a name="see-also"></a>另請參閱
[Filestream](../../relational-databases/blob/filestream-sql-server.md)
<br>[Filetable](../../relational-databases/blob/filetables-sql-server.md)
<br>[Filestream 及 FileTable 動態管理檢視 (Transact-SQL)](../system-dynamic-management-views/filestream-and-filetable-dynamic-management-views-transact-sql.md)
<br>[Filestream 和 FileTable 目錄檢視 (Transact-SQL)](../system-catalog-views/filestream-and-filetable-catalog-views-transact-sql.md)
  
  
