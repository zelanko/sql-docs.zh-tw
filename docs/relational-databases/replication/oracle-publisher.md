---
title: "Oracle 發行者 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.rep.newpubwizard.selectoraclepublisher.f1
ms.assetid: 019b7c49-dcca-445d-8969-5982a8ccbc1a
caps.latest.revision: 
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 467cadbe56d3789f4c656197ae47b18fc5548093
ms.sourcegitcommit: ab25b08a312d35489a2c4a6a0d29a04bbd90f64d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/08/2018
---
# <a name="oracle-publisher"></a>Oracle 發行者
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  從 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可讓您使用快照式和異動複寫來發行 Oracle 資料庫的資料。 如需詳細資訊，請參閱 [Oracle 發行概觀](../../relational-databases/replication/non-sql/oracle-publishing-overview.md)。  
  
 Oracle 發行者必須使用遠端 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 散發者；在安裝和測試必要的 Oracle 網路軟體之後，必須在此伺服器上執行此精靈。 如需詳細資訊，請參閱[設定 Oracle 發行者](../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md)。  
  
> [!IMPORTANT]  
>  如果另一位管理員將 Oracle 資料庫設定為發行者，則在按 **[下一步]** 之後，將提示您輸入用來連接 Oracle 資料庫進行複寫之登入的密碼。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 就會在您的登入和 Oracle 資料庫的連結伺服器連接之間建立對應。 對於後續的 Oracle 資料庫連接，您就不必再輸入密碼。  
  
## <a name="options"></a>選項。  
 **Oracle 發行者**  
 從清單中選取 Oracle 發行者。 此清單包含先前已設定執行此精靈之伺服器為其散發者的 Oracle 發行者。 如果清單是空的，或您要使用的 Oracle 發行者不在清單中，請按一下 **[加入 Oracle 發行者]**。  
  
 **[加入 Oracle 發行者]**  
 按一下以啟動 **[散發者屬性]** 對話方塊。 在此對話方塊中，按一下 **[加入]**，然後按一下 **[加入 Oracle 發行者]**。 在 **[連接到伺服器]** 對話方塊中，指定 Oracle 伺服器名稱，以及複寫管理的使用者結構描述之登入和密碼。 如需詳細資訊，請參閱[連線到伺服器 &#40;Oracle&#41;，登入](../../relational-databases/replication/connect-to-server-oracle-login.md)。  
  
> [!NOTE]  
>  如果執行精靈的伺服器尚未設定為散發者，則會提示您立即設定。  
  
## <a name="see-also"></a>另請參閱  
 [從 Oracle 資料庫建立發行集](../../relational-databases/replication/publish/create-a-publication-from-an-oracle-database.md)   
 [屬性參考 &#40;複寫&#41;](../../relational-databases/replication/properties-reference-replication.md)  
  
  
