---
title: 連接至 SQL Server 公用程式 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: b9b90b8d-241f-4b74-ac14-de7b10ea1821
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 08811675cce441406534da3c31e2d01f314a2c20
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2020
ms.locfileid: "68115425"
---
# <a name="connect-to-a-sql-server-utility"></a>連接至 SQL Server 公用程式
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  在您可以連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式之前，您必須建立公用程式控制點 (UCP)。 如需詳細資訊，請參閱 [SQL Server 公用程式的功能與工作](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)。  
  
 若要檢視及管理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資源健全狀況，請使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS) 連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式。  
  
 若要透過 SSMS 連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式：  
  
1.  啟動 SSMS。  
  
2.  在 SSMS 中，連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的執行個體。  
  
3.  按一下 [檢視]  ，然後按一下 [公用程式總管]  。  
  
4.  在公用程式總管導覽窗格中，按一下 ![[連線到公用程式]](../../relational-databases/manage/media/connect-to-utility.gif "Connect_to_Utility")  。  
  
5.  在 [連接到伺服器]  對話方塊中，指定 UCP 執行個體名稱，然後按一下 [連接]  。  
  
6.  檢視公用程式總管導覽窗格，以查看 UCP 中 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資源的樹狀檢視。  
  
 建立新的 UCP 也會連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式。 如需詳細資訊，請參閱[建立 SQL Server 公用程式控制點 &#40;SQL Server 公用程式&#41;](../../relational-databases/manage/create-a-sql-server-utility-control-point-sql-server-utility.md)。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server 公用程式的功能與工作](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)   
 [檢視資源健全狀況原則結果 &#40;SQL Server 公用程式&#41;](../../relational-databases/manage/view-resource-health-policy-results-sql-server-utility.md)  
  
  
