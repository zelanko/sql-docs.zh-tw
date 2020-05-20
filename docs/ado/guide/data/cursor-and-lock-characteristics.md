---
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
ms.openlocfilehash: 02f4be413ddcfc9215cdbf12142b883ade644f41
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82761114"
---
# <a name="cursor-and-lock-characteristics"></a>資料指標與鎖定的特性
雖然資料指標的特性取決於提供者的功能，但下列優點和缺點通常適用于各種類型的資料指標和鎖定。  
  
|游標或鎖定類型|優點|缺點|  
|-------------------------|----------------|-------------------|  
|**adOpenForwardOnly**|-低資源需求|-無法向後滾動<br />-無資料並行|  
|**adOpenStatic**|-可滾動|-無資料並行|  
|**adOpenKeyset**|-部分資料並行<br />-可滾動|-資源需求較高<br />-在中斷連線的案例中無法使用|  
|**adOpenDynamic**|-高資料並行<br />-可滾動|-最高資源需求<br />-在中斷連線的案例中無法使用|  
|**adLockReadOnly**|-低資源需求<br />-高度可擴充|-資料無法透過資料指標更新|  
|**adLockBatchOptimistic**|-批次更新<br />-允許中斷連線的案例<br />-能夠存取資料的其他使用者|-多個使用者可以一次變更資料|  
|**adLockPessimistic**|-鎖定時，其他使用者無法變更資料|-防止其他使用者在鎖定時存取資料|  
|**adLockOptimistic**|-能夠存取資料的其他使用者|-多個使用者可以一次變更資料|
