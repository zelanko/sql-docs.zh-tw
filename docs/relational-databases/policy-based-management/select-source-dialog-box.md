---
title: "選取來源對話方塊 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.dmf.selectsource.f1
ms.assetid: d664c2e5-dd0c-4da8-b27d-aa4ee4fc0ffd
caps.latest.revision: 16
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: a8ffe2ca7e33b741309b594c0a351825fee59b07
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="select-source-dialog-box"></a>選取來源對話方塊
  使用此對話方塊可選取要執行之原則的來源。 若要選取一或多個包含原則的 XML 檔案，請選取 [檔案]。 若要執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體上找到的原則，請選取 [伺服器]。  
  
 您可以利用以下幾種方式來開啟這個對話方塊。  
  
 **開啟這個對話方塊**  
  
-   在 [已註冊的伺服器] 中，以滑鼠右鍵按一下 [本機伺服器群組] 或 [本機伺服器群組] 底下的任何伺服器，或是 [中央管理伺服器] 底下的任何伺服器，然後選取 [評估原則]。 在 [評估原則] 對話方塊的 [原則選取] 頁面中，按一下 [瀏覽]\(...) 按鈕。  
  
-   在物件總管中，依序展開 [管理] 和 [原則管理]，並以滑鼠右鍵按一下 [原則]，然後選取 [匯入原則]。 在 [匯入] 對話方塊中，按一下 [瀏覽]\(...) 按鈕。  
  
-   在物件總管中，以滑鼠右鍵按一下伺服器、資料庫或資料庫物件，然後選取 [原則]，再選取 [評估]。 在 [評估原則] 對話方塊的 [原則選取] 頁面中，按一下 [瀏覽]\(...) 按鈕。  
  
## <a name="options"></a>選項。  
 **檔案**  
 選取一或多個包含原則的 XML 檔案。  
  
 **Server**  
 可讓您選取包含您想要執行之原則的伺服器。  
  
 **伺服器類型**  
 只有 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 伺服器才會包含原則。 這個方塊是唯讀的。  
  
 **伺服器名稱**  
 選取要連接的伺服器執行個體。 依預設，會顯示上次連接的伺服器執行個體。  
  
 **驗證**  
 當連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]執行個體時，有兩種可用的驗證模式。  
  
 **Windows 驗證模式 (Windows 驗證)**  
 Windows 驗證模式允許使用者透過 Windows 使用者帳戶連接。  
  
 **SQL Server 驗證**  
 當使用者從非信任連接使用指定的登入名稱與密碼進行連接時， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會查看是否已設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入帳戶，以及指定的密碼是否符合先前記錄的密碼，自行執行驗證。 如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 沒有登入帳戶集，驗證將失敗，而使用者會收到錯誤訊息。  
  
> [!IMPORTANT]  
>  盡可能使用 Windows 驗證。  
  
 **使用者名稱**  
 輸入要用來連接的使用者名稱。 只有在您已選取使用 Windows 驗證進行連接時，才能使用此選項。  
  
 **登入**  
 輸入要用來連接的登入。 只有在您已選取使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證進行連接時，才可以使用這個選項。  
  
 **密碼**  
 輸入登入的密碼。 只有在您已選取使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證進行連接時，才可編輯此選項。  
  
## <a name="see-also"></a>另請參閱  
 [原則管理節點 &#40;物件總管&#41;](../../relational-databases/policy-based-management/policy-management-node-object-explorer.md)   
 [使用原則式管理來管理伺服器](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)  
  
  
