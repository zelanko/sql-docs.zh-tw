---
title: MSSQLSERVER_17084 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: errors-events
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 17084 (Database Engine error)
ms.assetid: e579d104-3307-4edd-8587-b14ecbc02ed9
caps.latest.revision: 7
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: d033a32485b9fe5e4da7ed9cbc7589083d92485b
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2018
---
# <a name="mssqlserver17084"></a>MSSQLSERVER_17084
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
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
**ATOMIC** 區塊需要 **WITH** 選項 **TRANSACTION ISOLATION LEVEL** 和 **LANGUAGE** 的值。 例如：  
  
```  
BEGIN ATOMIC WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE= N’us_english’)  
```  
  
如需詳細資訊，請參閱[記憶體內部 OLTP &#40;記憶體內部最佳化&#41;](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)。  
  
## <a name="see-also"></a>另請參閱  
[記憶體內部 OLTP &#40;記憶體內部最佳化&#41;](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
