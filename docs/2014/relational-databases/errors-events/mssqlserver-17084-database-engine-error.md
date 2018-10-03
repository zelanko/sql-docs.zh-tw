---
title: MSSQLSERVER_17084 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 17084 (Database Engine error)
ms.assetid: e579d104-3307-4edd-8587-b14ecbc02ed9
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 8b3796b97b92c56618e1b9fa98198f83206c825d
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48215638"
---
# <a name="mssqlserver17084"></a>MSSQLSERVER_17084
    
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|事件識別碼|17084|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|P3_ATOMIC_WITH_MISSING_OPTION|  
|訊息文字|BEGIN ATOMIC 陳述式的 WITH 子句必須指定選項 '%ls' 的值。|  
  
## <a name="explanation"></a>說明  
 BEGIN ATOMIC 陳述式的 WITH 子句未指定選項的值。  
  
## <a name="user-action"></a>使用者動作  
 `ATOMIC` 區塊需要 `WITH` 選項 `TRANSACTION ISOLATION LEVEL` 和 `LANGUAGE` 的值。 例如：  
  
```  
BEGIN ATOMIC WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE= N’us_english’)  
```  
  
 如需詳細資訊，請參閱[記憶體內部 OLTP &#40;記憶體內部最佳化&#41;](../in-memory-oltp/in-memory-oltp-in-memory-optimization.md)。  
  
## <a name="see-also"></a>另請參閱  
 [記憶體內部 OLTP &#40;記憶體內部最佳化&#41;](../in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
