---
title: 散發者密碼 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.configuredistributionwizard.distributorpassword.f1
ms.assetid: 52787c5e-c9ef-440e-a000-0787111b7dbb
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 53605b1e88c47c5fa9b2f0ee37147993e0375808
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2020
ms.locfileid: "76283946"
---
# <a name="distributor-password"></a>散發者密碼
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  如果，在此精靈的 **[發行者]** 頁面上，您已啟用一或多個發行者使用此伺服器作為遠端散發者，則必須為發行者與使用 **distributor_admin** 登入的遠端散發者之間的連接複寫指定密碼。 針對使用此遠端散發者的每個發行者，也必須在新增發行集精靈或設定散發精靈的 **[管理密碼]** 頁面上輸入相同的密碼。 如需散發者安全性的詳細資訊，請參閱[保護散發者](../../relational-databases/replication/security/secure-the-distributor.md)。  
  
## <a name="options"></a>選項。  
 **密碼**  
 為發行者和遠端散發者之間的連接輸入增強式密碼。  
  
 **確認密碼**  
 重新輸入密碼，以確認密碼輸入正確。  
  
## <a name="see-also"></a>另請參閱  
 [[設定散發]](../../relational-databases/replication/configure-distribution.md)   
 [設定發行和散發](../../relational-databases/replication/configure-publishing-and-distribution.md)  
  
  
