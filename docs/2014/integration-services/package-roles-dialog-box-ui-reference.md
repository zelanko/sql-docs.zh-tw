---
title: 套件角色對話方塊 UI 參考 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.dtsserver.packageroles.f1
helpviewer_keywords:
- Package Roles dialog box
ms.assetid: 63f13416-c0aa-4480-a336-ef1e6e31a860
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 94bb72fd6cb9dca8dd76d3925f86ae64a819b7d7
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/26/2020
ms.locfileid: "85423795"
---
# <a name="package-roles-dialog-box-ui-reference"></a>封裝角色對話方塊 UI 參考
  使用 [封裝角色]  對話方塊 (可以在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 中使用)，即可指定擁有封裝之讀取權限的資料庫層級角色以及擁有封裝之寫入權限的資料庫層級角色。 資料庫層級角色僅適用於儲存在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] **msdb** 資料庫中的套件。  
  
 若要深入了解 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 資料庫層級角色及其權限，請參閱 [Integration Services 角色 &#40;SSIS 服務&#41;](security/integration-services-roles-ssis-service.md)。  
  
 對話方塊中所列出的角色是 **msdb** 系統資料庫的目前資料庫角色。 如果沒有選取角色，則會套用預設 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 角色。 依預設，讀取者角色包含 **db_ssisadmin**、 **db_ssisoperator**和建立封裝的使用者。 上述其中一個角色之成員或是建立封裝的使用者可以列舉、檢視、匯出和執行封裝。 依預設，寫入者角色包含 **db_ssisadmin** 以及建立封裝的使用者。 這個角色的成員使用者以及建立封裝的使用者，可以匯入、刪除和變更封裝。  
  
 **sysssispackages** 資料表中的 **ownersid** 資料行列出建立封裝之使用者的唯一安全性識別碼。  
  
## <a name="options"></a>選項。  
 **封裝名稱**  
 指定封裝的名稱。  
  
 **讀取器角色**  
 選取清單中的角色。  
  
 **寫入器角色**  
 選取清單中的角色  
  
## <a name="see-also"></a>另請參閱  
 [資料庫層級角色](../relational-databases/security/authentication-access/database-level-roles.md)   
 [安全性概觀 (Integration Services)](security/security-overview-integration-services.md)  
  
  
