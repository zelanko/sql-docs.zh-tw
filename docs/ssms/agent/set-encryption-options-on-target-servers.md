---
description: 在目標伺服器上設定加密選項
title: 在目標伺服器上設定加密選項
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent, encryption
- target servers [SQL Server], encryption
- multiserver environments [SQL Server], setting encryption options on target servers
ms.assetid: 1a9fd539-e166-4ea8-9f21-ac400ca74dee
author: markingmyname
ms.author: maghan
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 832b73c751a6c475afd75769c4cf18d8e2e609a5
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88418064"
---
# <a name="set-encryption-options-on-target-servers"></a>在目標伺服器上設定加密選項
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> [Azure SQL 受控執行個體](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)目前支援多數 (但非全部) 的 SQL Server Agent 功能。 如需詳細資料，請參閱 [Azure SQL 受控執行個體與 SQL Server 之間的 T-SQL 差異](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)。

如果您無法在主要伺服器與部分或全部目標伺服器之間，使用憑證來進行「傳輸層安全性」(TLS) (先前稱為「安全通訊端層」(SSL)) 加密通訊，但是想要加密其之間的通道，請將目標伺服器設定為使用所需的安全性層級。  
  
若要設定特定主要伺服器/目標伺服器通訊通道所需的適當安全性層級，請在目標伺服器上將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理程式登錄子機碼 **\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\\** \<*instance_name*> **\SQLServerAgent\MsxEncryptChannelOptions(REG_DWORD)** 設定為下列其中一個值。 \<*instance_name*> 的值為 **MSSQL.** _n_。 例如， **MSSQL.1** 或 **MSSQL.3**。  
  
|值|描述|  
|---------|---------------|  
|**0**|停用此目標伺服器與主要伺服器之間的加密。 只有在透過其他方法保護目標伺服器與主要伺服器間通道的安全之後，才能選擇這個選項。|  
|**1**|僅啟用此目標伺服器與主要伺服器之間的加密，但是不需要憑證驗證。|  
|**2**|啟用此目標伺服器與主要伺服器之間的完整 TLS 加密和憑證驗證。 這項設定是預設值。 除非您有特殊的理由要選擇不同的值，否則最好不要變更它。|  
  
如果指定了 **1** 或 **2**，則必須在主要與目標伺服器上都啟用 TLS。 而且如果指定了 **2** ，在主要伺服器上必須有已正確簽署的憑證。  
  
> [!CAUTION]  
> [!INCLUDE[ssNoteRegistry](../../includes/ssnoteregistry-md.md)]  
  
## <a name="see-also"></a>另請參閱  
[操作說明：啟用資料庫引擎的加密連線 (SQL Server 組態管理員)](https://msdn.microsoft.com/e1e55519-97ec-4404-81ef-881da3b42006)  
  
