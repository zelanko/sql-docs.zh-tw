---
title: MSSQLSERVER_41301 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 41301 (Database Engine error)
ms.assetid: c6127e1e-2846-4ee9-bc42-2d896ea9730e
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: eefac3ed02e97aff727c6741190a81a5973c0e15
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62914004"
---
# <a name="mssqlserver41301"></a>MSSQLSERVER_41301
    
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|事件識別碼|41301|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|COMMIT_DEPENDENCY_FAILURE|  
|訊息文字|目前交易具有相依性的先前交易已經中止，而且目前交易無法再認可。|  
  
## <a name="explanation"></a>說明  
 交易發生相依性失敗，現在注定要失敗。  
  
 相依交易過多可能也會造成這個錯誤。 任何寫入交易都可能具有有限數目的相依交易。 例如，如果太多讀取交易嘗試相依於更新交易，就可能會發生這個錯誤。  
  
## <a name="user-action"></a>使用者動作  
 請勿在交易中執行任何工作。 呼叫 ROLLBACK TRAN 回復交易。 如需詳細資訊，請參閱[記憶體內部 OLTP &#40;記憶體內部最佳化&#41;](../in-memory-oltp/in-memory-oltp-in-memory-optimization.md)。  
  
## <a name="see-also"></a>另請參閱  
 [啟用和停用 AlwaysOn 可用性群組 &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/enable-and-disable-always-on-availability-groups-sql-server.md)  
  
  
