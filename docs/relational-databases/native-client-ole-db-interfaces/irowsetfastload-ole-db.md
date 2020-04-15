---
title: IRowsetFastLoad (OLE DB) | Microsoft Docs
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
ms.openlocfilehash: feea17329a8e809083263a83217aeb87fbf91bc3
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307239"
---
# <a name="irowsetfastload-ole-db"></a>IRowsetFastLoad (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  **IRowsetFastLoad** 介面會公開 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 以記憶體為基礎的大量複製作業支援。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本機用戶端 OLE 資料庫提供程式使用者使用該介面快速將數據添加[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]到現有表。  
  
 如果您針對工作階段將 SSPROP_ENABLEFASTLOAD 設定為 VARIANT_TRUE，您無法讀取之後從該工作階段傳回之資料列集中的資料。 當 SSPROP_ENABLEFASTLOAD 設定為 VARIANT_TRUE 時，在工作階段上建立的所有資料列集都屬於 IRowsetFastLoad 類型。 IRowsetFastLoad 資料列集不支援資料列集擷取功能，因此無法從這些資料列集讀取資料。  
  
## <a name="in-this-section"></a>本節內容  
  
|方法|描述|  
|------------|-----------------|  
|[IRowsetFastLoad::Commit &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/irowsetfastload-commit-ole-db.md)|標示已插入之資料列批次的結尾，並將資料列寫入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表。|  
|[IRowsetFastLoad::InsertRow &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/irowsetfastload-insertrow-ole-db.md)|將資料列加入至大量複製資料列集。|  
  
## <a name="see-also"></a>另請參閱  
 [&#40;OLE DB&#41;的接口](https://msdn.microsoft.com/library/34c33364-8538-45db-ae41-5654481cda93)   
 [使用 IRowset 快速載入&#40;OLE DB&#41;批量复制数据](../../relational-databases/native-client-ole-db-how-to/bulk-copy-data-using-irowsetfastload-ole-db.md)   
 [使用 IROWSETFASTLOAD 和 ISEQUENTIALSTREAM 將 BLOB 資料傳送到 SQL SERVER &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-how-to/send-blob-data-to-sql-server-using-irowsetfastload-and-isequentialstream-ole-db.md)  
  
  
