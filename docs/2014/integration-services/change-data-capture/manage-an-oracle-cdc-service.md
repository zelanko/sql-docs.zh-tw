---
title: 管理 Oracle CDC 服務 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- createSrv
ms.assetid: 5972cee3-b1a9-4c56-aed6-bdddf84af283
author: chugugrace
ms.author: chugu
ms.openlocfilehash: f65f59a115fbfb1cebb1f92620d9085672835fd4
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/26/2020
ms.locfileid: "85438615"
---
# <a name="manage-an-oracle-cdc-service"></a>Manage an Oracle CDC Service
  您可以使用 CDC 服務組態主控台來管理特定的 CDC 服務。  
  
 **若要選取您想要使用的 CDC 服務**  
  
1.  從 CDC 服務組態主控台的左窗格中，展開 **[本機 CDC 服務]** 。  
  
2.  選取您想要使用的 CDC 服務。  
  
     您也可以用滑鼠右鍵按一下您想要使用的 CDC 服務，並選取所要的動作。 請參閱 [您可以使用 CDC 服務做什麼事](manage-an-oracle-cdc-service.md#BKMK_WhatcandowithCDCService)。  
  
 **OR**  
  
1.  從 CDC 服務組態主控台的左窗格選取 **[本機 CDC 服務]** 。  
  
2.  從 CDC 服務組態主控台的中間區段選取您想要使用的服務。  
  
     您也可以用滑鼠右鍵按一下您想要使用的 CDC 服務，並選取所要的動作。 請參閱 [您可以使用 CDC 服務做什麼事](manage-an-oracle-cdc-service.md#BKMK_WhatcandowithCDCService)。  
  
##  <a name="what-can-you-do-with-a-cdc-service"></a><a name="BKMK_WhatcandowithCDCService"></a> 您可以使用 CDC 服務做什麼事  
 當您使用 CDC 服務時，可以執行以下動作。  
  
### <a name="delete-the-service"></a>刪除服務  
 從 CDC 服務組態主控台右側的 **[動作]** 窗格中，按一下 **[刪除]** 刪除此服務。  
  
 您也可以用滑鼠右鍵按一下您想要刪除的 CDC 服務，然後選取 [刪除]  。  
  
 **注意**：如果當您刪除此服務時，它正在執行中，在刪除此服務之前會先將它停止。  
  
 若要刪除 Oracle CDC Windows 服務定義，此程式需要關聯 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體中 MSXDBCDC 資料庫的更新存取權。 當您按一下 [確定] 刪除此服務時，此程式會嘗試刪除 MSXDBCDC 資料庫中的 Oracle CDC 服務登錄。 如果此程式因為沒有適當的權限所以無法刪除 Oracle CDC 服務登錄，它會提示使用者輸入具有 MSXDBCDC 資料庫之更新權限的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入。  
  
 如需有關您必須在 [連接到 SQL Server] 對話方塊中輸入之資料的詳細資訊，請參閱＜ [Connection to SQL Server for Delete](connection-to-sql-server-for-delete.md)＞。  
  
### <a name="edit-the-cdc-service-properties"></a>編輯 CDC 服務屬性  
 從 CDC 服務組態主控台右側的 **[動作]** 窗格中，按一下 **[屬性]** 。  
  
 您也可以用滑鼠右鍵按一下您要編輯屬性的 CDC 服務，然後選取 [屬性]  。  
  
## <a name="see-also"></a>另請參閱  
 [如何管理本機 CDC 服務](how-to-manage-a-local-cdc-service.md)  
