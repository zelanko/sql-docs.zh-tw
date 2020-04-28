---
title: 權限階層 (Database Engine) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
f1_keywords:
- sql12.swb.server.permissions.f1--May use common.permissions
helpviewer_keywords:
- security [SQL Server], denying access
- hierarchies [SQL Server], permissions
- securables [SQL Server]
- security [SQL Server], permissions
- permissions [SQL Server], hierarchy
- security [SQL Server], granting access
ms.assetid: f6d20a55-ef03-4e14-85f9-009902889866
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 607ac55fe426cd086ce31ade33d3e772e7a3d9a9
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81487133"
---
# <a name="permissions-hierarchy-database-engine"></a>權限階層 (Database Engine)
  [!INCLUDE[ssDE](../../../includes/ssde-md.md)] 會管理階層式實體集合，這些實體可使用權限來確保安全性。 這些實體也稱為「安全性實體」  。 最明顯的安全性實體為伺服器和資料庫，但是個別權限可以在更細微的層次進行設定。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 透過驗證主體是否已被授與適當的權限，進而規範主體在安全性實體上的動作。

 下圖顯示 [!INCLUDE[ssDE](../../../includes/ssde-md.md)] 權限階層之間的關係。

 ![資料庫引擎權限階層的圖表](../../database-engine/media/wj-security-layers.gif "資料庫引擎權限階層的圖表")

## <a name="chart-of-sql-server-permissions"></a>SQL Server 權限的圖表
 如需 pdf 格式之所有[!INCLUDE[ssDE](../../../includes/ssde-md.md)]許可權的海報大小圖表，請[https://github.com/microsoft/sql-server-samples/blob/master/samples/features/security/permissions-posters/Microsoft_SQL_Server_2017_and_Azure_SQL_Database_permissions_infographic.pdf](https://github.com/microsoft/sql-server-samples/blob/master/samples/features/security/permissions-posters/Microsoft_SQL_Server_2017_and_Azure_SQL_Database_permissions_infographic.pdf)參閱。

## <a name="working-with-permissions"></a>使用權限
 您可以透過常見的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 查詢 GRANT、DENY 與 REVOKE 來操控權限。 您可以在 [sys.server_permissions](/sql/relational-databases/system-catalog-views/sys-server-permissions-transact-sql) 和 [sys.database_permissions](/sql/relational-databases/system-catalog-views/sys-database-permissions-transact-sql) 目錄檢視中查看權限的相關資訊。 此外，也支援使用內建函數來查詢權限資訊。

## <a name="see-also"></a>另請參閱
 [保護 SQL Server](securing-sql-server.md) [許可權 &#40;資料庫引擎&#41;](permissions-database-engine.md) [安全性實體](securables.md)[主體 &#40;資料庫引擎](authentication-access/principals-database-engine.md)&#41;sql [server 授與 &#40;](/sql/t-sql/statements/grant-transact-sql) transact-sql&#41;[撤銷 &#40;](/sql/t-sql/statements/revoke-transact-sql) transact-sql&#41;[&#40;transact-sql&#41;](/sql/t-sql/statements/deny-transact-sql) [HAS_PERMS_BY_NAME &#40;](/sql/t-sql/functions/has-perms-by-name-transact-sql) transact-sql&#41;[sys.](/sql/relational-databases/system-catalog-views/sys-server-permissions-transact-sql) [fn_builtin_permissions &#40;transact-sql](/sql/relational-databases/system-functions/sys-fn-builtin-permissions-transact-sql)&#41;server_permissions &#40;transact-sql&#41;。 database_permissions &#40;[transact-sql&#41;](/sql/relational-databases/system-catalog-views/sys-database-permissions-transact-sql)


