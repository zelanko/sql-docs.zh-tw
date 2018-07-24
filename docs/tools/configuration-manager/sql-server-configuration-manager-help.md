---
title: SQL Server 設定管理員說明 | Microsoft Docs
ms.custom: ''
ms.date: 02/01/2018
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.suite: sql
ms.technology: configuration
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Configuration Manager, help
ms.assetid: 6e909911-39a6-469b-b22a-3afdfd08a30b
caps.latest.revision: 28
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 064d6fb77dad0dd906c8783ebe82f99c48b14f2f
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2018
ms.locfileid: "37979974"
---
# <a name="sql-server-configuration-manager-help"></a>SQL Server 組態管理員說明
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
  您可以使用「 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員」來設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務以及設定網路連接性。 若要建立或管理資料庫物件、設定安全性以及撰寫 [!INCLUDE[tsql](../../includes/tsql-md.md)] 查詢，請使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。 如需有關 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]的詳細資訊，請參閱《 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 線上叢書》。  

 > [!TIP]
 > 如果您需要設定[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]在 Linux 上，使用**mssql conf**工具。 如需詳細資訊，請參閱 <<c0> [ 在 Linux 上使用 mssql-conf 工具的 設定 SQL Server](../../linux/sql-server-linux-configure-mssql-conf.md)。

 本節包含關於「 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員」中對話方塊的 F1 說明主題。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager 無法設定早於 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本。  
  
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
>  如需如何設定通訊協定並連接到 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]的簡要教學課程，請參閱 [教學課程：Database Engine 使用者入門](../../relational-databases/tutorial-getting-started-with-the-database-engine.md)。  
  
## <a name="sql-server-native-client-configuration"></a>SQL Server Native Client 組態  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 用戶端使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 網路程式庫連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 您可以使用「 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員」執行與此電腦用戶端應用程式相關的下列工作：  
  
-   針對此電腦上的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 用戶端應用程式，指定連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體時要使用的通訊協定順序。  
  
-   設定用戶端連接通訊協定。  
  
-   針對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 用戶端應用程式，建立 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體的別名，使用戶端可以用自訂的連接字串來連接。  
  
 如需有關這些工作的詳細資訊，請參閱各項工作的 F1 說明。  
  
#### <a name="to-open-sql-server-configuration-manager"></a>若要開啟 SQL Server 組態管理員  
  
-   在 [開始] 功能表上，依序指向 [所有程式]、[Microsoft SQL Server] (版本) 和 [組態工具]，然後按一下 [SQL Server 組態管理員]。  
  
  
 **使用 [!INCLUDE[win8](../../includes/win8-md.md)] 存取 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 設定管理員**  
  
 由於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員是 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Management Console 程式的嵌入式管理單元，而不是單獨的程式，在執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 時並不會出現 [!INCLUDE[win8](../../includes/win8-md.md)] 組態管理員這樣的應用程式。 若要開啟 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 設定管理員，請在 [搜尋] 常用鍵的 [應用程式] 下，鍵入 **SQLServerManager12.msc** (適用於 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]) 或鍵入 **SQLServerManager11.msc** (適用於 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)])，然後按 **Enter**。  
  

## <a name="see-also"></a>另請參閱  
 [SQL Server 服務](../../tools/configuration-manager/sql-server-services.md)   
 [SQL Server 網路設定](../../tools/configuration-manager/sql-server-network-configuration.md)   
 [SQL Native Client 11.0 設定](../../tools/configuration-manager/sql-native-client-11-0-configuration.md)   
 [選擇網路通訊協定](http://msdn.microsoft.com/library/6565fb7d-b076-4447-be90-e10d0dec359a)  
  
  
