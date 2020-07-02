---
title: CLR 使用者定義匯總 |Microsoft Docs
description: SQL Server CLR 整合可讓您在 managed 程式碼中建立自訂彙總函式，以執行一組值的計算並傳回值。
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
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
ms.openlocfilehash: 6775e9f4bda98f970fd5cdb666fb0bfdb8c1ac10
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85727875"
---
# <a name="clr-user-defined-aggregates"></a>CLR 使用者定義彙總
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  彙總函式會根據一組值來執行計算，再傳回單一值。 傳統 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 上，只支援在一組輸入純量值上運作的內建彙總函式（例如**SUM**或**MAX**），並從該集合產生單一匯總值。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 與 [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework Common Language Runtime (CLR) 的整合現在可讓開發人員以 Managed 程式碼建立自訂彙總函式，並讓這些函式可以存取 [!INCLUDE[tsql](../../includes/tsql-md.md)] 或其他 Managed 程式碼。  
  
 下表列出本節的主題。  
  
 [CLR 使用者定義彙總的需求](../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-aggregates-requirements.md)  
 提供實作 CLR 使用者定義彙總函式之需求的概觀。  
  
 [叫用 CLR 使用者定義彙總函式](../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-aggregate-invoking-functions.md)  
 說明如何叫用使用者定義彙總。  
  
  
