---
title: WMI 錯誤 0x8007052f | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- 0x8007052f (WMI error)
ms.assetid: a33f12bd-15c4-42a8-b343-de44c3e87729
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: c1668c2b4c96f23283f0eca87fdbac591f52b75f
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/03/2018
ms.locfileid: "52770270"
---
# <a name="wmi-error-0x8007052f"></a>WMI 錯誤 0x8007052f
    
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|[SQL Server]|  
|事件識別碼|0x8007052f|  
|事件來源|WMI 提供者錯誤|  
|元件|SQL Server 組態管理員|  
|符號名稱|NA|  
|訊息文字|登入失敗: 使用者帳戶限制。 可能的原因為不允許空的密碼，登入時數限制，或強制的原則限制。|  
  
## <a name="explanation"></a>說明  
 當 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 在 Windows Server 叢集或 Windows Server 網域控制站上執行時，如果您使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 組態管理員來切換至內建帳戶 (網路服務、本機服務或本機系統)，就可能會發生這個錯誤。 請勿在 Windows Server 叢集或 Windows Server 網域控制站上，使用內建帳戶來執行服務。 如需有關服務帳戶的建議事項，請參閱《[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 線上叢書》中的＜設定 Windows 服務帳戶＞主題。  
  
## <a name="user-action"></a>使用者動作  
 將 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 設定成使用網域帳戶。  
  
  
