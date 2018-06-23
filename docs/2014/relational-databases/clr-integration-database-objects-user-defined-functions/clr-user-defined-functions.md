---
title: CLR 使用者定義函數 |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- building database objects [CLR integration], user-defined functions
- functions [CLR integration]
- common language runtime [SQL Server], user-defined functions
- database objects [CLR integration], user-defined functions
- user-defined functions [CLR integration]
ms.assetid: 6f7491f1-9a46-4146-ae09-056248634de2
caps.latest.revision: 45
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: dd7a5d10a15b7072aced0c20b31193e3370488b9
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36030542"
---
# <a name="clr-user-defined-functions"></a>CLR 使用者定義函數
  使用者定義函數是可以使用參數、執行計算或其他動作，並傳回結果的常式。 從 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 開始，您可以使用任何 [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework 程式設計語言 (例如，[!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic .NET 或 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C#) 撰寫使用者定義函數。  
  
 函數有兩種類型：傳回單一值的純量值函式，以及傳回一組資料列的資料表值函式。  
  
 下表列出本節的主題。  
  
 [CLR 純量值函式](clr-scalar-valued-functions.md)  
 涵蓋純量值函式的實作需求與範例。  
  
 [CLR 資料表值函式](clr-table-valued-functions.md)  
 討論如何實作與使用資料表值函式 (TVF)，以及 [!INCLUDE[tsql](../../includes/tsql-md.md)] 和 Common Language Runtime (CLR) TVF 之間的差異。  
  
 [CLR 使用者定義彙總](clr-user-defined-aggregates.md)  
 描述如何實作及使用使用者定義彙總。  
  
## <a name="see-also"></a>另請參閱  
 [使用者定義的函式](../user-defined-functions/user-defined-functions.md)  
  
  