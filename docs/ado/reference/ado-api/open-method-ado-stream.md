---
title: Open 方法（ADO Stream） |Microsoft Docs
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
ms.openlocfilehash: d59fcbbd7edea7ac87b2c080d27160cb98732759
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82762156"
---
# <a name="open-method-ado-stream"></a>Open 方法 (ADO Stream)
開啟[資料流程](../../../ado/reference/ado-api/stream-object-ado.md)物件來操作二進位或文字資料的資料流程。  
  
## <a name="syntax"></a>語法  
  
```  
  
Stream.Open Source, Mode , OpenOptions, UserName, Password  
```  
  
#### <a name="parameters"></a>參數  
 *來源*  
 選擇性。 **變數**值，指定**資料流程**的資料來源。 *來源*可能包含指向已知樹狀結構中現有節點（例如電子郵件或檔案系統）的絕對 URL 字串。 您應該使用 url 關鍵字（"url =*配置*：//*伺服器* / *資料夾*"）來指定 url。 或者， *Source*可能包含已開啟[記錄](../../../ado/reference/ado-api/record-object-ado.md)物件的參考，這會開啟與**記錄**相關聯的預設資料流程。 如果未指定*Source* ，則會具現化並開啟**資料流程**，預設與沒有基礎來源相關聯。 如需 URL 配置及其相關聯提供者的詳細資訊，請參閱[絕對和相對 url](../../../ado/guide/data/absolute-and-relative-urls.md)。  
  
 *Mode*  
 選擇性。 [ConnectModeEnum](../../../ado/reference/ado-api/connectmodeenum.md)值，指定結果**資料流程**的存取模式（例如，讀取/寫入或唯讀）。 預設值為**adModeUnknown**。 如需存取模式的詳細資訊，請參閱[Mode](../../../ado/reference/ado-api/mode-property-ado.md)屬性。 如果未指定*模式*，則會由來源物件繼承。 例如，如果在唯讀模式中開啟來源**記錄**，則根據預設，**資料流程**也會以唯讀模式開啟。  
  
 *OpenOptions*  
 選擇性。 [StreamOpenOptionsEnum](../../../ado/reference/ado-api/streamopenoptionsenum.md)值。 預設值為**adOpenStreamUnspecified**。  
  
 *UserName*  
 選擇性。 包含使用者識別的**字串**值，如有需要，會存取**資料流程**物件。  
  
 *密碼*  
 選擇性。 包含密碼的**字串**值，如果需要的話，會存取**資料流程**物件。  
  
## <a name="remarks"></a>備註  
 當**記錄**物件當做來源參數傳入時，不會使用*UserID*和*Password*參數，因為已有**記錄**物件的存取權。 同樣地，**記錄**物件的[模式](../../../ado/reference/ado-api/mode-property-ado.md)會傳送至**資料流程**物件。 若未指定*Source* ，則開啟的**資料流程**不會包含任何資料，且[大小](../../../ado/reference/ado-api/size-property-ado-stream.md)為零（0）。 若要避免在**資料流程**關閉時遺失寫入此**資料流程**的任何資料，請使用[CopyTo](../../../ado/reference/ado-api/copyto-method-ado.md)或[SaveToFile](../../../ado/reference/ado-api/savetofile-method.md)方法儲存**資料流程**，或將它儲存至另一個記憶體位置。  
  
 **AdOpenStreamFromRecord**的*OpenOptions*值會將*Source*參數的內容識別為已開啟的**記錄**物件。 預設行為是將*Source*視為直接指向樹狀結構中之節點的 URL，例如檔案。 隨即開啟與該節點相關聯的預設資料流程。  
  
 當**資料流程**未開啟時，您可以讀取**資料流程**的所有唯讀屬性。 如果**資料流程**以非同步方式開啟，所有後續的作業（除了檢查[狀態](../../../ado/reference/ado-api/state-property-ado.md)和其他唯讀屬性以外）都會遭到封鎖，直到**開啟**作業完成為止。  
  
 除了稍早所討論的選項之外，藉由不指定*Source*，您可以在記憶體中建立**資料流程**物件的實例，而不需要將它與基礎來源產生關聯。 您可以使用[Write](../../../ado/reference/ado-api/write-method.md)或[WriteText](../../../ado/reference/ado-api/writetext-method.md)將二進位或文字資料**寫入資料流程，** 或從具有[LoadFromFile](../../../ado/reference/ado-api/loadfromfile-method-ado.md)的檔案載入資料，以動態方式將資料加入資料流程。  
  
## <a name="applies-to"></a>套用至  
 [Stream 物件 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [Open 方法（ADO Connection）](../../../ado/reference/ado-api/open-method-ado-connection.md)   
 [Open 方法（ADO Record）](../../../ado/reference/ado-api/open-method-ado-record.md)   
 [Open 方法（ADO Recordset）](../../../ado/reference/ado-api/open-method-ado-recordset.md)   
 [OpenSchema 方法](../../../ado/reference/ado-api/openschema-method.md)   
 [SaveToFile 方法](../../../ado/reference/ado-api/savetofile-method.md)
