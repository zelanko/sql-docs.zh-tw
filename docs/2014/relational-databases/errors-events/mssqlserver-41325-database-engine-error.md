---
title: MSSQLSERVER_41325 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 41325 (Database Engine error)
ms.assetid: 97c6a8bb-139a-44f3-9ed5-f46d047e8ed3
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: a79a8c63fa20aba4d1e64c8e8222b4899e5cb050
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/21/2020
ms.locfileid: "86551433"
---
# <a name="mssqlserver_41325"></a>MSSQLSERVER_41325
    
## <a name="details"></a>詳細資料  
  
|屬性|值|  
|-|-|  
|產品名稱|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|事件識別碼|41325|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|HK_TX_COMMIT_SR_VALIDATION|  
|訊息文字|目前的交易無法認可，因為可序列化驗證失敗。|  
  
## <a name="explanation"></a>說明  
 交易發生驗證失敗，現在注定要失敗。  
  
## <a name="user-action"></a>使用者動作  
 請重試失敗的交易。 如需詳細資訊，請參閱[記憶體內部 OLTP &#40;記憶體內部最佳化&#41;](../in-memory-oltp/in-memory-oltp-in-memory-optimization.md)。  
  
## <a name="see-also"></a>另請參閱  
 [記憶體內部 OLTP &#40;記憶體內部最佳化&#41;](../in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
