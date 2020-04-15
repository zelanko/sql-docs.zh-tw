---
title: BLOB 與 OLE 物件 | Microsoft Docs
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
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d0cb9751940489513f939ab8ee52728c6b75e925
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81297634"
---
# <a name="blobs-and-ole-objects"></a>BLOB 與 OLE 物件
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本機用戶端 OLE 資料庫提供程式公開**ISequentialStream**介面,[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]以支援使用者存取**ntext、****文本**、**圖像****、varchar(max)、nvarchar(max)、varbinary(max)** 和 xml 資料類型作為**nvarchar(max)****varbinary(max)** 二進位元物件 (BLOB)。 **ISequentialStream** 上的 **Read** 方法可讓取用者在可管理的區塊中擷取更多資料。  
  
 如需示範此功能的範例，請參閱[設定大型資料 &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-how-to/set-large-data-ole-db.md)。  
  
 當[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]消費者在綁定用於數據修改的訪問器中提供介面指標時,本機用戶端 OLE 資料庫提供者可以使用使用者實現的**IStorage**介面。  
  
 對於較大的值資料類型,[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本機用戶端 OLE 資料庫提供程式檢查**IRowset**和 DDL 介面中的類型大小假設。 具有**varchar、nvarchar**和**varbinary**數據類型的列,最大大小設置為無限制,將通過返回列數據類型的架構列集和介面表示**nvarchar**為 ISLONG。  
  
 本機[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]用戶端 OLE DB 提供程式分別將**varchar(最大值**)、varbinary(max) 和**nvarchar(max)****varbinary(max)** 類型公開為DBTYPE_STR、DBTYPE_BYTES和DBTYPE_WSTR。  
  
 為了使用這些類型，應用程式具有下列選項：  
  
-   繫結為類型 (DBTYPE_BYTES、DBTYPE_STR、DBTYPE_WSTR)。 如果緩衝區不夠大，就會進行截斷，這與舊版中的這些類型完全相同，只是現在使用的是較大數值。  
  
-   繫結為類型，同時指定 DBTYPE_BYREF。  
  
-   繫結為 DBTYPE_IUNKNOWN 並使用資料流。  
  
 如果繫結至 DBTYPE_IUNKNOWN，就會使用 ISequentialStream 資料流功能。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本機用戶端 OLE DB 提供程式支援綁定輸出參數作為大型值數據類型DBTYPE_IUNKNOWN,以方便儲存過程將這些數據類型返回為返回值的方案,這些返回值將作為DBTYPE_IUNKNOWN向客戶端公開。  
  
## <a name="storage-object-limitations"></a>儲存物件的限制  
  
-   本機[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]用戶端 OLE 資料庫提供者只能支援單個打開的儲存物件。 開啟多個儲存物件的嘗試 (取得多個 **ISequentialStream** 介面指標的參考) 會傳回 DBSTATUS_E_CANTCREATE。  
  
-   在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本機用戶端 OLE DB 提供程式中,DBPROP_BLOCKINGSTORAGEOBJECTS唯讀屬性的預設值VARIANT_TRUE。 這表示如果儲存物件作用中，某些方法 (非儲存物件的方法) 將會吃敗，並出現 E_UNEXPECTED。  
  
-   創建引用儲存物件的行訪問器時,必須讓[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本機用戶端 OLE DB 提供程式知道由消費者實現的儲存物件提供的數據長度。 取用者必須在建立存取子所使用的 DBBINDING 結構中繫結長度指標。  
  
-   如果一行包含多個較大的數據值,並且DBPROP_ACCESSORDER未DBPROPVAL_AO_RANDOM,則消費者必須使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本機用戶端 OLE DB 提供程式支援游標的行集來檢索行數據或在檢索其他行值之前處理所有大型數據值。 如果DBPROP_ACCESSORDERDBPROPVAL_AO_RANDOM,[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本機用戶端 OLE DB 提供程式會將所有 xml 資料類型緩存為二進位大型物件 (BLOB),以便可以按任意順序存取它。  
  
## <a name="in-this-section"></a>本節內容  
  
-   [取得大型資料](../../relational-databases/native-client-ole-db-blobs/getting-large-data.md)  
  
-   [設定大型資料](../../relational-databases/native-client-ole-db-blobs/setting-large-data.md)  
  
-   [BLOB 輸出參數的串流支援](../../relational-databases/native-client-ole-db-blobs/streaming-support-for-blob-output-parameters.md)  
  
## <a name="see-also"></a>另請參閱  
 [SQL 伺服器本機用戶端&#40;OLE DB&#41;](../../relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)   
 [使用大數值類型](../../relational-databases/native-client/features/using-large-value-types.md)  
  
  
