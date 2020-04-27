---
title: osql 不再支援 ED 和 !! 命令 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- ED command
- osql utility [SQL Server]
- '!! command'
ms.assetid: 7cc2852f-94e8-4292-9326-c3f1a1acd281
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 6ce7bfa0bbeec5c5ca83b7139f0ff28e3994021d
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "66093720"
---
# <a name="osql-no-longer-supports-the-ed-and--commands"></a>osql 不再支援 ED 和 !! 命令
  **Osql**公用程式不支援**ED**和 **！！** 指令.  
  
## <a name="corrective-action"></a>更正動作  
 移除**ED**和 **！！** 的參考 腳本中的命令。  
  
 如果您想要使用**ED**和 **！！** 命令，請使用**sqlcmd**公用程式，而不是**osql**。  
  
## <a name="see-also"></a>另請參閱  
 [資料庫引擎升級問題](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 Upgrade Advisor &#91;新的&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
