---
title: managed_backup.fn_get_current_xevent_settings (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-functions
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- fn_get_current_xevent_settings
- smart_admin.fn_get_current_xevent_settings_TSQL
- fn_get_current_xevent_settings_TSQL
- smart_admin.fn_get_current_xevent_settings
dev_langs:
- TSQL
helpviewer_keywords:
- smart_admin.fn_get_current_xevent_settings
- fn_get_current_xevent_settings
ms.assetid: 95d3adaa-bb9d-4833-b8b4-3d9fd4f9c82a
caps.latest.revision: 11
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 26fc0678d8597cc8a56211e829bdc598c734f168
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2018
ms.locfileid: "38029533"
---
# <a name="managedbackupfngetcurrentxeventsettings-transact-sql"></a>managed_backup.fn_get_current_xevent_settings & Amp;#40;transact-SQL&AMP;#41;
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  針對 Smart Admn 支援的每個擴充事件類型各傳回 1 個資料列。  
  
 使用此函數可傳回或檢閱目前的擴充事件設定，以識別可設定的事件類型及目前的組態。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```sql  
smart_admin.fn_get_current_xevent_settings ()   
```  
  
##  <a name="Arguments"></a> 引數  
 此函數沒有任何引數。  
  
## <a name="table-returned"></a>傳回的資料表  
 擴充事件的管理、分析和作業通道為必要且預設為啟用狀態，但不可設定。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|Event_name|NVARCHAR(128)|擴充事件類型|  
|is_configurable|NVARCHAR(128)|此值設為**真**是否可設定事件，否則會設定為**False**。|  
|is_enabled|NVARCHAR(128)|如果已啟用事件，則設定為 True；如果未啟用，則設定為 False。 使用 smart_admin.sp_set_parameter 可啟用偵錯事件。|  
  
## <a name="security"></a>Security  
  
### <a name="permissions"></a>Permissions  
 需要**選取**函式的權限。  
  
## <a name="examples"></a>範例  
 下列範例會傳回所有擴充事件及其目前狀態。  
  
```  
SELECT *   
FROM smart_admin.fn_get_current_xevent_settings ()  
  
```  
  
  
