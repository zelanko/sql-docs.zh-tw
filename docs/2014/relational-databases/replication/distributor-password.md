---
title: 散發者密碼 | Microsoft Docs
ms.custom: ''
ms.date: 06/30/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.configuredistributionwizard.distributorpassword.f1
ms.assetid: 52787c5e-c9ef-440e-a000-0787111b7dbb
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a6d3c7971f6d5e117ae923ee8697a4ec51e1a34e
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/03/2018
ms.locfileid: "52774850"
---
# <a name="distributor-password"></a>散發者密碼
  如果，在此精靈的 **[發行者]** 頁面上，您已啟用一或多個發行者使用此伺服器作為遠端散發者，則必須為發行者與使用 **distributor_admin** 登入的遠端散發者之間的連接複寫指定密碼。 針對使用此遠端散發者的每個發行者，也必須在新增發行集精靈或設定散發精靈的 **[管理密碼]** 頁面上輸入相同的密碼。 如需散發者安全性的詳細資訊，請參閱[保護散發者](security/secure-the-distributor.md)。  
  
## <a name="options"></a>選項。  
 **密碼**  
 為發行者和遠端散發者之間的連接輸入增強式密碼。  
  
 **確認密碼**  
 重新輸入密碼，以確認密碼輸入正確。  
  
## <a name="see-also"></a>另請參閱  
 [[設定散發]](configure-distribution.md)   
 [設定發行和散發](configure-publishing-and-distribution.md)  
  
  
