---
title: 建立網域系統管理員-Analytics Platform System |Microsoft Docs
description: 某些作業需要 Analytics Platform System 網域系統管理員權限。 這會說明如何建立其他設備網域系統管理員。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 18277b6db2a59c502c4aafbec98974385a4a053d
ms.sourcegitcommit: fc6a6eedcea2d98c93e33d39c1cecd99fbc9a155
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/12/2018
ms.locfileid: "49168784"
---
# <a name="create-an-aps-domain-administrator"></a>建立 APS 網域系統管理員
某些作業需要 Analytics Platform System 網域系統管理員權限。 這會說明如何建立其他設備網域系統管理員。  
  
## <a name="create-a-domain-administrator"></a>建立網域系統管理員  
若要擁有足夠的權限，若要設定所有的 APS 節點執行的使用者**APS Configuration Manager** (`dwconfig.exe`) 必須是成員**Domain Admins**群組。 若要啟動及停止 AP 服務，使用者必須隸屬**PdwControlNodeAccess**群組。  
  
#### <a name="to-add-a-user-to-the-domain-admins-group"></a>若要將使用者新增至 Domain Admins 群組  
  
1.  登入作用中的 AD 節點 **(_設備\_網域_-AD01**或是**_設備\_網域_-ad02 移**)使用現有的應用裝置網域系統管理員帳戶。  
  
2.  在 [開始] 功能表上，按一下 [執行]。 在 **開放**方塊中，輸入**dsa.msc**。 按一下 [確定] 。  
  
3.  在  **Active Directory 使用者和電腦**程式中，以滑鼠右鍵按一下**使用者**，指向**新增**，然後按一下**使用者**。  
  
4.  在 **新增物件-使用者** 對話方塊中，的完整描述，新的使用者，然後**下一步**。  
  
    完成 密碼 對話方塊，然後按一下**下一步**。  
  
    > [!WARNING]  
    > SQL Server PDW 不支援的貨幣符號字元 （$） 中的網域系統管理員或本機系統管理員密碼。 包含貨幣符號的密碼會有效並成為可用狀態，但可能會封鎖升級和維護活動  
  
    確認新的使用者描述，然後按一下**完成**。  
  
5.  在使用者清單中，按兩下新的使用者，以開啟 [使用者屬性] 對話方塊。  
  
6.  在 **隸屬**索引標籤上，按一下**新增**。  
  
    型別**Domain Admins;PdwControlNodeAccess** ，然後按一下 **檢查名稱**。 按一下 [確定] 。  
  
    這會將新增新的使用者**Domain Admins**群組並**PdwControlNodeAccess**群組。 按一下 [確定] 。  
  
## <a name="see-also"></a>另請參閱  
[啟動組態管理員 &#40;Analytics Platform System&#41;](launch-the-configuration-manager.md)  
  
