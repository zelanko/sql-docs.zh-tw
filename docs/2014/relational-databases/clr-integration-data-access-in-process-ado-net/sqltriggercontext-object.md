---
title: SqlTriggerCoNtext 物件 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: df384324ba16aac03a4c889cf4f3959c23374510
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "62874695"
---
# <a name="sqltriggercontext-object"></a>SqlTriggerContext 物件
  `SqlTriggerContext` 類別會提供觸發程序的內容資訊。 此內容相關資訊包括會造成引發觸發程序的動作類型 (已在 UPDATE 作業中修改其資料行)，而且若是資料定義語言 (DDL) 觸發程序，則包括描述觸發作業的 XML `EventData` 結構。 如需如何使用`SqlTriggerContext`類別的詳細資訊和範例，請參閱[CLR 觸發](../../database-engine/dev-guide/clr-triggers.md)程式。  
  
 如需詳細資訊，請參閱 .NET Framework SDK 文件集中的 `Microsoft.SqlServer.Server.SqlTriggerContext` 類別參考文件集。  
  
## <a name="see-also"></a>另請參閱  
 [CLR 觸發程式](../../database-engine/dev-guide/clr-triggers.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](/sql/t-sql/functions/eventdata-transact-sql)  
  
  
