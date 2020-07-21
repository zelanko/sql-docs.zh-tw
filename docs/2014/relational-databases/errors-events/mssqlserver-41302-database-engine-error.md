---
title: MSSQLSERVER_41302 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 41302 (Database Engine error)
ms.assetid: 01e75618-afec-4232-ba68-93ab7bc31003
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 8d872809cb8bddf62424523927eed37b44ec966a
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/21/2020
ms.locfileid: "86551463"
---
# <a name="mssqlserver_41302"></a>MSSQLSERVER_41302
    
## <a name="details"></a>詳細資料  
  
|屬性|值|  
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
  
  
