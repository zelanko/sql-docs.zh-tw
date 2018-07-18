---
title: Open 方法 （ADO 資料流） |Microsoft 文件
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::raw_Open
- _Stream::Open
helpviewer_keywords:
- Open method [ADO]
ms.assetid: d26f48fb-904e-4932-a245-3b4332ca1600
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4a2014c35383f1bc8dc30505cb26c602f7a22161
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/11/2018
ms.locfileid: "35280547"
---
# <a name="open-method-ado-stream"></a>Open 方法 （ADO 資料流）
開啟[資料流](../../../ado/reference/ado-api/stream-object-ado.md)來操作二進位或文字資料流的物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
Stream.Open Source, Mode , OpenOptions, UserName, Password  
```  
  
#### <a name="parameters"></a>參數  
 *Source*  
 選擇性。 A **Variant**值，指定之資料的來源**資料流**。 *來源*可能會包含指向已知的樹狀結構中，例如電子郵件或檔案系統中現有節點的絕對 URL 字串。 應指定 URL，利用 URL 關鍵字 (「 URL =*配置*://*伺服器*/*資料夾*")。 或者，*來源*可能包含的參考已經開啟[記錄](../../../ado/reference/ado-api/record-object-ado.md)物件，這會開啟相關聯的預設資料流**記錄**。 如果*來源*未指定，**資料流**具現化及開啟，根據預設，與沒有基礎來源相關聯。 如需 URL 結構描述和其相關聯的提供者的詳細資訊，請參閱[絕對和相對 Url](../../../ado/guide/data/absolute-and-relative-urls.md)。  
  
 *模式*  
 選擇性。 A [ConnectModeEnum](../../../ado/reference/ado-api/connectmodeenum.md)值，指定產生的存取模式**資料流**(例如，讀/寫或唯讀)。 預設值是**adModeUnknown**。 請參閱[模式](../../../ado/reference/ado-api/mode-property-ado.md)如需有關存取模式的屬性。 如果*模式*未指定，它會繼承的來源物件。 例如，如果來源**記錄**以唯讀模式開啟**資料流**也會跟著開啟唯讀模式中預設。  
  
 *OpenOptions*  
 選擇性。 A [StreamOpenOptionsEnum](../../../ado/reference/ado-api/streamopenoptionsenum.md)值。 預設值是**adOpenStreamUnspecified**。  
  
 *UserName*  
 選擇性。 A**字串**值，其中包含的使用者識別，必要時，存取**資料流**物件。  
  
 *密碼*  
 選擇性。 A**字串**值，其中包含的密碼，必要時，存取**資料流**物件。  
  
## <a name="remarks"></a>備註  
 當**記錄**做為來源參數，傳入的物件*UserID*和*密碼*參數不會因為存取**記錄**物件已經可供使用。 同樣地，[模式](../../../ado/reference/ado-api/mode-property-ado.md)的**記錄**物件傳送到**資料流**物件。 當*來源*未指定，**資料流**開啟且未包含任何資料[大小](../../../ado/reference/ado-api/size-property-ado-stream.md)為零 (0)。 為避免遺失任何資料寫入至這個**資料流**時**資料流**已關閉，儲存**資料流**與[CopyTo](../../../ado/reference/ado-api/copyto-method-ado.md)或[SaveToFile](../../../ado/reference/ado-api/savetofile-method.md)方法，或將它儲存到另一個記憶體位置。  
  
 *OpenOptions*值**adOpenStreamFromRecord**識別的內容*來源*參數必須為已開啟**記錄**物件。 預設行為是將視為*來源*為直接指向的節點樹狀結構，例如檔案的 URL。 會開啟與該節點相關聯的預設資料流。  
  
 雖然**資料流**是未開啟，便可讀取的所有唯讀屬性**資料流**。 如果**資料流**以非同步方式開啟所有的後續作業 (以外檢查[狀態](../../../ado/reference/ado-api/state-property-ado.md)和其他唯讀屬性) 會被封鎖直到**開啟**作業已完成。  
  
 我們已經討論過較舊版本，未指定的選項除了*來源*，您可以建立的執行個體**資料流**而不將它與基礎來源關聯的記憶體中的物件。 您可以動態地將資料加入資料流寫入二進位或文字資料**資料流**與[寫入](../../../ado/reference/ado-api/write-method.md)或[WriteText](../../../ado/reference/ado-api/writetext-method.md)，或藉由使用從檔案載入資料[LoadFromFile](../../../ado/reference/ado-api/loadfromfile-method-ado.md)。  
  
## <a name="applies-to"></a>適用於  
 [Stream 物件 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [Open 方法 （ADO 連接）](../../../ado/reference/ado-api/open-method-ado-connection.md)   
 [Open 方法 （ADO 資料錄）](../../../ado/reference/ado-api/open-method-ado-record.md)   
 [Open 方法 （ADO 資料錄集）](../../../ado/reference/ado-api/open-method-ado-recordset.md)   
 [OpenSchema 方法](../../../ado/reference/ado-api/openschema-method.md)   
 [SaveToFile 方法](../../../ado/reference/ado-api/savetofile-method.md)
