---
description: MSSQLSERVER_3156
title: MSSQLSERVER_3156 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 3156 (Database Engine error)
ms.assetid: 345d8ed4-177e-4ec3-bab3-25d30000e323
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 2fb5d71825e138c44cb0e7e756548fd610bbca73
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424350"
---
# <a name="mssqlserver_3156"></a>MSSQLSERVER_3156
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>詳細資料  
  
| 屬性 | 值 |  
| :-------- | :---- |  
|產品名稱|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|事件識別碼|3156|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|LDDB_CANT_WRITE|  
|訊息文字|檔案 '%ls' 無法還原到 '%ls'。 請使用 WITH MOVE 來識別該檔案的有效位置。|  
  
## <a name="explanation"></a>說明  
這個一般訊息表示由於指定的位置有問題，以致檔案無法還原邏輯檔案名稱或實體檔案名稱。  
  
### <a name="possible-causes"></a>可能的原因  
可能的原因包括：  
  
-   您可能必須對指定的 Windows 目錄有存取權。  
  
-   您所輸入的路徑可能有誤，或是指定的路徑不存在。  
  
-   檔案名稱可能正由另一檔案使用中，因而無法覆寫。  
  
## <a name="user-action"></a>使用者動作  
請查閱錯誤記錄檔中的其他訊息，以取得更多詳細資料。  
  
從指定的位置著手修正問題，例如授與存取權，或在 RESTORE 陳述式中使用 WITH MOVE 選項來重新放置檔案。  
  
## <a name="see-also"></a>另請參閱  
[將資料庫還原到新位置 &#40;SQL Server&#41;](~/relational-databases/backup-restore/restore-a-database-to-a-new-location-sql-server.md)  
[將檔案還原到新位置 &#40;SQL Server&#41;](~/relational-databases/backup-restore/restore-files-to-a-new-location-sql-server.md)  
[RESTORE &#40;Transact-SQL&#41;](~/t-sql/statements/restore-statements-transact-sql.md)  
  
