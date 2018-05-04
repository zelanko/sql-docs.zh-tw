---
title: Blob 與 OLE 物件 |Microsoft 文件
description: BLOB 與 OLE 物件
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: ole-db-blobs
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- BLOBs, OLE objects
- BLOBs
- storage object [OLE DB]
- OLE DB Driver for SQL Server, BLOBs
- large data, OLE objects
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: e78fe8db35684bb35e4111a38d3d0ba938891785
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="blobs-and-ole-objects"></a>BLOB 與 OLE 物件
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  SQL Server OLE DB 驅動程式會公開**ISequentialStream**介面，以支援取用者存取[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **ntext**，**文字**，**映像**， **varchar （max)**， **nvarchar （max)**， **varbinary （max)**，及 xml 資料類型為二進位大型物件 (Blob)。 **讀取**方法**ISequentialStream**可讓取用者擷取更多可管理的區塊中的資料。  
  
 如需示範這項功能的範例，請參閱[大型資料集 & #40; OLE DB & #41;](../../oledb/ole-db-how-to/set-large-data-ole-db.md)。  
  
 SQL Server OLE DB 驅動程式可以使用取用者實作**IStorage**介面，取用者提供的存取子中的介面指標時繫結的資料修改。  
  
 對於大數值資料類型，SQL Server OLE DB 驅動程式會檢查是否有型別中的大小假設**IRowset**和 DDL 介面。 具有資料行**varchar**， **nvarchar**，和**varbinary**資料類型和設定為無限制的大小上限會表示為 ISLONG 透過結構描述資料列，而傳回資料行資料類型的介面。  
  
 SQL Server OLE DB 驅動程式會公開**varchar （max)**， **varbinary （max)** 和**nvarchar （max)** 類型分別為 DBTYPE_STR、 DBTYPE_BYTES 和 DBTYPE_WSTR。  
  
 為了使用這些類型，應用程式具有下列選項：  
  
-   繫結為類型 (DBTYPE_BYTES、DBTYPE_STR、DBTYPE_WSTR)。 如果緩衝區不夠大，足以會截斷，完全與舊版中這些類型 （雖然較大的值現在是可用的）。  
  
-   繫結為類型，同時指定 DBTYPE_BYREF。  
  
-   繫結為 DBTYPE_IUNKNOWN 並使用資料流。  
  
 如果繫結至 DBTYPE_IUNKNOWN，就會使用 ISequentialStream 資料流功能。 SQL Server OLE DB 驅動程式支援大數值資料類型為 DBTYPE_IUNKNOWN 繫結 output 參數。 這是為了支援其中預存程序會傳回這些資料類型當做傳回值，將會傳回為 DBTYPE_IUNKNOWN，用戶端的案例。  
  
## <a name="storage-object-limitations"></a>儲存物件的限制  
  
-   SQL Server OLE DB 驅動程式可支援只有一個開啟的儲存物件。 嘗試開啟一個以上的儲存物件 (取得多個參考**ISequentialStream**介面指標) 傳回 DBSTATUS_E_CANTCREATE。  
  
-   OLE DB 驅動程式中的 SQL Server，DBPROP_BLOCKINGSTORAGEOBJECTS 唯讀屬性的預設值為 VARIANT_TRUE。 因此，如果儲存物件作用中，某些方法 （非儲存物件的方法） 將無法與 E_UNEXPECTED。  
  
-   取用者實作的儲存物件呈現的資料長度必須對已知 OLE DB 驅動程式適用於 SQL Server 的資料列存取子，參考儲存體物件建立時。 取用者必須在建立存取子所使用的 DBBINDING 結構中繫結長度指標。  
  
-   如果資料列都包含多個單一大型資料值和 DBPROP_ACCESSORDER 不是 DBPROPVAL_AO_RANDOM，取用者必須使用 SQL Server 資料指標支援資料列集 OLE DB 驅動程式來擷取資料列的資料或之前擷取其他處理所有大型資料值資料列的值。 如果 DBPROP_ACCESSORDER 是 DBPROPVAL_AO_RANDOM，SQL Server OLE DB 驅動程式會快取所有 xml 資料型別當做二進位大型物件 (Blob)，以便它可以依照任何順序存取。  
  
## <a name="in-this-section"></a>本節內容  
  
-   [取得大型資料](../../oledb/ole-db-blobs/getting-large-data.md)  
  
-   [設定大型資料](../../oledb/ole-db-blobs/setting-large-data.md)  
  
-   [BLOB 輸出參數的串流支援](../../oledb/ole-db-blobs/streaming-support-for-blob-output-parameters.md)  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server 程式設計的 OLE DB 驅動程式](../../oledb/ole-db/oledb-driver-for-sql-server-programming.md)        
 [使用大型值型別](../../oledb/features/using-large-value-types.md)  
  
  
