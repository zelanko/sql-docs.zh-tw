---
title: "使用 ADO 的網際網路發行 |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ADO, Internet publishing
- publishing to Internet [ADO]
- Internet publishing [ADO]
- urls [ADO]
ms.assetid: d399fce4-b70b-418f-8110-3deb3448863c
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 609f4574c7f8cf9cb13fd2d5b21f3504ec3ce9fb
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/09/2018
---
# <a name="using-ado-for-internet-publishing"></a>使用 ADO 的網際網路發行
[OLE DB Provider for Internet Publishing](../../../ado/guide/data/the-ole-db-provider-for-internet-publishing.md)顯示存取使用 ADO 的異質資料的特定範例。 雖然本節中的範例將會是適用於使用網際網路發行的提供者，示範的原則類似時應該使用 ADO 與其他異質資料，例如提供者的電子郵件存放區提供者。  
  
## <a name="urls"></a>URL  
 統一資源定位器 (Url) 可以用做為連接字串和命令文字替代，來指定資料來源和位置的檔案和目錄。 您可以使用 Url 與現有[連接](../../../ado/reference/ado-api/connection-object-ado.md)和**資料錄集**物件與**記錄**和**資料流**物件。  
  
 如需如何使用 Url 的詳細資訊，請參閱[絕對和相對 Url](../../../ado/guide/data/absolute-and-relative-urls.md)。  
  
## <a name="record-fields"></a>記錄欄位  
 異質資料與同質資料之間的區別差異在於，前者，每個資料列的資料，或**記錄**，可以有一組不同的資料行，或**欄位**。 同質資料，每個資料列都有相同的資料行集。 多個網際網路發行的提供者的特定欄位的詳細資訊，請參閱[記錄和 Provider-Supplied 額外欄位](../../../ado/guide/data/records-and-provider-supplied-fields.md)。  
  
### <a name="appending-new-fields"></a>附加新的欄位  
 有幾個 ADO 物件已增強為與搭配運作**記錄**和**資料流**物件。  
  
-   [欄位](../../../ado/reference/ado-api/fields-collection-ado.md)集合[附加](../../../ado/reference/ado-api/append-method-ado.md)方法，這個方法會建立，並將[欄位](../../../ado/reference/ado-api/field-object.md)物件至集合，也可以指定的值**欄位**.  
  
-   [更新](../../../ado/reference/ado-api/update-method.md)方法完成新增或刪除的欄位集合。  
  
-   為快顯和替代項目**附加**方法，您可以將此值指派到未定義或先前刪除的欄位建立欄位。  
  
 此章節包含下列主題。  
  
-   [適用於網際網路發佈的 OLE DB 提供者](../../../ado/guide/data/the-ole-db-provider-for-internet-publishing.md)  
  
-   [網際網路發佈案例](../../../ado/guide/data/internet-publishing-scenario.md)  
  
-   [絕對和相對 URL](../../../ado/guide/data/absolute-and-relative-urls.md)  
  
-   [記錄和提供者提供的欄位](../../../ado/guide/data/records-and-provider-supplied-fields.md)  
  
## <a name="see-also"></a>另請參閱  
 [記錄物件 (ADO)](../../../ado/reference/ado-api/record-object-ado.md)   
 [資料流物件 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)   
 [ADO 歷程記錄](../../../ado/guide/ado-history.md)
