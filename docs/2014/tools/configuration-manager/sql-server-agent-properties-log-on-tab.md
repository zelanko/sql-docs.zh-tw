---
title: SQL Server Agent 屬性 (登入索引標籤) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- configmgr-client
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 01fc6329-5d6b-4186-9565-395f375477bb
caps.latest.revision: 17
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 5d69d6f159e0e1597fdc6b59c0ba4aadf80b3748
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37234388"
---
# <a name="sql-server-agent-properties-log-on-tab"></a>SQL Server Agent 屬性 (登入索引標籤)
  您可以使用 **[SQL Server Agent 屬性]** 對話方塊的 **[登入]** 索引標籤指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務所使用的帳戶，以及啟動和停止該服務。 帳戶密碼的變更會立即生效，不需要重新啟動服務。  
  
> [!NOTE]  
>  在叢集執行個體上變更服務所使用的帳戶名稱時，新帳戶必須是所要變更之服務安裝期間所指定網域群組的成員，或者您必須擁有在該群組中加入成員的權限。 如果您沒有修改群組成員資格的權限，請與網域管理員連絡。  
  
## <a name="options"></a>選項。  
 **本機系統帳戶**  
 指定不需要密碼的本機系統帳戶。 但是，根據授與帳戶的權限，本機系統帳戶可能會限制服務與其他伺服器互動。  
  
 **這個帳戶**  
 指定使用 Windows 驗證的本機或網域使用者帳戶。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 建議您使用具有最少服務權限的網域使用者帳戶。 如需有關選取帳戶的資訊，請搜尋《線上叢書》的＜設定 Windows 服務帳戶＞。  
  
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
  
  
