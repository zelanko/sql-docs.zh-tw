---
title: SqlTrigger上下文物件 |微軟文件
description: 在 SQL Server CLR 整合中,SqlTriggerContext 類為觸發器提供上下文資訊,包括操作類型和在操作中修改的列。
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- SqlTriggerContext object
- triggers [CLR integration]
- context [CLR integration]
ms.assetid: 472a2d0b-64ae-4877-8f11-a5620aa698b7
author: rothja
ms.author: jroth
ms.openlocfilehash: 55e0ac850071615d9be7fb47442ed674eefab00a
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2020
ms.locfileid: "81487457"
---
# <a name="sqltriggercontext-object"></a>SqlTriggerContext 物件
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  **SqlTriggerContext**類提供有關觸發器的上下文資訊。 此上下文資訊包括導致觸發器觸發的操作類型、更新操作中修改的列,以及數據定義語言 (DDL) 觸發器(描述觸發操作的 XML EventData 結構)中的 XML **EventData**結構。 有關如何使用**SqlTriggerContext**類別的詳細資訊和範例,請參考[CLR 觸發器](https://msdn.microsoft.com/library/302a4e4a-3172-42b6-9cc0-4a971ab49c1c)。  
  
 有關詳細資訊,請參閱 .NET 框架 SDK 文檔中的**Microsoft.SqlServer.Server.SqlTriggerContext**類引用文檔。  
  
## <a name="see-also"></a>另請參閱  
 [CLR 觸發器](https://msdn.microsoft.com/library/302a4e4a-3172-42b6-9cc0-4a971ab49c1c)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
