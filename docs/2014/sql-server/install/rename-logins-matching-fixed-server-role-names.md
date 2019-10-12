---
title: 重新命名符合固定伺服器角色名稱的登入 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- user-defined login names [SQL Server]
- fixed server roles [SQL Server]
- renamed logins [SQL Server]
- logins [SQL Server], names
ms.assetid: 10a1d77c-3153-474f-a6a0-969556794467
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: df9d9e51846e286c67a4773823207524755d15dc
ms.sourcegitcommit: 710d60e7974e2c4c52aebe36fceb6e2bbd52727c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/11/2019
ms.locfileid: "72278212"
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
  
3.  使用**sp_addlogin**系統程式來建立新的登入。 針對每個對應的登入，在 **\@sid**參數中指定步驟1中傳回的 SID。  
  
## <a name="see-also"></a>另請參閱  
 [資料庫引擎升級問題](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 Upgrade Advisor &#91;新增&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
