---
title: 移除未記載之系統資料表的參考 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- undocumented system tables [SQL Server]
- system tables [SQL Server]
ms.assetid: 010b1236-2219-4bf4-a6db-e3fc3abfa37a
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 06249aa1849a1be9af40e183724e85b0f318f3dc
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "66093150"
---
# <a name="remove-references-to-undocumented-system-tables"></a>移除未記載之系統資料表的參考
  在舊版本中未記載的許多系統資料表都已變更或不存在，因此，在升級之後，使用這些資料表可能導致錯誤發生。 因為 Upgrade Advisor 會尋找系統資料表名稱的參考，所以它會報告與系統資料表有相同名稱的任何使用者資料表的參考。  
  
## <a name="component"></a>元件  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>描述  
 下列未記載的系統資料表已移除：  
  
-   **spt_datatype_info**  
  
-   **spt_datatype_info_ext**  
  
-   **spt_provider_types**  
  
-   **spt_server_info**  
  
-   **spt_values**  
  
-   **sysfulltextnotify**  
  
-   **syslocks**  
  
-   **sysproperties**  
  
-   **sysprotects_aux**  
  
-   **sysprotects_view**  
  
-   **SYSREMOTE_CATALOGS**  
  
-   **SYSREMOTE_COLUMN_PRIVILEGES**  
  
-   **SYSREMOTE_COLUMNS**  
  
-   **SYSREMOTE_FOREIGN_KEYS**  
  
-   **SYSREMOTE_INDEXES**  
  
-   **SYSREMOTE_PRIMARY_KEYS**  
  
-   **SYSREMOTE_PROVIDER_TYPES**  
  
-   **SYSREMOTE_SCHEMATA**  
  
-   **SYSREMOTE_STATISTICS**  
  
-   **SYSREMOTE_TABLE_PRIVILEGES**  
  
-   **SYSREMOTE_TABLES**  
  
-   **SYSREMOTE_VIEWS**  
  
-   **syssegments**  
  
-   **sysxlogins**  
  
## <a name="corrective-action"></a>更正動作  
 根據下表修改您的應用程式。  
  
|取代|用法|  
|----------------|---------|  
|**sysfulltextnotify**|OBJECTPROPERTYEX 函數的**TableFulltextPendingChanges**屬性。|  
|**syslocks**|**dm_tran_locks**動態管理檢視] 或 [sp_lock] 或 [ **syslockinfo** ] 相容性檢視。|  
|**sysproperties**|**extended_properties**目錄檢視或**fn_listextendedproperty**函數|  
|**sysxlogins**|**server_principals**目錄檢視或**syslogins**相容性檢視。|  
|所有**spt_** 資料表|沒有可用的取代項目|  
  
## <a name="see-also"></a>另請參閱  
 [資料庫引擎升級問題](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 Upgrade Advisor &#91;新的&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
