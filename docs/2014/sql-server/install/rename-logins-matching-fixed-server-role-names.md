---
title: 重新命名符合固定的伺服器角色名稱的登入 |Microsoft 文件
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
- user-defined login names [SQL Server]
- fixed server roles [SQL Server]
- renamed logins [SQL Server]
- logins [SQL Server], names
ms.assetid: 10a1d77c-3153-474f-a6a0-969556794467
caps.latest.revision: 18
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 54223b28e681115df1b4ecf11f4fb96d13c68fd9
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36033813"
---
# <a name="rename-logins-matching-fixed-server-role-names"></a>重新命名符合固定伺服器角色名稱的登入
  Upgrade Advisor 偵測到與固定伺服器角色名稱相符的一個或多個使用者自訂登入名稱。 會保留固定伺服器角色名稱。 升級之前，請先重新命名登入。  
  
## <a name="component"></a>元件  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>描述  
 下列固定伺服器角色名稱已保留，無法當做使用者自訂登入名稱使用。  
  
-   **sysadmin**  
  
-   **serveradmin**  
  
-   **setupadmin**  
  
-   **securityadmin**  
  
-   **processadmin**  
  
-   **dbcreator**  
  
-   **diskadmin**  
  
-   **bulkadmin**  
  
## <a name="corrective-action"></a>更正動作  
 升級之前，請執行下列步驟：  
  
1.  執行下列陳述式來記錄登入的安全性識別碼 (SID)。  
  
    ```  
    SELECT name, sid   
    FROM master.dbo.syslogins   
    WHERE name IN('sysadmin', 'serveradmin','setupadmin', 'securityadmin','processadmin', 'dbcreator','diskadmin','bulkadmin')  
    ```  
  
2.  卸除登入。  
  
3.  使用**sp_addlogin**系統程序來建立新的登入。 指定步驟 1 中傳回的 SID **@sid**參數的每個對應的登入。  
  
## <a name="see-also"></a>另請參閱  
 [Database Engine 升級問題](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 Upgrade Advisor&#91;新&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  
