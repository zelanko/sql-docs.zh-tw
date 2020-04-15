---
title: 資料類型 (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- mapping data types [OLE DB]
- SQL Server Native Client OLE DB provider, data types
- data types [OLE DB]
- OLE DB, data types
ms.assetid: 15953706-f0d1-45f5-a2eb-a8bd36e1a5fc
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 501e73cd5db2fbf79cd84c0184161f0c6ec6a341
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304432"
---
# <a name="data-types-ole-db"></a>資料類型 (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  為了[!INCLUDE[tsql](../../includes/tsql-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用 本機用戶端 OLE DB 提供程式執行敘述和處理[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]結果,您必須知道 本機用戶端 OLE[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]DB 提供程式如何在行集中 綁定參數或列時將資料類型映射到 OLE DB[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料類型,以及何時使用**ITable 定義**介面在中創建表。  
  
## <a name="in-this-section"></a>本節內容  
  
-   [行集與參數中的資料類型對應](../../relational-databases/native-client-ole-db-data-types/data-type-mapping-in-rowsets-and-parameters.md)  
  
-   [ITableDefinition 中的資料類型對應](../../relational-databases/native-client-ole-db-data-types/data-type-mapping-in-itabledefinition.md)  
  
-   [SSVARIANT 結構](../../relational-databases/native-client-ole-db-data-types/ssvariant-structure.md)  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Native Client &#40;OLE DB&#41;](../../relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)  
  
  
