---
title: 未知的服務 (登入索引標籤)
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: e9b35cb5-d8ae-42ea-b59e-deedc99c4823
author: markingmyname
ms.author: maghan
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 8fae62bb72e41cd9f87200a6bcfd2f17eb780697
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "75307597"
---
# <a name="unknown-service-log-on-tab"></a>未知的服務 (登入索引標籤)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員無法識別此服務。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員」從執行該服務之電腦的 WMI 提供者取得服務資訊。 讀取服務屬性時發生錯誤，或服務屬性不完整。 若要解決此問題，請嘗試關閉並重新開啟「 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員」，或檢查執行該服務之電腦的 WMI 提供者。  
  
 WMI 提供者是 Windows 元件。 如需有關如何檢查 WMI 提供者之權限的資訊，請參閱《SQL Server 線上叢書》中的＜如何：設定 WMI 在 SQL Server 工具中顯示伺服器狀態＞。  
  
 如果您確認自己檢視的是正確的服務，請使用 **[未知的服務屬性]** 對話方塊的 **[登入]** 索引標籤來指定此服務所使用的帳戶，以及啟動和停止該服務。  
  
## <a name="options"></a>選項。  
 **本機系統帳戶**  
 指定不需要密碼的本機系統帳戶。 但是，根據授與帳戶的權限，本機系統帳戶可能會禁止服務與其他伺服器互動。  
  
 **這個帳戶**  
 指定使用 Windows 驗證的本機或網域使用者帳戶。 建議您使用具有最少服務權限的網域使用者帳戶。 如需有關選取帳戶的資訊，請參閱《SQL Server 線上叢書》中的＜設定 Windows 服務帳戶＞。  
  
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
  
  
