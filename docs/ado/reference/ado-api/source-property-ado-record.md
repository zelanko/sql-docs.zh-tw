---
description: Source 屬性 (ADO Record)
title: 來源屬性 (ADO 記錄) |Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 0e755fb4a34e170efea760428021b540a182156c
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88777407"
---
# <a name="source-property-ado-record"></a>Source 屬性 (ADO Record)
指出 [記錄](./record-object-ado.md)所代表的資料來源或物件。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回 **Variant** 值，指出 **記錄**所表示的實體。  
  
## <a name="remarks"></a>備註  
 **Source**屬性會傳回**Record**物件[Open](./open-method-ado-record.md)方法的*來源*引數。 它可以包含絕對或相對的 URL 字串。 絕對 URL 可以在不設定 [ActiveConnection](./activeconnection-property-ado.md) 屬性的情況下用來直接開啟 **記錄** 物件。 在此情況下，會建立隱含 **連接** 物件。  
  
 **Source**屬性也可以包含已開啟之**記錄集**的參考，這會開啟代表**記錄集中**目前資料列的**記錄**物件。  
  
 **Source**屬性也可以包含[命令](./command-object-ado.md)物件的參考，該物件會從提供者傳回單一資料列。  
  
 如果 **ActiveConnection** 屬性也已設定，則 **來源** 屬性必須指向存在於該連接範圍內的某個物件。 例如，在樹狀結構的命名空間中，如果 **Source** 屬性包含絕對 URL，它必須指向連接字串中的 url 所識別之節點範圍記憶體在的節點。 如果 **Source** 屬性包含相對 URL，則會在 **ActiveConnection** 屬性所設定的內容中進行驗證。  
  
 **在記錄物件關閉**時，**來源**屬性是讀取/寫入，而且在**記錄**物件開啟時是唯讀的。  
  
> [!NOTE]
>  使用 HTTP 配置的 Url 會自動叫用 [Microsoft OLE DB 提供者進行網際網路發佈](../../guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)。 如需詳細資訊，請參閱 [絕對和相對 url](../../guide/data/absolute-and-relative-urls.md)。  
  
## <a name="applies-to"></a>套用至  
 [Record 物件 (ADO)](./record-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [ (ADO Error) 的 Source 屬性 ](./source-property-ado-error.md)   
 [Source 屬性 (ADO Recordset)](./source-property-ado-recordset.md)