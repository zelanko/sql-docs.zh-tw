---
title: 'Issasynchstatus:: Getstatus (OLE DB) |Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- ISSAsynchStatus::GetStatus (OLE DB)
apitype: COM
helpviewer_keywords:
- GetStatus method
ms.assetid: 354b6ee4-b5a1-48f6-9403-da3bdc911067
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: d39998e41fd26bb2928290f62dd08fc54a0f567a
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/03/2018
ms.locfileid: "37407860"
---
# <a name="issasynchstatusgetstatus-ole-db"></a>ISSAsynchStatus::GetStatus (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

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
 要在其中傳回的相對預期的最大值的非同步作業的目前進度的記憶體指標示*pulProgressMax*參數。 如需有關的意義*pulProgress*，請參閱的說明*peAsynchPhase*。  
  
 如果*pulProgress*為 null 指標，會傳回任何進度。  
  
 *pulProgressMax*[out]  
 要在其中傳回的預期最大值的記憶體指標*pulProgress*參數。 此值可能會在此方法的呼叫之間變更。 如需有關的意義*pulProgressMax*，請參閱的說明*peAsynchPhase*。  
  
 如果*pulProgressMax*為 null 指標，會傳回任何預期的最大值。  
  
 *peAsynchPhase*[out]  
 記憶體的指標，會從中傳回有關非同步作業的其他資訊。 有效值包括：  
  
 DBASYNCHPHASE_INITIALIZATION：物件正處於初始化階段。 引數*pulProgress*並*pulProgressMax*指出預估的完成率。 物件尚未完全具體化。 呼叫任何其他介面的嘗試可能失敗，而物件可能無法使用完整的介面集。 如果非同步作業的呼叫結果**icommand:: Execute**的更新時，命令會刪除，或插入資料列，而且如果*cParamSets*大於 1， *pulProgress*並*pulProgressMax*可能表示針對單一參數集或參數集完整陣列的進度。  
  
 DBASYNCHPHASE_POPULATION：物件正處於擴展階段。 雖然資料列集會完全初始化，而且物件可以使用完整的介面範圍，則可能有其他的資料列尚未擴展到資料列集中。 雖然*pulProgress*並*pulProgressMax*可能隨著填入的資料列數目，它們通常根據擴展資料列集所需的投入時間的時間。 因此呼叫者應該使用此項資訊 (而非最後的資料列計數) 做為處理序所可能花費時間的大略估計。 此階段只會在資料列集擴展期間傳回，而不會在初始化資料來源物件時傳回，或由更新、刪除或插入資料列的命令執行傳回。  
  
 DBASYNCHPHASE_COMPLETE：物件的所有非同步處理已完成。 **Issasynchstatus:: Getstatus**傳回 HRESULT，指出作業的結果。 一般而言，這會是在同步呼叫作業時所傳回的 HRESULT。 如果非同步作業呼叫的結果**icommand:: Execute**之命令的更新、 刪除或插入資料列*pulProgress*並*pulProgressMax*是等於受到該命令的資料列總數。 如果*cParamSets*是大於 1，這是執行所指定的參數集合的所有受影響的資料列總數。 如果*peAsynchPhase*為 null 指標，會傳回任何狀態碼。  
  
 DBASYNCHPHASE_CANCELED：物件的非同步處理已中止。 **Issasynchstatus:: Getstatus**會傳回 DB_E_CANCELED。 如果非同步作業的呼叫結果**icommand:: Execute**之命令的更新、 刪除或插入資料列*pulProgress*等於所有參數集，資料列的總數受影響之前取消命令。  
  
 *ppwszStatusText*[in/out]  
 記憶體的指標，這個記憶體包含有關作業的其他資訊。 提供者可以使用此值來區別作業的不同元素，例如，正在存取的不同資源。 這個字串會根據資料來源物件的 DBPROP_INIT_LCID 屬性而當地語系化。  
  
 如果*ppwszStatusText*為非 null 輸入上，提供者會傳回與所識別的特定元素相關聯的狀態*ppwszStatusText*。 如果*ppwszStatusText*不會指出項目的*eOperation*，提供者會傳回 S_OK，且*pulProgress*並*pulProgressMax*設為相同的值。 如果提供者不會區分文字識別碼為基礎的項目，它會設定*ppwszStatusText* NULL，並傳回整個; 作業的相關資訊，否則為如果*ppwszStatusText*為非 null 輸入上，提供者會保留*ppwszStatusText*不變。  
  
 如果*ppwszStatusText*為 null 輸入時，提供者集*ppwszStatusText*值，指出作業，或為 NULL 的詳細資訊，如果不未提供任何這類資訊或要**Issasynchstatus:: Getstatus**會傳回錯誤。 當*ppwszStatusText*是 null 輸入時，提供者會為狀態字串配置記憶體，並將位址傳回給這個記憶體。 取用者釋放這個記憶體**imalloc:: Free**它不再需要字串時。  
  
 如果*ppwszStatusText*輸入是 NULL，會傳回任何狀態字串和提供者會傳回一般作業的任何項目或是作業的相關資訊。  
  
## <a name="return-code-values"></a>傳回碼值  
 S_OK  
 此方法已成功傳回。  
  
-   如果*peAsynchPhase*是等於 DBASYNCHPHASE_INITIALIZATION，該物件尚未完全初始化; 嘗試呼叫任何其他介面可能會失敗，並可能無法在物件上進行完整的介面集。  
  
-   如果*peAsynchPhase*是等於 DBASYNCHPHASE_POPULATION，資料列集會完全初始化，而且完整的介面範圍可用的物件上; 不過，可能會有額外的資料列尚未擴展到資料列集。  
  
-   如果*peAsynchPhase*是等於 DBASYNCHPHASE_COMPLETE，物件的所有非同步處理已完成。 該物件會完全初始化並擴展。  
  
 DB_E_CANCELED  
 已在資料列集擴展期間取消非同步處理。 擴展停止，但資料列集對於已擴展的資料列仍保持有效。  
  
 已在資料來源物件初始化期間取消非同步處理。 資料來源物件處於未初始化的狀態。  
  
 E_INVALIDARG  
 *HChapter*參數不正確。  
  
 E_UNEXPECTED  
 **Issasynchstatus:: Getstatus**資料來源物件上呼叫並**idbinitialize:: Initialize**尚未呼叫資料來源物件。  
  
 **Issasynchstatus:: Getstatus**資料列集上呼叫**itransaction:: Commit**或是**itransaction:: Abort**呼叫，則會和物件處於廢止狀態。  
  
 **Issasynchstatus:: Getstatus**在其初始化階段已非同步地取消資料列集上呼叫。 此資料列集處於廢止狀態。  
  
 E_FAIL  
 發生了提供者特定的錯誤。  
  
## <a name="remarks"></a>備註  
 **Issasynchstatus:: Getstatus**方法的行為就像**idbasynchstatus:: Getstatus**方法，但如果來源物件的資料初始化會中止，會傳回 E_UNEXPECTED 而不是比 DB_E_CANCELED (雖然[issasynchstatus:: Waitforasynchcompletion](../../relational-databases/native-client-ole-db-interfaces/issasynchstatus-waitforasynchcompletion-ole-db.md)會傳回 DB_E_CANCELED)。 這是因為資料來源物件在中止後不會保留在一般的廢止狀態，如此可以讓系統嘗試進一步的初始化作業。  
  
 如果資料列集是非同步地初始化或擴展，則必須支援此方法。  
  
 除了列出的傳回值**issasynchstatus:: Getstatus**可以傳回任何的 HRESULT，會起始非同步作業，方法傳回指出成功或失敗的作業。  
  
 有些非同步作業可能不會傳回 "finished" 和 "not finished" 以外的任何狀態。 它們應該設定*pulProgressMax* 1 的值，指出其預估，孤注一擲資料粒度讓其回應會是 0/1 / 1。  
  
 提供者可能會變更*pulProgressMax*在後續呼叫，甚至是傳回較小的比例比過去，如果這反映出工作的完成度預估值。  
  
 提供者不必保證更高的精確度，但在可以提供合理的完成度預估值時，建議提供者加以提供。 此類努力可以提升使用者介面的品質，因為此函數的主要用途很可能是為使用者提供進度回應。 使用者的滿意度會隨著不可見的長時間執行工作的回應品質而增加。  
  
 呼叫**issasynchstatus:: Getstatus**初始化的資料來源物件或擴展的資料列集，或傳遞的值上*eOperation* DBASYNCHOP_OPEN，不會傳回 S_OK，且*pulProgress*並*pulProgressMax*設為相同的值。 如果**issasynchstatus:: Getstatus**所建立的更新、 刪除或插入資料列的命令執行的物件上呼叫兩者*pulProgress*和*pulProgressMax*指出受到該命令的資料列總數。  
  
## <a name="see-also"></a>另請參閱  
 [執行非同步作業](../../relational-databases/native-client/features/performing-asynchronous-operations.md)   
 [ISSAsynchStatus &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/issasynchstatus-ole-db.md)  
  
  
