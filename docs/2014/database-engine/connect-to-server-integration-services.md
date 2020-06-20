---
title: 連接到伺服器 (Integration Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- sql12.swb.connection.login.dtsserver.f1
ms.assetid: 5be897bd-f36c-4c6a-a91a-13d0d016f8b6
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 7b0d52d28440a92f79b08e90aff73b45fe643070
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84934649"
---
# <a name="connect-to-server-integration-services"></a>連線到伺服器 (Integration Services)
  連接到 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 時，使用此對話方塊來檢視或指定選項。  
  
## <a name="options"></a>選項。  
 **伺服器類型**  
 從 [物件總管] 註冊伺服器時，選取要連接的伺服器類型： [!INCLUDE[ssDE](../includes/ssde-md.md)]、Analysis Services、Reporting Services 或 Integration Services。 對話方塊的其他部分僅會顯示適用於所選取伺服器類型的選項。 從 [已註冊的伺服器] 註冊伺服器時，[伺服器類型] 方塊是唯讀的，且會與 [已註冊的伺服器] 元件中所顯示的伺服器類型相符。 若要註冊不同類型的伺服器，請先從 [已註冊的伺服器] 工具列中選取 [[!INCLUDE[ssDE](../includes/ssde-md.md)]]、[Analysis Services]、[Reporting Services] 或 [Integration Services]，再開始註冊新的伺服器。  
  
 **伺服器名稱**  
 選取要連接的伺服器。 預設會顯示上次連接的伺服器執行個體。  
  
> [!NOTE]  
>  請勿使用 *\<servername>* \\ *\<instancename>* ，因為不 [!INCLUDE[ssIS](../includes/ssis-md.md)] 支援在電腦上有多個實例。  
  
 **驗證**  
 [!INCLUDE[msCoName](../includes/msconame-md.md)] 僅有 [!INCLUDE[ssIS](../includes/ssis-md.md)]Windows 驗證可用。 Windows 驗證模式允許使用者透過 Windows 使用者帳戶連接。  
  
 **使用者名稱**  
 無法使用此選項，因為 [!INCLUDE[ssIS](../includes/ssis-md.md)]僅有 Windows 驗證可用。  
  
 **密碼**  
 無法使用此選項，因為 [!INCLUDE[ssIS](../includes/ssis-md.md)]僅有 Windows 驗證可用。  
  
 **[連接]**  
 按一下即可連接到上列所選的伺服器。  
  
 **選項**  
 按一下即可顯示其他伺服器連接選項，例如，註冊伺服器與記住密碼。  
  
  
