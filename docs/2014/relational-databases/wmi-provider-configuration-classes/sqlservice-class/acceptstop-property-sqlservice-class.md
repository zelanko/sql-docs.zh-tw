---
title: AcceptStop 屬性 （SqlService 類別） |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
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
caps.latest.revision: 35
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 19197db0e6d2679d0ad13bcb43472be4448fccb7
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36036730"
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
 A [SqlService 類別](sqlservice-class.md)代表服務的物件  
  
## <a name="property-valuereturn-value"></a>屬性值/傳回值  
 指定是否可停止服務的布林值：如果可停止服務為 `true`，如果無法停止則為 `false`。  
  
## <a name="remarks"></a>備註  
  
## <a name="see-also"></a>另請參閱  
 [啟動及停止服務](http://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  