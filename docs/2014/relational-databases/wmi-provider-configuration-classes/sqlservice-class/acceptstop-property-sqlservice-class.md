---
title: AcceptStop 屬性（SqlService 類別） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
api_name:
- AcceptStop Property (SqlService Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- AcceptStop property
ms.assetid: bf8ffe79-4f4c-4a2d-82e5-2ae8f5d466c5
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: d555a3763b4e8c769cd52ce72019b66bddd594fd
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85062634"
---
# <a name="acceptstop-property-sqlservice-class"></a>AcceptStop 屬性 (SqlService 類別)
  取得可指定是否可停止服務的布林屬性值。  
  
## <a name="syntax"></a>語法  
  
```  
  
object  
.AcceptStop [= value]  
```  
  
## <a name="parts"></a>組件  
 *object*  
 代表服務的[SqlService 類別](sqlservice-class.md)物件。  
  
## <a name="property-valuereturn-value"></a>屬性值/傳回值  
 指定是否可停止服務的布林值：如果可停止服務為 `true`，如果無法停止則為 `false`。  
  
## <a name="remarks"></a>備註  
  
## <a name="see-also"></a>另請參閱  
 [啟動及停止服務](https://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
