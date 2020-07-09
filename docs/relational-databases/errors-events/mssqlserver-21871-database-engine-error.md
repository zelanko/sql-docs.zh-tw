---
title: MSSQLSERVER_21871 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 21871 (Database Engine error)
ms.assetid: d3215378-9282-444f-a18b-00b96fd0133d
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: d2dd09da4c151119eb4b7fdf9acceb82fdedf383
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85780537"
---
# <a name="mssqlserver_21871"></a>MSSQLSERVER_21871
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>詳細資料  
  
| 屬性 | 值 |  
| :-------- | :---- |  
|產品名稱|SQL Server|  
|事件識別碼|21871|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|SQLErrorNum21871|  
|訊息文字|尚未重新導向資料庫 %s 的發行者 %s。|  
  
## <a name="explanation"></a>說明  
**sp_validate_replica_hosts_as_publishers** 會檢查散發資料庫中的 MSredirected_publishers 資料表，是否存在已識別發行者和發行者資料庫的項目。  **sp_validate_replica_hosts_as_publishers** 找不到任何項目時， 就會傳回錯誤 21871。  
  
## <a name="user-action"></a>使用者動作  
**sp_validate_replica_hosts_as_publishers** 只與重新導向的發行者有關。 如果發行者資料庫是可用性群組的成員，請使用 **sp_redirect_publisher** 預存程序，將發行者和發行者資料庫與可用性群組的可用性群組接聽程式名稱建立關聯。  
  
