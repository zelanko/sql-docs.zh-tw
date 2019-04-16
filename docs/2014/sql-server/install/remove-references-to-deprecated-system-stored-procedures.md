---
title: 移除已被取代的系統預存程序的參考 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- undocumented system stored procedures [SQL Server]
- system stored procedures [SQL Server]
ms.assetid: 487d24fc-41d5-495e-843c-0ac974ec472f
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 5f87cb9160925ccc813ee62737662f85f430f28b
ms.sourcegitcommit: 46a2c0ffd0a6d996a3afd19a58d2a8f4b55f93de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/15/2019
ms.locfileid: "59582861"
---
# <a name="remove-references-to-deprecated-system-stored-procedures"></a>移除已被取代之系統預存程序的參考
  Upgrade Advisor 偵測到陳述式參考了未記載的系統預存程序和擴充預存程序，而這些預存程序在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中已無法使用。 參考這些物件的陳述式會失敗。 請勿使用未記載的系統物件或 API，因為這些功能在未來的版本中會變更或移除，而不另行通知。  
  
## <a name="component"></a>元件  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>描述  
  
### <a name="documented-system-stored-procedures"></a>已記載的系統預存程序  
 下列已記載的系統預存程序已經被移除了：  
  
-   sp_addalias  
  
-   sp_addgroup  
  
-   sp_changegroup  
  
-   sp_dropgroup  
  
-   sp_helpgroup  
  
### <a name="undocumented-system-stored-procedures"></a>未記載的系統預存程序  
 下列未記載的系統預存程序和擴充預存程序已經被移除了：  
  
-   sp_articlesynctranprocs  
  
-   sp_diskdefault  
  
-   sp_EventLog  
  
-   sp_GetMBCSCharLen  
  
-   sp_helplog  
  
-   sp_helpsql  
  
-   sp_IsMBCSLeadByte  
  
-   sp_lock2  
  
-   sp_MSget_current_activity  
  
-   sp_MSset_current_activity  
  
-   sp_MSobjessearch  
  
-   xp_enum_ActiveScriptEngines  
  
-   xp_eventlog  
  
-   xp_GetAdminGroupName  
  
-   xp_GetFileDetails  
  
-   xp_GetLocalSystemAccountName  
  
-   xp_IsNTAdmin  
  
-   xp_MSLocalSystem  
  
-   xp_MSnt2000  
  
-   xp_MSplatform  
  
-   xp_SetSecurity  
  
-   xp_varbintohexstr  
  
## <a name="corrective-action"></a>更正動作  
  
### <a name="documented-system-stored-procedures"></a>已記載的系統預存程序  
 根據下表修改您的應用程式。  
  
|取代|執行方式|  
|----------------|-------------|  
|sp_addalias|以使用者帳戶和資料庫角色的組合來取代別名。 如需詳細資訊，請參閱《SQL Server 線上叢書》中的＜CREATE USER (Transact-SQL)＞和＜CREATE ROLE (Transact-SQL)＞。 使用 sp_dropalias 移除已升級之資料庫中的別名。|  
|sp_addgroupsp_changegroup<br /><br /> sp_dropgroup<br /><br /> sp_helpgroup|使用角色。 如需詳細資訊，請參閱《SQL Server 線上叢書》中的＜伺服器層級角色＞和＜資料庫層級角色＞。|  
  
### <a name="undocmented-system-stored-procedures"></a>未記載的系統預存程序  
 您可以建立含有對等功能的 CLR 預存程序來取代未記載的系統預存程序。 如需詳細資訊，請參閱《SQL Server 線上叢書》中的＜CLR 預存程序＞主題。  
  
## <a name="see-also"></a>另請參閱  
 [Database Engine 升級問題](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 Upgrade Advisor&#91;新增&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
