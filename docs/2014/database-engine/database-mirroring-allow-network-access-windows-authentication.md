---
title: 資料庫鏡像端點的網路存取
description: 瞭解如何允許 SQL Server 的 windows authenticatino 網路存取資料庫鏡像端點。
ms.custom: seo-lt-2019
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Windows authentication [SQL Server]
- database mirroring [SQL Server], security
ms.assetid: 28c8fec5-5feb-4c84-8d72-f2bd1ae3b40d
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e40a1eead54fe9d00eaf099410260023229796d0
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/19/2019
ms.locfileid: "75228571"
---
# <a name="allow-network-access-to-a-database-mirroring-endpoint-using-windows-authentication-sql-server"></a>使用 Windows 驗證允許資料庫鏡像的網路存取 (SQL Server)
  若要將 Windows 驗證用於連接兩個 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體的資料庫鏡像端點，在下列狀況下，需要手動設定登入帳戶：  
  
-   如果 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體會以服務的形式在不同的網域帳戶底下執行 (在相同或受信任的網域中)，您就必須在每個遠端伺服器執行個體的 **master** 中建立每個帳戶的登入，而且該登入必須被授與端點的 CONNECT 權限。  
  
-   如果 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體會以網路服務帳戶的身分執行，您就必須在每個遠端伺服器執行個體的 *master*** 中建立每個主機電腦帳戶的登入 (\\DomainName******ComputerName$** )，而且該登入必須被授與端點的 CONNECT 權限。 這是因為在 Network Service 帳戶底下執行的伺服器執行個體會使用主機電腦的網域帳戶進行驗證。  
  
> [!NOTE]  
>  請確定每個伺服器執行個體都有端點存在。 如需詳細資訊，請參閱[建立 Windows 驗證的資料庫鏡像端點 &#40;Transact-SQL&#41;](database-mirroring/create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md)。  
  
### <a name="to-configure-logins-for-windows-authentication"></a>若要設定 Windows 驗證登入  
  
1.  針對每個 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]執行個體的使用者帳戶，在其他 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]執行個體上建立登入。 將 [CREATE LOGIN](/sql/t-sql/statements/create-login-transact-sql) 陳述式與 FROM WINDOWS 子句搭配使用。  
  
     如需詳細資訊，請參閱 [建立登入](../relational-databases/security/authentication-access/create-a-login.md)。  
  
2.  另外，若要確定登入使用者擁有端點的存取權，請使用 [GRANT](/sql/t-sql/statements/grant-transact-sql) 陳述式將端點上的連接權限授與登入。 請注意，如果使用者是 Administrator，就不需要授與端點的連接權限。  
  
     如需詳細資訊，請參閱 [Grant a Permission to a Principal](../relational-databases/security/authentication-access/grant-a-permission-to-a-principal.md)。  
  
## <a name="example"></a>範例  
 下列 [!INCLUDE[tsql](../includes/tsql-md.md)] 範例會為屬於 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 網域的 `Otheruser` 使用者帳戶建立 `Adomain`登入。 接著，此範例會將預先存在的鏡像資料庫端點 `Mirroring_Endpoint`的連接權限授與此使用者。  
  
```  
USE master;  
GO  
CREATE LOGIN [Adomain\Otheruser] FROM WINDOWS;  
GO  
GRANT CONNECT on ENDPOINT::Mirroring_Endpoint TO [Adomain\Otheruser];  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [AlwaysOn 可用性群組 &#40;SQL Server 的總覽&#41;](availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [資料庫鏡像 &#40;SQL Server&#41;](database-mirroring/database-mirroring-sql-server.md)   
 [資料庫鏡像和 AlwaysOn 可用性群組的傳輸安全性 &#40;SQL Server&#41;](database-mirroring/transport-security-database-mirroring-always-on-availability.md)   
 [資料庫鏡像端點 &#40;SQL Server&#41;](database-mirroring/the-database-mirroring-endpoint-sql-server.md)  
  
  
