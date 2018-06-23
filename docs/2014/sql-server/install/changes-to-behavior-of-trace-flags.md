---
title: 追蹤旗標的行為變更 |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- trace flags [SQL Server], behavior changes
ms.assetid: d739df96-2659-4383-8e10-194657632526
caps.latest.revision: 25
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: f03a9db47c6296e7d1c4ab764488c44d343393c7
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36037386"
---
# <a name="changes-to-behavior-of-trace-flags"></a>追蹤旗標之行為的變更
  工作階段所設定的全域追蹤旗標會立即在其他工作階段中生效。 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 的某些追蹤旗標不存在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中。  
  
## <a name="component"></a>元件  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>描述  
 我們建議您在升級之前停用所有追蹤旗標。 修改資料庫可用性或復原模式的追蹤旗標可能會導致[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssDE](../../includes/ssde-md.md)]無法成功升級您的執行個體[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 在您確認這些追蹤旗標是必要的，而且在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中仍然有效之後，就可以啟用這些追蹤旗標。 如果您必須重新啟用追蹤旗標，就應該在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體上執行其他測試。  
  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 支援全域和工作階段層級追蹤旗標。 在 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 中，您可以在 DBCC TRACEON 命令中使用其他引數 (-1)，將追蹤旗標指定為本機或全域。 如果沒有指定這個引數，預設值就是本機。  
  
 此外，在 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 中，在工作階段 A 中設定的旗標不會自動在已經存在的工作階段 B 中生效。相反地，只有第一次在工作階段 B 中設定追蹤旗標之後，該追蹤旗標才會生效。這個行為在 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 中不具決定性，而在 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 和更新版本中則具決定性，因為在工作階段 A 中設定的全域追蹤旗標會立即在其他並行工作階段中設定。  
  
## <a name="see-also"></a>另請參閱  
 [Database Engine 升級問題](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 Upgrade Advisor&#91;新&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  
