---
description: 'Drop SQL Server index (Native Client OLE DB provider) '
title: 卸載 SQL Server index (Native Client OLE DB provider) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- removing indexes
- deleting indexes
- DropIndex function
- dropping indexes
- SQL Server Native Client OLE DB provider, indexes
- indexes [OLE DB]
ms.assetid: add3ba14-10b1-4723-b7c0-3e83689e9fdd
author: markingmyname
ms.author: maghan
ms.openlocfilehash: a53dcc5d6d5821f7f5501c38a196b270ad6108ae
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88498958"
---
# <a name="dropping-a-sql-server-native-client-index"></a>卸載 SQL Server Native Client 索引

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]原生用戶端 OLE DB 提供者會公開**IIndexDefinition：:D ropindex**函數。 如此可讓取用者從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表中移除索引。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]原生用戶端 OLE DB 提供者會公開一些 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 主鍵和唯一的條件約束做為索引。 資料表擁有者、資料庫擁有者以及某些系統管理角色成員都可以修改 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表，卸除條件約束。 根據預設，只有資料表擁有者可以卸除現有的索引。 因此，**DropIndex** 的成功或失敗，不但取決於應用程式使用者的存取權限，也取決於所指出之索引的類型。  
  
 取用者會在 *pTableID* 參數中，將資料表名稱指定為 *uName* 聯集之 *pwszName* 成員中的 Unicode 字元字串。 *pTableID* 的 *eKind* 成員必須是 DBKIND_NAME。  
  
 取用者會在 *pIndexID* 參數中，將索引名稱指定為 *uName* 聯集之 *pwszName* 成員中的 Unicode 字元字串。 *pIndexID* 的 *eKind* 成員必須是 DBKIND_NAME。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]當*pIndexID*為 null 時，Native Client OLE DB 提供者不支援在資料表上卸載所有索引的 OLE DB 功能。 如果 *pIndexID* 為 Null，會傳回 E_INVALIDARG。  
  
## <a name="see-also"></a>另請參閱  
 [資料表和索引](../../relational-databases/native-client-ole-db-tables-indexes/tables-and-indexes.md)   
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [DROP INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/drop-index-transact-sql.md)  
  
  
