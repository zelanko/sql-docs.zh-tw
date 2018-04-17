---
title: 增強式密碼 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: security
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- logins [SQL Server], passwords
- passwords [SQL Server], strong
- symbols [SQL Server]
- security [SQL Server], passwords
- passwords [SQL Server], symbols
- characters [SQL Server], password policies
- strong passwords [SQL Server]
ms.assetid: 338548f4-c4d8-47ca-b597-5c9c0f2fa205
caps.latest.revision: 30
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 7c5b783d4899479523d0e54fda7620ad0145b642
ms.sourcegitcommit: d6b1695c8cbc70279b7d85ec4dfb66a4271cdb10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/10/2018
---
# <a name="strong-passwords"></a>增強式密碼
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  密碼會是伺服器安全性部署中最薄弱的連結。 您在選取密碼的時候，應該始終保持小心謹慎的態度。 增強式密碼具有下列特性：  
  
-   長度至少為 8 個字元。  
  
-   密碼中結合字母、數字和符號字元。  
  
-   在字典中找不到。  
  
-   不是命令名稱。  
  
-   不是個人名稱。  
  
-   不是使用者名稱。  
  
-   不是電腦名稱。  
  
-   經常變更。  
  
-   與先前的密碼完全不同。  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 密碼可以包含最多 128 個字元，可由字母、符號和數字組成。 因為登入、使用者名稱、角色與密碼常用於 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式中，所以某些符號必須以雙引號 (") 或方括號 ([ ]) 括住。 當 [!INCLUDE[tsql](../../includes/tsql-md.md)] 登入、使用者、角色或密碼具有下列特性時，請在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 陳述式中使用這些分隔符號：  
  
-   包含空白字元，或以空白字元開始。  
  
-   以 $ 或 @ 字元開始。  
  
 如果是用在 OLE DB 或 ODBC 連接字串中，則登入或密碼中不能包含下列字元：[] {}() , ; ? * ! @. 這些字元是用來初始化連接或分隔連接值。  
  
## <a name="related-content"></a>相關內容  
 [密碼原則](../../relational-databases/security/password-policy.md)  
  
  
