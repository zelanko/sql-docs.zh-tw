---
title: 安全性實體 | Microsoft Docs
ms.custom: ''
ms.date: 10/14/2015
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: security
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.swb.roleproperties.selectobject.f1
helpviewer_keywords:
- securables [SQL Server]
- schemas [SQL Server], securables
- database securables [SQL Server]
- hierarchies [SQL Server], securables
- server securables [SQL Server]
ms.assetid: bfa748f0-70b0-453c-870a-04b7b205b9ff
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: da63c9918fb2d4c89ab32b3a06402c39bea0785b
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2018
ms.locfileid: "43029100"
---
# <a name="securables"></a>[安全性實體]
  安全性實體是一種資源， [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 授權系統會管理其存取權。 例如，資料表是安全性實體。 有些安全性實體可以包含在其他安全性實體內，因而建立稱為「範圍」的巢狀階層，以保護它們自己本身的安全。 安全性實體範圍為 **伺服器**、 **資料庫**以及 **結構描述**。  
  
## <a name="securable-scope-server"></a>安全性實體範圍：伺服器  
 **伺服器** 安全性實體範圍包含下列安全性實體：  
  
-   可用性群組  
  
-   端點  
  
-   登入  
  
-   伺服器角色  
  
-   [資料庫]  
  
## <a name="securable-scope-database"></a>安全性實體範圍：資料庫  
 **資料庫** 安全性實體範圍包含下列安全性實體：  
  
-   應用程式角色  
  
-   組件  
  
-   非對稱金鑰  
  
-   憑證  
  
-   合約  
  
-   FullText 目錄  
  
-   Fulltext 停用字詞表  
  
-   訊息類型  
  
-   遠端服務繫結  
  
-   (資料庫) 角色  
  
-   路由  
  
-   結構描述  
  
-   搜尋屬性清單  
  
-   服務  
  
-   對稱金鑰  
  
-   使用者  
  
## <a name="securable-scope-schema"></a>安全性實體範圍：結構描述  
 **結構描述** 安全性實體範圍包含下列安全性實體：  
  
-   類型  
  
-   XML 結構描述集合  
  
-   物件 – 物件類別有下列成員：  
  
    -   Aggregate  
  
    -   函數  
  
    -   程序  
  
    -   佇列  
  
    -   同義字  
  
    -   Table  
  
    -   檢視  
  
## <a name="controlling-access-to-a-securable"></a>控制對安全性實體的存取權  
 接收安全性實體權限的實體稱為主體。 最常見的主體就是登入和資料庫使用者。 安全性實體存取權的控制是透過授與或拒絕權限，或是將登入和使用者加入至具有存取權的角色。 如需控制權限的資訊，請參閱 [GRANT &#40;Transact-SQL&#41;](/sql/t-sql/statements/grant-transact-sql)、[REVOKE &#40;Transact-SQL&#41;](/sql/t-sql/statements/revoke-transact-sql)、[DENY &#40;Transact-SQL&#41;](/sql/t-sql/statements/deny-transact-sql)、[sp_addrolemember &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addrolemember-transact-sql) 和 [sp_droprolemember &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-droprolemember-transact-sql)。  
  
> [!CAUTION]  
>  在安裝時為系統物件授與的預設權限，經過仔細評估可能面臨的威脅，因此在強化 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 安裝的過程中無須改變。 系統物件的任何權限變更，都可能會限制或破壞其功效，而可能會讓您的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 安裝處於不支援的狀態。  
  
## <a name="related-content"></a>相關內容  
 [保護 SQL Server 的安全](securing-sql-server.md)  
  
 [sys.database_principals &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-database-principals-transact-sql)  
  
 [sys.database_role_members &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-database-role-members-transact-sql)  
  
 [sys.server_principals &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-server-principals-transact-sql)  
  
 [sys.server_role_members &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-server-role-members-transact-sql)  
  
 [sys.sql_logins &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-sql-logins-transact-sql)  
  
  
