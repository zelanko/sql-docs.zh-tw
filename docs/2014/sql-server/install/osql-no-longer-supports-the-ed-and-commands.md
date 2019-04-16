---
title: osql 不再支援 ED 和 !! 命令 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- ED command
- osql utility [SQL Server]
- '!! command'
ms.assetid: 7cc2852f-94e8-4292-9326-c3f1a1acd281
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: fd6c1da0c11c8fa71570dbb7034c885877e22b7a
ms.sourcegitcommit: 46a2c0ffd0a6d996a3afd19a58d2a8f4b55f93de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/15/2019
ms.locfileid: "59581531"
---
# <a name="osql-no-longer-supports-the-ed-and--commands"></a>osql 不再支援 ED 和 !! 命令
  **Osql**公用程式不支援**ED**和 **!!** 命令。  
  
## <a name="corrective-action"></a>更正動作  
 移除參考**ED**和 **!!** 從您的指令碼命令。  
  
 如果您想要使用**ED**和 **!!** 命令，請使用**sqlcmd**公用程式來取代**osql**。  
  
## <a name="see-also"></a>另請參閱  
 [Database Engine 升級問題](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 Upgrade Advisor&#91;新增&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
