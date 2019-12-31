---
title: 建立網域系統管理員
description: 某些作業需要 Analytics Platform System 網域系統管理員許可權。 這會說明如何建立額外的設備網域系統管理員。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 1a0d50e485f0e8f48de11b2e5a3c27c9f9be047e
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/22/2019
ms.locfileid: "74401236"
---
# <a name="create-an-aps-domain-administrator"></a>建立 AP 網域系統管理員
某些作業需要 Analytics Platform System 網域系統管理員許可權。 這會說明如何建立額外的設備網域系統管理員。  
  
## <a name="create-a-domain-administrator"></a>建立網域系統管理員  
若要擁有足夠的許可權來設定所有的 ap 節點，執行**ap Configuration Manager** （`dwconfig.exe`）的使用者必須是**Domain Admins**群組的成員。 若要啟動和停止 AP 服務，使用者必須是**PdwControlNodeAccess**群組的成員。  
  
#### <a name="to-add-a-user-to-the-domain-admins-group"></a>將使用者新增至 Domain Admins 群組  
  
1.  使用現有的設備網域系統管理員帳戶登入作用中的 AD 節點 **（_設備\_網域_-AD01**或**_設備\_網域_-AD02**）。  
  
2.  在 [開始] 功能表上，按一下 **[執行]**。 在 [**開啟**] 方塊中，輸入**dsa.msc**。 按一下 [確定]****。  
  
3.  在 [ **Active Directory 使用者和電腦**] 程式中，以滑鼠右鍵按一下 [**使用者**]，指向 [**新增**]，然後按一下 [**使用者**]。  
  
4.  在 [**新增物件-使用者**] 對話方塊中，完成新使用者的描述，然後按 **[下一步]**。  
  
    完成 [密碼] 對話方塊，然後按 **[下一步]**。  
  
    > [!WARNING]  
    > SQL Server PDW 不支援網域系統管理員或本機系統管理員密碼中的貨幣符號字元（$）。 包含貨幣正負號的密碼將會有效且可供使用，但可封鎖升級和維護活動  
  
    確認新的使用者描述，然後按一下 **[完成]**。  
  
5.  在使用者清單中，按兩下新使用者以開啟 [使用者屬性] 對話方塊。  
  
6.  在 [隸屬於]**** 索引標籤上，按一下 [新增]****。  
  
    輸入**Domain Admins;PdwControlNodeAccess** ，然後按一下 [**檢查名稱**]。 按一下 [確定]****。  
  
    這會將新的使用者新增至**Domain Admins**群組和**PdwControlNodeAccess**群組。 按一下 [確定]****。  
  
## <a name="see-also"></a>另請參閱  
[啟動 Configuration Manager &#40;分析平臺系統&#41;](launch-the-configuration-manager.md)  
  
