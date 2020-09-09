---
description: dbo.sysnotifications (Transact-SQL)
title: dbo.sys通知 (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dbo.sysnotifications_TSQL
- sysnotifications
- sysnotifications_TSQL
- dbo.sysnotifications
dev_langs:
- TSQL
helpviewer_keywords:
- sysnotifications system table
ms.assetid: c5150d18-e8b7-48a7-ada7-77c583af6e41
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 8bcfd6b5b52a4f091337d55681be149ccd3f7900
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/08/2020
ms.locfileid: "89540349"
---
# <a name="dbosysnotifications-transact-sql"></a>dbo.sysnotifications (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  針對每項通知，各包含一個資料列。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**alert_id**|**int**|警示的識別碼。|  
|**operator_id**|**int**|這項通知所應送往的操作員識別碼。|  
|**notification_method**|**tinyint**|通知方法：<br /><br /> **1** = 電子郵件<br /><br /> **2** = 呼機<br /><br /> **4**  = **netsend**<br /><br /> **7** = 全部|  
  
  
