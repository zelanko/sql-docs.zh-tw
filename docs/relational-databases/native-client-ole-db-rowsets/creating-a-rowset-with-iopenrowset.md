---
title: 以 IOpenRowset 建立資料列集 |Microsoft Docs
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
- IOpenRowset interface
- rowsets [OLE DB], creating
- SQL Server Native Client OLE DB provider, rowsets
- OLE DB rowsets, creating
ms.assetid: e8bc3de7-4b97-4de9-8df8-e11947d24045
caps.latest.revision: 30
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f7191d3df27eef77458aa7a423c870e3eaeb9dc2
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2018
ms.locfileid: "43101919"
---
# <a name="creating-a-rowset-with-iopenrowset"></a>以 IOpenRowset 建立資料列集
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會支援**iopenrowset:: Openrowset**方法具有下列限制：  
  
-   *pTableID* 參數指向的資料庫識別碼 (DBID) 結構中必須指定基底資料表或檢視表。  
  
-   DBID *eKind* 成員必須指示 DBKIND_NAME。  
  
-   DBID *uName* 成員必須將現有基底資料表或檢視表的名稱指定為 Unicode 字元字串。  
  
-   **OpenRowset** 的 *pIndexID* 參數必須為 NULL。  
  
 **IOpenRowset::OpenRowset** 的結果集包含單一資料列集。 包含單一資料列集的結果集可受到 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料指標的支援。 資料指標支援可讓開發人員使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 並行機制。  
  
## <a name="see-also"></a>另請參閱  
 [資料列集](../../relational-databases/native-client-ole-db-rowsets/rowsets.md)  
  
  
