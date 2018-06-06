---
title: 連接到伺服器 (Oracle)，登入 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.rep.oracleconnection.login.f1
helpviewer_keywords:
- Connect to Server dialog box, replication
ms.assetid: 86ed91a1-a07c-46f2-a913-67317ef2255e
caps.latest.revision: 20
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 161d787ca55a949be2733223964c15754e157f90
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="connect-to-server-oracle-login"></a>連接到伺服器 (Oracle)，登入
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  使用 **[連接到伺服器]** 對話方塊的 **[登入]** 索引標籤，即可指定從 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 散發者連接到 Oracle 發行者的帳戶。 您必須使用在發行者組態期間，為複寫管理的使用者結構描述指定之相同帳戶。 如需詳細資訊，請參閱[設定 Oracle 發行者](../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md)。  
  
## <a name="options"></a>選項。  
 **伺服器執行個體**  
 Oracle 發行者的透明網路基質 (Transparent Network Substrate，TNS) 名稱，是安裝在散發者上的 Oracle 用戶端軟體於組態期間指定的。  
  
 **驗證**  
 選取 **[Oracle 標準驗證]** (建議選項) 或 **[Windows 驗證]**。 如果您選取 **[Windows 驗證]**：  
  
-   Oracle 伺服器必須設定為允許使用 Windows 認證進行連接。 如需詳細資訊，請參閱 Oracle 文件集。  
  
-   您目前必須是使用與複寫管理的使用者結構描述所指定的相同 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 帳戶登入的。  
  
 **[登入]** 和 **[密碼]**  
 如果您在 **[驗證]** 選項選取了 **[Oracle 標準驗證]** ，請指定要使用的登入和密碼，這必須與複寫管理的使用者結構描述指定之登入和密碼相同。  
  
## <a name="see-also"></a>另請參閱  
 [Glossary of Terms for Oracle Publishing](../../relational-databases/replication/non-sql/glossary-of-terms-for-oracle-publishing.md)  
  
  
