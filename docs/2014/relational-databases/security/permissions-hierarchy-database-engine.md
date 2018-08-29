---
title: 權限階層 (Database Engine) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: security
ms.tgt_pltfrm: ''
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
ms.openlocfilehash: a3ffccce83685f3ec765264ab3eaf6b78a11953b
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2018
ms.locfileid: "43030620"
---
# <a name="permissions-hierarchy-database-engine"></a>權限階層 (Database Engine)
  [!INCLUDE[ssDE](../../../includes/ssde-md.md)] 會管理階層式實體集合，這些實體可使用權限來確保安全性。 這些實體也稱為「安全性實體」。 最明顯的安全性實體為伺服器和資料庫，但是個別權限可以在更細微的層次進行設定。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 透過驗證主體是否已被授與適當的權限，進而規範主體在安全性實體上的動作。  
  
 下圖顯示 [!INCLUDE[ssDE](../../../includes/ssde-md.md)] 權限階層之間的關係。  
  
 ![Database Engine 權限階層的圖表](../../database-engine/media/wj-security-layers.gif "Database Engine 權限階層的圖表")  
  
## <a name="chart-of-sql-server-permissions"></a>SQL Server 權限的圖表  
 如需所有 [!INCLUDE[ssDE](../../../includes/ssde-md.md)] 權限的 PDF 格式海報大小圖表，請參閱 [http://go.microsoft.com/fwlink/?LinkId=229142](http://go.microsoft.com/fwlink/?LinkId=229142)。  
  
## <a name="working-with-permissions"></a>使用權限  
 您可以透過常見的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 查詢 GRANT、DENY 與 REVOKE 來操控權限。 您可以在 [sys.server_permissions](/sql/relational-databases/system-catalog-views/sys-server-permissions-transact-sql) 和 [sys.database_permissions](/sql/relational-databases/system-catalog-views/sys-database-permissions-transact-sql) 目錄檢視中查看權限的相關資訊。 此外，也支援使用內建函數來查詢權限資訊。  
  
## <a name="see-also"></a>另請參閱  
 [保護 SQL Server 的安全](securing-sql-server.md)   
 [權限 &#40;資料庫引擎&#41;](permissions-database-engine.md)   
 [安全性實體](securables.md)   
 [主體 &#40;Database Engine&#41;](authentication-access/principals-database-engine.md)   
 [GRANT &#40;Transact-SQL&#41;](/sql/t-sql/statements/grant-transact-sql)   
 [REVOKE &#40;Transact-SQL&#41;](/sql/t-sql/statements/revoke-transact-sql)   
 [DENY &#40;Transact-SQL&#41;](/sql/t-sql/statements/deny-transact-sql)   
 [HAS_PERMS_BY_NAME &#40;Transact-SQL&#41;](/sql/t-sql/functions/has-perms-by-name-transact-sql)   
 [sys.fn_builtin_permissions &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/sys-fn-builtin-permissions-transact-sql)   
 [sys.server_permissions &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-server-permissions-transact-sql)   
 [sys.database_permissions &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-database-permissions-transact-sql)  
  
  
