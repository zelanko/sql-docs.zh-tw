---
title: ad hoc distributed queries 伺服器組態選項 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- OPENROWSET function, ad hoc distributed queries option
- Ad Hoc Distributed Queries option
- ad hoc distributed queries
- 7415 (Database Engine Error)
- OPENDATASOURCE function, ad hoc distributed queries option
- ad hoc access
ms.assetid: 5b982015-e196-44c3-83b8-275fb9d769b2
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: edd15d3d18b7b4d4d7a03689548186829389889f
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48093290"
---
# <a name="ad-hoc-distributed-queries-server-configuration-option"></a>特定分散式查詢伺服器組態選項
  根據預設， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不允許使用 OPENROWSET 和 OPENDATASOURCE 進行特定分散式查詢。 當此選項設定為 1 時， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 就會允許特定存取。 當此選項未設定或設定為 0 時， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 就不允許特定存取。  
  
 特定分散式查詢會使用 OPENROWSET 和 OPENDATASOURCE 函數，連接到使用 OLE DB 的遠端資料來源。 OPENROWSET 與 OPENDATASOURCE 只能用來參考不常存取的 OLE DB 資料來源。 對於經常存取的資料來源，請定義連結伺服器。  
  
> [!IMPORTANT]  
>  啟用特定名稱，表示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的任何驗證登入都可以存取該提供者。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 對於任何可安全由本機登入存取的提供者，系統管理員應該為他啟用此功能。  
  
## <a name="remarks"></a>備註  
 嘗試進行特定連接但是未啟用 **特定分散式查詢** 會產生錯誤：訊息 7415、層級 16、狀態 1、行 1  
  
 特定存取至 OLE DB 提供者 'Microsoft.ACE.OLEDB.12.0' 已經遭到拒絕。 您必須透過連結伺服器來存取此提供者。  
  
## <a name="examples"></a>範例  
 下列範例會啟用特定分散式查詢，然後使用 `Seattle1` 函數來查詢名為 `OPENROWSET` 的伺服器。  
  
```  
sp_configure 'show advanced options', 1;  
RECONFIGURE;  
sp_configure 'Ad Hoc Distributed Queries', 1;  
RECONFIGURE;  
GO  
  
SELECT a.*  
FROM OPENROWSET('SQLNCLI', 'Server=Seattle1;Trusted_Connection=yes;',  
     'SELECT GroupName, Name, DepartmentID  
      FROM AdventureWorks2012.HumanResources.Department  
      ORDER BY GroupName, Name') AS a;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [伺服器組態選項 &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [連結的伺服器 &#40;Database Engine&#41;](../../relational-databases/linked-servers/linked-servers-database-engine.md)   
 [OPENROWSET &#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql)   
 [OPENDATASOURCE &#40;Transact-SQL&#41;](/sql/t-sql/functions/opendatasource-transact-sql)   
 [sp_addlinkedserver &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql)  
  
  
