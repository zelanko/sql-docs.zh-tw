---
title: AcceptStop 屬性 （SqlService 類別） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
- docset-sql-devref
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
manager: craigg
ms.openlocfilehash: afce20f92e237a97b56e92b0d1a9c0c1c2d8f3b0
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48136078"
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
 A [SqlService 類別](sqlservice-class.md)物件，表示服務  
  
## <a name="property-valuereturn-value"></a>屬性值/傳回值  
 指定是否可停止服務的布林值：如果可停止服務為 `true`，如果無法停止則為 `false`。  
  
## <a name="remarks"></a>備註  
  
## <a name="see-also"></a>另請參閱  
 [啟動及停止服務](http://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
