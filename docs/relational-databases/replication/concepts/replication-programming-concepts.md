---
title: "複寫程式設計概念 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- replication [SQL Server], planning
- programming [SQL Server replication], planning
- programming [SQL Server replication]
ms.assetid: 2cd846e7-5bf3-4144-8772-703c4f439a2a
caps.latest.revision: 43
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 12b8b87460c4cb21776780af955eeecad3b5cda3
ms.contentlocale: zh-tw
ms.lasthandoff: 07/31/2017

---
# <a name="replication-programming-concepts"></a>複寫程式設計概念
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  在開發使用複寫功能的應用程式之前，您應該遵循下列一般規劃步驟：  
  
1.  定義您的複寫拓撲。  
  
2.  定義應用程式功能。  
  
3.  規劃安全性。  
  
4.  選擇開發環境。  
  
5.  選擇適當的複寫程式設計介面。  
  
 本主題的其餘部分將更詳細地描述這些步驟。 為了說明規劃程序，本主題中還包括範例。  
  
## <a name="defining-the-replication-topology"></a>定義複寫拓撲  
 程式設計複寫中的第一個步驟，是為應用程式定義複寫拓撲。 如果您正在撰寫將使用現有複寫拓撲的應用程式，例如存取現有訂閱者資料的用戶端應用程式，您應該移到下一個步驟。  
  
> [!NOTE]  
>  在某些情況下，部署複寫拓撲將是應用程式的唯一目的。  
  
 您定義的複寫拓撲取決於許多因素，其中包括下列項目：  
  
-   是否需要更新複寫的資料以及由誰來更新。  
  
-   有關您的一致性、自主性和延遲的資料散發需求。  
  
-   複寫環境，包括商務使用者、技術基礎結構、網路與安全性以及資料特性。  
  
-   複寫及複寫選項的類型。  
  
-   複寫拓撲以及它們如何搭配複寫類型使用。  
  
 如果您不熟悉 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 複寫，請參閱[複寫類型](../../../relational-databases/replication/types-of-replication.md)。  
  
## <a name="defining-application-functionality"></a>定義應用程式功能  
 定義好複寫拓撲之後，您應該決定應用程式將提供的功能。 這些功能包括的範圍可從同步處理訂閱的指令碼，到具有使用者介面以設定複寫的應用程式。 複寫支援下列一般程式設計工作：  
  
-   設定複寫。  
  
-   同步處理訂閱者。  
  
-   維護複寫拓撲。  
  
-   監視複寫拓撲。  
  
-   疑難排解複寫。  
  
 透過結合複寫功能與 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 提供的其他功能來擴充應用程式，也是很常見的事。 下表僅挑出一些您可在複寫應用程式中提供的擴充功能。  
  
|功能|範例|  
|-------------------|-------------|  
|使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 管理物件 (SMO) 的伺服器管理|允許管理員在複寫拓撲中將資料庫附加並設定為發行者的應用程式。|  
|使用 ADO.NET 的資料存取|這個應用程式允許使用者在離線時於本機訂閱者資料庫中，以程式設計方式存取和變更複寫的銷售資料，然後按一下按鈕連接和同步處理提取訂閱。|  
  
## <a name="planning-for-security"></a>安全性規劃  
 安全性在任何應用程式中都很重要，而且安全性的規劃應該在撰寫任何程式碼之前先完成。 應用程式安全性可以分成三個主要的部分：保護資料庫的安全、保護複寫的安全以及撰寫安全的程式碼。  
  
 下列主題提供有關安全性的資訊：  
  
-   [安全性與保護 &#40;複寫&#41;](../../../relational-databases/replication/security/security-and-protection-replication.md)  
  
-   [SQL Server Database Engine 和 Azure SQL Database 的資訊安全中心](../../../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md)  
  
## <a name="choosing-a-development-environment"></a>選擇開發環境  
 當開發複寫應用程式時，有三個要考慮的基本開發環境。 每個開發環境都可以存取相同的複寫功能，但有一些例外。 複寫應用程式可以在下列每個環境中開發。  
  
-   **Managed 程式碼**  
  
     物件導向開發環境，利用 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 程式設計與 .NET Common Language Runtime (CLR) 的優點。 Managed 程式碼是 .NET 開發與 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 應用程式建議的程式設計環境。 Managed 複寫介面允許以物件導向的方式設計複寫管理的程式，而無須了解 [!INCLUDE[tsql](../../../includes/tsql-md.md)]，而且當執行無法從指令碼中取得的複寫代理程式時，也提供一些回撥功能。 Managed 程式碼是開發可重複使用元件與使用者介面應用程式的最佳環境。  
  
-   **指令碼**  
  
     簡單的應用程式，可將一系列的命令以 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 指令碼的複寫系統預存程序或是批次檔中的命令來執行。 雖然您可以使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 同處理序 Managed 提供者在 Managed 環境中執行指令碼，不過也可以使用有提供回撥功能之 Managed 複寫介面來取得相同的功能。 執令碼是執行將只會執行數次且不需要回撥功能的工作之最佳環境，例如安裝複寫伺服器。  
  
-   **機器碼**  
  
     物件導向開發環境，利用系統或是 COM 物件的直接存取，例如不是由 CLR 管理的程式碼。 機器碼複寫介面已被取代或停止提供。 如需詳細資訊，請參閱 [SQL Server 複寫中已被取代的功能](../../../relational-databases/replication/deprecated-features-in-sql-server-replication.md)或[複寫回溯相容性](../../../relational-databases/replication/replication-backward-compatibility.md)。  
  
## <a name="choose-the-appropriate-replication-programming-interface"></a>選擇適當的複寫程式設計介面。  
 最後的規劃步驟是選擇適當的複寫程式設計介面，來為選擇的開發環境實作所需的複寫功能。 下表顯示可用的複寫程式設計介面。  
  
|介面|環境|使用|  
|---------------|-----------------|----------|  
|[複寫管理物件概念](../../../relational-databases/replication/concepts/replication-management-objects-concepts.md)|Managed 程式碼|管理、監視和同步處理。|  
|<xref:Microsoft.SqlServer.Replication>|Managed 程式碼|同步處理。|  
|<xref:Microsoft.SqlServer.Replication.BusinessLogicSupport>|Managed 程式碼|建立商務邏輯處理常式，以整合自訂邏輯及合併同步處理：|  
|[複寫預存程序 &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)|指令碼|管理和監視。|  
|[複寫代理程式可執行檔概念](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)|指令碼|同步處理。|  
  
## <a name="example"></a>範例  
 在 [!INCLUDE[ssSampleDBCoShort](../../../includes/sssampledbcoshort-md.md)]，需要為全世界的 200 位銷售代表發行資料。 銷售代表經常需要出差，而且將需要使用膝上型電腦或是個人數位助理 (PDA) 來變更客戶資料和增加新訂單。 銷售代表將膝上型電腦連接到網路時，將需要與發行者同步處理變更。  
  
 就這個應用程式而言，規劃步驟可能如下所示：  
  
1.  這個應用程式的複寫拓撲已經存在。 不過，在用戶端必須建立新的提取訂閱。 發行集應該使用參數化的篩選，來將唯一的資料集複寫到每個銷售代表。  
  
2.  除了銷售應用程式所需的一般資料存取之外，此應用程式應該允許銷售人員按一下按鈕，視需要同步處理提取訂閱。 既然銷售代表將會安裝和執行應用程式，因此它也需要能夠在用戶端設定訂閱並套用初始快照集。 否則，應用程式將使用 Windows 提供的基礎結構來感應無線連接，以便在偵測到連接時，自動同步處理訂閱。  
  
3.  當連接到發行者時，請遵循所有的複寫安全性指導方針，包括 Windows 驗證與虛擬的私人網路 (VPN)。 如果實作 Web 同步處理，請使用安全通訊端層 (SSL) 連接。 如需詳細資訊，請參閱[設定 Web 同步處理](../../../relational-databases/replication/configure-web-synchronization.md)。  
  
4.  為了利用 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 的功能，應用程式是使用 Managed 程式碼語言來開發。  
  
5.  根據這些需求，Replication Management Objects (RMO) 的管理介面，可以為這個應用程式提供所有需要的應用程式功能。  
  
 此範例案例已在可針對 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 下載的 AdventureWorks 範例應用程式中實作。  
  
  

