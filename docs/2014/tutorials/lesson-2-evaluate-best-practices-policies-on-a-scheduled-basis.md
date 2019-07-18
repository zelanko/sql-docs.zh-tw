---
title: 第 2 課：評估最佳做法原則根據排程 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
ms.assetid: 37ffad63-d6db-4609-8deb-786200659554
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 29513ec37a946b9ec613ccc483048396149dd15a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63042627"
---
# <a name="lesson-2-evaluate-best-practices-policies-on-a-scheduled-basis"></a>第 2 課：根據排程評估最佳做法原則
  您可以針對 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的一個或多個執行個體，設定最佳作法原則的排程評估。 若要設定最佳做法原則根據排程執行，您必須將原則匯入至目標執行個體。  
  
 若要將排程的原則部署至多個伺服器，您可以將原則匯入至一個執行個體、設定每個原則的排程、將排程的原則匯出至資料夾，然後透過已註冊的伺服器，將排程的原則部署至目標執行個體。  
  
> [!IMPORTANT]  
>  目標執行個體必須執行 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] 或更新版本。 若要進行自動化作業，原則必須儲存在本機的執行個體中，[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 之前的 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] 版本不支援此執行個體。  
  
 在這一課，您將進行下列作業：  
  
-   將最佳做法原則匯入至 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的執行個體。  
  
-   設定原則根據排程執行。  
  
-   將排程的最佳做法原則透過已註冊的伺服器，部署至多個執行個體。  
  
 這個課程包含下列主題：  
  
-   [將原則匯入至單一執行個體](../../2014/tutorials/import-the-policies-to-a-single-instance.md)  
  
-   [排程原則](../../2014/tutorials/schedule-the-policies.md)  
  
-   [將已排程的原則部署至多個執行個體](../../2014/tutorials/deploy-scheduled-policies-to-multiple-instances.md)  
  
## <a name="see-also"></a>另請參閱  
 [使用中央管理伺服器管理多部伺服器](../relational-databases/administer-multiple-servers-using-central-management-servers.md)  
  
  
