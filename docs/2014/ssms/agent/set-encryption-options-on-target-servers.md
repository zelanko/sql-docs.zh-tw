---
title: 在目標伺服器上設定加密選項 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent, encryption
- target servers [SQL Server], encryption
- multiserver environments [SQL Server], setting encryption options on target servers
ms.assetid: 1a9fd539-e166-4ea8-9f21-ac400ca74dee
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b27dd81df572e289d182fdaa637a3af972b3d603
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63244981"
---
# <a name="set-encryption-options-on-target-servers"></a>在目標伺服器上設定加密選項
  如果您無法在主要伺服器與部分或全部的目標伺服器之間，使用安全通訊端層 (SSL) 加密通訊的憑證，但是您想要加密它們之間的通道，請將目標伺服器設定為使用所需的安全性層級。  
  
 若要設定特定主要伺服器/目標伺服器通訊通道所需的適當安全性層級，請在目標伺服器上將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 登錄子機碼 **\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\\**\<*instance_name*>**\SQLServerAgent\MsxEncryptChannelOptions(REG_DWORD)** 設定為下列值之一。 \<*instance_name*> 的值是 **MSSQL.**_n_。 例如， **MSSQL.1** 或 **MSSQL.3**。  
  
|值|描述|  
|-----------|-----------------|  
|**0**|停用此目標伺服器與主要伺服器之間的加密。 只有在透過其他方法保護目標伺服器與主要伺服器間通道的安全之後，才能選擇這個選項。|  
|**1**|僅啟用此目標伺服器與主要伺服器之間的加密，但是不需要憑證驗證。|  
|**2**|啟用此目標伺服器與主要伺服器之間完整的 SSL 加密與憑證驗證。 這個設定是預設值。 除非您有特殊的理由要選擇不同的值，否則最好不要變更它。|  
  
 如果指定了 **1** 或 **2** ，則必須在主要和目標伺服器上都啟用 SSL。 而且如果指定了 **2** ，在主要伺服器上必須有已正確簽署的憑證。  
  
> [!CAUTION]  
>  [!INCLUDE[ssNoteRegistry](../../includes/ssnoteregistry-md.md)]  
  
## <a name="see-also"></a>另請參閱  
 [啟用 Database Engine 的加密連接 &#40;SQL Server 組態管理員&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)  
  
  
