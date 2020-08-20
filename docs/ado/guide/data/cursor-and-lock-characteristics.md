---
description: 資料指標與鎖定的特性
title: 資料指標和鎖定特性 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- locks [ADO], characteristics
- adOpenDynamic [ADO]
- cursors [ADO], characteristics
ms.assetid: 459c29cb-4230-42bf-8cc2-f3132ccc7aba
author: rothja
ms.author: jroth
ms.openlocfilehash: f903cdf8feab9b3e6d649f95b33b68c2de107194
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88453590"
---
# <a name="cursor-and-lock-characteristics"></a>資料指標與鎖定的特性
雖然資料指標的特性取決於提供者的功能，但下列優點和缺點通常適用于各種類型的資料指標和鎖定。  
  
|游標或鎖定類型|優點|缺點|  
|-------------------------|----------------|-------------------|  
|**adOpenForwardOnly**|-低資源需求|-無法向後滾動<br />-無資料並行|  
|**adOpenStatic**|-可滾動|-無資料並行|  
|**adOpenKeyset**|-部分資料並行<br />-可滾動|-資源需求較高<br />-在已中斷連線的案例中無法使用|  
|**adOpenDynamic**|-高資料並行<br />-可滾動|-最高資源需求<br />-在已中斷連線的案例中無法使用|  
|**adLockReadOnly**|-低資源需求<br />-可高度擴充|-無法透過資料指標更新資料|  
|**adLockBatchOptimistic**|-批次更新<br />-允許已中斷連線的案例<br />-可存取資料的其他使用者|-多個使用者可以一次變更資料|  
|**adLockPessimistic**|-鎖定時，其他使用者無法變更資料|-防止其他使用者在鎖定時存取資料|  
|**adLockOptimistic**|-可存取資料的其他使用者|-多個使用者可以一次變更資料|
