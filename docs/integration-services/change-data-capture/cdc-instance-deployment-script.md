---
description: CDC 執行個體部署指令碼
title: CDC 執行個體部署指令碼 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 8fa82822-ac99-48ef-a18d-f4f3a77105b4
author: chugugrace
ms.author: chugu
ms.openlocfilehash: b53daf02f3fae88f2ab9dd17e7be14373a774d45
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88484740"
---
# <a name="cdc-instance-deployment-script"></a>CDC 執行個體部署指令碼

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


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
 [準備 SQL Server 以使用 CDC](../../integration-services/change-data-capture/prepare-sql-server-for-cdc.md)  
  
  
