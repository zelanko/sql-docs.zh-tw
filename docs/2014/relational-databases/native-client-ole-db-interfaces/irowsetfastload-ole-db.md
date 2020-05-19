---
title: IRowsetFastLoad (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- IRowsetFastLoad interface
ms.assetid: d19a7097-48d9-409a-aff9-277891b7aca7
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 720ea095343abefb0b56f4f1f47bbd853d72378e
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/01/2020
ms.locfileid: "82707347"
---
# <a name="irowsetfastload-ole-db"></a>IRowsetFastLoad (OLE DB)
  `IRowsetFastLoad`介面會公開以 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 記憶體為基礎之大量複製作業的支援。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者取用者會使用介面，快速地將資料加入現有的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表。  
  
 如果您針對工作階段將 SSPROP_ENABLEFASTLOAD 設定為 VARIANT_TRUE，您無法讀取之後從該工作階段傳回之資料列集中的資料。 當 SSPROP_ENABLEFASTLOAD 設定為 VARIANT_TRUE 時，在工作階段上建立的所有資料列集都屬於 IRowsetFastLoad 類型。 IRowsetFastLoad 資料列集不支援資料列集擷取功能，因此無法從這些資料列集讀取資料。  
  
## <a name="in-this-section"></a>本節內容  
  
|方法|描述|  
|------------|-----------------|  
|[IRowsetFastLoad::Commit &#40;OLE DB&#41;](irowsetfastload-commit-ole-db.md)|標示已插入之資料列批次的結尾，並將資料列寫入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表。|  
|[IRowsetFastLoad::InsertRow &#40;OLE DB&#41;](irowsetfastload-insertrow-ole-db.md)|將資料列加入至大量複製資料列集。|  
  
## <a name="see-also"></a>另請參閱  
 [介面 &#40;OLE DB&#41;](../../database-engine/dev-guide/interfaces-ole-db.md)   
 [使用 IRowsetFastLoad &#40;OLE DB 的大量資料複製&#41;](../native-client-ole-db-how-to/bulk-copy-data-using-irowsetfastload-ole-db.md)   
 [使用 IROWSETFASTLOAD 和 ISEQUENTIALSTREAM 將 BLOB 資料傳送到 SQL SERVER &#40;OLE DB&#41;](../native-client-ole-db-how-to/send-blob-data-to-sql-server-using-irowsetfastload-and-isequentialstream-ole-db.md)  
  
  
