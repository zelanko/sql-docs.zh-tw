---
title: CLR 使用者定義彙總 |Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: clr
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- aggregate functions [CLR integration]
- custom aggregates [CLR integration]
- calculations [CLR integration]
- user-defined functions [CLR integration]
ms.assetid: bad9b7e8-5967-4afa-8dc8-6d840faf9372
caps.latest.revision: 35
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 23e17d38fdd38b398519457a64d0fc61115ad54a
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32918013"
---
# <a name="clr-user-defined-aggregates"></a>CLR 使用者定義彙總
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  彙總函式會根據一組值來執行計算，再傳回單一值。 傳統上， [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]已支援的只有內建彙總函式，例如**總和**或**MAX**，一組輸入純量值上運作，而且產生的單一彙總值的設定。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 與 [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework Common Language Runtime (CLR) 的整合現在可讓開發人員以 Managed 程式碼建立自訂彙總函式，並讓這些函式可以存取 [!INCLUDE[tsql](../../includes/tsql-md.md)] 或其他 Managed 程式碼。  
  
 下表列出本節的主題。  
  
 [CLR 使用者定義彙總的需求](../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-aggregates-requirements.md)  
 提供實作 CLR 使用者定義彙總函式之需求的概觀。  
  
 [叫用 CLR 使用者定義彙總函式](../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-aggregate-invoking-functions.md)  
 說明如何叫用使用者定義彙總。  
  
  
