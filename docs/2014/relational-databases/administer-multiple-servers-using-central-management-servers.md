---
title: 使用中央管理伺服器管理多部伺服器 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- multiserver queries
- central management server
- multiserver administration [SQL Server]
- master servers [SQL Server], central management servers
- target configuration [SQL Server]
- server configuration [SQL Server]
ms.assetid: 427911a7-57d4-4542-8846-47c3267a5d9c
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 62a954706d2e96cc83214df8c532994776b1be3f
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48205308"
---
# <a name="administer-multiple-servers-using-central-management-servers"></a>使用中央管理伺服器管理多部伺服器
  您可以透過指定中央管理伺服器並建立伺服器群組來管理多部伺服器。  
  
## <a name="benefits-of-central-management-servers-and-server-groups"></a>中央管理伺服器和伺服器群組的優點  
 指定為中央管理伺服器的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體，會針對一個或多個 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體維護含有連接資訊的伺服器群組。 您可以針對伺服器群組同時執行 [!INCLUDE[tsql](../includes/tsql-md.md)] 陳述式和以原則為基礎的管理原則。 您也可以在透過中央管理伺服器所管理的執行個體上檢視 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 記錄檔。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 之前的 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] 版本無法指定為中央管理伺服器。  
  
 [!INCLUDE[tsql](../includes/tsql-md.md)] 陳述式。  
  
### <a name="related-tasks"></a>相關工作  
 若要建立中央管理伺服器和伺服器群組，請使用 **中的** [已註冊的伺服器] [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]視窗。 請注意，中央管理伺服器不可以是它所維護之群組的成員。 如需如何建立中央管理伺服器和伺服器群組的詳細資訊，請參閱[建立中央管理伺服器和伺服器群組 &#40;SQL Server Management Studio&#41;](../ssms/register-servers/create-a-central-management-server-and-server-group.md)。  
  
## <a name="see-also"></a>另請參閱  
 [使用原則式管理來管理伺服器](policy-based-management/administer-servers-by-using-policy-based-management.md)  
  
  
