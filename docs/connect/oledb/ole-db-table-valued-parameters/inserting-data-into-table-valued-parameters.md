---
title: 將資料插入資料表值參數 (OLE DB Driver for SQL Server) | Microsoft Docs
description: OLE DB Driver for SQL Server 支援推送模型和提取模型，供取用者指定資料表值參數資料列的資料。
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- table-valued parameters, inserting data into
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5317574a09194b2a926bed88de7edf7db913df6a
ms.sourcegitcommit: c95f3ef5734dec753de09e07752a5d15884125e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/25/2020
ms.locfileid: "88859900"
---
# <a name="inserting-data-into-table-valued-parameters"></a>將資料插入至資料表值參數
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  OLE DB Driver for SQL Server 支援取用者的兩個模型，以指定資料表值參數資料列的資料：發送模型及提取模型。 您可使用示範提取模型的範例，請參閱 [SQL Server 資料程式設計範例](https://msftdpprodsamples.codeplex.com/)。  
  
> [!NOTE]  
>  資料表值參數資料行在所有資料列中都必須有非預設值，或在所有資料列中都必須有預設值。 在某些資料列中有預設值，而在其他資料列中則沒有預設值是不可能的。 因此，在資料表值參數繫結中，資料表值參數資料列集資料行資料所允許的唯一狀態值為 DBSTATUS_S_ISNULL 和 DBSTATUS_S_OK。 DBSTATUS_S_DEFAULT 將會導致失敗，而繫結的狀態值將會設定為 DBSTATUS_E_BADSTATUS。  
  
## <a name="push-model-loads-all-table-valued-parameter-data-in-memory"></a>發送模型 (將所有資料表值參數資料載入到記憶體中)  
 發送模型類似於使用參數集 (也就是 ICommand::Execute 中的 DBPARAMS 參數)。 只有在沒有 IRowset 介面之自訂實作的情況下使用資料表值參數資料列集物件時，才會使用發送模型。 當資料表值參數資料列集中的資料列數目很小，而且不打算在將過量的記憶體壓力放在應用程式上時，建議使用發送模型。 這比提取模型簡單，因為比起目前在一般 OLE DB 應用程式中常用的功能，發送模型不需要使用來自取用者應用程式的其他任何功能。  
  
 取用者應該在執行命令前，提供所有資料表值參數資料給提供者。 若要提供資料，取用者要針對每個資料表值參數擴展資料表值參數資料列集物件。 資料表值參數資料列集物件會公開資料列集的 Insert、Set 和 Delete 作業，取用者會使用這些作業來操作資料表值參數資料。 提供者將會在執行時間，從此資料表值參數資料列集物件提取資料。  
  
 將資料表值參數資料列集物件提供給取用者時，取用者可以將其當做資料列集物件處理。 取用者可以使用 IColumnsInfo::GetColumnInfo 或 IColumnsRowset::GetColumnsRowset 介面方法，取得每個資料行的類型資訊 (類型、最大長度、精確度與小數位數)。 接著，取用者會建立存取子來指定資料的繫結。 下一步是將資料的資料列插入到資料表值參數資料列集。 您可以使用 IRowsetChange::InsertRow 來完成此作業。 如果您必須操作資料，也可以在資料表值參數資料列集物件上使用 IRowsetChange::SetData 或 IRowsetChange::DeleteRows。 資料表值參數資料列集物件是計數的參考，類似於資料流物件。  
  
 如果使用 IColumnsRowset::GetColumnsRowset，則會在產生之資料行的資料列集物件上，進行 IRowset::GetNextRows、IRowset::GetData 和 IRowset::ReleaseRows 方法的後續呼叫。  
  
 OLE DB Driver for SQL Server 開始執行命令之後，將會從此資料表值參數資料列集物件擷取資料表值參數值，再傳送到伺服器。  
  
 發送模型需要取用者的最少工作，但是使用的記憶體比提取模型更多，因為所有資料表值參數資料在執行時間都必須位於記憶體中。  
  
## <a name="pull-model-obtaining-table-valued-parameter-data-on-demand-from-the-consumer"></a>提取模型 (視需要從取用者取得資料表值參數資料)  
 提取模型對於下列兩種案例很實用：  
  
-   以資料流方式處理資料列。  
  
-   如果其他提供者的資料列集當做資料表值參數值使用。  
  
 在提取模型中，取用者會視需要提供資料給提供者。 如果您的應用程式有許多資料插入，而且記憶體中的資料表值參數資料列集資料會導致過量的記憶體存取，請使用此方法。 如果使用多個 OLE DB 提供者，取用者提取模型會讓取用者提供任何資料列集物件，當做資料表值參數值。  
  
 若要使用提取模型，取用者必須提供資料列集物件自己的實作。 搭配資料表值參數資料列集 (CLSID_ROWSET_TVP) 使用提取模型時，需要取用者彙總提供者透過 ITableDefinitionWithConstraints::CreateTableWithConstraints 方法或 IOpenRowset::OpenRowset 方法公開的資料表值參數資料列集物件。 只有取用者物件會覆寫 IRowset 介面實作。 您必須覆寫下列函數：  
  
-   IRowset::GetNextRows  
  
-   IRowset::AddRefRows  
  
-   IRowset::GetData  
  
-   IRowset::ReleaseRows  
  
-   IRowset::RestartPosition  
  
 OLE DB Driver for SQL Server 會從取用者資料列集物件一次讀取一或多個資料列，以支援資料表值參數中的資料流行為。 例如，使用者在磁碟 (而不是記憶體) 上可能有資料表值參數資料列集資料，而且可能會在 OLE DB Driver for SQL Server 需要時，從磁碟實作功能來讀取資料。  
  
 取用者將透過使用資料表值參數資料列集物件上的 IAccessor::CreateAccessor，將其資料格式傳送到 OLE DB Driver for SQL Server。 從取用者緩衝區讀取資料時，提供者會確認透過至少一個存取子控制代碼可以取得所有可寫入，而且非預設的資料行，並使用對應的控制代碼來讀取資料行資料。 為避免模稜兩可的情況，在資料表值參數資料列集資料行和繫結之間應該有一對一的對應。 相同資料行的重複繫結將會導致錯誤。 同時，每個存取子依序都應該有 DBBindings 的 *iOrdinal* 成員。 IRowset::GetData 的呼叫將會與每個資料列的存取子數目一樣多，而且呼叫的順序將會以 *iOrdinal* 值的順序為基礎 (從低到高)。  
  
 提供者應該實作透過資料表值參數資料列集物件所公開的大部分介面。 取用者將會以最少的介面 (IRowset) 實作資料列集物件。 由於未公開彙總的緣故，剩餘的強制資料列集物件介面將會透過資料表值參數資料列集物件實作。  
  
 對於其他任何資料列集物件 (例如，針對任何 OLE DB 提供者取得的資料列集物件)，取用者提供的資料列集必須依照 OLE DB 規格所指定的方式，實作所有強制資料列集物件介面。  
  
 執行時，OLE DB Driver for SQL Server 將會回呼到資料列集物件來擷取資料列並讀取資料行資料。  
  
## <a name="see-also"></a>另請參閱  
 [資料表值參數 &#40;OLE DB&#41;](../../oledb/ole-db-table-valued-parameters/table-valued-parameters-ole-db.md)   
 [使用資料表值參數 &#40;OLE DB&#41;](../../oledb/ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  
