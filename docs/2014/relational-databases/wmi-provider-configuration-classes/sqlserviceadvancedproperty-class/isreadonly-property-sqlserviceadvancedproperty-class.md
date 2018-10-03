---
title: IsReadOnly 屬性 （SqlServiceAdvancedProperty 類別） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.topic: reference
api_name:
- IsReadOnly Property (SqlServiceAdvancedProperty Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- IsReadOnly property
ms.assetid: 9672e70f-1d8c-4133-ac73-3b5733a1c4ee
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 6d6239c0187047a05775d2ffdf2ab027413273ac
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48202558"
---
# <a name="isreadonly-property-sqlserviceadvancedproperty-class"></a>IsReadOnly 屬性 (SqlServiceAdvancedProperty 類別)
  取得或設定布林屬性，該屬性會指定進階屬性是否為唯讀。  
  
## <a name="syntax"></a>語法  
  
```  
  
object  
.IsReadOnly [= value]  
```  
  
## <a name="parts"></a>組件  
 *object*  
 代表進階屬性的 [SqlServiceAdvancedProperty 類別](sqlserviceadvancedproperty-class.md) 物件。  
  
## <a name="property-valuereturn-value"></a>屬性值/傳回值  
 指定進階屬性是否為唯讀的布林值：如果進階屬性為唯讀則為 `true`，如果可以修改進階屬性則為 `false`。  
  
## <a name="remarks"></a>備註  
  
## <a name="see-also"></a>另請參閱  
 [啟動及停止服務](http://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
