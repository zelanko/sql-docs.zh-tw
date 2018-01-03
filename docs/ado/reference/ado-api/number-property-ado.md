---
title: "Number 屬性 (ADO) |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Error::Number
- Error::GetNumber
- Error::get_Number
helpviewer_keywords: number property [ADO]
ms.assetid: f92323c5-dd11-4a63-a505-d9014a0f067f
caps.latest.revision: "13"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a0313ce53b07724a41491d5db827fc9deb3dae4e
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="number-property-ado"></a>Number 屬性 (ADO)
表示唯一識別數字[錯誤](../../../ado/reference/ado-api/error-object.md)物件。  
  
## <a name="return-value"></a>傳回值  
 傳回**長**可能對應至其中的值[ErrorValueEnum](../../../ado/reference/ado-api/errorvalueenum.md)常數。  
  
## <a name="remarks"></a>備註  
 使用**數目**屬性來判斷是否發生錯誤。 屬性的值是唯一的編號對應於錯誤狀況。  
  
 [錯誤](../../../ado/reference/ado-api/errors-collection-ado.md)集合會傳回 HRESULT，以十六進位格式 (例如，0x80004005) 或長數值 (例如，2147467259)。 基礎的元件，例如 OLE DB 或甚至 OLE 本身就會引發這些 Hresult。 如需有關這些數字的詳細資訊，請參閱[錯誤 (OLE DB)](http://msdn.microsoft.com/en-us/ed74e62d-4948-4eeb-a7c9-fd7ad46af7fd)中[OLE DB 程式設計人員參考](http://msdn.microsoft.com/en-us/3c5e2dd5-35e5-4a93-ac3a-3818bb43bbf8)*。*  
  
## <a name="applies-to"></a>適用於  
 [Error 物件](../../../ado/reference/ado-api/error-object.md)  
  
## <a name="see-also"></a>請參閱  
 [描述、 HelpContext、 說明檔案、 NativeError、 數字、 來源和 SQLState 屬性範例 (VB)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vb.md)   
 [描述、 HelpContext、 說明檔案、 NativeError、 數字、 來源和 SQLState 屬性範例 （VC + +）](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vc.md)   
 [Description 屬性](../../../ado/reference/ado-api/description-property.md)   
 [HelpContext，HelpFile 屬性](../../../ado/reference/ado-api/helpcontext-helpfile-properties.md)   
 [Source 屬性 (ADO Error)](../../../ado/reference/ado-api/source-property-ado-error.md)
