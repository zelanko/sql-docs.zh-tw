---
title: MSSQLSERVER_3181 | Microsoft Docs
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
- 3181 (Database Engine error)
ms.assetid: e6d2e716-5263-477c-ad0e-7bcbfef4c1f3
caps.latest.revision: 13
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 745311b0a43b588bc1aead412a0c47c9ba943bb3
ms.lasthandoff: 04/11/2017

---
# <a name="mssqlserver3181"></a>MSSQLSERVER_3181
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|事件識別碼|3181|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|LDDB_STORAGE_VERIFY|  
|訊息文字|嘗試還原這個備份可能會遭遇儲存空間的問題。 後續的訊息將會提供詳細資料。|  
  
## <a name="explanation"></a>說明  
RESTORE VERIFYONLY 陳述式會檢查資料庫還原所在磁碟的可用儲存空間。  
  
### <a name="possible-causes"></a>可能的原因  
可用的磁碟空間可能不足，無法還原受檢查的備份。  
  
## <a name="user-action"></a>使用者動作  
請將備份還原到磁碟空間足夠的位置，或增加磁碟的可用空間。  
  
## <a name="see-also"></a>另請參閱  
[將資料庫還原到新位置 &#40;SQL Server&#41;](~/relational-databases/backup-restore/restore-a-database-to-a-new-location-sql-server.md)  
[將檔案還原到新位置 &#40;SQL Server&#41;](~/relational-databases/backup-restore/restore-files-to-a-new-location-sql-server.md)  
[RESTORE &#40;Transact-SQL&#41;](~/t-sql/statements/restore-statements-transact-sql.md)  
[RESTORE VERIFYONLY &#40;Transact-SQL&#41;](~/t-sql/statements/restore-statements-verifyonly-transact-sql.md)  
  

