---
title: 如何建立及編輯 CDC 服務 | Microsoft Docs
ms.custom: ''
ms.date: 03/20/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 1b3d47a5-dc89-482d-bbc7-fff04f194c43
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: c0b136bf49b1d8d73ea01199a09d752e3283c1f5
ms.sourcegitcommit: de5e726db2f287bb32b7910831a0c4649ccf3c4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/12/2018
ms.locfileid: "35328588"
---
# <a name="how-to-create-and-edit-a-cdc-service"></a>如何建立及編輯 CDC 服務
  這些程序描述如何從 CDC 服務組態主控台來建立和編輯新的 Oracle CDC 服務。  
  
 此程序要求在設定 Oracle CDC 服務的電腦上必須有系統管理員權限的 Windows 使用者。  
  
### <a name="to-create-a-new-cdc-service"></a>若要建立新的 CDC 服務  
  
1.  從 **[開始]** 功能表，選取 **[Oracle CDC 服務組態]**。  
  
2.  您也可以從左窗格以滑鼠右鍵按一下 [本機 CDC 服務]，並選取 [新增服務]。  
  
     您也可以從 **[動作]** 窗格按一下 **[新增服務]** 。  
  
3.  在 [新增 Oracle CDC 服務] 對話方塊中輸入必要的資訊。 如需有關如何在 [新增 Oracle CDC 服務] 對話方塊中輸入資訊的詳細資訊，請參閱＜ [Create and Edit an Oracle CDC Service](../../integration-services/change-data-capture/create-and-edit-an-oracle-cdc-service.md) ＞。  
  
     當 Oracle CDC 服務執行時，此服務會使用在 [新增 Oracle CDC 服務] 對話方塊中所提供的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入。 此登入只要求它必須是公用固定伺服器角色的成員，不需要其他權限。 一旦加入新的 Oracle CDC 執行個體之後，該登入會收到關聯 **CDC 資料庫的** db_owner [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 存取權。  
  
4.  當您將所需的資訊輸入完畢時，請按一下 **[確定]**。  
  
     若要建立 Oracle CDC Windows 服務定義，此程式需要關聯 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體中 MSXDBCDC 資料庫的更新存取權。 當您按一下 **[確定]** 時，隨即出現一個對話方塊，提示使用者輸入具有 MSXDBCDC 資料庫之更新存取權的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入。  
  
     如需有關您必須在 [連接到 SQL Server] 對話方塊中輸入之資料的詳細資訊，請參閱＜ [Connection to SQL Server](../../integration-services/change-data-capture/connection-to-sql-server.md)＞。  
  
5.  按一下 **[確定]** 關閉 [新增 Oracle CDC 服務] 對話方塊。  
  
### <a name="to-edit-a-cdc-service"></a>若要編輯 CDC 服務  
  
1.  從 **[開始]** 功能表，選取 **[Oracle CDC 服務組態]**。  
  
2.  從左窗格選取 [Local CDC Services (本機 CDC 服務)]，然後以滑鼠右鍵按一下您想要編輯的本機服務，並選取 [屬性]。  
  
     您也可以在中間選取您要使用的服務，然後從 **[動作]** 窗格按一下 **[屬性]**。  
  
3.  在 [CDC 服務屬性] 對話方塊中輸入必要的資訊。 如需有關如何在 [CDC 服務屬性] 對話方塊中輸入資訊的詳細資訊，請參閱＜ [Create and Edit an Oracle CDC Service](../../integration-services/change-data-capture/create-and-edit-an-oracle-cdc-service.md) ＞。  
  
4.  當您將所需的資訊輸入完畢時，請按一下 **[確定]**，隨即開啟 [連接到 SQL Server] 對話方塊。  
  
     當沒有 MSXDBDCDC 資料庫寫入權限的登入嘗試建立新的 Oracle CDC 執行個體時，便會顯示錯誤訊息。 在這個對話方塊中按一下 **[確定]** ，隨即顯示 [連接到 SQL Server] 對話方塊。 在此對話方塊中，您必須輸入擁有 MSXDBCDC 資料庫寫入權限之登入的認證，例如 **db_owner** 資料庫角色。  
  
     如需有關您必須在 [連接到 SQL Server] 對話方塊中輸入之資料的詳細資訊，請參閱＜ [Connection to SQL Server](../../integration-services/change-data-capture/connection-to-sql-server.md)＞。  
  
5.  在 [連接到 Oracle] 對話方塊中按一下 **[確定]** 。 隨即關閉這兩個對話方塊，而且會更新及註冊此服務。  
  
## <a name="see-also"></a>另請參閱  
 [Attunity Oracle 異動資料擷取設計工具](../../integration-services/change-data-capture/change-data-capture-designer-for-oracle-by-attunity.md)   
 [建立及編輯 Oracle CDC 服務](../../integration-services/change-data-capture/create-and-edit-an-oracle-cdc-service.md)  
  
  
