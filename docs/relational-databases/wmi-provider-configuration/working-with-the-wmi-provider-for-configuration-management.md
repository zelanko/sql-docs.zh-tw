---
title: 使用組態管理的 WMI 提供者 |Microsoft Docs
ms.custom: ''
ms.date: 04/12/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
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
ms.openlocfilehash: 20a34f01908333650a4c5b566ccab2221a4e07c2
ms.sourcegitcommit: acb5de9f493238180d13baa302552fdcc30d83c0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/12/2019
ms.locfileid: "59542118"
---
# <a name="working-with-the-wmi-provider-for-configuration-management"></a>針對組態管理使用 WMI 提供者

[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

本文章提供有關如何搭配 WMI 提供者的程式的指導方針，針對電腦管理。

## <a name="binding"></a>繫結  
 組態管理的 WMI 提供者是 COM 物件模型，而且可支援早期和晚期繫結。 藉由晚期繫結，您可以使用指令碼語言 (例如 VBScript) 透過程式設計的方式來操作 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務、網路設定和別名。  
  
## <a name="specifying-a-connection-string"></a>指定連接字串

應用程式會藉由連接到組態管理的 WMI 提供者所定義的 WMI 命名空間，將該提供者導向 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體。 Windows WMI 服務將此命名空間對應至提供者 DLL，並將 DLL 載入到記憶體。 所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體都會以單一的 WMI 命名空間代表。

命名空間預設值為下列格式。 格式，`VV`是 SQL Server 主要版本號碼。 藉由執行的數字是可探索`SELECT @@VERSION;`。

```console
\\.\root\Microsoft\SqlServer\ComputerManagementVV
```

當您使用 PowerShell 連接，前置`\\.\`必須移除。 例如，下列 PowerShell 程式碼列出所有 WMI 類別適用於 SQL Server 2016 中，這是主要第 13 版。

```powershell
Get-WmiObject -Namespace 'root\Microsoft\SqlServer\ComputerManagement13' -List
```

<!--
Updated this on 2019-04-12, per:
   ~ https://github.com/MicrosoftDocs/sql-docs/issues/1817
   ~ https://github.com/rrg92/sql-docs/commit/3d518bfc0d55f819c762abc3e5c5c9eed85abe94?diff=unified

Thus from here I (GeneMi = MightyPen) removed the following text about 'instance_name':

'root\Microsoft\SqlServer\ComputerManagement13\instance_name'

where `instance_name` defaults to `MSSQLSERVER` in a default installation of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
-->

您可以使用下列 PowerShell 程式碼來查詢所有可用的 WMI ComputerManagement 命名空間。

```powershell
gwmi -ns 'root\Microsoft\SqlServer' __NAMESPACE | ? {$_.name -match 'ComputerManagement' } | select name
```

 **注意：** 如果您透過 Windows 防火牆連線，您必須先確定您的電腦均正確無誤。 請參閱 「 連線透過 Windows 防火牆 」 文章中的 Windows Management Instrumentation 文件上[!INCLUDE[msCoName](../../includes/msconame-md.md)]MSDN[網站](https://go.microsoft.com/fwlink/?linkid=15426)。  
  
## <a name="permissions-and-server-authentication"></a>權限和伺服器驗證  
 若要存取組態管理的 WMI 提供者，用戶端 WMI 管理指令碼必須在目標電腦的管理員內容中執行。 您在要管理的電腦上必須是本機 Windows 管理員群組的成員。  
  
 管理員可以設定群組原則，以控制使用者對 WMI 提供者的存取。 如需有關設定群組原則的詳細資訊，請參閱 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員說明中的＜群組原則和 MMC＞。  
  
 WMI 管理指令碼可用來更新用來執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務的帳戶。  
  
 安全性憑證受到組態管理的 WMI 提供者支援。 如需有關憑證的詳細資訊，請參閱 <<c0> [ 加密階層](../../relational-databases/security/encryption/encryption-hierarchy.md)。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server 組態管理員](../../relational-databases/sql-server-configuration-manager.md)  
  
  
