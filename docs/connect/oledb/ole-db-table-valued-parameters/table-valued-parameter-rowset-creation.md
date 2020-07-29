---
title: 建立資料表值參數資料列集 | Microsoft Docs
description: 以靜態及動態方式建立資料表值參數資料列集
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- table-valued parameters, rowset creation
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 00103e02efe284e9c5d60e2f251f8bc28646a30d
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/06/2020
ms.locfileid: "86003341"
---
# <a name="table-valued-parameter-rowset-creation"></a>建立資料表值參數資料列集
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  雖然取用者可以提供資料表值參數的任何資料列集物件，但是一般的資料列集物件都會針對後端資料存放區來實作，因此所提供的效能會受到限制。 基於這個原因，OLE DB Driver for SQL Server 會讓取用者在記憶體內部資料之上建立特殊的資料列集物件。 此特殊的記憶體中資料列集物件是一種新的 COM 物件，稱為資料表值參數資料列集。 它會提供類似參數集的功能。  
  
 資料表值參數資料列集物件是由取用者針對輸入參數所明確建立，而且是透過多個工作階段層級介面。 每個資料表值參數都有資料表值參數資料列集物件的一個執行個體。 取用者可以建立資料表值參數資料列集物件，其方式是提供已知的中繼資料資訊 (靜態案例) 或是透過提供者介面來探索 (動態案例)。 下列章節描述這兩個案例。  
  
## <a name="static-scenario"></a>靜態案例  
 當類型資訊已知時，取用者會使用 ITableDefinitionWithConstraints::CreateTableWithConstraints 來具現化對應至資料表值參數的資料表值參數資料列集物件。  
  
 *guid* 欄位 (*pTableID* 參數) 包含特殊 GUID (CLSID_ROWSET_TVP)。 *pwszName* 成員包含取用者想要具現化之資料表值參數類型的名稱。 *eKind* 欄位將會設定為 DBKIND_GUID_NAME。 當此陳述式為特定的 SQL 時，就需要這個名稱；如果它是程序呼叫，則此名稱為選擇性。  
  
 為了彙總，取用者會傳遞具有控制之 IUnknown 的 *pUnkOuter* 參數。  
  
 資料表值參數資料列集物件屬性是唯讀的，因此不會預期取用者在 *rgPropertySets* 中設定任何屬性。  
  
 對於每一個 DBCOLUMNDESC 結構的 *rgPropertySets* 數目而言，取用者可以為每一個資料行指定其他屬性。 這些屬性屬於 DBPROPSET_SQLSERVERCOLUMN 屬性集， 它們可讓您針對每一個資料行指定計算和預設的設定， 它們也支援現有的資料行屬性，例如 Null 屬性和識別。  
  
 若要從資料表值參數資料列集物件擷取對應的資訊，取用者會使用 IRowsetInfo::GetProperties。  
  
 若要擷取每個資料行的 null、unique、computed 與 update 狀態資訊，取用者可以使用 IColumnsRowset::GetColumnsRowset 或 IColumnsInfo::GetColumnInfo。 這些方法會提供有關每一個資料表值參數資料列集資料行的詳細資訊。  
  
 取用者會指定資料表值參數之每一個資料行的類型。 這類似於在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中建立資料表時指定資料行的方式。 取用者透過 *ppRowset* 輸出參數從 OLE DB Driver for SQL Server 取得資料表值參數資料列集物件。  
  
## <a name="dynamic-scenario"></a>動態案例  
 當取用者沒有類型資訊時，其應該使用 IOpenRowset::OpenRowset 來具現化資料表值參數資料列集物件。 取用者只需要提供類型名稱給提供者。  
  
 在此案例中，提供者會代表取用者包含來自伺服器之資料表值參數資料列集物件的相關類型資訊。  
  
 *pTableID* 和 *pUnkOuter* 參數的設定應該與靜態案例相同。 然後 OLE DB Driver for SQL Server 會從伺服器取得類型資訊 (資料行資訊和條件約束)，並透過 *ppRowset* 參數傳回資料表值參數資料列集物件。 這項作業需要與伺服器通訊，因此其效能不比靜態案例。 動態案例只適用於參數化程序呼叫。  
  
## <a name="see-also"></a>另請參閱  
 [資料表值參數 &#40;OLE DB&#41;](../../oledb/ole-db-table-valued-parameters/table-valued-parameters-ole-db.md)   
 [使用資料表值參數 &#40;OLE DB&#41;](../../oledb/ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  
