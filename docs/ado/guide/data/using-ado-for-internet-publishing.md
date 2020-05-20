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
author: rothja
ms.author: jroth
ms.openlocfilehash: b95700d30337363091815763a5e9fbf1547902e6
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82763059"
---
# <a name="using-ado-for-internet-publishing"></a>使用 ADO 進行網際網路發佈
[網際網路發佈的 OLE DB 提供者](../../../ado/guide/data/the-ole-db-provider-for-internet-publishing.md)會顯示使用 ADO 存取異質資料的特定範例。 雖然本節中的範例僅適用于使用網際網路發行提供者，但在將 ADO 與其他提供者搭配使用異質資料（例如電子郵件存放區的提供者）時，所示範的原則應該類似。  
  
## <a name="urls"></a>URL  
 您可以使用統一資源定位器（Url）做為連接字串和命令文字的替代方法，以指定資料來源和檔案和目錄的位置。 您可以使用 Url 搭配現有的[連接](../../../ado/reference/ado-api/connection-object-ado.md)和**記錄集**物件，以及**記錄**和**資料流程**物件。  
  
 如需如何使用 Url 的詳細資訊，請參閱[絕對和相對 url](../../../ado/guide/data/absolute-and-relative-urls.md)。  
  
## <a name="record-fields"></a>記錄欄位  
 異質資料和同質資料之間的差異在於，前者的每個資料列或**記錄**都可以有一組不同的資料行或**欄位**。 針對同質資料，每個資料列都有相同的資料行集合。 如需有關網際網路發行提供者特定欄位的詳細資訊，請參閱[記錄和提供者提供的額外欄位](../../../ado/guide/data/records-and-provider-supplied-fields.md)。  
  
### <a name="appending-new-fields"></a>附加新欄位  
 已增強數個 ADO 物件，可搭配**Record**和**Stream**物件一起使用。  
  
-   [Fields](../../../ado/reference/ado-api/fields-collection-ado.md)集合[Append](../../../ado/reference/ado-api/append-method-ado.md)方法會建立[欄位](../../../ado/reference/ado-api/field-object.md)物件，並將其加入至集合，也可以指定**欄位**的值。  
  
-   [Update](../../../ado/reference/ado-api/update-method.md)方法會完成將欄位新增或刪除至集合的作業。  
  
-   您可以將值指派給未定義或先前已刪除的欄位，以建立欄位，做為**附加**方法的快捷方式和替代方案。  
  
 此章節包含下列主題。  
  
-   [適用於網際網路發佈的 OLE DB 提供者](../../../ado/guide/data/the-ole-db-provider-for-internet-publishing.md)  
  
-   [網際網路發佈案例](../../../ado/guide/data/internet-publishing-scenario.md)  
  
-   [絕對和相對 URL](../../../ado/guide/data/absolute-and-relative-urls.md)  
  
-   [記錄和提供者提供的欄位](../../../ado/guide/data/records-and-provider-supplied-fields.md)  
  
## <a name="see-also"></a>另請參閱  
 [Record 物件（ADO）](../../../ado/reference/ado-api/record-object-ado.md)   
 [Stream 物件（ADO）](../../../ado/reference/ado-api/stream-object-ado.md)   
 [ADO 歷程記錄](../../../ado/guide/ado-history.md)
