---
title: MSSQLSERVER_15599 | Microsoft Docs
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
helpviewer_keywords: 15599 (Database Engine error)
ms.assetid: 97e427a9-8587-46ea-954b-974b5df9c223
caps.latest.revision: "8"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 52017ed6cc9280cb122f84e6ef0b0e884fe5f8ed
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="mssqlserver15599"></a>MSSQLSERVER_15599
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|15599|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|SEC_LOCAL_TEMP_AUDIT_PERMISSIONS|  
|訊息文字|本機暫存物件上不能設定稽核與權限。|  
  
## <a name="explanation"></a>說明  
為本機或全域暫存物件設定稽核與權限不會有任何作用。 陳述式不會產生錯誤 (作業將回報成功)，但不會有任何作用。  
  
此行為尚未改變，但從 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 起，使用者將會看到此訊息文字警示。  
  
## <a name="user-action"></a>使用者動作  
無須採取任何動作，但可考慮移除所有嘗試為本機或全域暫存物件設定稽核或權限的陳述式。  
  
