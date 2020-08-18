---
description: MSSQLSERVER_15599
title: MSSQLSERVER_15599 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 15599 (Database Engine error)
ms.assetid: 97e427a9-8587-46ea-954b-974b5df9c223
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: eca555fb3ced04a0258db78c89c53e8cef9d9c20
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88333814"
---
# <a name="mssqlserver_15599"></a>MSSQLSERVER_15599
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>詳細資料  
  
| 屬性 | 值 |  
| :-------- | :---- |  
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
  
