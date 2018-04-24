---
title: 資料指標及鎖定特性 |Microsoft 文件
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- locks [ADO], characteristics
- adOpenDynamic [ADO]
- cursors [ADO], characteristics
ms.assetid: 459c29cb-4230-42bf-8cc2-f3132ccc7aba
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e843192c1ad00c9e7ef6742938d7dfe3dcc1bd07
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/18/2018
---
# <a name="cursor-and-lock-characteristics"></a>資料指標及鎖定特性
當資料指標的特性，取決於提供者功能時，下列的優點和缺點一般也適用於各種類型的資料指標和鎖定。  
  
|資料指標或鎖定的類型|優點|缺點|  
|-------------------------|----------------|-------------------|  
|**adOpenForwardOnly**|-低的資源需求|-無法向後捲動<br />-沒有資料並行存取|  
|**adOpenStatic**|-   Scrollable|-沒有資料並行存取|  
|**adOpenKeyset**|的某些資料並行存取<br />-   Scrollable|-更新版本的資源需求<br />-無法中斷連接案例中使用|  
|**adOpenDynamic**|-高資料並行存取<br />-   Scrollable|高資源需求<br />-無法中斷連接案例中使用|  
|**adLockReadOnly**|-低的資源需求<br />-具有高擴充性|資料無法透過資料指標更新|  
|**adLockBatchOptimistic**|批次更新<br />-可讓連接中斷的情況<br />-其他使用者能夠存取資料|-可以變更資料由多個使用者一次|  
|**adLockPessimistic**|其他使用者鎖定時無法變更資料|-可以防止其他使用者存取資料時鎖定|  
|**adLockOptimistic**|-其他使用者能夠存取資料|-可以變更資料由多個使用者一次|
