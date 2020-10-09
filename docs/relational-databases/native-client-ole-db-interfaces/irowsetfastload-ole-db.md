---
description: 'IRowsetFastLoad (Native Client OLE DB 提供者) '
title: IRowsetFastLoad (Native Client OLE DB 提供者) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: COM
helpviewer_keywords:
- IRowsetFastLoad interface
ms.assetid: d19a7097-48d9-409a-aff9-277891b7aca7
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c0ec2d3318253e79ec9c8aa630d7ad0e7b5028a3
ms.sourcegitcommit: 4d370399f6f142e25075b3714e5c2ce056b1bfd0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/09/2020
ms.locfileid: "91866726"
---
# <a name="irowsetfastload-native-client-ole-db-provider"></a>IRowsetFastLoad (Native Client OLE DB 提供者) 
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  **IRowsetFastLoad** 介面會公開 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 以記憶體為基礎的大量複製作業支援。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 原生用戶端 OLE DB 提供者取用者會使用介面，快速地將資料加入至現有的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表。  
  
 如果您針對工作階段將 SSPROP_ENABLEFASTLOAD 設定為 VARIANT_TRUE，您無法讀取之後從該工作階段傳回之資料列集中的資料。 當 SSPROP_ENABLEFASTLOAD 設定為 VARIANT_TRUE 時，在工作階段上建立的所有資料列集都屬於 IRowsetFastLoad 類型。 IRowsetFastLoad 資料列集不支援資料列集擷取功能，因此無法從這些資料列集讀取資料。  
  
## <a name="in-this-section"></a>本節內容  
  
|方法|描述|  
|------------|-----------------|  
|[IRowsetFastLoad::Commit &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/irowsetfastload-commit-ole-db.md)|標示已插入之資料列批次的結尾，並將資料列寫入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表。|  
|[IRowsetFastLoad::InsertRow &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/irowsetfastload-insertrow-ole-db.md)|將資料列加入至大量複製資料列集。|  
  
## <a name="see-also"></a>另請參閱  
 [介面 &#40;OLE DB&#41;](./sql-server-native-client-ole-db-interfaces.md)   
 [使用 IRowsetFastLoad 大量複製資料 &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-how-to/bulk-copy-data-using-irowsetfastload-ole-db.md)   
 [使用 IROWSETFASTLOAD 和 ISEQUENTIALSTREAM 將 BLOB 資料傳送到 SQL SERVER &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-how-to/send-blob-data-to-sql-server-using-irowsetfastload-and-isequentialstream-ole-db.md)  
  
