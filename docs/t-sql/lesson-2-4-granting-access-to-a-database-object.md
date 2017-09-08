---
title: "授與存取權的資料庫物件 |Microsoft 文件"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
helpviewer_keywords:
- granting access to database objects
ms.assetid: a44d9bbf-f58e-4734-b7f4-eb3b492b777b
caps.latest.revision: 14
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 7cc5c15a44f16e4049974ff76095a389348707c7
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="lesson-2-4---granting-access-to-a-database-object"></a>課程 2-4-授與資料庫物件的存取權
如果是管理員，可以從 **Products** 資料表和 **vw_Names** 檢視中執行 SELECT，也可以執行 **pr_Names** 程序，但是 Mary 則無權這麼做。 若要授與 Mary 必要的權限，請使用 GRANT 陳述式。  
  
### <a name="procedure-title"></a>程序標題  
  
1.  執行下列陳述式，讓 `Mary` 具有 `EXECUTE` 預存程序的 `pr_Names` 權限。  
  
    ```  
    GRANT EXECUTE ON pr_Names TO Mary;  
    GO  
    ```  
  
在這個狀況中，Mary 只能使用預存程序來存取 **Products** 資料表。 如果您希望 Mary 能夠在檢視中執行 SELECT 陳述式，則必須也要執行 `GRANT SELECT ON vw_Names TO Mary`。 若要移除資料庫物件的存取權，請使用 REVOKE 陳述式。  
  
> [!NOTE]  
> 如果資料表、檢視和預存程序並不是由相同的結構描述所擁有，則授與權限的過程將會更加複雜。  
  
## <a name="about-grant"></a>關於 GRANT  
您必須具有 EXECUTE 權限，才能執行預存程序。 若要存取和變更資料，則必須具有 SELECT、INSERT、UPDATE 和 DELETE 權限。 GRANT 陳述式也可以用來授與其他權限，例如建立資料表的權限。  
  
## <a name="next-task-in-lesson"></a>本課程的下一項工作  
[摘要：設定資料庫物件的權限](../t-sql/lesson-2-5-summary-configuring-permissions-on-database-objects.md)  
  
## <a name="see-also"></a>另請參閱  
[GRANT &#40;Transact-SQL&#41;](../t-sql/statements/grant-transact-sql.md)  
[REVOKE &#40;Transact-SQL&#41;](../t-sql/statements/revoke-transact-sql.md)  
  
  
  

