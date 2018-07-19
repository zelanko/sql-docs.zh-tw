---
title: SqlTriggerContext 物件 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: clr
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SqlTriggerContext object
- triggers [CLR integration]
- context [CLR integration]
ms.assetid: 472a2d0b-64ae-4877-8f11-a5620aa698b7
caps.latest.revision: 18
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: ff176908a3ef66f9c1d14d1c5a695932075e8735
ms.sourcegitcommit: 022d67cfbc4fdadaa65b499aa7a6a8a942bc502d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/03/2018
ms.locfileid: "37353270"
---
# <a name="sqltriggercontext-object"></a>SqlTriggerContext 物件
  `SqlTriggerContext` 類別會提供觸發程序的內容資訊。 此內容相關資訊包括會造成引發觸發程序的動作類型 (已在 UPDATE 作業中修改其資料行)，而且若是資料定義語言 (DDL) 觸發程序，則包括描述觸發作業的 XML `EventData` 結構。 如需詳細資訊和範例，示範如何使用`SqlTriggerContext`類別，請參閱[CLR 觸發程序](../../database-engine/dev-guide/clr-triggers.md)。  
  
 如需詳細資訊，請參閱 .NET Framework SDK 文件集中的 `Microsoft.SqlServer.Server.SqlTriggerContext` 類別參考文件集。  
  
## <a name="see-also"></a>另請參閱  
 [CLR 觸發程序](../../database-engine/dev-guide/clr-triggers.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](/sql/t-sql/functions/eventdata-transact-sql)  
  
  
