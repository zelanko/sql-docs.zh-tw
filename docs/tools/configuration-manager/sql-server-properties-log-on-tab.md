---
title: SQL Server 屬性 （登入 索引標籤） |Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: configuration-manager
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 405073fc-eaa3-43c6-bf82-2cd58cacc1c3
caps.latest.revision: 25
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8e12e87d3135f88e04dc159e7433ade959625daf
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MTE
ms.contentlocale: zh-TW
ms.lasthandoff: 02/03/2018
---
# <a name="sql-server-properties-log-on-tab"></a>SQL Server 屬性 (登入索引標籤)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
您可以使用 **[SQL Server 屬性]** 對話方塊的 **[登入]** 索引標籤，來指定要供 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務使用的帳戶、變更帳戶的密碼，以及啟動和停止該服務。 帳戶密碼的變更會立即生效。  
  
> [!NOTE]  
>  在叢集執行個體上變更服務所使用的帳戶名稱時，新帳戶必須是所要變更之服務安裝期間所指定網域群組的成員，或者您必須擁有在該群組中加入成員的權限。 如果您沒有修改群組成員資格的權限，請與網域管理員連絡。  
>   
>  如需有關選取帳戶以執行服務的詳細資訊，請參閱《 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 線上叢書》中的＜設定 Windows 服務帳戶＞。  
  
## <a name="options"></a>選項。  
 **內建帳戶**  
 **本機系統**  
 -   指定本機系統帳戶。 這個帳戶不需要密碼。 但是，根據授與帳戶的權限，本機系統帳戶可能會禁止服務與其他伺服器互動。  
  
 **本機服務**  
 -   指定本機服務帳戶。 這個帳戶不需要密碼。 但是，根據授與帳戶的權限，本機服務帳戶可能會禁止服務與其他伺服器互動。  
  
 **網路服務**  
 -   我們建議您不要在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務上，使用網路服務帳戶。 本機使用者或網域使用者帳戶更適合這些服務。  
  
 **這個帳戶**  
 指定使用 Windows 驗證的本機或網域使用者帳戶。 建議您使用具有最少服務權限的網域使用者帳戶。  
  
 **帳戶名稱**  
 指定本機或網域使用者帳戶名稱。  
  
 **密碼**  
 輸入帳戶的密碼。  
  
 **確認密碼**  
 再次輸入帳戶的密碼。  
  
 **啟動**  
 啟動服務。  
  
 **停止**  
 停止服務。  
  
 **暫停**  
 暫停服務。  
  
 **繼續**  
 繼續已暫停的服務。  
  
> [!IMPORTANT]  
>  根據預設，只有本機 Administrators 群組的成員能夠啟動、停止、暫停、繼續或重新啟動服務。 若要將管理服務的能力授與非系統管理員，請參閱 [How to grant users rights to manage services in Windows Server 2003](http://support.microsoft.com/kb/325349)(如何在 Windows Server 2003 中，將管理服務的權限授與使用者)。 (其他 Windows 版本的程序都很相似)。  
  
> [!NOTE]  
>  啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]時，包含「未實作 [0x80004001]」片語的 WMI 錯誤，可能表示目標電腦上並未安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
  
