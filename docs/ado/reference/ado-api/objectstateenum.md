---
title: "ObjectStateEnum |Microsoft 文件"
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
f1_keywords: ObjectStateEnum
helpviewer_keywords: ObjectStateEnum enumeration [ADO]
ms.assetid: 32746558-097b-4749-989e-519aadf7e3f4
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 74958339c47cc5fa461fa8571465af4d31a16e36
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="objectstateenum"></a>ObjectStateEnum
指定物件是否為開啟或關閉、 連接到執行命令，或擷取資料的資料來源。  
  
|常數|ReplTest1|描述|  
|--------------|-----------|-----------------|  
|**adStateClosed**|0|指出物件已關閉。|  
|**adStateOpen**|@shouldalert|指出物件開啟。|  
|**adStateConnecting**|2|表示正在連接物件。|  
|**adStateExecuting**|4|表示物件正在執行命令。|  
|**adStateFetching**|8|指出，正在抓取物件的資料列。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 對等項目  
 封裝： **com.ms.wfc.data**  
  
|常數|  
|--------------|  
|AdoEnums.ObjectState.CLOSED|  
|AdoEnums.ObjectState.OPEN|  
|AdoEnums.ObjectState.CONNECTING|  
|AdoEnums.ObjectState.EXECUTING|  
|AdoEnums.ObjectState.FETCHING|  
  
## <a name="applies-to"></a>適用於  
  
|||  
|-|-|  
|[State 屬性 (ADO MD)](../../../ado/reference/ado-md-api/state-property-ado-md.md)|[State 屬性 (ADO)](../../../ado/reference/ado-api/state-property-ado.md)|
