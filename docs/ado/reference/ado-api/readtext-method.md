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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b095e034df987fd580b5f5855993c9cf070a1236
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63278605"
---
# <a name="readtext-method"></a>ReadText 方法
讀取指定的文字的字元數[Stream](../../../ado/reference/ado-api/stream-object-ado.md)物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
String = Stream.ReadText ( NumChars)  
```  
  
#### <a name="parameters"></a>參數  
 *NumChars*  
 選擇性。 A**長**值，指定要從檔案讀取的字元數或有[StreamReadEnum](../../../ado/reference/ado-api/streamreadenum.md)值。 預設值是**adReadAll**。  
  
## <a name="return-value"></a>傳回值  
 **ReadText**方法會讀取指定的字元數、 整行或從整個資料流**Stream**物件，並傳回產生的字串。  
  
## <a name="remarks"></a>備註  
 如果*數不足 NumChar*的字元數超過保留資料流中，只有剩餘的字元，才會傳回。 讀取的字串不會填補到符合所指定的長度*數不足 NumChar*。 如果沒有供讀取字元，則會傳回其值為 null 的 variant。 **ReadText**無法用來讀取回溯。  
  
> [!NOTE]
>  **ReadText**方法搭配文字資料流 ([型別](../../../ado/reference/ado-api/type-property-ado-stream.md)會**adTypeText**)。 二進位資料流 (**型別**是**adTypeBinary**)，使用[讀取](../../../ado/reference/ado-api/read-method.md)。  
  
 導致大量透過傳回的 XML 資料的查詢**ReadText** ActiveX Data Object (ADO) 的 Stream 物件的方法可能會花費很長的時間執行;，如果進行此設定會從叫用 COM + 元件中ASP 網頁上，使用者的工作階段可能會逾時。ADO 將從 utf-8 編碼為 Unicode; 轉換 Stream 物件資料頻繁的記憶體重新配置參與一次轉換的這類數量龐大的資料是很耗時。 若要解決，請重複的呼叫**ReadText**方法 ADO 命令物件，並指定較少的字元。 測試顯示的值等於 128 K (131,072) 是最佳。 回應時間減少為這個值會減少。 如需詳細資訊，請參閱知識庫文章 280067，「 PRB:使用 ADO 資料流物件 ReadText 方法來擷取從 SQL Server 2000 的非常大型的 XML 文件可能會變慢 」，Microsoft 知識庫中在 https://support.microsoft.com。  
  
## <a name="applies-to"></a>適用於  
 [Stream 物件 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [Read 方法](../../../ado/reference/ado-api/read-method.md)
