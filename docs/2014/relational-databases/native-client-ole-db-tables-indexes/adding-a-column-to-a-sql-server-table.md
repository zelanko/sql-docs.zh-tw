---
title: 將資料行新增至 SQL Server 資料表 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- columns [OLE DB]
- AddColumn function
- SQL Server Native Client OLE DB provider, columns
- adding columns
ms.assetid: 22bae18a-bc9d-4617-8660-ed8b17a468d4
author: rothja
ms.author: jroth
ms.openlocfilehash: 97aa2656ccde662a34e1dd80fd662b22f601d4ec
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85018004"
---
# <a name="adding-a-column-to-a-sql-server-table"></a>將資料行加入至 SQL Server 資料表
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者會公開**ITableDefinition：： AddColumn**函數。 如此可讓取用者將資料行加入至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表。  
  
 當您將資料行加入至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表時， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者取用者的限制如下：  
  
-   如果 DBPROP_COL_AUTOINCREMENT 是 VARIANT_TRUE，DBPROP_COL_NULLABLE 就必須是 VARIANT_FALSE。  
  
-   如果資料行是使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **timestamp** 資料類型所定義，DBPROP_COL_NULLABLE 就必須是 VARIANT_FALSE。  
  
-   如果是其他任何資料行定義，DBPROP_COL_NULLABLE 必須為 VARIANT_TRUE。  
  
 取用者會在 *pTableID* 參數中，將資料表名稱指定為 *uName* 聯集之 *pwszName* 成員中的 Unicode 字元字串。 *pTableID* 的 *eKind* 成員必須是 DBKIND_NAME。  
  
 在 *pColumnDesc* 之 DBCOLUMNDESC 參數的 *dbcid* 成員中，新的資料行名稱會指定為 *uName* 聯集之 *pwszName* 成員內的 Unicode 字元字串。 *eKind* 成員必須是 DBKIND_NAME。  
  
## <a name="see-also"></a>另請參閱  
 [資料表和索引](tables-and-indexes.md)   
 [ALTER TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-table-transact-sql)  
  
  
