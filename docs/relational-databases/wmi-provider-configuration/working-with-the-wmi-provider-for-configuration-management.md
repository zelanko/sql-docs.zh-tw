---
title: "使用組態管理的 WMI 提供者 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: wmi
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- permissions [WMI]
- connection strings [WMI]
- security [WMI]
- WMI Provider for Configuration Management, connection strings
- WMI Provider for Configuration Management, security
- late binding [WMI]
- WMI Provider for Configuration Management, late binding
- binding [WMI]
ms.assetid: 34daa922-7074-41d0-9077-042bb18c222a
caps.latest.revision: "25"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 672720d9c807d2b8eef78a5c0f0b3865679738bb
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="working-with-the-wmi-provider-for-configuration-management"></a>針對組態管理使用 WMI 提供者
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]請考慮針對電腦管理的 WMI 提供者進行程式設計前下列：  
  
## <a name="binding"></a>繫結  
 組態管理的 WMI 提供者是 COM 物件模型，而且可支援早期和晚期繫結。 藉由晚期繫結，您可以使用指令碼語言 (例如 VBScript) 透過程式設計的方式來操作 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務、網路設定和別名。  
  
 如需程式設計使用指令碼語言的 WMI 提供者實作的進一步資訊，請參閱[!INCLUDE[msCoName](../../includes/msconame-md.md)]MSDN[網站](http://go.microsoft.com/fwlink/?linkid=15426)。  
  
## <a name="specifying-a-connection-string"></a>指定連接字串  
 應用程式會藉由連接到組態管理的 WMI 提供者所定義的 WMI 命名空間，將該提供者導向 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體。 Windows WMI 服務會將此命名空間對應至提供者 DLL 並將其載入記憶體中。 所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體都會以單一的 WMI 命名空間代表。 命名空間預設為  
  
```  
\\.\root\Microsoft\SqlServer\ComputerManagement12\instance_name  
```  
  
 其中 `instance_name` 預設為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 預設安裝中的 `MSSQLSERVER`。  
  
 **注意：**如果您透過 Windows 防火牆，您必須確定已適當地設定您的電腦連接。 請參閱 「 透過 Windows 防火牆連線 」 文件中的 Windows Management Instrumentation 文件上[!INCLUDE[msCoName](../../includes/msconame-md.md)]MSDN[網站](http://go.microsoft.com/fwlink/?linkid=15426)。  
  
## <a name="permissions-and-server-authentication"></a>權限和伺服器驗證  
 若要存取組態管理的 WMI 提供者，用戶端 WMI 管理指令碼必須在目標電腦的管理員內容中執行。 您在要管理的電腦上必須是本機 Windows 管理員群組的成員。  
  
 管理員可以設定群組原則，以控制使用者對 WMI 提供者的存取。 如需有關設定群組原則的詳細資訊，請參閱 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員說明中的＜群組原則和 MMC＞。  
  
 WMI 管理指令碼可用來更新用來執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務的帳戶。  
  
 安全性憑證受到組態管理的 WMI 提供者支援。 如需有關憑證的詳細資訊，請參閱[加密階層](../../relational-databases/security/encryption/encryption-hierarchy.md)。  
  
## <a name="see-also"></a>請參閱  
 [SQL Server 組態管理員](../../relational-databases/sql-server-configuration-manager.md)  
  
  
