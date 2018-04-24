---
title: 設定 Active Directory 密碼-Analytics Platform System |Microsoft 文件
description: 目錄服務還原模式 Analytics Platform System (AP) 中設定 Active Directory 節點管理登入密碼。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: e74689216c1485fc0c11c588acb151269e2b5d2b
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/19/2018
---
# <a name="set-admin-password-for-logging-on-to-ad-nodes-in-directory-services-restore-mode-dsrm---analytics-platform-system"></a>設定登入 AD 節點，在 目錄服務還原模式 (DSRM)-Analytics Platform System 系統管理員密碼
目錄服務還原模式 (DSRM) 為修復或復原 Active Directory 網域服務 (AD DS) 的開機模式。 它用來登入應用裝置 AD 節點失敗 AD DS 之後，或需要還原的 AD DS。 Dsrm 密碼已經初始化應用裝置設定硬體供應商站台期間，並且應該變更應用裝置系統管理員。 Analytics Platform System 有兩個 AD DS （網域控制站）。***appliance_domain *-AD01**和 ***appliance_domain *-ad02 移**。 每個應用裝置 AD 節點，變更 使用下列步驟將 DSRM 密碼。  
  
## <a name="HowToDSRM"></a>若要重設管理員密碼  
  
1.  開啟命令提示字元視窗上的 AD 應用裝置節點***appliance_domain*– AD*xx***虛擬機器。  
  
2.  在命令提示字元中，輸入`ntdsutil`。  
  
3.  在**ntdsutil**提示中，輸入`set dsrm password`。  
  
4.  在**重設管理員密碼：**提示中，輸入`reset password on server null`。  
  
5.  在提示字元中輸入新密碼。  
  
6.  針對每個應用裝置 AD 虛擬機器重複步驟 1 – 5 上方。  
  
    > [!WARNING]  
    > Analytics Platform System 不支援在網域系統管理員或本機系統管理員密碼貨幣符號字元 （$）。 包含貨幣符號的密碼將會驗證，而且是可使用，但可能會封鎖升級與維護的活動。  
  
> [!NOTE]  
> 如果 Active Directory 網域服務或虛擬機器、 損毀的特定 AD 虛擬機器執行**ReplaceVM**受影響的 ad 虛擬機器是建議的更正動作。 如需協助的連絡 CSS。  
  
## <a name="see-also"></a>另請參閱  
[密碼重設&#40;Analytics Platform System&#41;](password-reset.md)  
  
