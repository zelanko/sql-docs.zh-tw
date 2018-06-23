---
title: 無法升級唯讀資料庫 |Microsoft 文件
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
- database cannot be upgraded
ms.assetid: 27964211-ea30-4390-b791-dcf225fb9ae7
caps.latest.revision: 13
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 11f94ceed205d8984ed5a253e1d989211012f10f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36146691"
---
# <a name="read-only-databases-cannot-be-upgraded"></a>無法升級唯讀資料庫
  Upgrade Advisor 已確定此 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體上的某些資料庫無法升級。  
  
## <a name="component"></a>元件  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>描述  
 已偵測到唯讀資料庫。 若要升級資料庫，安裝程式必須可以寫入資料庫。  
  
## <a name="corrective-action"></a>更正動作  
 當沒有任何人使用資料庫時，使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Enterprise Manager [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]，或若要變更成讀寫資料庫的 ALTER DATABASE 陳述式。 下列陳述式會將資料庫變更為可讀寫。  
  
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
 [SQL Server 2014 Upgrade Advisor&#91;新&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  
