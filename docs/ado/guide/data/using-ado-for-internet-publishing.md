---
title: 使用 ADO 進行網際網路發佈 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- ADO, Internet publishing
- publishing to Internet [ADO]
- Internet publishing [ADO]
- urls [ADO]
ms.assetid: d399fce4-b70b-418f-8110-3deb3448863c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d779204046b9bca2591fbdc9459d7c6b53061ff4
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47778996"
---
# <a name="using-ado-for-internet-publishing"></a>使用 ADO 進行網際網路發佈
[OLE DB Provider for Internet Publishing](../../../ado/guide/data/the-ole-db-provider-for-internet-publishing.md)顯示存取搭配 ADO 的異質資料的特定範例。 雖然會專用於網際網路發佈提供者搭配使用這一節中的範例，示範的原則應該類似使用 ADO 與其他異質資料，例如電子郵件存放區提供者的提供者時。  
  
## <a name="urls"></a>URL  
 統一資源定位器 (Url) 可用來當做連接字串和命令文字的替代方式來指定資料來源 」 和 「 檔案和目錄的位置。 您可以使用 Url 與現有[連接](../../../ado/reference/ado-api/connection-object-ado.md)並**資料錄集**物件與**記錄**並**Stream**物件。  
  
 如需如何使用 Url 的詳細資訊，請參閱[絕對和相對 Url](../../../ado/guide/data/absolute-and-relative-urls.md)。  
  
## <a name="record-fields"></a>記錄欄位  
 區別異質資料與同質資料之間的差別在於針對先前的功能，每個資料列的資料，或是**記錄**，可以有一組不同的資料行，或**欄位**。 同質性的資料，每個資料列會有相同的資料行集。 多個網際網路發佈提供者的特定欄位的詳細資訊，請參閱[記錄和 Provider-Supplied 額外欄位](../../../ado/guide/data/records-and-provider-supplied-fields.md)。  
  
### <a name="appending-new-fields"></a>附加新的欄位  
 數個 ADO 物件已經過加強，才能搭配**記錄**並**Stream**物件。  
  
-   [欄位](../../../ado/reference/ado-api/fields-collection-ado.md)集合[附加](../../../ado/reference/ado-api/append-method-ado.md)方法，這個方法會建立，並將[欄位](../../../ado/reference/ado-api/field-object.md)物件集合，也可以指定的值**欄位**.  
  
-   [更新](../../../ado/reference/ado-api/update-method.md)方法完成的新增或刪除的欄位集合。  
  
-   為快顯和替代項目**Append**方法，您可以將值指派到未定義或先前刪除的欄位建立欄位。  
  
 此章節包含下列主題。  
  
-   [適用於網際網路發佈的 OLE DB 提供者](../../../ado/guide/data/the-ole-db-provider-for-internet-publishing.md)  
  
-   [網際網路發佈案例](../../../ado/guide/data/internet-publishing-scenario.md)  
  
-   [絕對和相對 URL](../../../ado/guide/data/absolute-and-relative-urls.md)  
  
-   [記錄和提供者提供的欄位](../../../ado/guide/data/records-and-provider-supplied-fields.md)  
  
## <a name="see-also"></a>另請參閱  
 [Record 物件 (ADO)](../../../ado/reference/ado-api/record-object-ado.md)   
 [Stream 物件 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)   
 [ADO 歷程記錄](../../../ado/guide/ado-history.md)
