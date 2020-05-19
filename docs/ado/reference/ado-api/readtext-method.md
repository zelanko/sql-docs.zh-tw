---
title: ReadText 方法 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::raw_ReadText
- _Stream::ReadText
helpviewer_keywords:
- ReadText method [ADO]
ms.assetid: be5a409e-cf87-4859-9ea5-713401755a77
author: rothja
ms.author: jroth
ms.openlocfilehash: 8afabd90ee6251be650036b285de0f08a3776723
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82754238"
---
# <a name="readtext-method"></a>ReadText 方法
從文字[資料流程](../../../ado/reference/ado-api/stream-object-ado.md)物件讀取指定的字元數。  
  
## <a name="syntax"></a>語法  
  
```  
  
String = Stream.ReadText ( NumChars)  
```  
  
#### <a name="parameters"></a>參數  
 *NumChars*  
 選擇性。 **Long**值，指定要從檔案讀取的字元數，或[StreamReadEnum](../../../ado/reference/ado-api/streamreadenum.md)值。 預設值為**adReadAll**。  
  
## <a name="return-value"></a>傳回值  
 **ReadText**方法會從**資料流程**物件讀取指定的字元數、整行或整個資料流程，並傳回產生的字串。  
  
## <a name="remarks"></a>備註  
 如果*不足 numchar*大於資料流程中剩餘的字元數，則只會傳回剩下的字元。 字串 read 不會填補以符合*不足 numchar*所指定的長度。 如果沒有要讀取的字元，則會傳回其值為 null 的 variant。 **ReadText**不能用來向後讀取。  
  
> [!NOTE]
>  **ReadText**方法用於文字資料流程（[類型](../../../ado/reference/ado-api/type-property-ado-stream.md)為**adTypeText**）。 若為二進位資料流程（**類型**為**adTypeBinary**），請使用[Read](../../../ado/reference/ado-api/read-method.md)。  
  
 導致大量 XML 資料透過 ActiveX Data Object （ADO）資料流程物件的**ReadText**方法傳回的查詢，可能需要很長的時間才能執行;如果這是在從 ASP 網頁叫用的 COM + 元件中完成，使用者的會話可能會超時。ADO 將資料流程物件資料從 UTF-8 編碼轉換成 Unicode;這類大量資料一次轉換時經常發生的記憶體重新配置非常耗時。 若要解決此問題，請重複呼叫 ADO command 物件的**ReadText**方法，並指定較少的字元數。 測試已顯示相當於128K （131072）的值是最佳的。 回應時間會隨著此值減少而降低。 如需詳細資訊，請參閱知識庫文章280067「PRB：使用 ADO stream 物件的 ReadText 方法從 SQL Server 2000 抓取非常大的 XML 檔，可能會變慢」，在 Microsoft 知識庫中的 https://support.microsoft.com 。  
  
## <a name="applies-to"></a>套用至  
 [Stream 物件 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [Read 方法](../../../ado/reference/ado-api/read-method.md)
