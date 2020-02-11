---
title: Blob 和 OLE 物件 |Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "63195223"
---
# <a name="blobs-and-ole-objects"></a>BLOB 與 OLE 物件
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會公開**ISequentialStream**介面，以支援取用者[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **存取 Ntext**、 **text**、 **image**、 **Varchar （max）**、 **Nvarchar （max）**、 **Varbinary （max）** 和 xml 資料類型做為二進位大型物件（blob）。 
  **ISequentialStream** 上的 **Read** 方法可讓取用者在可管理的區塊中擷取更多資料。  
  
 如需示範這項功能的範例，請參閱[Set 大型資料 &#40;OLE DB&#41;](../native-client-ole-db-how-to/set-large-data-ole-db.md)。  
  
 當[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]取用者在針對資料修改所系結的存取子中提供介面指標時，Native Client OLE DB 提供者可以使用取用者實**IStorage**介面。  
  
 對於大數值資料類型， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會在**IRowset**和 DDL 介面中檢查類型大小假設。 將 max 大小設為 [無限制] 的**Varchar**、 **Nvarchar**和**Varbinary**資料類型的資料行，將會以 ISLONG 的方式，透過架構資料列集和傳回資料類型的介面來表示。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會將**Varchar （max）**、 **Varbinary （max）** 和**Nvarchar （max）** 類型分別公開為 DBTYPE_STR、DBTYPE_BYTES 和 DBTYPE_WSTR。  
  
 為了使用這些類型，應用程式具有下列選項：  
  
-   繫結為類型 (DBTYPE_BYTES、DBTYPE_STR、DBTYPE_WSTR)。 如果緩衝區不夠大，就會進行截斷，這與舊版中的這些類型完全相同，只是現在使用的是較大數值。  
  
-   繫結為類型，同時指定 DBTYPE_BYREF。  
  
-   繫結為 DBTYPE_IUNKNOWN 並使用資料流。  
  
 如果繫結至 DBTYPE_IUNKNOWN，就會使用 ISequentialStream 資料流功能。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者支援將輸出參數系結為大數值資料類型的 DBTYPE_IUNKNOWN，以加速預存程式傳回這些資料類型做為傳回值（將公開為用戶端的 DBTYPE_IUNKNOWN）的案例。  
  
## <a name="storage-object-limitations"></a>儲存物件的限制  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者只能支援單一開啟的儲存物件。 開啟多個儲存物件的嘗試 (取得多個 **ISequentialStream** 介面指標的參考) 會傳回 DBSTATUS_E_CANTCREATE。  
  
-   在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者中，DBPROP_BLOCKINGSTORAGEOBJECTS 唯讀屬性的預設值為 VARIANT_TRUE。 這表示如果儲存物件作用中，某些方法 (非儲存物件的方法) 將會吃敗，並出現 E_UNEXPECTED。  
  
-   當建立參考儲存物件的資料列存取子時，由取用者所實儲存[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]物件所呈現的資料長度必須由 Native Client OLE DB 提供者知道。 取用者必須在建立存取子所使用的 DBBINDING 結構中繫結長度指標。  
  
-   如果資料列包含一個以上的單一大型資料值，但未 DBPROPVAL_AO_RANDOM DBPROP_ACCESSORDER，取用者必須使用 Native Client [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] OLE DB 提供者資料指標支援的資料列集，以在抓取其他資料列值之前，先取得資料列資料或處理所有的大型資料值。 如果 DBPROPVAL_AO_RANDOM DBPROP_ACCESSORDER， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會快取所有 xml 資料類型做為二進位大型物件（blob），以便依任何順序存取。  
  
## <a name="in-this-section"></a>本節內容  
  
-   [取得大型資料](getting-large-data.md)  
  
-   [設定大型資料](setting-large-data.md)  
  
-   [BLOB 輸出參數的串流支援](streaming-support-for-blob-output-parameters.md)  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Native Client &#40;OLE DB&#41;](../native-client/ole-db/sql-server-native-client-ole-db.md)   
 [使用大數值類型](../native-client/features/using-large-value-types.md)  
  
  
