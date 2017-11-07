---
title: "IMDEmbeddedData 介面 |Microsoft 文件"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
ms.assetid: 9dba8c68-4bef-4c2b-815c-c286f1a1939b
caps.latest.revision: 9
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 0fae25125663ceca4a0cc2c7ddf94f72841ace2a
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="imdembeddeddata-interface"></a>IMDEmbeddedData 介面

[!INCLUDE[ssas-appliesto-sqlas-all](../../includes/ssas-appliesto-sqlas-all.md)]

  IMDEmbeddedData 介面是用來管理內嵌的公用介面[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]資料庫或表格式模型資料庫。 此介面繼承自**IPersistStream**介面。 允許下列作業：  
  
-   取得容器文件中之內嵌資料流的識別碼。  
  
-   取得包含文件 URL。  
  
-   設定旗標，指出內嵌應用程式是否在主控環境中。  
  
-   設定內嵌應用程式所使用之暫存檔的路徑。  
  
-   取消目前的內嵌作業。  
  
-   取得要用來內嵌物件之資料流的估計大小 (以位元組為單位)。 繼承自**IPersistStream**。  
  
-   確認內嵌資料庫自上次儲存後是否已經變更。 繼承自**IPersistStream**。  
  
-   將內嵌資料庫載入至本機或同處理序引擎。 繼承自**IPersistStream**。  
  
-   將本機或同處理序資料庫儲存至容器文件中的內嵌資料流。 繼承自**IPersistStream**。  
  
## <a name="reference"></a>參考  
 下列參考文件**IMDEmbeddedData**介面中，呈現**msmd.h**標頭檔。  
  
### <a name="source-file-pxoembeddeddataidl"></a>來源檔案：PXOEmbeddedData.idl  
  
```  
[  
  local,                            
  object,                           
  uuid(6B6691CF-5453-41c2-ADD9-4F320B7FD421),                       
  pointer_default(unique)           
]  
interface IMDEmbeddedData : IPersistStream  
{  
 [id(1), helpstring("Set flag indicating if the application is in a hosted environment")]   
 HRESULT SetHosted(  
  [in] BOOL in_fIsHosted);  
  
 [id(2), helpstring("Set the URL for the document containing the embedded stream")]   
 HRESULT SetContainerURL(  
  [in] BSTR in_bstrURL);  
  
 [id(3), helpstring("Get identifier used to look up embedded stream in container document")]   
 HRESULT GetStreamIdentifier(  
  [out, retval] BSTR* out_pbstrStreamId);  
  
 [id(4), helpstring("Set the path used by the embedding application for temporary files")]   
 HRESULT SetTempDirPath(  
  [in]  BSTR in_bstrPath);  
  
 [id(5), helpstring("Cancel the current operation")]   
 HRESULT Cancel();  
};  
```  
  
### <a name="imdembeddeddatagetstreamidentifier"></a>IMDEmbeddedData::GetStreamIdentifier  
  
```  
HRESULT GetStreamIdentifier (  
    [out, retval] BSTR * out_pbstrStreamId  
    )  
```  
  
#### <a name="description"></a>Description  
 取得主應用程式用來識別容器文件中之內嵌資料流的識別碼。  
  
#### <a name="parameters"></a>參數  
 *out_pbstrStreamId*  
 指定資料流識別碼的位置。  
  
#### <a name="return-value"></a>傳回值  
 **S_OK**  
 成功傳回資料流識別碼。  
  
 **S_FALSE**  
 沒有資料流識別碼。  
  
 **E_FAIL**  
 存取資料流識別碼時發生錯誤。  
  
#### <a name="remarks"></a>備註  
 若要確認目前連接是否包含內嵌資料庫，使用者應該從 OLE DB 連接屬性檢查 DBPROP_MSMD_EMBEDDED_DATA 屬性的值。  
  
 DBPROP_MSMD_EMBEDDED_DATA 的可能值如下：  
  
|名稱|值|定義|  
|----------|-----------|----------------|  
|DBPROPVAL_EMBED_NONE|0x00|沒有可用的內嵌資料庫|  
|DBPROPVAL_EMBED_EMBEDDED|0x01|目前應用程式包含內嵌資料庫|  
|DBPROPVAL_EMBED_LINKED|0x02|內嵌資料庫裝載於遠端應用程式 (即 SharePoint Server)|  
  
#### <a name="source"></a>Source  
  
```  
[id(1), helpstring("Get identifier used to look up embedded stream in container document")]   
 HRESULT GetStreamIdentifier(  
  [out, retval] BSTR* out_pbstrStreamId);  
```  
  
### <a name="imdembeddeddatasetcontainerurl"></a>IMDEmbeddedData::SetContainerURL  
  
```  
HRESULT SetContainerURL (  
    [in] BSTR in_bstrURL  
    )  
```  
  
#### <a name="description"></a>Description  
 設定包含內嵌資料流之檔案的 URL。  
  
#### <a name="parameters"></a>參數  
 *in_bstrURL*  
 指定包含文件 URL。  
  
#### <a name="return-value"></a>傳回值  
 **S_OK**  
 成功設定容器 URL。  
  
 **E_FAIL**  
 設定容器 URL 時發生錯誤。  
  
#### <a name="source"></a>Source  
  
```  
[id(2), helpstring("Set the URL for the document containing the embedded stream")]   
 HRESULT SetContainerURL(  
  [in] BSTR in_bstrURL);  
```  
  
### <a name="imdembeddeddatasethosted"></a>IMDEmbeddedData::SetHosted  
  
```  
HRESULT SetHosted (  
    [in] BOOL in_fIsHosted  
    )  
```  
  
#### <a name="description"></a>Description  
 設定旗標，指出內嵌應用程式是否在主控環境中。  
  
#### <a name="parameters"></a>參數  
 *in_ftHosted*  
 如果呼叫端裝載於服務應用程式 (如 IIS)，則為 TRUE。  
  
#### <a name="return-value"></a>傳回值  
 **S_OK**  
 成功設定旗標。  
  
 **E_FAIL**  
 設定旗標時發生錯誤。  
  
#### <a name="source"></a>Source  
  
```  
[id(5), helpstring("Set flag indicating if the application is in a hosted environment")]   
 HRESULT SetHosted(  
  [in]  BOOL in_fIsHosted);  
```  
  
### <a name="imdembeddeddatasettempdirpath"></a>IMDEmbeddedData::SetTempDirPath  
  
```  
HRESULT SetTempDirPath (  
    [in] BSTR in_bstrPath  
    )  
```  
  
#### <a name="description"></a>Description  
 設定內嵌應用程式所使用之暫存檔的路徑。  
  
#### <a name="parameters"></a>參數  
 *in_bstrPath*  
 主應用程式用於暫存檔的路徑。  
  
#### <a name="return-value"></a>傳回值  
 **S_OK**  
 成功設定暫存檔目錄。  
  
 **E_FAIL**  
 設定路徑時發生錯誤。  
  
#### <a name="source"></a>Source  
  
```  
[id(4), helpstring("Set the path used by the host application for temporary files")]   
 HRESULT SetTempDirPath(  
  [in]  BSTR in_bstrPath);  
```  
  
### <a name="imdembeddeddatacancel"></a>IMDEmbeddedData::Cancel  
  
```  
HRESULT Cancel ( void )  
```  
  
#### <a name="description"></a>Description  
 取消目前的內嵌資料庫作業。  
  
#### <a name="parameters"></a>參數  
 無。  
  
#### <a name="return-value"></a>傳回值  
 **S_OK**  
 成功取消作業。  
  
 **DB_E_CANTCANCEL**  
 目前沒有進行中的可取消作業。  
  
 **E_FAIL**  
 取消內嵌作業時發生錯誤。  
  
#### <a name="source"></a>Source  
  
```  
[id(5), helpstring("Cancel the current operation")]   
 HRESULT Cancel();  
```  
  
### <a name="imdembeddeddatagetsizemax-ipersiststreamgetsizemax"></a>IMDEmbeddedData::GetSizeMax (IPersistStream::GetSizeMax)  
  
```  
HRESULT GetSizeMax (  
    [out] ULARGE_INTEGER * out_pcbSize  
    )  
```  
  
#### <a name="description"></a>Description  
 取得要用來儲存內嵌物件之資料流的估計大小 (以位元組為單位)。 繼承自**IPersistStream**。  
  
#### <a name="parameters"></a>參數  
 *in_bstrPath*  
 內嵌資料庫影像的估計大小 (以位元組為單位)。  
  
#### <a name="return-value"></a>傳回值  
 **S_OK**  
 成功取得大小。  
  
 **E_FAIL**  
 取得大小時發生錯誤。  
  
### <a name="imdembeddeddataisdirty-ipersiststreamisdirty"></a>IMDEmbeddedData::IsDirty (IPersistStream::IsDirty)  
  
```  
HRESULT IsDirty ( void )  
```  
  
#### <a name="description"></a>Description  
 確認內嵌資料庫自上次儲存後是否已經變更。 繼承自**IPersistStream**。  
  
#### <a name="parameters"></a>參數  
 無  
  
#### <a name="return-values"></a>傳回值  
 **S_OK**  
 資料庫自上次儲存後已經變更。  
  
 **S_FALSE**  
 資料庫自上次儲存後尚未變更。  
  
 **E_FAIL**  
 取得資料庫狀態時發生錯誤。  
  
### <a name="imdembeddeddataload-ipersiststreamload"></a>IMDEmbeddedData::Load (IPersistStream::Load)  
  
```  
HRESULT Load (   
    [in] IStream * in_pStm   
    )  
```  
  
#### <a name="description"></a>Description  
 將內嵌資料庫載入至本機或同處理序引擎。 繼承自**IPersistStream**。  
  
#### <a name="parameters"></a>參數  
 *in_pStm*  
 載入內嵌資料庫之來源資料流介面的指標。  
  
#### <a name="return-values"></a>傳回值  
 **S_OK**  
 成功載入資料庫。  
  
 **E_OUTOFMEMORY**  
 記憶體不足，無法載入資料庫。  
  
 **E_FAIL**  
 載入不同的資料庫時發生錯誤**E_OUTOFMEMORY**。  
  
### <a name="imdembeddeddatasave-ipersiststreamsave"></a>IMDEmbeddedData::Save (IPersistStream::Save)  
  
```  
HRESULT Save (   
    [in] IStream * in_pStm,  
    [in] BOOL in_fClearDirty  
    )  
```  
  
#### <a name="description"></a>Description  
 將本機或同處理序資料庫儲存至容器文件中的內嵌資料流。 繼承自**IPersistStream**。  
  
#### <a name="parameters"></a>參數  
 *in_pStm*  
 要用來儲存內嵌資料庫之資料流介面的指標。  
  
 *in_fClearDirty*  
 旗標，指出是否應該在這項作業後清除記錄變更旗標。  
  
#### <a name="return-values"></a>傳回值  
 **S_OK**  
 成功儲存資料庫。  
  
 **STG_E_CANTSAVE**  
 將資料庫，不同於儲存時發生錯誤**STG_E_MEDIUMFULL**。  
  
 **STG_E_MEDIUMFULL**  
 因為儲存裝置上沒有剩餘空間，無法儲存資料庫。  
  
  

