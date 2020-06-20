---
title: CLR 使用者定義匯總 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- aggregate functions [CLR integration]
- custom aggregates [CLR integration]
- calculations [CLR integration]
- user-defined functions [CLR integration]
ms.assetid: bad9b7e8-5967-4afa-8dc8-6d840faf9372
author: rothja
ms.author: jroth
ms.openlocfilehash: d1ef5d07fe082d0eeb2c3484d6e99572d8fc80e5
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84954607"
---
# <a name="clr-user-defined-aggregates"></a>CLR 使用者定義彙總
  彙總函式會根據一組值來執行計算，再傳回單一值。 傳統上， [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 僅支援內建的彙總函式（例如 `SUM` 或），該函式 `MAX` 會在一組輸入純量值上運作，並從該集合產生單一匯總值。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 與 [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework Common Language Runtime (CLR) 的整合現在可讓開發人員以 Managed 程式碼建立自訂彙總函式，並讓這些函式可以存取 [!INCLUDE[tsql](../../includes/tsql-md.md)] 或其他 Managed 程式碼。  
  
 下表列出本節的主題。  
  
 [CLR 使用者定義彙總的需求](clr-user-defined-aggregates-requirements.md)  
 提供實作 CLR 使用者定義彙總函式之需求的概觀。  
  
 [叫用 CLR 使用者定義彙總函式](clr-user-defined-aggregate-invoking-functions.md)  
 說明如何叫用使用者定義彙總。  
  
  
