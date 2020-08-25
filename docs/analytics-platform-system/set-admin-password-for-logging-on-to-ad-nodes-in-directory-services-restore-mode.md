---
title: 設定 Active Directory 密碼
description: 在 Analytics Platform System (AP) 中，以目錄服務還原模式設定 Active Directory 節點管理員登入密碼。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 6bbbf42106602a25b03072a9c9abfb04f04d3c49
ms.sourcegitcommit: 33e774fbf48a432485c601541840905c21f613a0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/25/2020
ms.locfileid: "74400329"
---
# <a name="set-admin-password-for-logging-on-to-ad-nodes-in-directory-services-restore-mode-dsrm---analytics-platform-system"></a>設定用來登入目錄服務還原模式 AD 節點的系統管理員密碼 (DSRM) -Analytics Platform System
目錄服務還原模式 (DSRM) 是用來修復或復原 Active Directory Domain Services (AD DS) 的開機模式。 當 AD DS 失敗或需要還原 AD DS 時，它會用來登入設備 AD 節點。 DSRM 的密碼是在硬體廠商網站上的設備設定期間初始化的，應由裝置管理員變更。 分析平臺系統有兩個 AD DS (網域控制站) ;** _appliance_domain_-AD01**和** _appliance_domain_-AD02**。 針對每個應用裝置 AD 節點，使用下列步驟來變更 DSRM 密碼。  
  
## <a name="to-reset-the-administrator-password"></a><a name="HowToDSRM"></a>若要重設系統管理員密碼  
  
1.  在設備 AD 節點<strong> _appliance_domain_AD_xx_</strong>虛擬機器上開啟命令提示字元視窗。  
  
2.  在命令提示字元中，輸入 `ntdsutil`。  
  
3.  在 **ntdsutil** 提示字元中，輸入 `set dsrm password` 。  
  
4.  在 [ **重設系統管理員密碼：** ] 提示中，輸入 `reset password on server null` 。  
  
5.  出現提示時，輸入新密碼。  
  
6.  針對每個應用裝置 AD 虛擬機器重複上述步驟 1-5。  
  
    > [!WARNING]  
    > Analytics Platform System 不支援網域系統管理員或本機系統管理員密碼 ($) 的貨幣符號字元。 包含貨幣符號的密碼將會驗證並可供使用，但可以封鎖升級和維護活動。  
  
> [!NOTE]  
> 如果特定 AD 虛擬機器的 Active Directory Domain Services 或虛擬機器損毀，建議的更正動作是針對受影響的 AD 虛擬機器執行 **ReplaceVM** 。 請聯絡 CSS 以取得協助。  
  
## <a name="see-also"></a>另請參閱  
[&#40;Analytics Platform System&#41;的密碼重設 ](password-reset.md)  
  
