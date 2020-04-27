---
title: 從 SQL Server 資料表中移除資料行 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- columns [OLE DB]
- removing columns
- DropColumn function
- SQL Server Native Client OLE DB provider, columns
ms.assetid: 210811b7-cbd6-421e-bc6e-df9482236768
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 919bd28a82171068349e4019bb1bd5c190d08cd0
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "63213912"
---
# <a name="removing-a-column-from-a-sql-server-table"></a>從 SQL Server 資料表中移除資料行
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會公開**ITableDefinition：:D ropcolumn**函數。 如此可讓取用者從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表中移除資料行。  
  
 取用者會在 *pTableID* 參數中，將資料表名稱指定為 *uName* 聯集 *pwszName* 成員中的 Unicode 字元字串。 *pTableID* 的 *eKind* 成員必須是 DBKIND_NAME。  
  
 此取用者會在 *pColumnID* 參數內指示 *uName* 聯集之 *pwszName* 成員內的資料行名稱。 資料行名稱是一個 Unicode 字元字串。 *pColumnID* 的 *eKind* 成員必須是 DBKIND_NAME。  
  
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
  
  
