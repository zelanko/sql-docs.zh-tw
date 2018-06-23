---
title: 移除卸除系統物件的陳述式 |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- drop system objects [SQL Server]
ms.assetid: cdfc3c50-c801-4039-a4bf-b35f876f1c61
caps.latest.revision: 18
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 4c017e6fedbc7fd994e5b2d2ca4de184a082da65
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36023923"
---
# <a name="remove-statements-that-drop-system-objects"></a>移除卸除系統物件的陳述式
  Upgrade Advisor 偵測到卸除系統物件的陳述式。 系統物件，包含擴充預存程序，部署在唯讀**資源**資料庫 (mssqlsystemresource) 中，而且無法卸除。 請修改您的應用程式，以便撤銷或拒絕系統物件的 EXECUTE 權限。  
  
## <a name="component"></a>元件  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>描述  
 陳述式，例如卸除資料表，卸除程序和**sp_dropextendedproc**無法用來移除系統物件中，因為這些物件部署在唯讀**資源**資料庫。  
  
## <a name="corrective-action"></a>更正動作  
 請移除嘗試從應用程式中卸除系統物件的所有陳述式。 請修改您的應用程式，以便撤銷或拒絕系統物件的 EXECUTE 權限。 或者，您也可以使用介面區組態 (SAC) 工具來停用其中某些物件。 例如， **xp_cmdshell**擴充預存程序可以停用或啟用使用 SAC 工具。  
  
## <a name="see-also"></a>另請參閱  
 [Database Engine 升級問題](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 Upgrade Advisor&#91;新&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  
