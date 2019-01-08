---
title: SQL Server Agent 屬性 (一般頁面) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql12.ag.agent.general.f1
ms.assetid: b51601e9-5454-43c6-bb5e-24eb2ff043c8
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 66a7b7cd9328f70e5b5ca374a04ad5e9dd6e079a
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/03/2018
ms.locfileid: "52769080"
---
# <a name="sql-server-agent-properties-general-page"></a>SQL Server Agent 屬性 (一般頁面)
  使用此頁面來檢視和修改 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務的一般屬性。  
  
## <a name="options"></a>選項。  
 **服務狀態**  
 顯示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務的目前狀態。  
  
 **如果 SQL Server 非預期地停止，則自動予以重新啟動**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 非預期地停止，Agent 就會重新啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
 **如果 SQL Server Agent 非預期地停止，則自動予以重新啟動**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 非預期地停止，就會重新啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent。  
  
 **檔名**  
 指定錯誤記錄檔的檔案名稱。  
  
 **...**  
 瀏覽錯誤記錄檔。  
  
 **包含執行追蹤訊息**  
 在錯誤記錄檔中包含執行追蹤訊息。 追蹤訊息提供 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 作業的詳細資訊。 因此，選取此選項時，記錄檔需要更多磁碟空間。 只有在疑難排解與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 相關的問題時，才應該選取此選項。  
  
 **寫入 OEM 檔**  
 將錯誤記錄檔寫成非 Unicode 檔案。 如此可減少記錄檔所用的磁碟空間大小。 不過，啟用此選項時，可能更難以讀取包含 Unicode 資料的訊息。  
  
 **Net Send 收件者**  
 鍵入接收 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 寫入記錄檔之訊息的 Net Send 通知的操作員名稱。  
  
## <a name="see-also"></a>另請參閱  
 [運算子](operators.md)   
 [SQL Server Agent 錯誤記錄檔](sql-server-agent-error-log.md)  
  
  
