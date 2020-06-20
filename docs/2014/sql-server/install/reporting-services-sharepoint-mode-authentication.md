---
title: Reporting Services SharePoint 模式驗證 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Upgrade SharePoint Mode [Reporting Services]
- SharePoint integration
- SharePoint Mode
ms.assetid: 2c19794a-dd55-4fe5-b901-6dd93e9f6beb
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 3b1316a1a49726ab0754f39160125425fec116d4
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85059019"
---
# <a name="reporting-services-sharepoint-mode-authentication"></a>Reporting Services SharePoint 模式驗證
  您可以使用 ****[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 頁面，來指定目前 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 安裝中所用服務帳戶的認證。 認證將會用於建立新的 SharePoint 應用程式集區。 此外，也會建立一個新的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 服務應用程式 服務應用程式名稱會包含上一個 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 執行個體的名稱。  
  
## <a name="options"></a>選項  
  
-   **[SSRS 應用程式集區帳戶名稱]** 選項是唯讀的。 此值是用您所升級的現有 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 安裝中的目前值來自動填入。  
  
-   如果應用程式集區帳戶不需要密碼， **[SSRS 應用程式集區帳戶密碼]** 選項就會停用。 例如，"NT Authority\NetworkService"。 如果應用程式集區帳戶需要密碼，您必須輸入正確密碼，才能繼續升級。  
  
 如需詳細資訊，請參閱[升級和遷移 Reporting Services](https://go.microsoft.com/fwlink/?LinkID=245628) （ https://go.microsoft.com/fwlink/?LinkID=245628) 。  
  
## <a name="see-also"></a>另請參閱  
 [升級和移轉 Reporting Services](https://go.microsoft.com/fwlink/?LinkID=245628)  
  
  
