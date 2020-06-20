---
title: SQL Server Agent 屬性 (進階頁面) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql12.ag.agent.advanced.f1
ms.assetid: a4d798ee-4c18-40d4-b6af-63d17503738c
author: stevestein
ms.author: sstein
ms.openlocfilehash: 950dbb7a082af95abfe79e48e18e2cb894e71173
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85058736"
---
# <a name="sql-server-agent-properties-advanced-page"></a>SQL Server Agent 屬性 (進階頁面)
  使用此頁面來查看和修改 Agent 服務的 advanced 屬性 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
## <a name="options"></a>選項  
 **SQL Server 事件轉送**  
 此類別目錄中的選項會啟動和設定事件轉送。  
  
 **轉送事件到另一部伺服器**  
 轉送 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 事件到另一部伺服器。  
  
 **Server**  
 選取要接收轉送事件之伺服器的名稱。  
  
 **未處理的事件**  
 只轉送未處理的事件到指定的伺服器。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 只轉送警示未回應的事件。  
  
 **所有事件**  
 轉送所有事件。 當邏輯執行個體中的警示回應事件時， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 將同時轉送事件和處理警示。  
  
 **如果事件的嚴重性等於或高於**  
 只轉送等於或高於指定層級的嚴重性層級事件。  
  
 **閒置 CPU 的條件**  
 此類別目錄中的選項，會定義 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 執行已排程要在閒置 CPU 排程上執行之作業的條件。  
  
 **定義閒置 CPU 的條件**  
 定義 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 將 CPU 視為閒置的條件。  
  
 **平均 CPU 使用量低於**  
 低於此百分比的 CPU 使用量百分比，就將 CPU 視為閒置。  
  
 **並且持續低於此狀態達**  
 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 執行閒置 CPU 排程上的作業之前，平均 CPU 必須低於指定層級的時間量。  
  
## <a name="see-also"></a>另請參閱  
 [建立排程並將其附加至作業](create-and-attach-schedules-to-jobs.md)   
 [管理事件](manage-events.md)  
  
  
