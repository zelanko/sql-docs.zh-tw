---
title: System_function_schema 中不允許使用者定義函數 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- system functions [SQL Server]
- user-defined functions [SQL Server], system
ms.assetid: 3cb54053-ef65-4558-ae96-8686b6b22f4f
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 7242f9fda74288a2b7354ac0550ff4966e05c555
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85058779"
---
# <a name="user-defined-functions-are-not-allowed-in-system_function_schema"></a>system_function_schema 中不允許有使用者定義函數
  Upgrade Advisor 偵測到使用者定義的函數，這些函式是由未記載的使用者**system_function_schema**所擁有。 您無法藉由指定這個使用者建立使用者定義的系統函數。 **System_function_schema**的使用者名稱不存在，而且與此名稱相關聯的使用者識別碼（UID = 4）是保留供**sys**架構使用，而且僅限於內部使用。  
  
## <a name="component"></a>元件  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>描述  
 系統物件儲存和存取已發生下列方式的變更：  
  
-   系統物件會儲存在唯讀的**Resource**資料庫中，而且不允許直接系統物件更新。  
  
     系統物件在邏輯上會出現在每個資料庫的**sys**架構中。 這可藉由指定單部分函數名稱，維持從任何資料庫叫用系統函數的能力。 例如，可以從任何資料庫執行 `SELECT * FROM fn_helpcollations()` 陳述式。  
  
-   已移除未記載的使用者**system_function_schema** 。  
  
-   與**system_function_schema**相關聯的使用者識別碼（UID = 4）是保留給**sys**架構，而且僅限內部使用。  
  
 這些變更對於使用者自訂系統函數具有下列影響：  
  
-   參考**system_function_schema**的資料定義語言（DDL）語句將會失敗。 例如，語句 `CREATE FUNCTION system` _ `function` \_ `schema.fn` \_ `MySystemFunction` .。。將不會成功。  
  
-   升級至之後 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ， **system_function_schema**所擁有的現有物件只會包含在**master**資料庫的**sys**架構中。 由於無法修改系統物件，因此這些函數永遠不會變更或從**master**資料庫中卸載。 此外，您無法透過只指定單部分函數名稱，從其他資料庫叫用這些函數。  
  
## <a name="corrective-action"></a>更正動作  
 在升級之前，請完成下列工作：  
  
1.  使用**sp_changeobjectowner**系統預存程式，將現有使用者定義函數的擁有權變更為**dbo** 。  
  
2.  請考慮重新命名函數，讓它不會使用前置詞 'fn_'。 這可避免與目前或未來的系統函數發生可能的名稱衝突。  
  
3.  在每個使用已修改之函數的資料庫中，加入這些函數的副本。  
  
4.  在包含使用者定義函數 DDL 語句的所有腳本中，以**dbo**取代**system_function_schema**的參考。  
  
5.  修改用來叫用這些函式的腳本，以使用兩部分名稱 dbo **。**_function_name_，或三部分名稱_database_name_**。** 供.*function_name*。  
  
 如需詳細資訊，請參閱《SQL Server 線上叢書》中的下列主題：  
  
-   ＜sp_changeobjectowner＞  
  
-   ＜使用者結構描述分隔＞  
  
-   ＜資源資料庫＞  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server 2014 Upgrade Advisor &#91;新的&#93;](sql-server-2014-upgrade-advisor.md)   
 [資料庫引擎升級問題](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [移除修改系統物件的語句](../../../2014/sql-server/install/remove-statements-that-modify-system-objects.md)   
 [移除卸除系統物件的陳述式](../../../2014/sql-server/install/remove-statements-that-drop-system-objects.md)  
  
  
