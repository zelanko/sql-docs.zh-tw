---
title: 移除修改系統物件的語句 |Microsoft Docs
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
ms.openlocfilehash: 526181bc4bf7ab81df2eaa25f19e7627c9b7af10
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85059159"
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
 請修改您的 SQL 指令碼，以使用官方與有記載的應用程式開發介面。 例如，使用 ALTER DATABASE *database_name*設定緊急，而不是在**sysdatabases**系統資料表上執行 UPDATE 語句。  
  
## <a name="see-also"></a>另請參閱  
 [資料庫引擎升級問題](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 Upgrade Advisor &#91;新的&#93;](https://docs.microsoft.com/sql/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  
