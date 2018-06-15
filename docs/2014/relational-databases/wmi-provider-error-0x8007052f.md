---
title: WMI 錯誤 0x8007052f | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- 0x8007052f (WMI error)
ms.assetid: a33f12bd-15c4-42a8-b343-de44c3e87729
caps.latest.revision: 9
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 7f1df2b6b5b656cf9995643aa1dfad93cef9eebb
ms.sourcegitcommit: d2573a8dec2d4102ce8882ee232cdba080d39628
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/07/2018
ms.locfileid: "34424091"
---
# <a name="wmi-error-0x8007052f"></a>WMI 錯誤 0x8007052f
    
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|이벤트 ID|0x8007052f|  
|이벤트 원본|WMI 提供者錯誤|  
|元件|SQL Server 組態管理員|  
|심볼 이름|NA|  
|메시지 텍스트|登入失敗: 使用者帳戶限制。 可能的原因為不允許空的密碼，登入時數限制，或強制的原則限制。|  
  
## <a name="explanation"></a>說明  
 當 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 在 Windows Server 叢集或 Windows Server 網域控制站上執行時，如果您使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 組態管理員來切換至內建帳戶 (網路服務、本機服務或本機系統)，就可能會發生這個錯誤。 請勿在 Windows Server 叢集或 Windows Server 網域控制站上，使用內建帳戶來執行服務。 如需有關服務帳戶的建議事項，請參閱《[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 線上叢書》中的＜設定 Windows 服務帳戶＞主題。  
  
## <a name="user-action"></a>사용자 동작  
 將 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 設定成使用網域帳戶。  
  
  