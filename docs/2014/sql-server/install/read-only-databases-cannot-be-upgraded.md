---
title: 無法升級唯讀資料庫 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- database cannot be upgraded
ms.assetid: 27964211-ea30-4390-b791-dcf225fb9ae7
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f3f751f4058d29c6ce27a5a1d608f3fb076cc300
ms.sourcegitcommit: 46a2c0ffd0a6d996a3afd19a58d2a8f4b55f93de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/15/2019
ms.locfileid: "59583251"
---
# <a name="read-only-databases-cannot-be-upgraded"></a>無法升級唯讀資料庫
  Upgrade Advisor 已確定此 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體上的某些資料庫無法升級。  
  
## <a name="component"></a>元件  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>描述  
 已偵測到唯讀資料庫。 若要升級資料庫，安裝程式必須可以寫入資料庫。  
  
## <a name="corrective-action"></a>更正動作  
 在沒有人使用資料庫，使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Enterprise Manager [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]，或 ALTER DATABASE 陳述式變更為讀寫資料庫。 下列陳述式會將資料庫變更為可讀寫。  
  
```  
USE master;  
GO  
ALTER DATABASE <database name>  
SET READ_WRITE;  
GO  
```  
  
 如需有關 ALTER DATABASE 陳述式的詳細資訊，請參閱《[!INCLUDE[tsql](../../includes/tsql-md.md)] 線上叢書》中的＜ALTER DATABASE ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)])＞主題。  
  
## <a name="see-also"></a>另請參閱  
 [Database Engine 升級問題](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 Upgrade Advisor&#91;新增&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
