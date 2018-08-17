---
title: 從 SQL Server 資料表中移除資料行 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
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
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: 586db18e1e4782f532b17f480db5729933949d1b
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/06/2018
ms.locfileid: "39561972"
---
# <a name="removing-a-column-from-a-sql-server-table"></a>從 SQL Server 資料表中移除資料行
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會公開**itabledefinition:: Dropcolumn**函式。 這可讓取用者移除的資料行[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料表。  
  
 取用者指定為 Unicode 字元字串中的資料表名稱 *pwszName* 隸屬 *uName* 聯集 *pTableID* 參數。 *EKind* 隸屬 *pTableID* 必須是 DBKIND_NAME。  
  
 取用者表示中的資料行名稱 *pwszName* 隸屬 *uName* 聯集 *Ekind* 參數。 資料行名稱是一個 Unicode 字元字串。 *EKind* 隸屬 *Ekind* 必須是 DBKIND_NAME。  
  
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
 [資料表和索引](../../relational-databases/native-client-ole-db-tables-indexes/tables-and-indexes.md)  
  
  
