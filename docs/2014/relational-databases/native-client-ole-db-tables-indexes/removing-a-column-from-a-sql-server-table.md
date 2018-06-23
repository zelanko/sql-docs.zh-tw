---
title: 從 SQL Server 資料表移除資料行 |Microsoft 文件
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
- removing columns
- DropColumn function
- SQL Server Native Client OLE DB provider, columns
ms.assetid: 210811b7-cbd6-421e-bc6e-df9482236768
caps.latest.revision: 33
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 9cecee484e16f2394e9bbef33ff5ed258a0f1752
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36136411"
---
# <a name="removing-a-column-from-a-sql-server-table"></a>從 SQL Server 資料表中移除資料行
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會公開**itabledefinition:: Dropcolumn**函式。 這可讓取用者移除的資料行[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料表。  
  
 取用者指定的資料表名稱中的 Unicode 字元字串*pwszName*隸屬*uName*聯集*Createtable*參數。 *EKind*隸屬*Createtable*必須是 DBKIND_NAME。  
  
 取用者表示中的資料行名稱*pwszName*隸屬*uName*聯集*Ekind*參數。 資料行名稱是一個 Unicode 字元字串。 *EKind*隸屬*Ekind*必須是 DBKIND_NAME。  
  
## <a name="example"></a>範例  
  
### <a name="code"></a>程式碼  
  
```  
DBID TableID;  
DBID ColumnID;  
HRESULT hr;  
  
TableID.eKind = DBKIND_NAME;  
TableID.uName.pwszName = L"MyTableName";  
  
ColumnID.eKind = DBKIND_NAME;  
ColumnID.uName.pwszName = L"MyColumnName";  
  
hr = m_pITableDefinition->DropColumn(&TableID, &ColumnID);  
```  
  
## <a name="see-also"></a>另請參閱  
 [資料表和索引](tables-and-indexes.md)  
  
  