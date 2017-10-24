---
title: "來源屬性 （ADO 資料錄） |Microsoft 文件"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
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
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 524845f59338a483df89586847157e6d9eaa598c
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="source-property-ado-record"></a>來源屬性 （ADO 資料錄）
指出資料來源或所代表的物件[記錄](../../../ado/reference/ado-api/record-object-ado.md)。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回**Variant**值，指出所代表的實體**記錄**。  
  
## <a name="remarks"></a>備註  
 **來源**屬性會傳回*來源*引數的**記錄**物件[開啟](../../../ado/reference/ado-api/open-method-ado-record.md)方法。 它可以包含為絕對或相對的 URL 字串。 如果沒有設定可以使用絕對 URL [ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md)直接開啟屬性**記錄**物件。 隱含**連接**在此情況下建立物件。  
  
 **來源**屬性也可以包含的參考已經開啟**資料錄集**，這會開啟**記錄**物件，代表目前的資料列中**資料錄集**。  
  
 **來源**屬性也可以包含的參考[命令](../../../ado/reference/ado-api/command-object-ado.md)會傳回單一資料列從提供者的物件。  
  
 如果**ActiveConnection**也設定屬性，則**來源**屬性必須指向某個存在於該連接的範圍內的物件。 例如，在樹狀結構的命名空間，如果**來源**屬性包含絕對 URL，必須指向存在的連接字串中的 URL 所識別的節點範圍內的節點。 如果**來源**屬性包含相對 URL，然後驗證所設定的內容內**ActiveConnection**屬性。  
  
 **來源**屬性是讀取/寫入時**記錄**物件已關閉，而且是唯讀時**記錄**物件是否開啟。  
  
> [!NOTE]
>  使用 http 配置 Url 將會自動叫用[Microsoft OLE DB Provider for Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)。 如需詳細資訊，請參閱[絕對和相對 Url](../../../ado/guide/data/absolute-and-relative-urls.md)。  
  
## <a name="applies-to"></a>適用於  
 [記錄物件 (ADO)](../../../ado/reference/ado-api/record-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [來源屬性 （ADO 錯誤）](../../../ado/reference/ado-api/source-property-ado-error.md)   
 [來源屬性 （ADO 資料錄集）](../../../ado/reference/ado-api/source-property-ado-recordset.md)

