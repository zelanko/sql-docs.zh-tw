---
title: 以 IOpenRowset 建立資料列集 |Microsoft 文件
description: IOpenRowset 介面的 OLE DB 驅動程式的資料列集建立適用於 SQL Server
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|ole-db-rowsets
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IOpenRowset interface
- rowsets [OLE DB], creating
- OLE DB Driver for SQL Server, rowsets
- OLE DB rowsets, creating
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: dd1b48ee3ba9439f5a1cddbfed07196480265b74
ms.sourcegitcommit: 03ba89937daeab08aa410eb03a52f1e0d212b44f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/16/2018
ms.locfileid: "35689061"
---
# <a name="creating-a-rowset-with-iopenrowset"></a>以 IOpenRowset 建立資料列集
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-asdbmi-md](../../../includes/appliesto-ss-asdb-asdw-pdw-asdbmi-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  SQL Server 的 OLE DB 驅動程式支援**iopenrowset:: Openrowset**方法有下列限制：  
  
-   基底資料表或檢視表中必須指定資料庫識別碼 (DBID) 結構*Createtable*參數所指向。  
  
-   DBID *eKind*成員必須指示 DBKIND_NAME。  
  
-   DBID *uName*成員必須將現有的基底資料表或檢視的名稱指定為 Unicode 字元字串。  
  
-   *PIndexID*參數**OpenRowset**必須是 NULL。  
  
 在結果集的**iopenrowset:: Openrowset**包含單一資料列集。 包含單一資料列集的結果集可受到[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]資料指標。 資料指標支援可讓開發人員使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 並行機制。  
  
## <a name="see-also"></a>另請參閱  
 [資料列集](../../oledb/ole-db-rowsets/rowsets.md)  
  
  
