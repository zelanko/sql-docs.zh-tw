---
title: 建立或刪除用戶端使用的伺服器別名 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- server alias
helpviewer_keywords:
- aliases [SQL Server], deleting
- aliases [SQL Server], creating
ms.assetid: b687e376-ee33-470d-b65a-87246bfefe6f
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: a0a678d3b5df450377517bc9c94d3771c45f22e0
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2020
ms.locfileid: "68012067"
---
# <a name="create-or-delete-a-server-alias-for-use-by-a-client"></a>建立或刪除用戶端使用的伺服器別名
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  此主題描述如何使用 SQL Server 組態管理員，在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中建立或刪除伺服器別名。 別名是可用於進行連接的替代名稱。 別名會封裝連接字串的必要元素，並以使用者選擇的名稱來公開這些元素。 別名可用於任何用戶端應用程式。 藉由建立伺服器別名，用戶端電腦可使用不同網路通訊協定來連接到多個伺服器，而不必指定每一個伺服器的通訊協定和連接詳細資料。 此外，您也可以一直啟用不同的網路通訊協定，即使您只需要偶而使用它們。 若您已設定伺服器在非預設通訊埠編號或具名管道上接聽，且您已停用 SQL Server Browser 服務，請建立指定新通訊埠編號或具名管道的別名。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server 組態管理員  
  
#### <a name="to-create-an-alias"></a>若要建立別名  
  
1.  在 SQL Server 組態管理員中，展開 [SQL Server Native Client Configuration (SQL Server Native Client 組態)]  ，並以滑鼠右鍵按一下 [別名]  ，然後按一下 [新增別名]  。  
  
2.  在 [別名名稱]  方塊中，輸入別名的名稱。 當用戶端應用程式連接時使用此名稱。  
  
3.  在 [伺服器]  方塊中，輸入伺服器的名稱或 IP 位址。 針對具名執行個體，請附加執行個體名稱。  
  
4.  在 [通訊協定]  方塊中，選取用於此別名的通訊協定。 選取通訊協定，將選用屬性方塊的標題變更為「通訊埠編號」、「管道名稱」或「連接字串」。  
  
 ＜[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員說明＞中描述的連接字串，對於建立自己連接字串的程式設計人員會很有幫助。 若要存取此資訊，在 [新增別名]  對話方塊，按 F1，或按一下 [說明]  。  
  
> [!NOTE]  
>  如果已設定的別名連接到錯誤的伺服器或執行個體，請停用再重新啟用相關的網路通訊協定。 這麼做可清除任何快取的連接資訊，讓用戶端能夠正確連接。  
  
#### <a name="to-delete-an-alias"></a>若要刪除別名  
  
1.  在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員中，展開 [SQL Server Native Client Configuration (SQL Server Native Client 組態)]  ，再按一下 [別名]  。  
  
2.  在詳細資料窗格中，以滑鼠右鍵按一下要刪除的別名，然後按一下 [刪除]  。  
  
  
