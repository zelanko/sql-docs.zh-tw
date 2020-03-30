---
title: BLOB 與 OLE 物件 | Microsoft Docs
description: BLOB 與 OLE 物件
ms.custom: ''
ms.date: 06/14/2018
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
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 70d3ffccfc9613434b09335944e445a2705b95c3
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "67988676"
---
# <a name="blobs-and-ole-objects"></a>BLOB 與 OLE 物件
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  OLE DB Driver for SQL Server 會公開 **ISequentialStream** 介面，以支援取用者存取 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **ntext**、**text**、**image**、**varchar(max)** 、**nvarchar(max)** 、**varbinary(max)** 及 xml 資料類型作為二進位大型物件 (BLOB)。 **ISequentialStream** 上的 **Read** 方法可讓取用者在可管理的區塊中擷取更多資料。  
  
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
  
  
