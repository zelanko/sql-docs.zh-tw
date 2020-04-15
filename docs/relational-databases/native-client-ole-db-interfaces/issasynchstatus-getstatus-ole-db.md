---
title: ISSAsynchStatus::GetStatus (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apiname:
- ISSAsynchStatus::GetStatus (OLE DB)
apitype: COM
helpviewer_keywords:
- GetStatus method
ms.assetid: 354b6ee4-b5a1-48f6-9403-da3bdc911067
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 90ddf4e4617e1182e50979f051fa6ee2657166ba
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306706"
---
# <a name="issasynchstatusgetstatus-ole-db"></a>ISSAsynchStatus::GetStatus (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  傳回以非同步方式執行作業的狀態。  
  
## <a name="syntax"></a>語法  
  
```  
  
HRESULT GetStatus(  
        HCHAPTER hChapter,  
        DBASYNCHOP eOperation,  
        DBCOUNTITEM *pulProgress,  
        DBCOUNTITEM *pulProgressMax,  
        DBASYNCHPHASE *peAsynchPhase,  
        LPOLESTR *ppwszStatusText);  
```  
  
## <a name="arguments"></a>引數  
 *hChapter*[in]  
 章節控制代碼。 如果輪詢的物件不是資料列集物件，或者作業不適用於章節，則這應該設定為 DB_NULL_HCHAPTER (會由提供者忽略)。  
  
 *eOperation*[in]  
 正在要求其非同步狀態的作業。 這應該為下列值：  
  
 DBASYNCHOP_OPEN：取用者會要求有關非同步開啟或資料列集擴展的資訊，或有關資料來源物件的非同步初始化的資訊。 如果提供者是 OLE DB 2.5 相容且支援 URL 直接繫結的提供者，則取用者會要求有關非同步初始化或資料來源、資料列集、資料列或資料流物件擴展的資訊。  
  
 *pulProgress*[out]  
 記憶體的指標，會從中傳回相對於 *pulProgressMax* 參數所指出之預期最大值的非同步作業的目前進度。 如需 *pulProgress* 之意義的詳細資訊，請參閱 *peAsynchPhase* 的描述。  
  
 如果 *pulProgress* 是 Null 指標，則不會傳回任何進度。  
  
 *pulProgressMax*[out]  
 記憶體的指標，會從中傳回 *pulProgress* 參數的預期最大值。 此值可能會在此方法的呼叫之間變更。 如需 *pulProgressMax* 之意義的詳細資訊，請參閱 *peAsynchPhase* 的描述。  
  
 如果 *pulProgressMax* 是 Null 指標，則不會傳回預期的最大值。  
  
 *peAsynchPhase*[out]  
 記憶體的指標，會從中傳回有關非同步作業的其他資訊。 有效值包括：  
  
 DBASYNCHPHASE_INITIALIZATION：物件正處於初始化階段。 *pulProgress* 和 *pulProgressMax* 引數指出預估的完成率。 物件尚未完全具體化。 呼叫任何其他介面的嘗試可能失敗，而物件可能無法使用完整的介面集。 如果非同步作業是針對更新、刪除或插入資料列的命令呼叫 **ICommand::Execute** 的結果，而且如果 *cParamSets* 大於 1，則 *pulProgress* 和 *pulProgressMax* 可能代表單一參數集或參數集完整陣列的進度。  
  
 DBASYNCHPHASE_POPULATION：物件正處於擴展階段。 雖然資料列集會完全初始化，而且物件可以使用完整的介面範圍，則可能有其他的資料列尚未擴展到資料列集中。 *pulProgress* 和 *pulProgressMax* 雖然可以根據擴展的資料列數目而定，但通常是根據擴展資料列集所需的時間或努力來決定。 因此呼叫者應該使用此項資訊 (而非最後的資料列計數) 做為處理序所可能花費時間的大略估計。 此階段只會在資料列集擴展期間傳回，而不會在初始化資料來源物件時傳回，或由更新、刪除或插入資料列的命令執行傳回。  
  
 DBASYNCHPHASE_COMPLETE：物件的所有非同步處理已完成。 **ISSAsynch狀態:獲取狀態**返回指示操作結果的 HRESULT。 一般而言，這會是在同步呼叫作業時所傳回的 HRESULT。 如果非同步作業是針對更新、刪除或插入資料列的命令呼叫 **ICommand::Execute** 的結果，則 *pulProgress* 和 *pulProgressMax* 等於受到該命令影響的資料列總數。 如果 *cParamSets* 大於 1，這是受到執行所指定的所有參數集影響的資料列總數。 如果 *peAsynchPhase* 是 Null 指標，則不會傳回狀態碼。  
  
 DBASYNCHPHASE_CANCELED：物件的非同步處理已中止。 **ISSSynch 狀態:獲取狀態**返回DB_E_CANCELED。 如果非同步作業是針對更新、刪除或插入資料列的命令呼叫 **ICommand::Execute** 的結果，則 *pulProgress* 等於所有參數集在該命令取消前受其影響的資料列總數。  
  
 *ppwszStatusText*[in/out]  
 記憶體的指標，這個記憶體包含有關作業的其他資訊。 提供者可以使用此值來區別作業的不同元素，例如，正在存取的不同資源。 這個字串會根據資料來源物件的 DBPROP_INIT_LCID 屬性而當地語系化。  
  
 如果輸入上的 *ppwszStatusText* 非 Null，則提供者會傳回與 *ppwszStatusText* 所識別的特定元素相關聯的狀態。 如果 *ppwszStatusText* 並不代表 *eOperation* 的元素，則提供者會傳回 S_OK，且 *pulProgress* 和 *pulProgressMax* 會設定為相同的值。 如果提供者並未根據文字識別碼來區分元素，則它會將 *ppwszStatusText* 設定為 NULL，並傳回整個作業的相關資訊；否則，如果輸入上的 *ppwszStatusText* 非 Null，提供者會保留 *ppwszStatusText* 不變。  
  
 如果*ppwszStatusText*在輸入時為空,則提供程式將*ppwszStatusText*設定為指示有關操作的詳細資訊的值,或者將「無此類資訊可用」或**ISSAsynchStatus:getStatus**傳回錯誤時設定為 NULL。 當輸入上的 *ppwszStatusText* 是 Null 時，提供者會為狀態字串配置記憶體，並將位址傳回給這個記憶體。 當取用者不再需要字串時，可以使用 **IMalloc::Free** 釋出這個記憶體。  
  
 如果輸入上的 *ppwszStatusText* 是 NULL，則不會傳回任何狀態字串，而且提供者會傳回有關作業之任何元素或一般作業的資訊。  
  
## <a name="return-code-values"></a>傳回碼值  
 S_OK  
 此方法已成功傳回。  
  
-   如果 *peAsynchPhase* 等於 DBASYNCHPHASE_INITIALIZATION，則物件尚未完全初始化；嘗試呼叫任何其他的介面可能會失敗，而且物件上可能無法使用完整的介面集。  
  
-   如果 *peAsynchPhase* 等於 DBASYNCHPHASE_POPULATION，資料列集會完全初始化，而且物件上可以使用完整的介面範圍；不過可能有其他尚未擴展到資料列集中的資料列。  
  
-   如果 *peAsynchPhase* 等於 DBASYNCHPHASE_COMPLETE，物件的所有非同步處理都已完成。 該物件會完全初始化並擴展。  
  
 DB_E_CANCELED  
 已在資料列集擴展期間取消非同步處理。 擴展停止，但資料列集對於已擴展的資料列仍保持有效。  
  
 已在資料來源物件初始化期間取消非同步處理。 資料來源物件處於未初始化的狀態。  
  
 E_INVALIDARG  
 *hChapter* 參數錯誤。  
  
 E_UNEXPECTED  
 **ISSAsynchStatus:getStatus**在資料源物件上調用,**並且 IDB 初始化::** 尚未在數據源物件上調用初始化。  
  
 **ISSAsynchStatus:getStatus**在行集 **「I事務:提交**」或 **「I事務::已調用中止**」,並且對象處於殭屍狀態。  
  
 **ISSAsynchStatus:GetStatus**被調用在初始化階段異步取消的行集上。 此資料列集處於廢止狀態。  
  
 E_FAIL  
 發生了提供者特定的錯誤。  
  
## <a name="remarks"></a>備註  
 **ISSAsynchStatus::GetStatus** 方法的行為與 **IDBAsynchStatus::GetStatus** 方法完全相同，不同的是如果中止資料來源物件的初始化，便會傳回 E_UNEXPECTED，而不是 DB_E_CANCELED (雖然 [ISSAsynchStatus::WaitForAsynchCompletion](../../relational-databases/native-client-ole-db-interfaces/issasynchstatus-waitforasynchcompletion-ole-db.md) 會傳回 DB_E_CANCELED)。 這是因為資料來源物件在中止後不會保留在一般的廢止狀態，如此可以讓系統嘗試進一步的初始化作業。  
  
 如果資料列集是非同步地初始化或擴展，則必須支援此方法。  
  
 除了列出的傳回值外，**ISSAsynchStatus::GetStatus** 可以傳回任何的 HRESULT，此值會由初始化非同步作業的方法所傳回，指出作業是成功還是失敗。  
  
 有些非同步作業可能不會傳回 "finished" 和 "not finished" 以外的任何狀態。 這些作業應該將 *pulProgressMax* 設定為 1 的值，指出其預估值全有或全無的資料粒度，所以其回應會是 0/1 或 1/1。  
  
 提供者可能會在連續的呼叫中變更 *pulProgressMax*，而且甚至會傳回比先前更小的比率 (如果這反映出更為精確的工作完成度預估值)。  
  
 提供者不必保證更高的精確度，但在可以提供合理的完成度預估值時，建議提供者加以提供。 此類努力可以提升使用者介面的品質，因為此函數的主要用途很可能是為使用者提供進度回應。 使用者的滿意度會隨著不可見的長時間執行工作的回應品質而增加。  
  
 在初始化的資料來源物件或擴展的資料列集上呼叫 **ISSAsynchStatus::GetStatus**，或者為 *eOperation* 傳遞 DBASYNCHOP_OPEN 以外的值，會傳回 S_OK，且 *pulProgress* 和 *pulProgressMax* 都設定為相同值。 如果在執行更新、刪除或插入行的命令時創建的物件上調用**ISSAsynchStatus:GetStatus,** 則 pulProgress 和*pulProgressMax*都表示受*pulProgressMax*該命令影響的行總數。  
  
## <a name="see-also"></a>另請參閱  
 [執行非同步作業](../../relational-databases/native-client/features/performing-asynchronous-operations.md)   
 [ISSAsynchStatus &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/issasynchstatus-ole-db.md)  
  
  
