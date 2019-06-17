---
title: 資料指標和鎖定的特性 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: a3a206a21cf7c6680a656c89c48b8f52d1069d78
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66702112"
---
# <a name="cursor-and-lock-characteristics"></a>資料指標與鎖定的特性
資料指標的特性，取決於提供者的能力，雖然下列優點和缺點通常適用於各種類型的資料指標和鎖定。  
  
|資料指標或鎖定類型|優點|缺點|  
|-------------------------|----------------|-------------------|  
|**adOpenForwardOnly**|-低的資源需求|-無法向右捲動<br />-沒有資料的並行|  
|**adOpenStatic**|-   Scrollable|-沒有資料的並行|  
|**adOpenKeyset**|-部分的資料並行<br />-   Scrollable|-較高的資源需求<br />-在中斷連線無法使用|  
|**adOpenDynamic**|-高效的資料並行<br />-   Scrollable|-最高的資源需求<br />-在中斷連線無法使用|  
|**adLockReadOnly**|-低的資源需求<br />-具有高擴充性|資料無法透過資料指標更新|  
|**adLockBatchOptimistic**|批次更新<br />-允許中斷連線的狀況<br />-其他使用者能夠存取資料|資料可以變更多個使用者一次|  
|**adLockPessimistic**|其他使用者鎖定時無法變更資料|-可以防止其他使用者存取資料時鎖定|  
|**adLockOptimistic**|-其他使用者能夠存取資料|資料可以變更多個使用者一次|
