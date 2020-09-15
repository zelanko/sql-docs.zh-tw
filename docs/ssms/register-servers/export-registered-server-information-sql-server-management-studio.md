---
description: 匯出已註冊的伺服器資訊 (SQL Server Management Studio)
title: 匯出已註冊的伺服器資訊
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.swb.exportregisteredservers.f1
helpviewer_keywords:
- Registered Servers [SQL Server], exporting
- exporting registered server information
- transferring registered server information
ms.assetid: b65e168f-b6bf-489c-b8ad-3b8644acf0b6
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.openlocfilehash: d770a7396f48aa11e00eb4f4663285f4cf6eef9a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88370304"
---
# <a name="export-registered-server-information-sql-server-management-studio"></a>匯出已註冊的伺服器資訊 (SQL Server Management Studio)

[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

本主題描述如何儲存並匯出 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]中已註冊伺服器的資訊，並將資訊散發給其他員工或伺服器。 您可以使用此匯出功能，在多部電腦上顯示一致的使用者介面。  
  
 先匯出然後再匯入已註冊的伺服器檔案，可以讓您輕鬆地在 [已註冊的伺服器] 中使用相同的伺服器設定數部電腦。 從各地的電腦管理大量的伺服器時，或要為較沒有經驗的使用者設定基本連接設定時，這個作法非常有用。  
  
> [!NOTE]  
>  使用 SQL Server 驗證的伺服器註冊，會以每一使用者為基礎的方式來儲存密碼。 先匯出然後匯入伺服器註冊後，使用者第一次連接到每個伺服器時都必須輸入密碼，將密碼儲存在他們的已註冊的伺服器清單中。 針對使用 Windows 驗證註冊的伺服器，則不需如此。  
  
##  <a name="SSMSProcedure"></a>  
  
#### <a name="to-export-registered-server-information"></a>匯出已註冊的伺服器資訊  
  
1.  在 [已註冊的伺服器] 中，以滑鼠右鍵按一下伺服器群組，然後按一下 [匯出]****。  
  
    > [!NOTE]  
    >  您可以匯出個別伺服器、整個已註冊的伺服器樹狀目錄，或已註冊的伺服器樹狀目錄之子集。  
  
2.  在 **[匯出已註冊的伺服器]** 對話方塊中，進行下列選取。  
  
     **伺服器群組**  
     指定將要匯出的伺服器群組。 將所有已註冊的伺服器、特定伺服器群組中已註冊的伺服器，或單一已註冊的伺服器匯出至匯出檔案。 匯出功能是遞迴的；例如，如果伺服器群組 A 包含伺服器群組 B，而伺服器群組 B 包含伺服器群組 C 和 D，則匯出伺服器群組 A 會匯出 A、B、C 以及 D 中的所有項目。  
  
     伺服器群組僅會顯示目前已註冊的伺服器樹狀目錄的伺服器群組。  
  
     **匯出檔案**  
     在文字方塊中鍵入匯出檔案的名稱，或使用瀏覽按鈕 (**...**) 以找出用戶端電腦上的匯出檔案。 如果您選取現有的檔案，則已註冊的伺服器資訊會附加至該檔案。 使用 .regsrvr 副檔名。 如果您要提供已註冊的伺服器資訊給其他使用者或另一部電腦使用，您可以將檔案儲存在網路上。 其他使用者就可以存取檔案，並匯入部分或全部已註冊的伺服器資訊。 如果您選取現有的檔案作為匯出檔案，則伺服器註冊資訊會覆寫該檔案的內容。  
  
     **不要在匯出檔案中包含使用者名稱與密碼**  
     匯出檔案時排除使用者名稱。  
  
    > [!IMPORTANT]  
    >  雖然匯出檔案已加密，但是如果使用者名稱與 SQL Server 驗證密碼均包含在檔案中，則要小心控制該檔案的存取權。 因此，依預設使用者名稱與密碼會排除在匯出檔案之外。  
  
## <a name="see-also"></a>另請參閱  
 [匯入已註冊的伺服器資訊 &#40;SQL Server Management Studio&#41;](../../tools/sql-server-management-studio/import-registered-server-information-sql-server-management-studio.md)   
 [建立新的已註冊伺服器 &#40;SQL Server Management Studio&#41;](../../tools/sql-server-management-studio/create-a-new-registered-server-sql-server-management-studio.md)  
  
  
