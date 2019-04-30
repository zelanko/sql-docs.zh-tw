---
title: Open 方法 (ADO Stream) |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0df165514a10bc667c8bd2cc6d2a8569faa79d11
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63239711"
---
# <a name="open-method-ado-stream"></a>Open 方法 (ADO Stream)
會開啟[Stream](../../../ado/reference/ado-api/stream-object-ado.md)來操作二進位或文字資料流的物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
Stream.Open Source, Mode , OpenOptions, UserName, Password  
```  
  
#### <a name="parameters"></a>參數  
 *Source*  
 選擇性。 A **Variant**值，指定的資料來源**Stream**。 *來源*可能包含指向已知的樹狀結構中，例如電子郵件或檔案系統中的現有節點的絕對 URL 字串。 應該使用 URL 關鍵字指定 URL ("URL =*配置*://*伺服器*/*資料夾*")。 或者，*來源*可能會包含已開啟的參考[記錄](../../../ado/reference/ado-api/record-object-ado.md)物件，這會開啟相關聯的預設資料流**記錄**。 如果*來源*未指定，則**Stream**是具現化及開啟，根據預設，沒有基礎來源相關聯。 如需有關 URL 配置和其相關聯的提供者的詳細資訊，請參閱[絕對和相對 Url](../../../ado/guide/data/absolute-and-relative-urls.md)。  
  
 *模式*  
 選擇性。 A [ConnectModeEnum](../../../ado/reference/ado-api/connectmodeenum.md)值，指定結果的存取模式**Stream** (比方說，讀取/寫入或唯寫)。 預設值是**adModeUnknown**。 請參閱[模式](../../../ado/reference/ado-api/mode-property-ado.md)存取模式的詳細資訊的屬性。 如果*模式*未指定，它會繼承的來源物件。 例如，如果來源**記錄**以唯讀模式開啟**Stream**將也會開啟唯讀模式的預設值。  
  
 *OpenOptions*  
 選擇性。 A [StreamOpenOptionsEnum](../../../ado/reference/ado-api/streamopenoptionsenum.md)值。 預設值是**adOpenStreamUnspecified**。  
  
 *UserName*  
 選擇性。 A**字串**值，其中包含使用者識別，必要時，存取**Stream**物件。  
  
 *密碼*  
 選擇性。 A**字串**值，其中包含的密碼，如果有需要存取**Stream**物件。  
  
## <a name="remarks"></a>備註  
 時**記錄**做為來源參數，傳入物件*UserID*並*密碼*參數不會因為存取**記錄**物件已可使用。 同樣地，[模式](../../../ado/reference/ado-api/mode-property-ado.md)的**記錄**物件傳送至**Stream**物件。 當*來源*未指定，則**Stream**開啟不包含任何資料，且具有[大小](../../../ado/reference/ado-api/size-property-ado-stream.md)為零 (0)。 若要避免遺失任何資料寫入這**Stream**時**Stream**會關閉，儲存**Stream**與[CopyTo](../../../ado/reference/ado-api/copyto-method-ado.md)或[SaveToFile](../../../ado/reference/ado-api/savetofile-method.md)方法，或將它儲存到另一個記憶體位置。  
  
 *OpenOptions*的值**adOpenStreamFromRecord**識別的內容*來源*參數必須已經開啟**記錄**物件。 預設行為是將*來源*成為樹狀結構中，例如檔案中的節點直接所指向的 URL。 開啟與該節點相關聯的預設資料流。  
  
 雖然**Stream**是未開啟，就可以讀取的所有唯讀屬性**Stream**。 如果**Stream**非同步開啟，所有後續的作業 (而不檢查[狀態](../../../ado/reference/ado-api/state-property-ado.md)和其他唯讀屬性) 會封鎖直到**開啟**已完成作業。  
  
 除了先前討論過，未指定的選項外*來源*，您可以建立的執行個體**Stream**而不需要與基礎來源相關聯的記憶體中的物件。 您可以動態地將資料加入至資料流寫入二進位或文字資料**Stream**具有[撰寫](../../../ado/reference/ado-api/write-method.md)或是[WriteText](../../../ado/reference/ado-api/writetext-method.md)，或從檔案載入資料[LoadFromFile](../../../ado/reference/ado-api/loadfromfile-method-ado.md)。  
  
## <a name="applies-to"></a>適用於  
 [Stream 物件 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [Open 方法 (ADO Connection)](../../../ado/reference/ado-api/open-method-ado-connection.md)   
 [Open 方法 （ADO 記錄）](../../../ado/reference/ado-api/open-method-ado-record.md)   
 [Open 方法 (ADO Recordset)](../../../ado/reference/ado-api/open-method-ado-recordset.md)   
 [OpenSchema 方法](../../../ado/reference/ado-api/openschema-method.md)   
 [SaveToFile 方法](../../../ado/reference/ado-api/savetofile-method.md)
