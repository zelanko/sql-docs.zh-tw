---
title: MaxRecords 屬性（ADO） |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5acd8997af6993a49ac4cbcca6e3b4c8bd26acfd
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "67932239"
---
# <a name="maxrecords-property-ado"></a>MaxRecords 屬性 (ADO)
指出從查詢傳回記錄[集](../../../ado/reference/ado-api/recordset-object-ado.md)的最大記錄數目。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回**Long**值，指出要傳回的記錄數目上限。 預設值為零（**0**），表示沒有限制。  
  
## <a name="remarks"></a>備註  
 使用**MaxRecords**屬性可限制提供者從資料來源傳回的記錄數目。 這個屬性的預設設定為零，表示提供者會傳回所有要求的記錄。  
  
 當**記錄集**關閉時， **MaxRecords**屬性是讀取/寫入，而當它開啟時則為唯讀。  
  
## <a name="applies-to"></a>套用至  
 [Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [MaxRecords 屬性範例（VB）](../../../ado/reference/ado-api/maxrecords-property-example-vb.md)   
 [MaxRecords 屬性範例 (VC++)](../../../ado/reference/ado-api/maxrecords-property-example-vc.md)   
