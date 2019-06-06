---
title: 來源屬性 (ADO Record) |Microsoft Docs
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
manager: jroth
ms.openlocfilehash: 9217658a645d731645b0c85a419ecf759b1fd3bb
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/05/2019
ms.locfileid: "66711103"
---
# <a name="source-property-ado-record"></a>Source 屬性 (ADO Record)
指出資料來源或所代表的物件[記錄](../../../ado/reference/ado-api/record-object-ado.md)。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回**Variant**值，指出所代表之實體**記錄**。  
  
## <a name="remarks"></a>備註  
 **來源**屬性會傳回*來源*引數**記錄**物件[開啟](../../../ado/reference/ado-api/open-method-ado-record.md)方法。 它可以包含為絕對或相對的 URL 字串。 如果沒有設定可用的絕對 URL [ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md)屬性，以直接開啟**記錄**物件。 隱含**連線**在此情況下建立物件。  
  
 **來源**屬性也可以包含的參考已經開啟**Recordset**，這會開啟**記錄**物件，表示目前的資料列中**資料錄集**。  
  
 **來源**屬性也可能包含參考[命令](../../../ado/reference/ado-api/command-object-ado.md)會傳回單一資料列，從提供者的物件。  
  
 如果**ActiveConnection**也設定屬性，則**來源**屬性必須指向某個範圍內的該連線是否存在的物件。 例如，在樹狀結構的命名空間，如果**來源**屬性包含絕對 URL，它必須指向存在的連接字串中的 URL 所識別的節點範圍內的節點。 如果**來源**屬性包含相對的 URL，則會進行驗證所設定的內容內**ActiveConnection**屬性。  
  
 **來源**屬性是讀取/寫入時**記錄**物件已關閉，而且是唯讀時**記錄**物件已經開啟。  
  
> [!NOTE]
>  使用 http 配置 Url 將會自動叫用[Microsoft OLE DB Provider for Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)。 如需詳細資訊，請參閱 <<c0> [ 絕對和相對 Url](../../../ado/guide/data/absolute-and-relative-urls.md)。  
  
## <a name="applies-to"></a>適用於  
 [Record 物件 (ADO)](../../../ado/reference/ado-api/record-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [來源屬性 (ADO Error)](../../../ado/reference/ado-api/source-property-ado-error.md)   
 [Source 屬性 (ADO Recordset)](../../../ado/reference/ado-api/source-property-ado-recordset.md)
