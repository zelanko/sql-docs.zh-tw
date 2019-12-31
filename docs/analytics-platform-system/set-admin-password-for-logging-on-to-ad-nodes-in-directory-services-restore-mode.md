---
title: 設定 Active Directory 密碼
description: 在分析平臺系統（AP）中，以目錄服務還原模式設定 Active Directory 節點的系統管理員登入密碼。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 6bbbf42106602a25b03072a9c9abfb04f04d3c49
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/22/2019
ms.locfileid: "74400329"
---
# <a name="set-admin-password-for-logging-on-to-ad-nodes-in-directory-services-restore-mode-dsrm---analytics-platform-system"></a>設定系統管理員密碼，以登入目錄服務還原模式（DSRM）中的 AD 節點-Analytics Platform System
目錄服務還原模式（DSRM）是用於修復或復原 Active Directory Domain Services （AD DS）的開機模式。 它可用來在 AD DS 失敗或需要還原 AD DS 後，登入應用裝置 AD 節點。 DSRM 的密碼已在硬體廠商網站的設備設定期間初始化，且應由裝置管理員變更。 Analytics Platform System 有兩個 AD DS （網域控制站）;** _appliance_domain_-AD01**和** _appliance_domain_-AD02**。 針對每個應用裝置 AD 節點，使用下列步驟變更 DSRM 密碼。  
  
## <a name="HowToDSRM"></a>若要重設系統管理員密碼  
  
1.  在應用裝置 AD 節點上開啟 [命令提示字元] 視窗， <strong> _appliance_domain_AD_xx_</strong>虛擬機器]。  
  
2.  在命令提示字元中，輸入 `ntdsutil`。  
  
3.  在**ntdsutil**提示字元中， `set dsrm password`輸入。  
  
4.  在 [**重設系統管理員密碼：** ] `reset password on server null`提示字元中，輸入。  
  
5.  在提示字元中，輸入新的密碼。  
  
6.  針對每個應用裝置 AD 虛擬機器重複上述步驟 1-5。  
  
    > [!WARNING]  
    > Analytics Platform System 不支援網域系統管理員或本機系統管理員密碼中的貨幣符號字元（$）。 包含貨幣符號的密碼將會進行驗證並可供使用，但可封鎖升級和維護活動。  
  
> [!NOTE]  
> 如果特定 AD 虛擬機器的 Active Directory Domain Services 或虛擬機器損毀，建議的修正動作是針對受影響的 AD 虛擬機器執行**ReplaceVM** 。 請聯繫 CSS 以取得協助。  
  
## <a name="see-also"></a>另請參閱  
[&#40;分析平臺系統&#41;的密碼重設](password-reset.md)  
  
