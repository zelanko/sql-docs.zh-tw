---
title: 提取資料列 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- fetching rows
- OLE DB rowsets, fetching
- rowsets [OLE DB], fetching
- IRowset interface
- SQL Server Native Client OLE DB provider, fetching
ms.assetid: 5e6dbe36-b682-464d-adfa-8e886f9bd452
caps.latest.revision: 30
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: 21d63022b01f91977472e07b777e4d061e36c24b
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/06/2018
ms.locfileid: "39565992"
---
# <a name="fetching-rows"></a>提取資料列
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  **IRowset** 介面是基底資料列集介面。 **IRowset** 介面提供的方法會循序擷取資料列、從這些資料列中取得資料，以及管理資料列。 取用者會使用 **IRowset** 中的方法，進行所有基本資料列集作業。 這包括提取與釋放資料列，以及取得資料行值。  
  
 當取用者取得資料列集的介面指標時，第一個步驟通常是使用 **IRowsetInfo::GetProperties** 方法，決定資料列集的功能。 這會傳回由資料列集公開之介面的相關資訊，同時也會傳回不當做不同介面顯示之資料列集的功能，例如，使用中資料列的數目上限，以及可以同時擁有擱置中更新之資料列的數目。  
  
 取用者的下一個步驟是決定資料列集中資料行的特性或中繼資料。 因此，他們會針對簡單的資料行資訊使用 **IColumnsInfo** 方法，或針對擴充的資料行資訊使用 **IColumnsRowset** 方法。 **GetColumnInfo** 方法會傳回下列資訊：  
  
-   結果集中的資料行數目。  
  
-   DBCOLUMNINFO 結構的陣列，每個資料行一個。  
  
     結構的順序就是資料行出現在資料列集中的順序。 每個 DBCOLUMNINFO 結構都包含資料行中繼資料，例如，資料行名稱、資料行的序數、資料行中值的可能最大長度、資料行的資料類型、有效位數以及長度。  
  
-   單一配置區塊內，用於儲存所有字串值的指標。  
  
 取用者會從中繼資料，或根據產生資料列集的文字命令，決定所需的資料行。 它會從 **IColumnsInfo** 所傳回之資料行資訊的順序，或從 **IColumnsRowset** 所傳回之資料行中繼資料資料列集中的序數，決定所需資料行的序數。  
  
 **IColumnsInfo** 和 **IColumnsRowset** 介面用於擷取資料列集中資料行的相關資訊。 **IColumnsInfo** 介面會傳回一組有限的資訊，而 **IColumnsRowset** 則會提供所有中繼資料。  
  
> [!NOTE]  
>  在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0 和更早版本中，**IColumnsInfo::GetColumnsInfo** 所傳回的選擇性中繼資料行 DBCOLUMN_COMPUTEMODE 會傳回 DBSTATUS_S_ISNULL (而非描述資料行是否經過計算的值)，因為無法判斷基礎資料行是否經過計算。  
  
 序數用於指定資料行的繫結。 繫結是一種結構，可讓取用者結構的元素與資料行產生關聯。 繫結可以繫結資料行的資料值、長度與狀態值。  
  
 在存取子中，會將一組繫結收集在一起。 這是使用 **IAccessor::CreateAccessor** 方法建立的。 一個存取子可能包含多個繫結，讓多個資料行的資料可以在單一呼叫中擷取或設定。 取用者可以建立數個存取子來比對應用程式不同部分中的不同使用模式。 它可以建立與釋放存取子，並讓資料列集仍保持存在。  
  
 若要從資料庫擷取資料列，取用者會呼叫一個方法，例如 **IRowset::GetNextRows** 或 **IRowsetLocate::GetRowsAt**。 這些提取作業會將伺服器中的原始資料放入提供者的資料列緩衝區中。 取用者無法直接存取提供者的資料列緩衝區。 取用者會使用 **IRowset::GetData**，將提供者緩衝區的資料複製到取用者緩衝區，並使用 **IRowsetChange::SetData**，將取用者緩衝區的資料變更複製到提供者緩衝區。  
  
 取用者會呼叫 **GetData** 方法，並將控制代碼傳遞到資料列、將控制代碼傳遞到存取子，以及將指標傳遞到取用者配置的緩衝區中。 **GetData** 會轉換資料，並依照建立存取子所使用之繫結的指定，傳回資料行。 取用者可以使用不同的存取子和緩衝區，針對資料列呼叫多次 **GetData**，讓取用者可以取得相同資料的多個複本。  
  
 可變長度資料行的資料可以用數種方式處理。 首先，此類資料行可以繫結至有限的取用者結構區段。 這在資料長度超過緩衝區長度時，會造成截斷。 取用者可以檢查 DBSTATUS_S_TRUNCATED 狀態來判斷截斷已發生。 傳回的長度永遠是真實的位元組長度，讓取用者也可以決定要截斷多少資料。  
  
 當取用者完成資料列的擷取或更新時，它會以 **ReleaseRows** 方法釋放這些資料列。 這樣會從資料列集的資料列複本中釋放資源，並為新的資料列騰出空間。 接著，取用者可以重複其提取或建立資料列，並存取其中資料的循環。  
  
 當取用者完成資料列集時，它會呼叫 **IAccessor::ReleaseAccessor** 方法來釋放所有存取子。 它會針對資料列集所公開的所有介面呼叫 **IUnknown::Release** 方法，藉以釋放資料列集。 進行資料列集釋放時，它會強制釋放取用者可能保存的所有剩餘資料列或存取子。  
  
## <a name="in-this-section"></a>本節內容  
  
-   [下一個擷取位置](../../relational-databases/native-client-ole-db-rowsets/fetching-rows-next-fetch-position.md)  
  
## <a name="see-also"></a>另請參閱  
 [資料列集](../../relational-databases/native-client-ole-db-rowsets/rowsets.md)  
  
  
