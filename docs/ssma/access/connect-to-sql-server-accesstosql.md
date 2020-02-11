---
title: 連接到 SQL Server （AccessToSQL） |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: ceb77a97-d6d5-4a92-90a6-342e97d12b54
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 006a90ca082861aea4fecbe6934947afa2020335
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68006666"
---
# <a name="connect-to-sql-server-accesstosql"></a>連接到 SQL Server （AccessToSQL）
使用 [**連接到 SQL Server** ] 對話方塊，即可連接到您想[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]要遷移到的實例。 若要存取 [**連接到 SQL Server** ] 對話方塊，請**在 [檔案] 功能表上**，按一下 [**連接到 SQL Server]**。  
  
## <a name="options"></a>選項。  
**伺服器名稱**  
輸入或選取要連接的 SQL Server 實例。 根據預設，會顯示您最近連線到的實例。  
  
-   如果您要連接到本機電腦上的預設實例，可以輸入**localhost**或句點（**.**）。  
  
-   如果您要連接到另一部電腦上的預設實例，請輸入電腦的名稱。  
  
-   如果您要連接到另一部電腦上的已命名實例，請輸入電腦名稱稱、反斜線和實例名稱，例如*MyServer*\\*MyInstance*。  
  
**伺服器埠**  
如果您的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]實例未設定為接受預設通訊埠（1433）上的連接，請輸入埠號碼。 否則，請將此值保留空白。  
  
**Database**  
指定要將物件和資料移轉至其中的資料庫。 重新連接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]時，無法使用此選項。  
  
**驗證**  
選取用來連接的驗證方法[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 若要使用您目前的 Windows 帳戶，請選取 [Windows 驗證]。 若要指定[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]登入和密碼， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]請選取 [驗證]。  
  
**使用者名稱**  
如果您使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]驗證，請輸入該實例的登入[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 如果您使用 Windows 驗證，則無法使用此選項。  
  
**密碼**  
如果您使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]驗證，請在該實例上輸入登入的密碼[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 如果您使用 Windows 驗證，則無法使用此選項。  
  
**加密連接**  
如果您想要安全地連線到 SQL Server，請核取 [**加密連接**] 核取方塊，以使用 [加密] 連接。  
  
**信任伺服器憑證**  
如果您想要使用此選項，請選取 [**信任伺服器憑證**] 核取方塊。  
  
> [!NOTE]  
> 若要啟用**信任伺服器憑證**，必須將「加密」設定為**True**。  
  
