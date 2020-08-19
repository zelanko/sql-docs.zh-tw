---
description: MaxRecords 屬性 (ADO)
title: " (ADO) 的 MaxRecords 屬性 |Microsoft Docs"
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::MaxRecords
helpviewer_keywords:
- MaxRecords property [ADO]
ms.assetid: 20c76571-8c9a-482c-a99e-726ab1d93f8b
author: rothja
ms.author: jroth
ms.openlocfilehash: 905897cfa08591aaefce3aceb46e1892d41d3d7a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88443270"
---
# <a name="maxrecords-property-ado"></a>MaxRecords 屬性 (ADO)
指出從查詢傳回 [記錄集](../../../ado/reference/ado-api/recordset-object-ado.md) 的記錄數目上限。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回 **Long** 值，表示要傳回的記錄數目上限。 預設值為零 (**0**) ，表示沒有限制。  
  
## <a name="remarks"></a>備註  
 您可以使用 **MaxRecords** 屬性來限制提供者從資料來源傳回的記錄數目。 這個屬性的預設設定為零，表示提供者會傳回所有要求的記錄。  
  
 當**記錄集**已關閉時， **MaxRecords**屬性是讀取/寫入，而當記錄開啟時，則為唯讀屬性。  
  
## <a name="applies-to"></a>套用至  
 [Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [ (VB) 的 MaxRecords 屬性範例 ](../../../ado/reference/ado-api/maxrecords-property-example-vb.md)   
 [MaxRecords 屬性範例 (VC++)](../../../ado/reference/ado-api/maxrecords-property-example-vc.md)   
