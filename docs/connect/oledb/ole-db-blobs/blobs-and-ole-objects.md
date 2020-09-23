---
title: BLOB 與 OLE 物件 (OLE DB 驅動程式) | Microsoft Docs
description: 了解 OLE DB Driver for SQL Server 中的 ISequentialStream 介面如何支援取用者以二進位大型物件的形式存取 SQL Server 資料類型。
ms.custom: ''
ms.date: 05/25/2020
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- BLOBs, OLE objects
- BLOBs
- storage object [OLE DB]
- OLE DB Driver for SQL Server, BLOBs
- large data, OLE objects
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 50c19527b536da0a61d8aa6c7c76ec34010ea268
ms.sourcegitcommit: c95f3ef5734dec753de09e07752a5d15884125e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/25/2020
ms.locfileid: "88861417"
---
# <a name="blobs-and-ole-objects"></a>BLOB 與 OLE 物件
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  OLE DB Driver for SQL Server 會公開 **ISequentialStream** 介面，以支援取用者存取 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **ntext**、**text**<a href="#text_note"><sup>**1**</sup></a>、**image**、**varchar(max)** 、**nvarchar(max)** 、**varbinary(max)** 及 XML 資料類型作為二進位大型物件 (BLOB)。 **ISequentialStream** 上的 **Read** 方法可讓取用者在可管理的區塊中擷取更多資料。

 <b id="text_note">[1]：</b>使用 ISequentialStream 介面將 UTF-8 編碼資料插入舊版文字資料行僅限於支援 UTF-8 的伺服器。 當以不支援 UTF-8 的伺服器為目標時，如果嘗試執行此案例，將會導致驅動程式張貼下列錯誤訊息：「選取的資料行型別不支援資料流」。

 如需示範此功能的範例，請參閱[設定大型資料 &#40;OLE DB&#41;](../../oledb/ole-db-how-to/set-large-data-ole-db.md)。  
  
 當取用者在針對資料修改所繫結的存取子中提供介面指標時，OLE DB Driver for SQL Server 可以使用取用者實作的 **IStorage** 介面。  
  
 針對大數值資料類型，OLE DB Driver for SQL Server 會在 **IRowset** 和 DDL 介面中檢查假設的類型大小。 資料類型為 **varchar**、**nvarchar** 和 **varbinary**，而且大小上限設定為無限的資料行將會透過結構描述資料列集和傳回資料行資料類型的介面，以 ISLONG 表示。  
  
 OLE DB Driver for SQL Server 會將 **varchar(max)** 、**varbinary(max)** 和 **nvarchar(max)** 類型分別公開為 DBTYPE_STR、DBTYPE_BYTES 和 DBTYPE_WSTR。  
  
 為了使用這些類型，應用程式具有下列選項：  
  
-   繫結為類型 (DBTYPE_BYTES、DBTYPE_STR、DBTYPE_WSTR)。 如果緩衝區不夠大，就會進行截斷，這與舊版中的這些類型完全相同，只是現在使用的是較大數值。  
  
-   繫結為類型，同時指定 DBTYPE_BYREF。  
  
-   繫結為 DBTYPE_IUNKNOWN 並使用資料流。  
  
 如果繫結至 DBTYPE_IUNKNOWN，就會使用 ISequentialStream 資料流功能。 OLE DB Driver for SQL Server 支援將輸出參數繫結為 DBTYPE_IUNKNOWN，以供大數值資料類型使用。 這是為了支援預存程序會以傳回值來傳回這些資料類型的案例，而其將會以 DBTYPE_IUNKNOWN 傳回給用戶端。  
  
## <a name="storage-object-limitations"></a>儲存物件的限制  
  
-   OLE DB Driver for SQL Server 僅可支援單一開啟的儲存物件。 開啟多個儲存物件的嘗試 (取得多個 **ISequentialStream** 介面指標的參考) 會傳回 DBSTATUS_E_CANTCREATE。  
  
-   在 OLE DB Driver for SQL Server 中，DBPROP_BLOCKINGSTORAGEOBJECTS 唯讀屬性的預設值為 VARIANT_TRUE。 因此，如果儲存物件作用中，某些方法 (非儲存物件的方法) 將會失敗，並出現 E_UNEXPECTED。  
  
-   建立參考儲存物件的資料列存取子時，以取用者實作之儲存物件呈現的資料長度必須讓 OLE DB Driver for SQL Server 知道。 取用者必須在建立存取子所使用的 DBBINDING 結構中繫結長度指標。  
  
-   如果資料列包含一個以上的單一大型資料集，而且 DBPROP_ACCESSORDER 不是 DBPROPVAL_AO_RANDOM，取用者必須使用 OLE DB Driver for SQL Server 資料指標支援的資料列集來擷取資料列資料，或在擷取其他資料列值前處理所有大型資料值。 如果 DBPROP_ACCESSORDER 是 DBPROPVAL_AO_RANDOM，OLE DB Driver for SQL Server 會快取所有 XML 資料類型當作二進位大型物件 (BLOB)，因此可以用任何順序進行存取。  
  
## <a name="in-this-section"></a>本節內容  
  
-   [取得大型資料](../../oledb/ole-db-blobs/getting-large-data.md)  
  
-   [設定大型資料](../../oledb/ole-db-blobs/setting-large-data.md)  
  
-   [BLOB 輸出參數的串流支援](../../oledb/ole-db-blobs/streaming-support-for-blob-output-parameters.md)  
  
## <a name="see-also"></a>另請參閱  
 [OLE DB Driver for SQL Server 程式設計](../../oledb/ole-db/oledb-driver-for-sql-server-programming.md)        
 [使用大型實值型別](../../oledb/features/using-large-value-types.md)  
  
  
