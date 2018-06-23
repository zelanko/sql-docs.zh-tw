---
title: CDC 執行個體部署指令碼 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 8fa82822-ac99-48ef-a18d-f4f3a77105b4
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 588c413c66560399941e75c4f8287b1b31da3067
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36134762"
---
# <a name="cdc-instance-deployment-script"></a>CDC 執行個體部署指令碼
  顯示 CDC 執行個體部署指令碼的 [CDC 執行個體部署指令碼] 對話方塊。 此指令碼可用來重新建立 CDC 資料庫，並將其所有成品放在另一個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體上。  
  
 在完成部署指令碼之後，您應該確定以下事項：  
  
-   部署指令碼假設已針對 Oracle CDC 準備好目標 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體，其方式是使用 Oracle CDC 服務組態主控台，或是使用程式所建立的 **[準備指令碼]** 。  
  
-   用來啟用 CDC 之資料庫的部分指令碼必須由 `sysadmin`執行。  
  
-   此指令碼不會保留 Oracle 記錄採礦密碼。 在執行指令碼及啟動 Oracle CDC 服務之後，需要手動設定這個選項。  
  
 在 **[CDC 執行個體部署指令碼]** 對話方塊中選取以下選項。  
  
 **另存新檔**  
 將指令碼以文字檔格式儲存在您想要儲存的任何位置。 您可以將包含指令碼的檔案複製到其他任何伺服器上，並在該處執行。  
  
 **複製**  
 將指令碼複製到剪貼簿。 然後您可以將指令碼貼到 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或任何文字編輯器中，於日後執行指令碼。  
  
## <a name="see-also"></a>另請參閱  
 [準備 SQL Server 以使用 CDC](prepare-sql-server-for-cdc.md)  
  
  