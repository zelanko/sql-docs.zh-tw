---
title: 只有系統管理員（sysadmin）使用者可以將作業步驟記錄檔寫入檔案系統 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- job step log files [SQL Server Agent]
- log files [SQL Server Agent]
- writing job step log files
ms.assetid: d26a7cef-1a60-4c95-b9df-f8b4fec59f9b
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 9e2bf5095ac1e6b67f6c6f3f87444879913916e1
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85012178"
---
# <a name="only-sysadmin-users-can-write-job-step-log-files-to-the-file-system"></a>只有系統管理員 (sysadmin) 使用者可以將作業步驟記錄檔寫入檔案系統
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 會選擇性地為每個作業步驟寫入記錄。  
  
## <a name="component"></a>元件  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent  
  
## <a name="description"></a>描述  
 在中 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] ， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 可以針對系統**管理員（sysadmin** ）固定伺服器角色的成員所擁有的作業，將記錄寫入檔案系統。 如果作業擁有者不是**系統管理員（sysadmin** ）角色的成員，而且 proxy 帳戶已啟用， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 就可以使用 proxy 帳戶的認證，將記錄寫入檔案系統。  
  
 升級之後，不是**系統管理員（sysadmin** ）固定伺服器角色成員之使用者所擁有的作業，就無法再將記錄寫入檔案系統。 相反地，這些使用者可以選取選項，將其記錄寫入**msdb**資料庫中的資料表。 **系統管理員（sysadmin** ）角色的成員仍然可以將記錄檔寫入檔案系統。  
  
## <a name="corrective-action"></a>更正動作  
 升級之後，不屬於**系統管理員（sysadmin** ）角色成員的使用者所擁有的工作將會繼續執行，但不會建立記錄。 若要將作業步驟記錄到資料表，非**系統管理員（sysadmin** ）角色成員的使用者必須手動更新其作業。  
  
 如需詳細資訊，請參閱《[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 線上叢書》中的＜建立作業＞、＜建立作業步驟＞和＜處理多個作業步驟＞主題。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Agent 升級問題](../../../2014/sql-server/install/sql-server-agent-upgrade-issues.md)  
  
  
