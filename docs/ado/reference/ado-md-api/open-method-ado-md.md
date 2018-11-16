---
title: Open 方法 (ADO MD) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Open
- Cellset::Open
helpviewer_keywords:
- Open method [ADO MD]
ms.assetid: a87d8080-a238-45e5-bc80-9a8625b3810f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 091073431b3ff349b8ae107fcb6a37bfab94e46e
ms.sourcegitcommit: 63b4f62c13ccdc2c097570fe8ed07263b4dc4df0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/13/2018
ms.locfileid: "51602778"
---
# <a name="open-method-ado-md"></a>Open 方法 (ADO MD)
擷取多維度查詢的結果，並傳回結果[資料格集](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)。  
  
## <a name="syntax"></a>語法  
  
```  
  
Cellset.Open Source, ActiveConnection  
```  
  
#### <a name="parameters"></a>參數  
 *Source*  
 選擇性。 A **Variant**評估為有效的多維度查詢，例如多維度運算式 (MDX) 查詢。 *來源*引數對應至[來源](../../../ado/reference/ado-md-api/source-property-ado-md.md)屬性。 如需有關 MDX 的詳細資訊，請參閱 < [OLE DB 的線上分析處理 (OLAP)](https://msdn.microsoft.com/8a7673c6-3ca1-4411-9f1e-adf1e47df4f3) Microsoft Data Access Components SDK 中的文件。  
  
 *ActiveConnection*  
 選擇性。 A **Variant**評估為字串，指定有效的 ADO[連線](../../../ado/reference/ado-api/connection-object-ado.md)物件變數的名稱或連接的定義。 *ActiveConnection*引數會指定用來開啟連接[資料格集](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)物件。 如果您傳遞連接定義為這個引數時，ADO 會開啟新的連線，使用指定的參數。 *ActiveConnection*引數對應至[ActiveConnection](../../../ado/reference/ado-md-api/activeconnection-property-ado-md.md)屬性。  
  
## <a name="remarks"></a>備註  
 **開啟**方法會產生錯誤，如果省略了其中一個參數，且尚未設定及其對應的屬性值之前嘗試開啟**資料格集**。  
  
## <a name="applies-to"></a>適用於  
 [Cellset 物件 (ADO MD)](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)  
  
## <a name="see-also"></a>另請參閱  
 [Cellset 範例 (VB)](../../../ado/reference/ado-md-api/cellset-example-vb.md)   
 [ActiveConnection 屬性 (ADO MD)](../../../ado/reference/ado-md-api/activeconnection-property-ado-md.md)   
 [Close 方法 (ADO MD)](../../../ado/reference/ado-md-api/close-method-ado-md.md)   
 [連接物件 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [來源屬性 (ADO MD)](../../../ado/reference/ado-md-api/source-property-ado-md.md)   
 [State 屬性 (ADO MD)](../../../ado/reference/ado-md-api/state-property-ado-md.md)
