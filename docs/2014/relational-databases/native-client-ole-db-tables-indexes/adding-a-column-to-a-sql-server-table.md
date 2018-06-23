---
title: SQL Server 資料表中加入一個資料行 |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- columns [OLE DB]
- AddColumn function
- SQL Server Native Client OLE DB provider, columns
- adding columns
ms.assetid: 22bae18a-bc9d-4617-8660-ed8b17a468d4
caps.latest.revision: 29
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 45909b981b21a496411b46200aceeaded0a9af47
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36030762"
---
# <a name="adding-a-column-to-a-sql-server-table"></a>將資料行加入至 SQL Server 資料表
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會公開 **:: Addcolumn**函式。 這可讓取用者加入至資料行[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料表。  
  
 當您將加入的資料行[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料表[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者取用者會受到限制，如下所示：  
  
-   如果 DBPROP_COL_AUTOINCREMENT 是 VARIANT_TRUE，DBPROP_COL_NULLABLE 就必須是 VARIANT_FALSE。  
  
-   如果資料行定義使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**時間戳記**資料類型，dbprop_col_nullable 就必須是 VARIANT_FALSE。  
  
-   如果是其他任何資料行定義，DBPROP_COL_NULLABLE 必須為 VARIANT_TRUE。  
  
 取用者指定的資料表名稱中的 Unicode 字元字串*pwszName*隸屬*uName*聯集*Createtable*參數。 *EKind*隸屬*Createtable*必須是 DBKIND_NAME。  
  
 新的資料行名稱指定為 Unicode 字元字串中*pwszName*隸屬*uName*聯集*pwszname*之 DBCOLUMNDESC 參數成員*Pwszname*。 *EKind*成員必須是 DBKIND_NAME。  
  
## <a name="see-also"></a>另請參閱  
 [資料表和索引](tables-and-indexes.md)   
 [ALTER TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-table-transact-sql)  
  
  
