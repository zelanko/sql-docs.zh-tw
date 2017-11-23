---
title: "資料指標及鎖定特性 |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- locks [ADO], characteristics
- adOpenDynamic [ADO]
- cursors [ADO], characteristics
ms.assetid: 459c29cb-4230-42bf-8cc2-f3132ccc7aba
caps.latest.revision: "9"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 84f06591c70a42701ca264c99af00e4f072aadd0
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="cursor-and-lock-characteristics"></a>資料指標及鎖定特性
當資料指標的特性，取決於提供者功能時，下列的優點和缺點一般也適用於各種類型的資料指標和鎖定。  
  
|資料指標或鎖定的類型|優點|缺點|  
|-------------------------|----------------|-------------------|  
|**adOpenForwardOnly**|-低的資源需求|-無法向後捲動<br />-沒有資料並行存取|  
|**adOpenStatic**|可捲動|-沒有資料並行存取|  
|**adOpenKeyset**|的某些資料並行存取<br />可捲動|-更新版本的資源需求<br />-無法中斷連接案例中使用|  
|**adOpenDynamic**|-高資料並行存取<br />可捲動|高資源需求<br />-無法中斷連接案例中使用|  
|**Recordset**|-低的資源需求<br />-具有高擴充性|資料無法透過資料指標更新|  
|**Adlockpessimistic**|批次更新<br />-可讓連接中斷的情況<br />-其他使用者能夠存取資料|-可以變更資料由多個使用者一次|  
|**Locktype**|其他使用者鎖定時無法變更資料|-可以防止其他使用者存取資料時鎖定|  
|**Adlockreadonly**|-其他使用者能夠存取資料|-可以變更資料由多個使用者一次|
