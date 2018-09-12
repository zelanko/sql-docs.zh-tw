---
title: 建立多伺服器環境 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent, multiserver environments
- master servers [SQL Server], about master servers
- target servers [SQL Server], about target servers
- multiserver environments [SQL Server]
ms.assetid: edc2b60d-15da-40a1-8ba3-f1d473366ee6
caps.latest.revision: 41
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 149b7f15a59dd6f3532353e757faac69fc25befd
ms.sourcegitcommit: 8ae6e6618a7e9186aab3c6a37ea43776aa9a382b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/06/2018
ms.locfileid: "43811894"
---
# <a name="create-a-multiserver-environment"></a>建立多伺服器環境
  多伺服器管理會要求您設定一部主要伺服器 (MSX) 以及一或多部目標伺服器 (TSX)。 將在所有目標伺服器上處理的作業會先在主要伺服器上定義，然後再下載至目標伺服器。  
  
 根據預設，系統會針對主要伺服器與目標伺服器之間的連接，啟用完整的安全通訊端層 (SSL) 加密和憑證驗證。 如需詳細資訊，請參閱 [在目標伺服器上設定加密選項](set-encryption-options-on-target-servers.md)。  
  
 如果您有許多台目標伺服器，請避免在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 其他功能具有重大效能要求的實際伺服器上定義主要伺服器，因為目標伺服器可能會拖慢實際伺服器的效能。 如果也將事件轉寄到專用的主要伺服器，您就可以在一部伺服器上集中化管理。 如需詳細資訊，請參閱 [管理作業步驟](manage-events.md)。  
  
> [!NOTE]  
>  若要使用多伺服器作業處理， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務帳戶必須是主要伺服器上 **msdb** 資料庫角色 **TargetServersRole** 的成員。 [主要伺服器精靈] 會在編列處理序的過程中，自動將服務帳戶加入至此角色  
  
## <a name="considerations-for-multiserver-environments"></a>多伺服器環境的考量事項  
 如需受支援的 MSX/TSX 組態，請參閱下表。  
  
||**TSX = 7.0**|**TSX = 8.0 &LT; SP3**|**TSX = 8.0 SP3 或更高版本**|**TSX = 9.0**|**TSX = 10.0**|**TSX = 10.5**|**TSX = 11.0**|  
|-|--------------------|---------------------------|----------------------------------|--------------------|--------------------|---------------------|---------------------|  
|**MSX = 7.0**|是|是|否|否|否|否|否|  
|**MSX = 8.0 &LT; SP3**|是|是|否|否|否|否|否|  
|**MSX = 8.0 SP3 或更高版本**|否|否|是|是|是|是|是|  
|**MSX = 9.0**|否|否|否|是|是|是|是|  
|**MSX = 10.0**|否|否|否|否|是|是|是|  
|**MSX = 10.5**|否|否|否|否|否|是|是|  
|**MSX = 11.0**|否|否|否|否|否|否|是|  
  
 建立多伺服器環境時，請考慮下列問題：  
  
-   每個目標伺服器只能向一個主要伺服器報告。 您必須先使目標伺服器脫離主要伺服器，才能將它編列到不同的主要伺服器中。  
  
-   變更目標伺服器的名稱時，必須先將它脫離後才能變更名稱，等變更後再重新編列。  
  
-   如果您想要解除多重伺服器組態，您必須使所有的目標伺服器脫離主伺服器。  
  
-   SQL Server Integration Services 僅支援與主要伺服器版本相同或更新版本的目標伺服器。  
  
## <a name="related-tasks"></a>相關工作  
 下列主題說明建立多伺服器環境的常見工作。  
  
|描述|主題|  
|-----------------|-----------|  
|描述如何建立主要伺服器。|[設為主要伺服器](make-a-master-server.md)|  
|描述如何建立目標伺服器。|[設為目標伺服器](make-a-target-server.md)|  
|描述如何將目標伺服器編列到主要伺服器中。|[將目標伺服器編列至主要伺服器](enlist-a-target-server-to-a-master-server.md)|  
|描述如何使目標伺服器脫離主要伺服器，|[使目標伺服器脫離主要伺服器](defect-a-target-server-from-a-master-server.md)|  
|描述如何從主要伺服器脫離多部目標伺服器。|[從主要伺服器脫離多個目標伺服器](defect-multiple-target-servers-from-a-master-server.md)|  
|描述如何檢查目標伺服器的狀態。|[sp_help_targetserver &#40;-SQL&AMP;#41;&#41;](/sql/relational-databases/system-stored-procedures/sp-help-targetserver-transact-sql)<br /><br /> [sp_help_targetservergroup &#40;-SQL&AMP;#41;&#41;](/sql/relational-databases/system-stored-procedures/sp-help-targetservergroup-transact-sql)|  
  
## <a name="see-also"></a>另請參閱  
 [為使用 Proxy 的多伺服器作業疑難排解](troubleshoot-multiserver-jobs-that-use-proxies.md)  
  
  
