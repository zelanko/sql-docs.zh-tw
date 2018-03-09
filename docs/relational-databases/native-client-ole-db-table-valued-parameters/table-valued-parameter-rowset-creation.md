---
title: "資料表值參數資料列集建立 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-ole-db-table-valued-parameters
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- table-valued parameters, rowset creation
ms.assetid: ffe213ca-cc0e-465e-b31c-a8272324c4fe
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b748b0c9966250c9430a1a54c59d38f713c57689
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="table-valued-parameter-rowset-creation"></a>建立資料表值參數資料列集
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  雖然取用者可以提供資料表值參數的任何資料列集物件，但是一般的資料列集物件都會針對後端資料存放區來實作，因此所提供的效能會受到限制。 基於這個原因，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會讓取用者在記憶體中的資料之上建立特殊的資料列集物件。 這個特殊的記憶體中的資料列集物件是新的 COM 物件，稱為資料表值參數資料列集。 它會提供類似參數集的功能。  
  
 資料表值參數資料列集物件是由取用者針對輸入參數所明確建立，而且是透過多個工作階段層級介面。 每個資料表值參數都有資料表值參數資料列集物件的一個執行個體。 取用者可以建立資料表值參數資料列集物件，其方式是提供已知的中繼資料資訊 (靜態案例) 或是透過提供者介面來探索 (動態案例)。 下列章節描述這兩個案例。  
  
## <a name="static-scenario"></a>靜態案例  
 當已知型別資訊時，取用者使用 ITableDefinitionWithConstraints::CreateTableWithConstraints 具現化都對應至資料表值參數的資料表值參數資料列集物件。  
  
 *Guid*欄位 (*Createtable*參數) 包含特殊 GUID (CLSID_ROWSET_TVP)。 *PwszName*成員包含取用者想要具現化資料表值參數類型的名稱。 *EKind*欄位將會設定為 DBKIND_GUID_NAME。 當此陳述式為特定的 SQL 時，就需要這個名稱；如果它是程序呼叫，則此名稱為選擇性。  
  
 對於彙總，取用者會傳遞*pUnkOuter* controlling IUnknown 參數。  
  
 資料表值參數資料列集物件屬性唯讀，因此取用者不應該在中設定任何屬性*rgPropertySets*。  
  
 如*rgPropertySets*成員的每一個 DBCOLUMNDESC 結構時，取用者可以指定每個資料行的其他屬性。 這些屬性屬於 DBPROPSET_SQLSERVERCOLUMN 屬性集， 它們可讓您針對每一個資料行指定計算和預設的設定， 它們也支援現有的資料行屬性，例如 Null 屬性和識別。  
  
 若要從資料表值參數資料列集物件擷取對應的資訊，取用者會使用 irowsetinfo:: Getproperties。  
  
 若要擷取資訊 null、 唯一、 計算，並更新每個資料行的狀態，取用者會使用 icolumnsrowset:: Getcolumnsrowset 或 icolumnsinfo:: Getcolumninfo。 這些方法會提供有關每一個資料表值參數資料列集資料行的詳細資訊。  
  
 取用者會指定資料表值參數之每一個資料行的類型。 這類似於在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中建立資料表時指定資料行的方式。 取用者包含從資料表值參數資料列集物件[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者透過*ppRowset*輸出參數。  
  
## <a name="dynamic-scenario"></a>動態案例  
 當取用者沒有類型資訊時，它應該使用 iopenrowset:: Openrowset 來具現化資料表值參數資料列集物件。 取用者只需要提供類型名稱給提供者。  
  
 在此案例中，提供者會代表取用者包含來自伺服器之資料表值參數資料列集物件的相關類型資訊。  
  
 *Createtable*和*pUnkOuter*參數應該設定與靜態案例相同。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者從伺服器取得的型別資訊 （資料行資訊和條件約束），然後傳回資料表值參數資料列集物件，用來*ppRowset*參數。 這項作業需要與伺服器通訊，因此其效能不比靜態案例。 動態案例只適用於參數化程序呼叫。  
  
## <a name="see-also"></a>另請參閱  
 [資料表值參數 &#40; OLE DB &#41;](../../relational-databases/native-client-ole-db-table-valued-parameters/table-valued-parameters-ole-db.md)   
 [使用資料表值參數 &#40; OLE DB &#41;](../../relational-databases/native-client-ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  
