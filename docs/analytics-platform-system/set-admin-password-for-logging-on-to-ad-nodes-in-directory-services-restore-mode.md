---
title: 設定 Active Directory 密碼-Analytics Platform System |Microsoft Docs
description: 在 目錄服務還原模式 Analytics Platform System (APS) 中設定 Active Directory 節點管理員登入密碼。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: cd116bbb0305f56302f679881ef0a2a795739eb3
ms.sourcegitcommit: 0638b228980998de9056b177c83ed14494b9ad74
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/14/2018
ms.locfileid: "51641395"
---
# <a name="set-admin-password-for-logging-on-to-ad-nodes-in-directory-services-restore-mode-dsrm---analytics-platform-system"></a>設定系統管理員密碼的登入 AD 節點，在 目錄服務還原模式 (DSRM)-Analytics Platform System
目錄服務還原模式 (DSRM) 是可修復或復原 Active Directory 網域服務 (AD DS) 的開機模式。 它用來登入設備 AD 節點失敗 AD DS 之後，或需要還原的 AD DS。 DSRM 密碼已經初始化應用裝置設定硬體供應商站台期間，並且應用裝置系統管理員才可變更。 Analytics Platform System 有兩個 AD DS （網域控制站）; **_appliance_domain_-AD01**並 **_appliance_domain_-ad02 移**。 針對每個設備 AD] 節點中，變更 [使用下列步驟將 DSRM 密碼。  
  
## <a name="HowToDSRM"></a>若要重設管理員密碼  
  
1.  開啟命令提示字元 視窗，在設備 AD 節點***appliance_domain *– AD*xx***虛擬機器。  
  
2.  在命令提示字元中，輸入 `ntdsutil`。  
  
3.  在**ntdsutil**提示中，輸入`set dsrm password`。  
  
4.  在**重設管理員密碼：** 提示中，輸入`reset password on server null`。  
  
5.  在提示中，輸入新密碼。  
  
6.  針對每個設備 AD 虛擬機器重複步驟 1 – 5 上方。  
  
    > [!WARNING]  
    > Analytics Platform System 不支援在網域系統管理員或本機系統管理員密碼的貨幣符號字元 （$）。 包含貨幣符號的密碼會驗證，並且可使用，但可能會封鎖升級和維護活動。  
  
> [!NOTE]  
> 如果 Active Directory 網域服務或虛擬機器損毀特定的 AD 虛擬機器中，執行**ReplaceVM**受影響的 ad 虛擬機器是建議的更正動作。 以取得協助的連絡 CSS。  
  
## <a name="see-also"></a>另請參閱  
[密碼重設&#40;Analytics Platform System&#41;](password-reset.md)  
  
