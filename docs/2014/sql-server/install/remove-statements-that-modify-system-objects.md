---
title: 移除修改系統物件的陳述式 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- direct system catalog updates [SQL Server]
- system catalogs [SQL Server]
ms.assetid: 221b46c2-c27e-4df8-bd8c-8b990d6d5e98
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c722d1d40d206ab300b4b6c90fdf6648575c356b
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/23/2019
ms.locfileid: "66093008"
---
# <a name="remove-statements-that-modify-system-objects"></a>移除修改系統物件的陳述式
  Upgrade Advisor 偵測到更新系統目錄的陳述式。 不允許直接更新系統目錄。 請修改您的 SQL 指令碼，以使用官方與有記載的應用程式開發介面。  
  
## <a name="component"></a>元件  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>描述  
 不允許直接更新系統目錄。 任何執行這個動作的嘗試都將產生下列錯誤：  
  
 `Server: Msg 259, Level 16, State 1, Line 1`  
  
 `Ad hoc updates to system catalogs are not allowed.`  
  
## <a name="corrective-action"></a>更正動作  
 請修改您的 SQL 指令碼，以使用官方與有記載的應用程式開發介面。 例如，使用 ALTER DATABASE *database_name* SET EMERGENCY，而不是執行 UPDATE 陳述式**sysdatabases**系統資料表。  
  
## <a name="see-also"></a>另請參閱  
 [Database Engine 升級問題](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 Upgrade Advisor&#91;新增&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  
