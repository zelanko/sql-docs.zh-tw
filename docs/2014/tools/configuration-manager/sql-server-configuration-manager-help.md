---
title: SQL Server 設定管理員說明 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Configuration Manager, help
ms.assetid: 6e909911-39a6-469b-b22a-3afdfd08a30b
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a9968f22db053bf12a28e3e491817a2c3ac23008
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "68186762"
---
# <a name="sql-server-configuration-manager-help"></a>SQL Server 組態管理員說明
  您可以使用「 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員」來設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務以及設定網路連接性。 若要建立或管理資料庫物件、設定安全性以及撰寫 [!INCLUDE[tsql](../../includes/tsql-md.md)] 查詢，請使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。 如需有關 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]的詳細資訊，請參閱《 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 線上叢書》。  
  
 本節包含關於「 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員」中對話方塊的 F1 說明主題。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員無法設定早於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]版本。  
  
## <a name="services"></a>服務  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員」可用來管理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 雖然大部分的工作可以使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 的 [Windows 服務] 對話方塊來完成，但請特別注意，「 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員」可對其所管理的服務執行其他作業，如在服務帳戶變更時套用正確的權限。 使用一般的 [Windows 服務] 對話方塊來設定任一 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務可能會導致服務異常。  
  
 您可以使用「 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員」來執行下列服務工作：  
  
-   啟動、停止與暫停服務  
  
-   將服務設定為自動或手動啟動、停用服務，或變更其他服務設定  
  
-   變更 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務使用的帳戶密碼  
  
-   使用追蹤旗標 (命令列參數) 啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
-   檢視服務屬性  
  
## <a name="sql-server-network-configuration"></a>SQL Server 網路組態  
 您可以使用「 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員」來執行此電腦上與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務相關的下列工作：  
  
-   啟用或停用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 網路通訊協定  
  
-   設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 網路通訊協定  
  
> [!NOTE]  
>  如需有關如何設定通訊協定並連線到 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 的簡要教學課程，請參閱[教學課程：Database Engine 使用者入門](../../relational-databases/tutorial-getting-started-with-the-database-engine.md)。  
  
## <a name="sql-server-native-client-configuration"></a>SQL Server Native Client 組態  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 用戶端使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 網路程式庫連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 您可以使用「 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員」執行與此電腦用戶端應用程式相關的下列工作：  
  
-   針對此電腦上的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 用戶端應用程式，指定連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體時要使用的通訊協定順序。  
  
-   設定用戶端連接通訊協定。  
  
-   針對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 用戶端應用程式，建立 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體的別名，使用戶端可以用自訂的連接字串來連接。  
  
 如需有關這些工作的詳細資訊，請參閱各項工作的 F1 說明。  
  
#### <a name="to-open-sql-server-configuration-manager"></a>若要開啟 SQL Server 組態管理員  
  
-   在 [開始]  功能表上，依序指向 [所有程式]  、[Microsoft SQL Server]  (版本) 和 [組態工具]  ，然後按一下 [SQL Server 組態管理員]  。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server 服務](../../../2014/tools/configuration-manager/sql-server-services.md)   
 [SQL Server 網路組態](sql-server-network-configuration.md)   
 [SQL Native Client 11.0 組態](../../../2014/tools/configuration-manager/sql-native-client-11-0-configuration.md)   
 [選擇網路通訊協定](../../../2014/tools/configuration-manager/choosing-a-network-protocol.md)  
  
  
