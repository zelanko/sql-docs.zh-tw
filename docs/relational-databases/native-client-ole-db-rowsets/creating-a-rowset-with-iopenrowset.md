---
title: "以 IOpenRowset 建立資料列集 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-ole-db-rowsets
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- IOpenRowset interface
- rowsets [OLE DB], creating
- SQL Server Native Client OLE DB provider, rowsets
- OLE DB rowsets, creating
ms.assetid: e8bc3de7-4b97-4de9-8df8-e11947d24045
caps.latest.revision: "30"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7c78658537d6af6bd08423aa2be3add03bdaba7b
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="creating-a-rowset-with-iopenrowset"></a>以 IOpenRowset 建立資料列集
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者支援**iopenrowset:: Openrowset**方法有下列限制：  
  
-   基底資料表或檢視表中必須指定資料庫識別碼 (DBID) 結構*Createtable*參數所指向。  
  
-   DBID *eKind*成員必須指示 DBKIND_NAME。  
  
-   DBID *uName*成員必須將現有的基底資料表或檢視的名稱指定為 Unicode 字元字串。  
  
-   *PIndexID*參數**OpenRowset**必須是 NULL。  
  
 在結果集的**iopenrowset:: Openrowset**包含單一資料列集。 包含單一資料列集的結果集可受到[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料指標。 資料指標支援可讓開發人員使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 並行機制。  
  
## <a name="see-also"></a>請參閱＜  
 [資料列集](../../relational-databases/native-client-ole-db-rowsets/rowsets.md)  
  
  
