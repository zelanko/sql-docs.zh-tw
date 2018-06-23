---
title: 重新命名使用者 sys |Microsoft 文件
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
- sys user names [SQL Server]
ms.assetid: d622d646-83e4-4b6f-9a21-77b301af04b5
caps.latest.revision: 25
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 959eb9877fa4b73ff9bd307019976a05514b8f8f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36030710"
---
# <a name="rename-user-sys"></a>重新命名使用者 sys
  Upgrade Advisor 偵測到的使用者名稱**sys**資料庫中。 這個名稱是保留的。 請在升級之前重新命名使用者。 如果使用者未重新命名，在升級程序之後，資料庫將處於可疑狀態，要等到資料庫連線後才可供使用。  
  
## <a name="component"></a>元件  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>描述  
 使用者**sys**已保留。  
  
## <a name="corrective-action"></a>更正動作  
  
### <a name="before-upgrade-procedure"></a>升級前程序  
 在升級每個包含使用者的資料庫中之前**sys**，執行下列動作：  
  
1.  建立新的使用者。  
  
2.  使用下列陳述式來顯示所有使用者授與的權限**sys**和授與使用者**sys**。  
  
    ```  
    -- Return permissions granted by user sys.  
    SELECT * FROM sysprotects WHERE grantor = USER_ID('sys')  
    -- Return permissions granted to user sys.  
    SELECT * FROM sysprotects WHERE uid = USER_ID('sys')  
    ```  
  
3.  若要傳送擁有的所有物件的擁有權**sys**給新的使用者，使用**sp_changeobjectowner**。  
  
4.  卸除使用者**sys**。  
  
5.  若要還原在步驟 2 中擷取原始的權限，請使用 AS *new_user* GRANT 陳述式的子句。  
  
6.  修改指令碼以參考新使用者。 例如，包含 `SELECT * FROM sys.my`_`table` 等陳述式的指令碼必須變更為 `SELECT * FROM new_user.my_table`。  
  
### <a name="after-upgrade-procedure"></a>升級後程序  
 如果使用者**sys**已在升級之前並未重新命名，執行下列動作：  
  
1.  執行陳述式 `ALTER DATABASE db_name SET ONLINE`。 資料庫將處於 SINGLE_USER 模式中。  
  
2.  遵循「升級前程序」一節中的所有步驟。  
  
3.  執行陳述式 `ALTER DATABASE db_name SET MULTI_USER`。  
  
## <a name="see-also"></a>另請參閱  
 [Database Engine 升級問題](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 Upgrade Advisor&#91;新&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  
