---
title: SQL Server Agent 服務無法使用 SQL Server 驗證 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- authentication [SQL Server Agent]
- SQL Server Authentication [SQL Server Agent]
ms.assetid: c39f3ec3-fc2c-4c12-940f-60d8d3d17660
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 32188b1c47168aefbca914fa15f71850df716153
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85036251"
---
# <a name="sql-server-agent-service-cannot-use-sql-server-authentication"></a>SQL Server Agent 服務無法使用 SQL Server 驗證
  當 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理程式服務連接至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體時，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理程式只支援 Windows 驗證。  
  
## <a name="component"></a>元件  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent  
  
## <a name="description"></a>描述  
 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理程式服務只可以使用 Windows 驗證來登入資料庫。 這表示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理程式服務帳戶必須是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用者。  
  
 如需詳細資訊，請參閱《[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 線上叢書》中的＜自動系統管理安全性＞和＜實作 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理程式安全性＞主題。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Agent 升級問題](../../../2014/sql-server/install/sql-server-agent-upgrade-issues.md)  
  
  
