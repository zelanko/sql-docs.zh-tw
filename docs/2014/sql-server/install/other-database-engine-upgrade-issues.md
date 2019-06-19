---
title: 其他 Database Engine 升級問題 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Database Engine [SQL Server], upgrading
ms.assetid: 78a1d8e8-fa97-476f-8777-84617d145340
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f247f9addde6baa949f3260d7a9d9f86ce0c5bff
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66093703"
---
# <a name="other-database-engine-upgrade-issues"></a>其他 Database Engine 升級問題
  目前的 Upgrade Advisor 版本無法偵測到下列升級問題。 請檢閱下列問題，以便評估它們可能對您系統造成的影響。  
  
## <a name="multiple-database-engine-deprecated-features"></a>多個 Database Engine 已被取代的功能  
 下列 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式或選項會被取代：  
  
-   BACKUP LOG 的 NO_LOG 和 TRUNCATE_ONLY 選項  
  
-   BACKUP TRANSACTION  
  
-   RESTORE TRANSACTION  
  
-   DUMP  
  
-   LOAD  
  
-   DBCC CONCURRENCYVIOLATION  
  
-   sp_addalias  
  
-   sp_addgroup  
  
-   sp_changegroup  
  
-   sp_dropgroup  
  
-   sp_helpgroup  
  
-   syssegments  
  
 使用 VIA 通訊協定連接至 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 已被取代。  
  
## <a name="new-data-types"></a>新的資料類型  
 下面是保留的系統類型。 請在升級之前或之後，重新命名現有且衝突的使用者定義型別。  
  
-   Geography  
  
-   幾何  
  
-   Datetime2  
  
-   HierarchyID  
  
## <a name="target-table-of-the-output-into-clause-cannot-have-any-defined-triggers"></a>OUTPUT INTO 子句的目標資料表不得具有任何已定義的觸發程序  
 不支援 OUTPUT INTO 目標資料表時的資料表有任何啟用的觸發程序。  
  
## <a name="compile-time-error-for-udfs-when-the-target-of-an-output-into-clause-is-a-table"></a>當 OUTPUT INTO 子句的目標是資料表時，就會針對 UDF 發生編譯時間錯誤  
 使用者定義函數 (UDF) 無法用於執行修改資料庫狀態的動作。 例如，UDF 無法針對任何物件 (資料表變數除外) 執行任何 DDL (CREATE/ALTER/DROP) 或 DML (INSERT/UPDATE/DELETE) 動作。  
  
## <a name="merge-is-a-reserved-keyword"></a>MERGE 是保留關鍵字  
 MERGE 現在是完整的保留關鍵字。 應用程式不能再具有名為 MERGE 的物件 (資料表、資料行等等)。  
  
## <a name="rename-cdc-schema"></a>重新命名 CDC 結構描述  
 有名稱為 CDC 的結構描述。 此結構描述名稱不能在用於**異動資料擷取**啟用資料庫。  
  
 啟用之前，您必須卸除 CDC 結構描述**異動資料擷取**資料庫。 您可以在升級之前或之後完成此步驟。 若要卸除此結構描述，請使用下列步驟：  
  
1.  使用 ALTER SCHEMA，將這些物件從 CDC 結構描述傳送至新的結構描述名稱。  
  
2.  確認新結構描述中物件的權限。  
  
3.  針對應用程式進行必要的修改。  
  
4.  使用 DROP SCHEMA 來卸除 CDC 結構描述。  
  
## <a name="see-also"></a>另請參閱  
 [資料庫引擎升級問題](../../../2014/sql-server/install/database-engine-upgrade-issues.md)  
  
  
