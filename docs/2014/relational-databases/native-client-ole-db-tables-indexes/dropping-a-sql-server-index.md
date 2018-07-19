---
title: 卸除 SQL Server 索引 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- removing indexes
- deleting indexes
- DropIndex function
- dropping indexes
- SQL Server Native Client OLE DB provider, indexes
- indexes [OLE DB]
ms.assetid: add3ba14-10b1-4723-b7c0-3e83689e9fdd
caps.latest.revision: 30
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 148565f2866e571ba783c58d1ff10413510ef6db
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/03/2018
ms.locfileid: "37422227"
---
# <a name="dropping-a-sql-server-index"></a>卸除 SQL Server 索引
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會公開 **:: Dropindex<** 函式。 這可讓取用者從索引中移除[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料表。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會公開某些[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]PRIMARY KEY 和 UNIQUE 條件約束當做索引。 資料表擁有者、 資料庫擁有者，以及某些系統管理角色成員可以修改[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料表，卸除條件約束。 根據預設，只有資料表擁有者可以卸除現有的索引。 因此， **DropIndex**成功或失敗取決於應用程式使用者的存取權限，同時也在所指出之索引的類型。  
  
 取用者指定為 Unicode 字元字串中的資料表名稱*pwszName*隸屬*uName*聯集*pTableID*參數。 *EKind*隸屬*pTableID*必須是 DBKIND_NAME。  
  
 取用者索引名稱指定之 Unicode 字元字串*pwszName*隸屬*uName*聯集*pIndexID*參數。 *EKind*隸屬*pIndexID*必須是 DBKIND_NAME。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者不支援資料表上卸除所有索引的 OLE DB 功能時*pIndexID*為 null。 如果*pIndexID*是 null，則會傳回 E_INVALIDARG。  
  
## <a name="see-also"></a>另請參閱  
 [資料表和索引](tables-and-indexes.md)   
 [ALTER TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-table-transact-sql)   
 [DROP INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-index-transact-sql)  
  
  
