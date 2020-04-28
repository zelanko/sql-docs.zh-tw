---
title: Source 屬性（ADO Record） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Record::Source
- _Record::PutRefSource
- _Record::GetSource
- _Record::put_Source
- _Record::putref_Source
- _Record::get_Source
helpviewer_keywords:
- Source property [ADO Record]
ms.assetid: 2c18279e-6f35-4af0-b12e-8f1543d9ed20
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b1870d8cd8253e1b6de74ce093d51ca6e33c5c6d
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "67930939"
---
# <a name="source-property-ado-record"></a>Source 屬性 (ADO Record)
表示[記錄](../../../ado/reference/ado-api/record-object-ado.md)所代表的資料來源或物件。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回表示**記錄**所表示之實體的**Variant**值。  
  
## <a name="remarks"></a>備註  
 **Source**屬性會傳回**Record**物件[Open](../../../ado/reference/ado-api/open-method-ado-record.md)方法的*source*引數。 它可以包含絕對或相對 URL 字串。 絕對 URL 可以使用，而不需將[ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md)屬性設定為直接開啟**記錄**物件。 在此情況下，會建立隱含的**連接**物件。  
  
 **Source**屬性也可以包含已經開啟之**記錄集**的參考，這會開啟**記錄**物件，代表**記錄集**內的目前資料列。  
  
 **Source**屬性也可以包含[命令](../../../ado/reference/ado-api/command-object-ado.md)物件的參考，該物件會從提供者傳回單一資料列。  
  
 如果同時設定**ActiveConnection**屬性，則**來源**屬性必須指向存在於該連接範圍內的某個物件。 例如，在樹狀結構化的命名空間中，如果**Source**屬性包含絕對 URL，它必須指向連接字串中 URL 所識別之節點範圍內的節點。 如果**Source**屬性包含相對 URL，則會在**ActiveConnection**屬性所設定的內容中進行驗證。  
  
 當**記錄物件關閉**時， **Source**屬性會是讀取/寫入，而在**記錄**物件開啟時，則是唯讀的。  
  
> [!NOTE]
>  使用 HTTP 配置的 Url 會自動叫用[Microsoft OLE DB 提供者以進行網際網路發佈](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)。 如需詳細資訊，請參閱[絕對和相對 url](../../../ado/guide/data/absolute-and-relative-urls.md)。  
  
## <a name="applies-to"></a>套用至  
 [Record 物件 (ADO)](../../../ado/reference/ado-api/record-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [Source 屬性（ADO Error）](../../../ado/reference/ado-api/source-property-ado-error.md)   
 [Source 屬性 (ADO Recordset)](../../../ado/reference/ado-api/source-property-ado-recordset.md)
