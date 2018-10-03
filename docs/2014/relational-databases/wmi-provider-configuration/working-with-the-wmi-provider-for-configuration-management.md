---
title: 使用組態管理的 WMI 提供者 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
- docset-sql-devref
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
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: c2722d608b4f373de92c49f1d75b887c658417e3
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48183234"
---
# <a name="working-with-the-wmi-provider-for-configuration-management"></a>針對組態管理使用 WMI 提供者
  在使用電腦管理的 WMI 提供者進行程式設計之前，請考慮下列事項：  
  
## <a name="binding"></a>繫結  
 組態管理的 WMI 提供者是 COM 物件模型，而且可支援早期和晚期繫結。 藉由晚期繫結，您可以使用指令碼語言 (例如 VBScript) 透過程式設計的方式來操作 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務、網路設定和別名。  
  
 如需程式設計使用指令碼語言的 WMI 提供者實作的進一步資訊，請參閱[!INCLUDE[msCoName](../../includes/msconame-md.md)]MSDN[網站](http://go.microsoft.com/fwlink/?linkid=15426)。  
  
## <a name="specifying-a-connection-string"></a>指定連接字串  
 應用程式會藉由連接到組態管理的 WMI 提供者所定義的 WMI 命名空間，將該提供者導向 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體。 Windows WMI 服務會將此命名空間對應至提供者 DLL 並將其載入記憶體中。 所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體都會以單一的 WMI 命名空間代表。 命名空間預設為  
  
```  
\\.\root\Microsoft\SqlServer\ComputerManagement12\instance_name  
```  
  
 其中 `instance_name` 預設為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 預設安裝中的 `MSSQLSERVER`。  
  
 **注意：** 如果您要連接通過 Windows 防火牆，您必須先確定您的電腦均正確無誤。 請參閱 「 連線透過 Windows 防火牆 」 文章中的 Windows Management Instrumentation 文件上[!INCLUDE[msCoName](../../includes/msconame-md.md)]MSDN[網站](http://go.microsoft.com/fwlink/?linkid=15426)。  
  
## <a name="permissions-and-server-authentication"></a>權限和伺服器驗證  
 若要存取組態管理的 WMI 提供者，用戶端 WMI 管理指令碼必須在目標電腦的管理員內容中執行。 您在要管理的電腦上必須是本機 Windows 管理員群組的成員。  
  
 管理員可以設定群組原則，以控制使用者對 WMI 提供者的存取。 如需有關設定群組原則的詳細資訊，請參閱 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員說明中的＜群組原則和 MMC＞。  
  
 WMI 管理指令碼可用來更新用來執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務的帳戶。  
  
 安全性憑證受到組態管理的 WMI 提供者支援。 如需有關憑證的詳細資訊，請參閱 <<c0> [ 加密階層](../security/encryption/encryption-hierarchy.md)。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server 組態管理員](../sql-server-configuration-manager.md)  
  
  
