---
title: Blob 與 OLE 物件 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e459682da63bac8359fa8310233c234e456f4e5b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63195223"
---
# <a name="blobs-and-ole-objects"></a>BLOB 與 OLE 物件
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會公開**ISequentialStream**介面，以支援取用者存取[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **ntext**，**文字**，**映像**， **varchar （max)**， **nvarchar （max)**， **varbinary （max)**，以及 xml 資料類型當做二進位大型物件 (Blob). **ISequentialStream** 上的 **Read** 方法可讓取用者在可管理的區塊中擷取更多資料。  
  
 如需示範這項功能的範例，請參閱 <<c0> [ 大型資料集&#40;OLE DB&#41;](../native-client-ole-db-how-to/set-large-data-ole-db.md)。</c0>  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者可以使用取用者實作**IStorage**介面時取用者提供的介面指標，存取子中繫結的資料修改。  
  
 對於大數值資料類型， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會檢查型別中的大小假設**IRowset**和 DDL 介面。 資料行**varchar**， **nvarchar**，並**varbinary**會透過結構描述資料列和介面以 ISLONG 表示資料型別，且設定為無限制的大小上限傳回資料行資料類型。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會公開**varchar （max)**， **varbinary （max)** 並**nvarchar （max)** 為 DBTYPE_STR、 DBTYPE_BYTES 和 DBTYPE_ 類型WSTR 分別。  
  
 為了使用這些類型，應用程式具有下列選項：  
  
-   繫結為類型 (DBTYPE_BYTES、DBTYPE_STR、DBTYPE_WSTR)。 如果緩衝區不夠大，就會進行截斷，這與舊版中的這些類型完全相同，只是現在使用的是較大數值。  
  
-   繫結為類型，同時指定 DBTYPE_BYREF。  
  
-   繫結為 DBTYPE_IUNKNOWN 並使用資料流。  
  
 如果繫結至 DBTYPE_IUNKNOWN，就會使用 ISequentialStream 資料流功能。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者支援將繫結的輸出參數針對大數值資料類型為 dbtype_iunknown，預存程序會傳回這些資料類型以傳回的值將會公開為 DBTYPE_IUNKNOWN用戶端。  
  
## <a name="storage-object-limitations"></a>儲存物件的限制  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者可支援只有單一開啟的儲存體物件。 開啟多個儲存物件的嘗試 (取得多個 **ISequentialStream** 介面指標的參考) 會傳回 DBSTATUS_E_CANTCREATE。  
  
-   在  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者，DBPROP_BLOCKINGSTORAGEOBJECTS 唯讀屬性的預設值為 VARIANT_TRUE。 這表示如果儲存物件作用中，某些方法 (非儲存物件的方法) 將會吃敗，並出現 E_UNEXPECTED。  
  
-   取用者實作的儲存物件呈現的資料長度必須成為已知[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者建立參考儲存體物件的資料列存取子時。 取用者必須在建立存取子所使用的 DBBINDING 結構中繫結長度指標。  
  
-   如果資料列都包含多個單一的大型資料值，而且 DBPROP_ACCESSORDER 不是 DBPROPVAL_AO_RANDOM，取用者必須使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者資料指標支援資料列集來擷取資料列的資料，或處理所有大型資料值之前正在擷取其他資料列值。 如果 DBPROP_ACCESSORDER 是 DBPROPVAL_AO_RANDOM， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會快取所有 xml 資料類型當做二進位大型物件 (Blob)，使它可以依照任何順序存取。  
  
## <a name="in-this-section"></a>本節內容  
  
-   [取得大型資料](getting-large-data.md)  
  
-   [設定大型資料](setting-large-data.md)  
  
-   [BLOB 輸出參數的串流支援](streaming-support-for-blob-output-parameters.md)  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Native Client &#40;OLE DB&#41;](../native-client/ole-db/sql-server-native-client-ole-db.md)   
 [使用大型實值型別](../native-client/features/using-large-value-types.md)  
  
  
