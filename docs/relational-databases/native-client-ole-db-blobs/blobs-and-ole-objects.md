---
description: 'Blob 與 OLE 物件 (Native Client OLE DB 提供者) '
title: Blob 與 OLE 物件 (Native Client OLE DB 提供者) |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- BLOBs, OLE objects
- BLOBs
- storage object [OLE DB]
- SQL Server Native Client OLE DB provider, BLOBs
- large data, OLE objects
ms.assetid: 767fa2f6-9cd2-436f-add5-e760bed29a58
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c7661a35eae2a178df57a1c83f1e0912044f4b1c
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97439959"
---
# <a name="blobs-and-ole-objects-in-sql-server-native-client"></a>SQL Server Native Client 中的 Blob 與 OLE 物件
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]原生用戶端 OLE DB 提供者會公開 **ISequentialStream** 介面，以支援取用者存取 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Ntext**、 **text**、 **image**、 **Varchar (max)**、 **Nvarchar (max)**、 **Varbinary (max)** 和 xml 資料類型做為二進位大型物件 (blob) 。 **ISequentialStream** 上的 **Read** 方法可讓取用者在可管理的區塊中擷取更多資料。  
  
 如需示範此功能的範例，請參閱[設定大型資料 &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-how-to/set-large-data-ole-db.md)。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]當取用者在針對資料修改所系結的存取子中提供介面指標時，Native Client OLE DB 提供者可以使用取用者實 **IStorage** 介面。  
  
 若為大數值資料類型， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會在 **IROWSET** 和 DDL 介面中檢查類型大小假設。 具有 **Varchar**、 **Nvarchar** 和 **Varbinary** 資料類型的資料行，且大小上限設為 [無限制]，將會透過傳回資料行資料類型的架構資料列集和介面，以 ISLONG 的方式呈現。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]原生用戶端 OLE DB 提供者會公開 **Varchar (max)**、 **Varbinary (max)** 和 **Nvarchar (最大**) 類型 DBTYPE_STR DBTYPE_BYTES、DBTYPE_WSTR 和。  
  
 為了使用這些類型，應用程式具有下列選項：  
  
-   繫結為類型 (DBTYPE_BYTES、DBTYPE_STR、DBTYPE_WSTR)。 如果緩衝區不夠大，就會進行截斷，這與舊版中的這些類型完全相同，只是現在使用的是較大數值。  
  
-   繫結為類型，同時指定 DBTYPE_BYREF。  
  
-   繫結為 DBTYPE_IUNKNOWN 並使用資料流。  
  
 如果繫結至 DBTYPE_IUNKNOWN，就會使用 ISequentialStream 資料流功能。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]原生用戶端 OLE DB 提供者支援將輸出參數系結為大數值資料類型的 DBTYPE_IUNKNOWN，以促進預存程式傳回這些資料類型做為傳回值的案例，而這些值會公開為用戶端的 DBTYPE_IUNKNOWN。  
  
## <a name="storage-object-limitations"></a>儲存物件的限制  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]原生用戶端 OLE DB 提供者只能支援單一開啟的儲存物件。 開啟多個儲存物件的嘗試 (取得多個 **ISequentialStream** 介面指標的參考) 會傳回 DBSTATUS_E_CANTCREATE。  
  
-   在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者中，會 VARIANT_TRUE DBPROP_BLOCKINGSTORAGEOBJECTS 唯讀屬性的預設值。 這表示如果儲存物件作用中，某些方法 (非儲存物件的方法) 將會吃敗，並出現 E_UNEXPECTED。  
  
-   當您建立參考儲存物件的資料列存取子時，必須將取用者所執行的儲存物件所顯示的資料長度， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 提供給 Native Client OLE DB 提供者。 取用者必須在建立存取子所使用的 DBBINDING 結構中繫結長度指標。  
  
-   如果資料列包含一個以上的單一大型資料值，但未 DBPROPVAL_AO_RANDOM DBPROP_ACCESSORDER，取用者必須使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 原生用戶端 OLE DB 提供者資料指標支援的資料列集，以在取得資料列資料或處理所有大型資料值之前，先取得資料列的值。 如果 DBPROP_ACCESSORDER DBPROPVAL_AO_RANDOM， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會將所有 xml 資料類型快取為二進位大型物件 (blob) ，如此就能以任何順序來存取它。  
  
## <a name="in-this-section"></a>本節內容  
  
-   [取得大型資料](../../relational-databases/native-client-ole-db-blobs/getting-large-data.md)  
  
-   [設定大型資料](../../relational-databases/native-client-ole-db-blobs/setting-large-data.md)  
  
-   [BLOB 輸出參數的串流支援](../../relational-databases/native-client-ole-db-blobs/streaming-support-for-blob-output-parameters.md)  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Native Client &#40;OLE DB&#41;](../../relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)   
 [使用大型實值型別](../../relational-databases/native-client/features/using-large-value-types.md)  
  
  
