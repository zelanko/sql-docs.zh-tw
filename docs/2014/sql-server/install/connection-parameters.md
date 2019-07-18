---
title: 連接參數 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Upgrade Advisor [SQL Server], connections
- authentication [Upgrade Advisor]
- SQL Server Upgrade Advisor, connections
- connections [Upgrade Advisor]
- server instances [Upgrade Advisor]
- default server instances
- analyzing system [Upgrade Advisor], connections
ms.assetid: f754d038-637a-4d8e-85b0-b242e6499d26
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ca5d6ed8f1e8a92d22bd32e39c8afe946a0fcfee
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66095983"
---
# <a name="connection-parameters"></a>連接參數
  若要分析特定伺服器類型 (例如 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)])，您必須選取 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的特定執行個體。 系統會自動選取 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的預設執行個體。 您可以變更此選擇，但一次只能選取一個執行個體供 Upgrade Advisor 分析。 如果您已加入需要驗證的伺服器類型，就必須輸入驗證模式和認證。  
  
## <a name="options"></a>選項  
 **伺服器名稱**  
 預先填入您在 [[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 元件] 窗格中輸入的電腦名稱。  
  
 **執行個體名稱**  
 從電腦上可用的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體中選取。 如果您沒有看見執行個體的清單，請使用 MSSQLSERVER 來掃描預設執行個體。 這與遠端電腦尤其有關。 此外，您也可以使用 "default" 一詞來掃描預設執行個體。  
  
 **驗證**  
 從這部電腦上可用的驗證模式清單中選取。 根據預設，驗證模式是 Windows 驗證。  
  
 **使用者名稱**  
 如果您要使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證，請在此方塊中輸入使用者名稱。 我們建議使用者名稱擁有這部電腦的管理認證。  
  
> [!NOTE]  
>  如果您選取 Windows 驗證時，會填入目前登入使用者的使用者名稱**使用者名**文字方塊。  
  
 **密碼**  
 請輸入指定之使用者的密碼。  
  
## <a name="see-also"></a>另請參閱  
 [使用 Upgrade Advisor](../../../2014/sql-server/install/working-with-upgrade-advisor.md)   
 [Upgrade Advisor 使用者介面參考](../../../2014/sql-server/install/upgrade-advisor-user-interface-reference.md)  
  
  
