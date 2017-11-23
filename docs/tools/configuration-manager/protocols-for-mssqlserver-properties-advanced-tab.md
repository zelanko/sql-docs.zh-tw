---
title: "MSSQLSERVER 通訊協定屬性 （進階頁籤） |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: abd5ca68-825f-4c07-b27c-3b3a79d03d74
caps.latest.revision: "7"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5f006e161323a8f86147a63e2dde9ae4eebbcbb5
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="protocols-for-mssqlserver-properties-advanced-tab"></a>MSSQLSERVER 的通訊協定內容 (進階索引標籤)
  您可以使用 [MSSQLSERVER 的通訊協定內容] 對話方塊的 [進階] 索引標籤來設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的 [驗證擴充保護]。 [擴充保護] 是作業系統實作的網路元件功能。 [擴充保護] 可在 Windows 7 和 Windows Server 2008 R2 中使用，而且會包含在舊版作業系統的 Service Pack 中。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在使用 **擴充保護**進行連接時較安全。 [擴充保護] 的某些優點需要在 [旗標] 索引標籤上選取 [強制加密]。  
  
> [!IMPORTANT]  
>  Windows 預設不會啟用 **[擴充保護]** 。 如需如何在 Windows 中啟用 [擴充保護] 的資訊，請參閱知識庫文章：[驗證擴充保護](http://go.microsoft.com/fwlink/?LinkId=178431)。  
  
 如需如何設定其他 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務的詳細資訊及 [擴充保護] 的完整說明，請參閱 [Microsoft.com](http://go.microsoft.com/fwlink/?LinkId=177752) 上最新的資訊。  
  
 從 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 開始，[擴充保護] 就受到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 的完整支援。 目前不支援其他 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 用戶端提供者的 [擴充保護] 支援。  
  
## <a name="options"></a>選項。  
 **擴充保護**  
 有三個可能的值：  
  
-   當設定為 **[關閉]**時，便會停用 **[擴充保護]** 。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體將會接受來自任何用戶端的連接，不論用戶端是否受到保護。 **[關閉]** 與舊版及未修補的作業系統相容，但是比較不安全。 只有當您知道用戶端作業系統不支援擴充保護時，才使用這個設定。  
  
-   當設定為 **[允許]**時，支援 **[擴充保護]** 之作業系統的連接便需要 **[擴充保護]**。 如果未受保護的用戶端應用程式在受保護的用戶端作業系統上執行，則會拒絕來自該應用程式的連接。 如果未受保護的作業系統發出連接，則會忽略 [擴充保護]。 這個設定要比 **[關閉]**安全，但不是最安全的設定。 請在某些作業系統或應用程式支援 [擴充保護] 但某些不支援的混合式環境中使用這個設定。  
  
-   當設定為 **[必要]**時，只會接受來自受保護之作業系統上的受保護應用程式的連接。 這個設定是三個選項中最安全的一種，但是不支援 [擴充保護] 之作業系統的連接將無法連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
 **接受的 NTLM SPN**  
 當 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體由一個以上的 NTLM 服務主要名稱 (SPN) 所識別時，將 SPN 列在這裡當做一系列由分號分隔的字串。 例如， **MSSQLSvc/HostName1.Contoso.com;MSSQLSvc/HostName2.Contoso.com**值表示允許用戶端嘗試連接名為 **MSSQLSvc/HOST1.Contoso.com** 和 **MSSQLSvc/HOST2.Contoso.com** 的 SPN。 此變數的最大長度為 2048,048 個字元。  
  
## <a name="see-also"></a>請參閱＜  
 [含有 Reporting Services 的驗證擴充保護](../../reporting-services/security/extended-protection-for-authentication-with-reporting-services.md)  
  
  
