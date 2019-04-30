---
title: Reporting Services SharePoint 模式驗證 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- Upgrade SharePoint Mode [Reporting Services]
- SharePoint integration
- SharePoint Mode
ms.assetid: 2c19794a-dd55-4fe5-b901-6dd93e9f6beb
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 583f68004ef6633c7bd2a87817968c66ec13bd40
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63058074"
---
# <a name="reporting-services-sharepoint-mode-authentication"></a>Reporting Services SharePoint 模式驗證
  您可以使用   [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 頁面，來指定目前 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 安裝中所用服務帳戶的認證。 認證將會用於建立新的 SharePoint 應用程式集區。 此外，也會建立一個新的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 服務應用程式 服務應用程式名稱會包含上一個 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 執行個體的名稱。  
  
## <a name="options"></a>選項。  
  
-   **[SSRS 應用程式集區帳戶名稱]** 選項是唯讀的。 此值是用您所升級的現有 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 安裝中的目前值來自動填入。  
  
-   如果應用程式集區帳戶不需要密碼， **[SSRS 應用程式集區帳戶密碼]** 選項就會停用。 例如，"NT Authority\NetworkService。 」 如果應用程式集區帳戶需要密碼，您必須輸入正確密碼，才能繼續升級。  
  
 如需詳細資訊，請參閱 < [Upgrade and Migrate Reporting Services](https://go.microsoft.com/fwlink/?LinkID=245628) (https://go.microsoft.com/fwlink/?LinkID=245628)。  
  
## <a name="see-also"></a>另請參閱  
 [升級和移轉 Reporting Services](https://go.microsoft.com/fwlink/?LinkID=245628)  
  
  
