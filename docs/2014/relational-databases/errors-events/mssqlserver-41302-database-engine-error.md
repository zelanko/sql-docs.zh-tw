---
title: MSSQLSERVER_41302 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- 41302 (Database Engine error)
ms.assetid: 01e75618-afec-4232-ba68-93ab7bc31003
caps.latest.revision: 7
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 0a04955a6aa51872362485965fc7f0bd385680bd
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36036124"
---
# <a name="mssqlserver41302"></a>MSSQLSERVER_41302
    
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|事件識別碼|41302|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|WRITE_WRITE_CONFLICT|  
|訊息文字|目前交易嘗試更新自從此交易啟動以來已經更新的記錄。 交易已中止。|  
  
## <a name="explanation"></a>說明  
 交易發生寫入/寫入衝突，陳述式已結束。  
  
## <a name="user-action"></a>使用者動作  
 稍後在其他交易中重試作業。 如需詳細資訊，請參閱[記憶體內部 OLTP &#40;記憶體內部最佳化&#41;](../in-memory-oltp/in-memory-oltp-in-memory-optimization.md)。  
  
## <a name="see-also"></a>另請參閱  
 [記憶體內部 OLTP &#40;記憶體內部最佳化&#41;](../in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  