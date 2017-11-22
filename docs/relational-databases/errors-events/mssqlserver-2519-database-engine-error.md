---
title: MSSQLSERVER_2519 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: errors-events
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 2519 (Database Engine error)
ms.assetid: 8dc6ad98-5db8-4c88-8dea-6d455e63b839
caps.latest.revision: "18"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 63976b50718522a6bc087c646b8bdc141a785e3d
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="mssqlserver2519"></a>MSSQLSERVER_2519
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|2519|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|DBCC_NO_EXPRESSION_EVALUATOR|  
|訊息文字|無法檢查物件識別碼 O_ID (物件 "O_NAME") 的計算資料行和使用者自訂類型，因為內部運算式評估工具無法初始化。|  
  
## <a name="explanation"></a>說明  
這項參考用訊息指出查詢處理器無法提供 DBCC 與內部物件，以便評估計算資料行和 Common Language Runtime (CLR) 使用者自訂類型。 這表示 DBCC 不會在檢查索引和基底資料表的一致性時檢查計算資料行和 CLR 使用者自訂類型的正確性，或是使用這些使用者自訂類型。  
  
## <a name="user-action"></a>使用者動作  
無  
  
## <a name="see-also"></a>另請參閱  
[MSSQLSERVER_2518](~/relational-databases/errors-events/mssqlserver-2518-database-engine-error.md)  
  
