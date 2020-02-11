---
title: Filestream 和 FileTable 系統預存程式（Transact-sql） |Microsoft Docs
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
ms.openlocfilehash: 1ebcaf4659d7be880f0f0e901b2eadcc9002b2d9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67942246"
---
# <a name="filestream-and-filetable-system-stored-procedures-transact-sql"></a>Filestream 和 FileTable 系統預存程式（Transact-sql）
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  本節描述 FileTable 和 Filestream 功能的系統預存程式。  

## <a name="filestream-and-filetable-system-stored-procedures"></a>Filestream 和 Filetable 系統預存程式
  [sp_filestream_force_garbage_collection (Transact-SQL)](filestream-and-filetable-sp-filestream-force-garbage-collection.md)

   強制執行 FILESTREAM 記憶體回收行程，刪除任何不必要的 FILESTREAM 檔案。

  [sp_kill_filestream_non_transacted_handles (Transact-SQL)](filestream-and-filetable-sp-kill-filestream-non-transacted-handles.md)

  關閉 FileTable 資料的非交易式檔案控制代碼。


## <a name="see-also"></a>另請參閱
[檔案資料流](../../relational-databases/blob/filestream-sql-server.md)
<br>[Filetable](../../relational-databases/blob/filetables-sql-server.md)
<br>[Filestream 及 FileTable 動態管理檢視 (Transact-SQL)](../system-dynamic-management-views/filestream-and-filetable-dynamic-management-views-transact-sql.md)
<br>[Filestream 和 FileTable 目錄檢視 (Transact-SQL)](../system-catalog-views/filestream-and-filetable-catalog-views-transact-sql.md)
  
  
