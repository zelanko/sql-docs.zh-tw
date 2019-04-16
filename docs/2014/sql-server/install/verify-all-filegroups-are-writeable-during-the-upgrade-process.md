---
title: 確認在升級過程中，所有檔案群組都可寫入 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- filegroups [SQL Server], writeable
- writeable filegroups [SQL Server]
ms.assetid: 2985efc1-4b14-46c3-abbd-a656b159f23c
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 98633674559feead48a5b1c3cbe997863ad0f18a
ms.sourcegitcommit: 46a2c0ffd0a6d996a3afd19a58d2a8f4b55f93de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/15/2019
ms.locfileid: "59583081"
---
# <a name="verify-all-filegroups-are-writeable-during-the-upgrade-process"></a>在升級過程中，確認所有檔案群組都是可寫入的
  Upgrade Advisor 偵測到具有一或多個唯讀檔案群組的資料庫。 在升級之前，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體中的所有資料庫都必須將檔案群組設為 READ_WRITE。  
  
## <a name="component"></a>元件  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="corrective-action"></a>更正動作  
 請使用 ALTER DATABASE 將檔案群組設定為 READ_WRITE。  
  
## <a name="see-also"></a>另請參閱  
 [Database Engine 升級問題](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 Upgrade Advisor&#91;新增&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
