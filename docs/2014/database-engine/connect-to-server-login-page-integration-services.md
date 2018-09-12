---
title: 連接到伺服器 (登入頁面) Integration Services | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.swb.connecttodtsserver.login.f1
- sql12.swb.connecttodts.login.f1
ms.assetid: 402c2de4-f4ea-40b0-909f-3ddf3bd59950
caps.latest.revision: 23
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 95eac72a39ec2d110411fbae2d2494108e5cff41
ms.sourcegitcommit: 8ae6e6618a7e9186aab3c6a37ea43776aa9a382b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/06/2018
ms.locfileid: "43812394"
---
# <a name="connect-to-server-login-page-integration-services"></a>連接到伺服器 (登入頁面) Integration Services
  連線到 [!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 時，可使用此索引標籤檢視或指定下列選項。  
  
## <a name="options"></a>選項。  
 **伺服器類型**  
 從 [物件總管] 註冊伺服器時，選取要連接的伺服器類型： [!INCLUDE[ssDE](../includes/ssde-md.md)]、Analysis Services、Reporting Services 或 Integration Services。 對話方塊的其他部分僅會顯示適用於所選取伺服器類型的選項。 從已註冊的伺服器註冊伺服器時，[伺服器類型] 方塊會呈現唯讀，並會與已註冊的伺服器元件中所顯示的伺服器類型進行比對。 若要註冊不同類型的伺服器，請先從 [已註冊的伺服器] 工具列中選取 [[!INCLUDE[ssDE](../includes/ssde-md.md)]]、[Analysis Services]、[Reporting Services] 或 [Integration Services]，再開始註冊新的伺服器。  
  
 **伺服器名稱**  
 選取要連接的伺服器。 預設會顯示上次連接的伺服器執行個體。  
  
> [!NOTE]  
>  請勿使用*\<伺服器名稱 >*\\*\<執行個體名稱 >*，因為[!INCLUDE[ssIS](../includes/ssis-md.md)]不支援多個執行個體的電腦上。  
  
 **驗證**  
 [!INCLUDE[msCoName](../includes/msconame-md.md)] 僅有 [!INCLUDE[ssIS](../includes/ssis-md.md)]Windows 驗證可用。 Windows 驗證模式允許使用者透過 Windows 使用者帳戶連接。  
  
 **使用者名稱**  
 無法使用此選項，因為 [!INCLUDE[ssIS](../includes/ssis-md.md)]僅有 Windows 驗證可用。  
  
 **密碼**  
 無法使用此選項，因為 [!INCLUDE[ssIS](../includes/ssis-md.md)]僅有 Windows 驗證可用。  
  
 **記住密碼**  
 無法使用此選項，因為 [!INCLUDE[ssIS](../includes/ssis-md.md)]僅有 Windows 驗證可用。  
  
 **[連接]**  
 連接到上列所選的伺服器。  
  
 **選項。**  
 按一下即可變更對話方塊，並隱藏其他伺服器連接選項，例如記住密碼。  
  
  
