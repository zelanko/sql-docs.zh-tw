---
title: 重新命名使用者 sys |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- sys user names [SQL Server]
ms.assetid: d622d646-83e4-4b6f-9a21-77b301af04b5
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 8e227e4d382dac627626b977427aae05d0295744
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62855315"
---
# <a name="rename-user-sys"></a>重新命名使用者 sys
  Upgrade Advisor 偵測到的使用者名稱**sys**資料庫中。 這個名稱是保留的。 請在升級之前重新命名使用者。 如果使用者未重新命名，在升級程序之後，資料庫將處於可疑狀態，要等到資料庫連線後才可供使用。  
  
## <a name="component"></a>元件  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>描述  
 使用者**sys**已保留。  
  
## <a name="corrective-action"></a>更正動作  
  
### <a name="before-upgrade-procedure"></a>升級前程序  
 在升級中包含使用者的每個資料庫之前**sys**，執行下列動作：  
  
1.  建立新的使用者。  
  
2.  使用下列的陳述式來顯示所有使用者授與的權限**sys**以及授與使用者**sys**。  
  
    ```  
    -- Return permissions granted by user sys.  
    SELECT * FROM sysprotects WHERE grantor = USER_ID('sys')  
    -- Return permissions granted to user sys.  
    SELECT * FROM sysprotects WHERE uid = USER_ID('sys')  
    ```  
  
3.  若要所擁有的所有物件的擁有權轉移**sys**新的使用者，以使用**sp_changeobjectowner**。  
  
4.  卸除使用者**sys**。  
  
5.  若要還原在步驟 2 中擷取原始的權限，使用 AS *new_user* GRANT 陳述式的子句。  
  
6.  修改指令碼以參考新使用者。 例如，包含 `SELECT * FROM sys.my`_`table` 等陳述式的指令碼必須變更為 `SELECT * FROM new_user.my_table`。  
  
### <a name="after-upgrade-procedure"></a>升級後程序  
 如果使用者**sys**已升級之前無法重新命名，執行下列動作：  
  
1.  執行陳述式 `ALTER DATABASE db_name SET ONLINE`。 資料庫將處於 SINGLE_USER 模式中。  
  
2.  遵循「升級前程序」一節中的所有步驟。  
  
3.  執行陳述式 `ALTER DATABASE db_name SET MULTI_USER`。  
  
## <a name="see-also"></a>另請參閱  
 [Database Engine 升級問題](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 Upgrade Advisor&#91;新增&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
