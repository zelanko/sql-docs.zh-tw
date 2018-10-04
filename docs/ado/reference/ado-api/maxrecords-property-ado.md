---
title: MaxRecords 屬性 (ADO) |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: ac5097a8692ed7a9e6566707354112547c5a619c
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47789396"
---
# <a name="maxrecords-property-ado"></a>MaxRecords 屬性 (ADO)
表示要傳回的記錄數目上限[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)從查詢。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回**長**值，指出要傳回的記錄數目上限。 預設值為零 (**0**)，這表示沒有限制。  
  
## <a name="remarks"></a>備註  
 使用**MaxRecords**屬性來限制從資料來源提供者所傳回的記錄數目。 此屬性的預設設定為零，表示提供者會傳回所有要求的記錄。  
  
 **MaxRecords**屬性是讀取/寫入時**資料錄集**開啟時，會關閉，且為唯讀狀態。  
  
## <a name="applies-to"></a>適用於  
 [Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [MaxRecords 屬性範例 (VB)](../../../ado/reference/ado-api/maxrecords-property-example-vb.md)   
 [MaxRecords 屬性範例 (VC++)](../../../ado/reference/ado-api/maxrecords-property-example-vc.md)   
