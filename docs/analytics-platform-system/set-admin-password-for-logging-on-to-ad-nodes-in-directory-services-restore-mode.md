---
title: "在 目錄服務還原模式 (AP) 中設定 AD 節點的管理員登入密碼"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: sql-non-specified
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: analytics-platform-system
ms.technology: mpp-data-warehouse
ms.custom: 
ms.date: 01/05/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 97a9c715-2763-417d-b45c-bb0180759e47
caps.latest.revision: "20"
ms.openlocfilehash: 1496e3e18bde0fbe1daad452081191bbe0ffb23e
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="set-admin-password-for-logging-on-to-ad-nodes-in-directory-services-restore-mode-dsrm"></a>在 目錄服務還原模式 (DSRM) 中設定登入 AD 節點的系統管理員密碼
目錄服務還原模式 (DSRM) 為修復或復原 Active Directory 網域服務 (AD DS) 的開機模式。 它用來登入應用裝置 AD 節點失敗 AD DS 之後，或需要還原的 AD DS。 Dsrm 密碼已經初始化應用裝置設定硬體供應商站台期間，並且應該變更應用裝置系統管理員。 Analytics Platform System 有兩個 AD DS （網域控制站）。 ***appliance_domain*-AD01**和 ***appliance_domain*-ad02 移**。 每個應用裝置 AD 節點，變更 使用下列步驟將 DSRM 密碼。  
  
## <a name="HowToDSRM"></a>若要重設管理員密碼  
  
1.  開啟命令提示字元視窗上的 AD 應用裝置節點  ***appliance_domain*– AD*xx** * 虛擬機器。  
  
2.  在命令提示字元中，輸入`ntdsutil`。  
  
3.  在**ntdsutil**提示中，輸入`set dsrm password`。  
  
4.  在**重設管理員密碼：**提示中，輸入`reset password on server null`。  
  
5.  在提示字元中輸入新密碼。  
  
6.  針對每個應用裝置 AD 虛擬機器重複步驟 1 – 5 上方。  
  
    > [!WARNING]  
    > Analytics Platform System 不支援在網域系統管理員或本機系統管理員密碼貨幣符號字元 （$）。 包含貨幣符號的密碼將會驗證，而且是可使用，但可能會封鎖升級與維護的活動。  
  
> [!NOTE]  
> 如果 Active Directory 網域服務或虛擬機器、 損毀的特定 AD 虛擬機器執行**ReplaceVM**受影響的 ad 虛擬機器是建議的更正動作。 如需協助的連絡 CSS。  
  
## <a name="see-also"></a>請參閱＜  
[密碼重設 &#40;Analytics Platform System &#41;](password-reset.md)  
  
