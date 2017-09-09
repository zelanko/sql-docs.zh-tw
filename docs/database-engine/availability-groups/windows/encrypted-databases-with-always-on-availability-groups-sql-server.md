---
title: "加密資料庫與 AlwaysOn 可用性群組 (SQL Server) | Microsoft Docs"
ms.custom: 
ms.date: 05/17/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Transparent Data Encryption, AlwaysOn Availability Groups
- TDE, AlwaysOn Availability Groups
- Availability Groups [SQL Server], interoperability
ms.assetid: 09eb6ebc-3051-4fff-86a5-93524507b1fc
caps.latest.revision: 10
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 7b4f037616e0559ac62bbae5dbe04aeffe529b06
ms.openlocfilehash: 448a46ee3d01b3d14a71b1889f201814f0ec5dd1
ms.contentlocale: zh-tw
ms.lasthandoff: 08/28/2017

---
# <a name="encrypted-databases-with-always-on-availability-groups-sql-server"></a>加密的資料庫與 AlwaysOn 可用性群組 (SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  本主題包含在 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 中使用目前加密或最近解密之資料庫搭配 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]的相關資訊。  
  
 **本主題內容：**  
  
-   [限制事項](#Restrictions)  
  
-   [相關工作](#RelatedTasks)  
  
##  <a name="Restrictions"></a> 限制事項  
  
-   如果資料庫已加密，甚至包含資料庫加密金鑰 (DEK)，您就無法使用 [!INCLUDE[ssAoNewAgWiz](../../../includes/ssaonewagwiz-md.md)] 或 [!INCLUDE[ssAoAddDbWiz](../../../includes/ssaoadddbwiz-md.md)] ，將資料庫加入至可用性群組。 即使加密的資料庫已經解密，其記錄備份可能包含加密資料。 在此情況中，資料庫的完整初始資料同步處理可能會失敗。 這是因為還原記錄作業可能需要資料庫加密金鑰 (DEK) 所使用的憑證，而該憑證可能無法使用。  
  
     若要讓解密的資料庫能夠透過精靈加入至可用性群組：  
  
    1.  建立主要資料庫的記錄備份。  
  
    2.  建立主要資料庫的完整資料庫備份。  
  
    3.  在裝載次要複本的伺服器執行個體上還原資料庫備份。  
  
    4.  從主要資料庫建立新的記錄備份。  
  
    5.  在次要資料庫上還原這個記錄備份。  
  
##  <a name="RelatedTasks"></a> 相關工作  
  
-   [針對可用性群組手動準備次要資料庫 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md)  
  
-   [使用可用性群組精靈 &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-availability-group-wizard-sql-server-management-studio.md)  
  
-   [使用將資料庫加入至可用性群組精靈 &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/availability-group-add-database-to-group-wizard.md)  
  
## <a name="see-also"></a>另請參閱  
 [AlwaysOn 可用性群組概觀 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [透明資料加密 &#40;TDE&#41;](../../../relational-databases/security/encryption/transparent-data-encryption.md)  
  
  

