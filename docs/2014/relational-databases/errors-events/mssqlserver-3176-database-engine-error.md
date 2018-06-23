---
title: MSSQLSERVER_3176 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- 3176 (Database Engine error)
ms.assetid: 4be24c64-2d52-4cb4-b4d7-36efbe4555b6
caps.latest.revision: 12
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 4d9c0da49aaf3f2cb8d55bf63923d6f718ff26f4
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36133719"
---
# <a name="mssqlserver3176"></a>MSSQLSERVER_3176
    
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|事件識別碼|3176|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|LDDB_FILE_CLAIM|  
|訊息文字|檔案 '%ls' 已被 '%ls'(%d) 和 '%ls'(%d) 所要求。 WITH MOVE 子句可以用來重新放置一個或多個檔案。|  
  
## <a name="explanation"></a>說明  
 試圖使用單一檔案從事多種用途。  
  
### <a name="possible-causes"></a>可能的原因  
 檔案名稱正由另一資料庫使用中。  
  
## <a name="user-action"></a>使用者動作  
 請將資料庫檔案還原到其他位置。 在 RESTORE 陳述式中，使用 WITH MOVE 子句搬移每個檔案。 使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 開啟 [還原資料庫] 對話方塊，在 [選項] 頁面的 [將資料庫檔案還原為] 方格中變更檔案位置。  
  
## <a name="see-also"></a>另請參閱  
 [將資料庫還原到新位置 &#40;SQL Server&#41;](../backup-restore/restore-a-database-to-a-new-location-sql-server.md)   
 [檔案還原到新位置&#40;SQL Server&#41;](../backup-restore/restore-files-to-a-new-location-sql-server.md)   
 [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)  
  
  
