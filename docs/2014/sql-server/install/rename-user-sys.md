---
title: 重新命名使用者 sys |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- sys user names [SQL Server]
ms.assetid: d622d646-83e4-4b6f-9a21-77b301af04b5
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ce8656df63c9d415ca09b54ecb86b87aba8bd83a
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "66092854"
---
# <a name="rename-user-sys"></a>重新命名使用者 sys
  Upgrade Advisor 偵測到資料庫中有使用者名稱**sys** 。 這個名稱是保留的。 請在升級之前重新命名使用者。 如果使用者未重新命名，在升級程序之後，資料庫將處於可疑狀態，要等到資料庫連線後才可供使用。  
  
## <a name="component"></a>元件  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>描述  
 使用者**sys**已保留。  
  
## <a name="corrective-action"></a>更正動作  
  
### <a name="before-upgrade-procedure"></a>升級前程序  
 在升級之前，請在包含使用者**sys**的每個資料庫中執行下列動作：  
  
1.  建立新的使用者。  
  
2.  使用下列語句來顯示由使用者**sys**授與並授與使用者**sys**的擁有權限。  
  
    ```  
    -- Return permissions granted by user sys.  
    SELECT * FROM sysprotects WHERE grantor = USER_ID('sys')  
    -- Return permissions granted to user sys.  
    SELECT * FROM sysprotects WHERE uid = USER_ID('sys')  
    ```  
  
3.  若要將**sys**所擁有之所有物件的擁有權轉移給新的使用者，請使用**sp_changeobjectowner**。  
  
4.  卸載使用者**sys**。  
  
5.  若要還原在步驟2中所捕獲的原始許可權，請使用 GRANT 語句的 AS *new_user*子句。  
  
6.  修改指令碼以參考新使用者。 例如，包含 `SELECT * FROM sys.my`_`table` 等陳述式的指令碼必須變更為 `SELECT * FROM new_user.my_table`。  
  
### <a name="after-upgrade-procedure"></a>升級後程序  
 如果在升級之前未重新命名使用者**sys** ，請執行下列動作：  
  
1.  執行陳述式 `ALTER DATABASE db_name SET ONLINE`。 資料庫將處於 SINGLE_USER 模式中。  
  
2.  遵循「升級前程序」一節中的所有步驟。  
  
3.  執行陳述式 `ALTER DATABASE db_name SET MULTI_USER`。  
  
## <a name="see-also"></a>另請參閱  
 [資料庫引擎升級問題](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 Upgrade Advisor &#91;新的&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
