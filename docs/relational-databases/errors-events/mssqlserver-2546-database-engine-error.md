---
title: MSSQLSERVER_2546 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 2546 (Database Engine error)
ms.assetid: c8f0e1b4-c7c4-45f2-9221-746714172313
caps.latest.revision: 20
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: bb3f01e875daa3ee2a12c0a7d7f927f1cd106ebd
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/19/2018
---
# <a name="mssqlserver2546"></a>MSSQLSERVER_2546
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|[SQL Server]|  
|事件識別碼|2546|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|DBCC_INDEX_MARKED_DISABLED|  
|訊息文字|資料表 'OBJECT_NAME' 上的索引 'INDEX_NAME' 已標示為停用。 請重建索引使其上線。|  
  
## <a name="explanation"></a>說明  
指定的索引已標示為離線或停用。 因此，無法檢查此索引。  
  
## <a name="user-action"></a>使用者動作  
使用 ALTER INDEX 來重建索引。  
  
## <a name="see-also"></a>另請參閱  
[ALTER INDEX &#40;Transact-SQL&#41;](~/t-sql/statements/alter-index-transact-sql.md)  
[重新組織與重建索引](~/relational-databases/indexes/reorganize-and-rebuild-indexes.md)  
  
