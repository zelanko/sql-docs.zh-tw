---
description: Open 方法 (ADO Stream)
title: " (ADO Stream) 的 Open 方法 |Microsoft Docs"
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::raw_Open
- _Stream::Open
helpviewer_keywords:
- Open method [ADO]
ms.assetid: d26f48fb-904e-4932-a245-3b4332ca1600
author: rothja
ms.author: jroth
ms.openlocfilehash: 333d20ee58123e9f1120e22d1770bd2a74ad97ae
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88773777"
---
# <a name="open-method-ado-stream"></a>Open 方法 (ADO Stream)
開啟 [資料流程](./stream-object-ado.md) 物件，以操作二進位或文字資料的資料流程。  
  
## <a name="syntax"></a>語法  
  
```  
  
Stream.Open Source, Mode , OpenOptions, UserName, Password  
```  
  
#### <a name="parameters"></a>參數  
 *Source*  
 選擇性。 **變數**值，指定**資料流程**的資料來源。 *來源* 可能包含指向已知樹狀結構中現有節點的絕對 URL 字串，例如電子郵件或檔案系統。 您應使用 url 關鍵字來指定 url， ( "url =*配置*：//*伺服器* / *資料夾*" ) 。 或者， *來源* 可能包含已經開啟之 [記錄](./record-object-ado.md) 物件的參考，該物件會開啟與 **記錄**相關聯的預設資料流程。 如果未指定 *來源* ，則會具現化並開啟 **資料流程** ，且預設不會與基礎來源建立關聯。 如需 URL 配置及其相關提供者的詳細資訊，請參閱 [絕對和相對 url](../../guide/data/absolute-and-relative-urls.md)。  
  
 *模式*  
 選擇性。 [ConnectModeEnum](./connectmodeenum.md)值，指定結果**資料流程**的存取模式 (例如，讀取/寫入或唯讀) 。 預設值為 **adModeUnknown**。 如需存取模式的詳細資訊，請參閱 [Mode](./mode-property-ado.md) 屬性。 如果未指定 *模式* ，則會由來源物件繼承。 例如，如果來源 **記錄** 是在唯讀模式中開啟，則 **資料流程** 預設也會以唯讀模式開啟。  
  
 *OpenOptions*  
 選擇性。 [StreamOpenOptionsEnum](./streamopenoptionsenum.md)值。 預設值為 **adOpenStreamUnspecified**。  
  
 *UserName*  
 選擇性。 包含使用者識別的 **字串** 值，如果需要的話，會存取 **資料流程** 物件。  
  
 *密碼*  
 選擇性。 包含密碼的 **字串** 值，如果需要的話，會存取 **資料流程** 物件。  
  
## <a name="remarks"></a>備註  
 當 **記錄** 物件當做來源參數傳入時，不會使用 *UserID* 和 *Password* 參數，因為已有 **記錄** 物件的存取權。 同樣地，**記錄**物件的[模式](./mode-property-ado.md)會傳送至**資料流程**物件。 未指定 *來源* 時，開啟的 **資料流程** 不包含任何資料，且 [大小](./size-property-ado-stream.md) 為零 (0) 。 若要避免在**資料流程**關閉時遺失任何寫入此**資料流程**的資料，請使用[CopyTo](./copyto-method-ado.md)或[SaveToFile](./savetofile-method.md)方法儲存**資料流程**，或將它儲存到另一個記憶體位置。  
  
 **AdOpenStreamFromRecord**的*OpenOptions*值會將*Source*參數的內容識別為已經開啟的**記錄**物件。 預設行為是將 *來源* 視為直接指向樹狀結構中節點（例如檔案）的 URL。 會開啟與該節點相關聯的預設資料流程。  
  
 當 **資料流程** 未開啟時，可以讀取 **資料流程**的所有唯讀屬性。 如果以非同步方式開啟**資料流程**，則在**開啟**作業完成之前，會封鎖所有後續作業 (檢查[狀態](./state-property-ado.md)和其他唯讀屬性) 。  
  
 除了先前所討論的選項之外，藉由不指定 *來源*，您可以在記憶體中建立 **資料流程** 物件的實例，而不將它與基礎來源產生關聯。 您可以使用[寫入](./write-method.md)或[WriteText](./writetext-method.md)將二進位或文字資料寫入**資料流程**，或使用[LoadFromFile](./loadfromfile-method-ado.md)從檔案載入資料，以動態方式將資料新增至資料流程。  
  
## <a name="applies-to"></a>套用至  
 [Stream 物件 (ADO)](./stream-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [ (ADO Connection) 的 Open 方法 ](./open-method-ado-connection.md)   
 [ (ADO 記錄) 的 Open 方法 ](./open-method-ado-record.md)   
 [ (ADO 記錄集的 Open 方法) ](./open-method-ado-recordset.md)   
 [OpenSchema 方法](./openschema-method.md)   
 [SaveToFile 方法](./savetofile-method.md)