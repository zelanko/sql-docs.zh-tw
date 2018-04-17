---
title: Blob 與 OLE 物件 |Microsoft 文件
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: native-client-ole-db-blobs
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- BLOBs, OLE objects
- BLOBs
- storage object [OLE DB]
- SQL Server Native Client OLE DB provider, BLOBs
- large data, OLE objects
ms.assetid: 767fa2f6-9cd2-436f-add5-e760bed29a58
caps.latest.revision: 43
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 686f9f7c4ec9562e6e5141553a3a36d779e7ad68
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="blobs-and-ole-objects"></a>BLOB 與 OLE 物件
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會公開**ISequentialStream**介面，以支援取用者存取[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **ntext**，**文字**，**映像**， **varchar （max)**， **nvarchar （max)**， **varbinary （max)**，及 xml 資料類型為二進位大型物件 (Blob)。 **讀取**方法**ISequentialStream**可讓取用者擷取更多可管理的區塊中的資料。  
  
 如需示範這項功能的範例，請參閱[大型資料集 & #40; OLE DB & #41;](../../relational-databases/native-client-ole-db-how-to/set-large-data-ole-db.md)。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者可以使用取用者實作**IStorage**介面，取用者提供的存取子中的介面指標時繫結的資料修改。  
  
 對於大數值資料類型， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會檢查類型中的大小假設**IRowset**和 DDL 介面。 具有資料行**varchar**， **nvarchar**，和**varbinary**大小上限設定為無限制的資料類型會以 ISLONG 表示透過結構描述資料列和傳回資料行資料類型的介面。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會公開**varchar （max)**， **varbinary （max)**和**nvarchar （max)**類型分別為 DBTYPE_STR、 DBTYPE_BYTES 和 DBTYPE_WSTR。  
  
 為了使用這些類型，應用程式具有下列選項：  
  
-   繫結為類型 (DBTYPE_BYTES、DBTYPE_STR、DBTYPE_WSTR)。 如果緩衝區不夠大，就會進行截斷，這與舊版中的這些類型完全相同，只是現在使用的是較大數值。  
  
-   繫結為類型，同時指定 DBTYPE_BYREF。  
  
-   繫結為 DBTYPE_IUNKNOWN 並使用資料流。  
  
 如果繫結至 DBTYPE_IUNKNOWN，就會使用 ISequentialStream 資料流功能。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者支援繫結的輸出參數針對大數值資料類型為 dbtype_iunknown 其中是預存程序會傳回這些資料類型為傳回值會公開為 DBTYPE_IUNKNOWN 給用戶端。  
  
## <a name="storage-object-limitations"></a>儲存物件的限制  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者可支援只有一個開啟的儲存物件。 嘗試開啟一個以上的儲存物件 (取得多個參考**ISequentialStream**介面指標) 傳回 DBSTATUS_E_CANTCREATE。  
  
-   在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者，DBPROP_BLOCKINGSTORAGEOBJECTS 唯讀屬性的預設值為 VARIANT_TRUE。 這表示如果儲存物件作用中，某些方法 (非儲存物件的方法) 將會吃敗，並出現 E_UNEXPECTED。  
  
-   取用者實作的儲存物件呈現的資料長度必須設定成已知[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者的資料列存取子，參考儲存體物件建立時。 取用者必須在建立存取子所使用的 DBBINDING 結構中繫結長度指標。  
  
-   如果資料列包含一個以上的單一大型資料值，而且 DBPROP_ACCESSORDER 不是 DBPROPVAL_AO_RANDOM，取用者必須使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者資料指標支援資料列集來擷取資料列資料，或擷取其他資料列值前處理所有大型資料值。 如果 DBPROP_ACCESSORDER 是 DBPROPVAL_AO_RANDOM， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會快取所有 xml 資料型別當做二進位大型物件 (Blob)，以便它可以依照任何順序存取。  
  
## <a name="in-this-section"></a>本節內容  
  
-   [取得大型資料](../../relational-databases/native-client-ole-db-blobs/getting-large-data.md)  
  
-   [設定大型資料](../../relational-databases/native-client-ole-db-blobs/setting-large-data.md)  
  
-   [BLOB 輸出參數的串流支援](../../relational-databases/native-client-ole-db-blobs/streaming-support-for-blob-output-parameters.md)  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Native Client & #40; OLE DB & #41;](../../relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)   
 [使用大型值型別](../../relational-databases/native-client/features/using-large-value-types.md)  
  
  
