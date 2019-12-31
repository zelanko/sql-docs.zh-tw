---
title: 匯入已註冊的伺服器資訊
ms.custom: seo-lt-2019
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql12.swb.importregisteredservers.f1
helpviewer_keywords:
- transferring registered server information
- Registered Servers [SQL Server], importing
- importing registered server information
ms.assetid: cc497a14-1360-4887-b70c-002f042823b6
author: markingmyname
ms.author: maghan
manager: jroth
ms.openlocfilehash: 32ef669c238c52ec5e5e20804c896b4364c8bc85
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/19/2019
ms.locfileid: "75241345"
---
# <a name="import-registered-server-information-sql-server-management-studio"></a>匯入已註冊的伺服器資訊 (SQL Server Management Studio)
  本主題描述如何在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]中匯入儲存的已註冊伺服器資訊。 先匯出然後再匯入已註冊的伺服器檔案，可以讓您輕鬆地在 [已註冊的伺服器] 中，使用相同的伺服器設定數部電腦。 從各地的電腦管理大量的伺服器時，或要為較沒有經驗的使用者設定基本連接設定時，這個作法非常有用。  
  
> [!NOTE]  
>  您無法從舊版 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 將已註冊的伺服器資訊匯入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中。  
  
##  <a name="SSMSProcedure"></a>  
  
#### <a name="to-import-registered-server-information"></a>匯入已註冊的伺服器資訊  
  
1.  在 [已註冊的伺服器] 中，按一下 [已註冊的伺服器] 工具列上的伺服器類型。 伺服器類型必須和已註冊伺服器的匯出檔案同類型。 例如，如果您已匯出 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 已註冊的伺服器資訊，則必須在 [已註冊的伺服器] 工具列上按一下 **[SQL Server]** 。  
  
2.  以滑鼠右鍵按一下伺服器群組，並選取 [匯入]****。  
  
3.  在 **[匯入已註冊的伺服器]** 對話方塊中，選取要匯入的已註冊伺服器檔案，然後按一下 **[確定]**。  
  
     **匯入檔案**  
     在文字方塊中鍵入匯入檔案的名稱，或按一下瀏覽按鈕 (**...**) 以找出用戶端電腦上的匯入檔案。 如果您選取現有的檔案，則已註冊的伺服器資訊會附加至該檔案。 匯入檔案僅可為先前匯出之已註冊的伺服器檔案。 已註冊的伺服器檔案的副檔名為 .regsrvr。  
  
     **選取要匯入的伺服器群組**  
     選取檔案中已註冊的伺服器項目將要匯入的根節點或特定伺服器群組。 您可以將所有已註冊的伺服器、特定伺服器群組中已註冊的伺服器或單一已註冊的伺服器匯入至匯出檔案。 匯入功能是遞迴的；例如，如果伺服器群組 A 包含伺服器群組 B，而伺服器群組 B 包含伺服器群組 C 和 D，則匯入伺服器群組 A 會匯出 A、B、C 以及 D 中的所有項目。  
  
     伺服器群組僅會顯示目前已註冊的伺服器樹狀目錄的伺服器群組。  
  
     如果選取匯入現有的伺服器群組或伺服器，就會出現訊息，確認您想要覆寫現有的伺服器或伺服器群組。  
  
 使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證的伺服器註冊會以每位使用者的方式儲存密碼。 匯入伺服器註冊後，使用者第一次連接到每個伺服器時都必須輸入密碼，將密碼儲存在他們的已註冊的伺服器清單中。 透過 Windows 驗證註冊的伺服器則不需如此。  
  
## <a name="see-also"></a>另請參閱  
 [變更伺服器的註冊 &#40;SQL Server Management Studio&#41;](change-a-server-s-registration-sql-server-management-studio.md) [匯出已註冊的伺服器資訊 &#40;SQL Server Management Studio&#41;](export-registered-server-information-sql-server-management-studio.md)   
 [建立新的已註冊伺服器 &#40;SQL Server Management Studio&#41;](create-a-new-registered-server-sql-server-management-studio.md)  
  
  
