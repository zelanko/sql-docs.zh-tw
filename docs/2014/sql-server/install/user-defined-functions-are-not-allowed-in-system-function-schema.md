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
manager: craigg
ms.openlocfilehash: 10813b7bc0a97f0ba8a81f3f48447142659cd596
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/23/2019
ms.locfileid: "66091325"
---
# <a name="user-defined-functions-are-not-allowed-in-systemfunctionschema"></a>system_function_schema 中不允許有使用者定義函數
  Upgrade Advisor 偵測到未記載之使用者所擁有的使用者定義函數**system_function_schema**。 您無法藉由指定這個使用者建立使用者定義的系統函數。 **System_function_schema**使用者名稱不存在，而且使用者識別碼與此名稱相關聯 (UID = 4) 是保留供**sys**結構描述和限制為僅供內部使用。  
  
## <a name="component"></a>元件  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>描述  
 系統物件儲存和存取已發生下列方式的變更：  
  
-   系統物件會儲存在唯讀**資源**資料庫，然後直接不允許更新系統物件。  
  
     系統物件邏輯上會出現在**sys**每個資料庫的結構描述。 這可藉由指定單部分函數名稱，維持從任何資料庫叫用系統函數的能力。 例如，可以從任何資料庫執行 `SELECT * FROM fn_helpcollations()` 陳述式。  
  
-   未記載之的使用者**system_function_schema**已移除。  
  
-   使用者識別碼相關聯**system_function_schema** (UID = 4) 是保留供**sys**結構描述和限制為僅供內部使用。  
  
 這些變更對於使用者自訂系統函數具有下列影響：  
  
-   參考的資料定義語言 (DDL) 陳述式**system_function_schema**將會失敗。 例如，陳述式`CREATE FUNCTION system`_`function` \_ `schema.fn` \_ `MySystemFunction` ...將會失敗。  
  
-   在升級到之後[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]，所擁有的現有物件**system_function_schema**只會包含在**sys**的結構描述**主要**資料庫。 因為無法修改系統物件，這些函式可以永遠不會變更或卸除**主要**資料庫。 此外，您無法透過只指定單部分函數名稱，從其他資料庫叫用這些函數。  
  
## <a name="corrective-action"></a>更正動作  
 在升級之前，請完成下列工作：  
  
1.  變更現有使用者定義函數的擁有權**dbo**利用**sp_changeobjectowner**系統預存程序。  
  
2.  請考慮重新命名函數，讓它不會使用前置詞 'fn_'。 這可避免與目前或未來的系統函數發生可能的名稱衝突。  
  
3.  在每個使用已修改之函數的資料庫中，加入這些函數的副本。  
  
4.  取代參考**system_function_schema**具有**dbo**中所有包含使用者定義函數 DDL 陳述式的指令碼。  
  
5.  修改指令碼，以叫用這些函式來使用兩部分名稱 dbo **。**_function_name_，或三部分名稱_database_name_**。** dbo。*function_name*。  
  
 如需詳細資訊，請參閱《SQL Server 線上叢書》中的下列主題：  
  
-   ＜sp_changeobjectowner＞  
  
-   ＜使用者結構描述分隔＞  
  
-   ＜資源資料庫＞  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server 2014 Upgrade Advisor&#91;新增&#93;](sql-server-2014-upgrade-advisor.md)   
 [Database Engine 升級問題](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [移除修改系統物件的陳述式](../../../2014/sql-server/install/remove-statements-that-modify-system-objects.md)   
 [移除卸除系統物件的陳述式](../../../2014/sql-server/install/remove-statements-that-drop-system-objects.md)  
  
  
