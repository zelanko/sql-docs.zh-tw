---
title: Clustered 屬性 （SqlService 類別） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
api_name:
- Clustered Property (SqlService Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- Clustered property
ms.assetid: f714e7f5-c2db-45c6-9536-6ca2cb5b42aa
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 065440d834033d1c1c999ea9d38d321be9a6278c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63223321"
---
# <a name="clustered-property-sqlservice-class"></a>Clustered 屬性 (SqlService 類別)
  取得可指定服務是否為叢集執行個體之一部分的布林屬性值。  
  
## <a name="syntax"></a>語法  
  
```  
  
object  
.Clustered [= value]  
```  
  
## <a name="parts"></a>組件  
 *object*  
 表示此服務的 [SqlService 類別](sqlservice-class.md) 物件。  
  
## <a name="property-valuereturn-value"></a>屬性值/傳回值  
 指定服務是否正在參與叢集執行個體的布林值：如果服務正在參與叢集執行個體為 `true`，如果服務未參與叢集執行個體則為 `false`。  
  
## <a name="remarks"></a>備註  
  
## <a name="see-also"></a>另請參閱  
 [啟動及停止服務](https://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
