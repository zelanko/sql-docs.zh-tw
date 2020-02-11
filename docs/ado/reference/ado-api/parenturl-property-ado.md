---
title: ParentURL 屬性（ADO） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Record::ParentURL
helpviewer_keywords:
- ParentURL property [ADO]
ms.assetid: 65120ce6-3900-4cd4-b322-3b9816d74737
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 54b2db44fe2e1971356f96d33aa8de0b02781b1e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67931647"
---
# <a name="parenturl-property-ado"></a>ParentURL 屬性 (ADO)
表示指向目前**記錄**物件之父[記錄](../../../ado/reference/ado-api/record-object-ado.md)的絕對 URL 字串。  
  
## <a name="return-value"></a>傳回值  
 傳回**字串**值，表示父**記錄**的 URL。  
  
## <a name="remarks"></a>備註  
 **ParentURL**屬性取決於用來開啟**記錄**物件的來源。 例如，您可以使用包含[ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md)屬性所參考之目錄的相對路徑名稱的來源來開啟**記錄**。  
  
 假設 "second" 是包含在 "first" 之下的資料夾。 使用下列語法開啟**記錄**物件：  
  
```  
record.ActiveConnection = "https://first"  
record.Open "second"  
```  
  
 現在， `the` **ParentURL**屬性的值是`"https://first"`，與**ActiveConnection**相同。  
  
 來源也可以是絕對 URL，例如， `"https://first/second"`。 然後**** `"https://first"`，ParentURL 屬性會是上方`"second"`的層級。  
  
 如果下列情況，這個屬性可能是 null 值：  
  
-   目前的物件沒有父系。例如，如果**記錄**物件代表目錄的根目錄，則為。  
  
-   **Record**物件代表無法以 URL 指定的實體。  
  
 這個屬性是唯讀的。  
  
> [!NOTE]
>  只有檔來源提供者支援此屬性，例如[用於網際網路發行的 Microsoft OLE DB 提供者](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)。 如需詳細資訊，請參閱[記錄和提供者提供的欄位](../../../ado/guide/data/records-and-provider-supplied-fields.md)。  
  
> [!NOTE]
>  使用 HTTP 配置的 Url 會自動叫用[Microsoft OLE DB 提供者以進行網際網路發佈](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)。 如需詳細資訊，請參閱[絕對和相對 url](../../../ado/guide/data/absolute-and-relative-urls.md)。  
  
> [!NOTE]
>  如果目前記錄包含來自 ADO**記錄集**的資料記錄，存取**ParentURL**屬性會造成執行階段錯誤，表示沒有可能的 URL。  
  
## <a name="applies-to"></a>套用至  
 [Record 物件 (ADO)](../../../ado/reference/ado-api/record-object-ado.md)
