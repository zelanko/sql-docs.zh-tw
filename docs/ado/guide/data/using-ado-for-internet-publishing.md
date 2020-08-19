---
description: 使用 ADO 進行網際網路發佈
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
ms.openlocfilehash: 5f08edfbd56b900759c004cbf0fca8a634ab1010
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88452600"
---
# <a name="using-ado-for-internet-publishing"></a>使用 ADO 進行網際網路發佈
[適用于網際網路發佈的 OLE DB 提供者](../../../ado/guide/data/the-ole-db-provider-for-internet-publishing.md) 會顯示使用 ADO 存取異質資料的特定範例。 雖然本節中的範例是使用網際網路發佈提供者所特有的，但使用 ADO 搭配其他提供者來處理異質資料（例如電子郵件存放區的提供者）時，所示範的原則應該很類似。  
  
## <a name="urls"></a>URL  
  (Url) 的統一資源定位器可以用來做為連接字串和命令文字的替代方式，以指定資料來源和檔案和目錄的位置。 您可以使用 Url 搭配現有的 [連接](../../../ado/reference/ado-api/connection-object-ado.md) 和 **記錄集** 物件，以及 **記錄** 和 **資料流程** 物件。  
  
 如需如何使用 Url 的詳細資訊，請參閱 [絕對和相對 url](../../../ado/guide/data/absolute-and-relative-urls.md)。  
  
## <a name="record-fields"></a>記錄欄位  
 異質資料和同質資料之間的差異在於，前者的每個資料列或 **記錄**都可以有一組不同的資料行或 **欄位**。 針對同質資料，每個資料列都有相同的資料行集合。 如需有關網際網路發佈提供者特定欄位的詳細資訊，請參閱 [記錄和提供者提供的額外欄位](../../../ado/guide/data/records-and-provider-supplied-fields.md)。  
  
### <a name="appending-new-fields"></a>附加新欄位  
 許多 ADO 物件已經過增強，可搭配 **Record** 和 **Stream** 物件一起使用。  
  
-   [Fields](../../../ado/reference/ado-api/fields-collection-ado.md)集合[附加](../../../ado/reference/ado-api/append-method-ado.md)方法會建立[欄位](../../../ado/reference/ado-api/field-object.md)物件，並將其加入至集合中，也可以指定**欄位**的值。  
  
-   [Update](../../../ado/reference/ado-api/update-method.md)方法會完成將欄位加入或刪除集合的作業。  
  
-   您可以藉由將值指派給未定義或先前刪除的欄位，來建立欄位，作為 **附加** 方法的快捷方式和替代方法。  
  
 此章節包含下列主題。  
  
-   [適用於網際網路發佈的 OLE DB 提供者](../../../ado/guide/data/the-ole-db-provider-for-internet-publishing.md)  
  
-   [網際網路發佈案例](../../../ado/guide/data/internet-publishing-scenario.md)  
  
-   [絕對和相對 URL](../../../ado/guide/data/absolute-and-relative-urls.md)  
  
-   [記錄和提供者提供的欄位](../../../ado/guide/data/records-and-provider-supplied-fields.md)  
  
## <a name="see-also"></a>另請參閱  
 [ (ADO) 的記錄物件 ](../../../ado/reference/ado-api/record-object-ado.md)   
 [ (ADO) 的資料流程物件 ](../../../ado/reference/ado-api/stream-object-ado.md)   
 [ADO 歷程記錄](../../../ado/guide/ado-history.md)
