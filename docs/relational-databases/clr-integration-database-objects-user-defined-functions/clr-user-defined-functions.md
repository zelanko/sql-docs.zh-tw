---
title: CLR 使用者定義的功能 |微軟文件
description: SQL Server CLR 集成允許您在任何 .NET 框架程式設計語言中創建使用者定義的標量值、表值和聚合函數。
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- building database objects [CLR integration], user-defined functions
- functions [CLR integration]
- common language runtime [SQL Server], user-defined functions
- database objects [CLR integration], user-defined functions
- user-defined functions [CLR integration]
ms.assetid: 6f7491f1-9a46-4146-ae09-056248634de2
author: rothja
ms.author: jroth
ms.openlocfilehash: 0da524de3a21a97daf6e3b2d2e0277631a4467c0
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2020
ms.locfileid: "81488267"
---
# <a name="clr-user-defined-functions"></a>CLR 使用者定義函數
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  使用者定義函數是可以使用參數、執行計算或其他動作，並傳回結果的常式。 從 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 開始，您可以使用任何 [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework 程式設計語言 (例如，[!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic .NET 或 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C#) 撰寫使用者定義函數。  
  
 函數有兩種類型：傳回單一值的純量值函式，以及傳回一組資料列的資料表值函式。  
  
 下表列出本節的主題。  
  
 [CLR 純量值函式](../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-scalar-valued-functions.md)  
 涵蓋純量值函式的實作需求與範例。  
  
 [CLR 資料表值函式](../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-table-valued-functions.md)  
 討論如何實作與使用資料表值函式 (TVF)，以及 [!INCLUDE[tsql](../../includes/tsql-md.md)] 和 Common Language Runtime (CLR) TVF 之間的差異。  
  
 [CLR 使用者定義彙總](../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-aggregates.md)  
 描述如何實作及使用使用者定義彙總。  
  
## <a name="see-also"></a>另請參閱  
 [使用者定義的函數](../../relational-databases/user-defined-functions/user-defined-functions.md)  
  
  
