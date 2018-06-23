---
title: 只有系統管理員使用者可以寫入檔案系統的作業步驟記錄檔 |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- job step log files [SQL Server Agent]
- log files [SQL Server Agent]
- writing job step log files
ms.assetid: d26a7cef-1a60-4c95-b9df-f8b4fec59f9b
caps.latest.revision: 24
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: e0b7638bbbf33cdd820467cd21edc40a6f5c42ee
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36037145"
---
# <a name="only-sysadmin-users-can-write-job-step-log-files-to-the-file-system"></a>只有系統管理員 (sysadmin) 使用者可以將作業步驟記錄檔寫入檔案系統
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 會選擇性地為每個作業步驟寫入記錄。  
  
## <a name="component"></a>元件  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent  
  
## <a name="description"></a>描述  
 在[!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]代理程式可以寫入檔案系統中的成員所擁有的作業的記錄檔**sysadmin**固定的伺服器角色。 如果作業擁有者不是成員的**sysadmin**角色以及是否已啟用 proxy 帳戶，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]代理程式可以寫入至檔案系統記錄檔所使用的 proxy 帳戶的認證。  
  
 您升級時，不是成員的使用者所擁有的作業之後的**sysadmin**固定的伺服器角色可以不會再記錄檔寫入檔案系統。 相反地，這些使用者可以選取要寫入記錄檔中的資料表選項**msdb**資料庫。 成員**sysadmin**角色仍然可以寫入至檔案系統的記錄檔。  
  
## <a name="corrective-action"></a>更正動作  
 您升級時，不是成員的使用者所擁有的作業之後的**sysadmin**角色將會繼續執行，但將不會建立記錄檔。 若要將作業步驟記錄至資料表，而不是成員的使用者的**sysadmin**角色必須手動更新他們的工作。  
  
 如需詳細資訊，請參閱《[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 線上叢書》中的＜建立作業＞、＜建立作業步驟＞和＜處理多個作業步驟＞主題。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Agent 升級問題](../../../2014/sql-server/install/sql-server-agent-upgrade-issues.md)  
  
  