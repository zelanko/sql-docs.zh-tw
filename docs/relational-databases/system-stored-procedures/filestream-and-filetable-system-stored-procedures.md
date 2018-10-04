---
title: Filestream 和 FileTable 系統預存程序 (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- FileTables [SQL Server], catalog views
ms.assetid: 2c83a4a7-720b-4435-a3b5-788c29f56949
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 79d01c66d26e15518f2acdb2babfa0fa805da536
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47842364"
---
# <a name="filestream-and-filetable-system-stored-procedures-transact-sql"></a>Filestream 和 FileTable 系統預存程序 & Amp;#40;transact-SQL&AMP;#41;
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  本章節描述與 FileTable 和 Filestream 功能的系統預存程序。  

## <a name="filestream-and-filetable-system-stored-procedures"></a>Filestream 和 Filetable 系統預存程序
  [sp_filestream_force_garbage_collection & Amp;#40;transact-SQL&AMP;#41;](filestream-and-filetable-sp-filestream-force-garbage-collection.md)

   強制執行 FILESTREAM 記憶體回收行程，刪除任何不必要的 FILESTREAM 檔案。

  [sp_kill_filestream_non_transacted_handles & Amp;#40;transact-SQL&AMP;#41;](filestream-and-filetable-sp-kill-filestream-non-transacted-handles.md)

  關閉 FileTable 資料的非交易式檔案控制代碼。


## <a name="see-also"></a>另請參閱
[Filestream](../../relational-databases/blob/filestream-sql-server.md)
<br>[Filetable](../../relational-databases/blob/filetables-sql-server.md)
<br>[Filestream 及 FileTable 動態管理檢視 (Transact-SQL)](../system-dynamic-management-views/filestream-and-filetable-dynamic-management-views-transact-sql.md)
<br>[Filestream 和 FileTable 目錄檢視 (Transact-SQL)](../system-catalog-views/filestream-and-filetable-catalog-views-transact-sql.md)
  
  
