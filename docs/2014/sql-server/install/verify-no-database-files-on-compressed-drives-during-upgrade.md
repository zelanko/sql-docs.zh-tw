---
title: 請確認沒有資料庫檔案會壓縮磁碟機上升級的程序期間 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- compressed drives [SQL Server]
ms.assetid: 63be6853-c54a-42b2-ae1a-db2175f1d28e
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 41c183c72188cccb21838e1e574992bfb723c022
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66091154"
---
# <a name="verify-that-no-database-files-are-on-compressed-drives-during-the-upgrade-process"></a>確認在升級過程中，壓縮磁碟機上沒有資料庫檔案
  Upgrade Advisor 在壓縮磁碟機上偵測到資料庫檔案。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不能在壓縮磁碟機上建立或升級資料庫。  
  
## <a name="component"></a>元件  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="corrective-action"></a>更正動作  
 當您安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 時，請為系統資料庫選取未壓縮磁碟機，並確認要升級的資料庫不在壓縮磁碟機上。 不過請注意，在資料庫升級之後，您可以在 NTFS 壓縮檔案系統上放置唯讀資料庫和唯讀次要檔案群組。  
  
## <a name="see-also"></a>另請參閱  
 [Database Engine 升級問題](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 Upgrade Advisor&#91;新增&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
