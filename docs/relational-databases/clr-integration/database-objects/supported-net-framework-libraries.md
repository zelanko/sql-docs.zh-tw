---
title: 支援 .NET 框架庫 |微軟文件
description: 使用 SQL Server 中託管 CLR 後,您可以使用支援的 .NET Framework 類庫和向資料庫註冊的不受支援的庫進行創作。
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- common language runtime [SQL Server], .NET Framework libraries
- .NET Framework [CLR Integration]
ms.assetid: 417544ff-c25c-496e-add4-2f278f8a4911
author: rothja
ms.author: jroth
ms.openlocfilehash: 459cd091043d567b4c93555c271213d066f3989e
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2020
ms.locfileid: "81487100"
---
# <a name="supported-net-framework-libraries"></a>支援的 .NET Framework 程式庫
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  利用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中裝載的 Common Language Runtime (CLR)，您能夠以 Managed 程式碼撰寫預存程序、觸發程序、使用者定義函數、使用者定義型別及使用者定義彙總。 藉由 .NET Framework 類別庫所提供的功能，您可以存取預先建立的類別，這些類別可提供字串操作、進階數學運算、檔案存取、加密等多項功能。 您可以透過任何 Managed 預存程序、使用者定義型別、觸發程序、使用者定義函數或使用者定義彙總來存取這些類別。  
  
> [!NOTE]  
>  如果在全域組件快取 (GAC) 中服務或升級不受支援的組件，則 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 應用程式可能會停止運作。 這是因為 GAC 中的服務或升級程式庫不會升級 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 內的這些組件。 如果某個組件同時存在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料庫和 GAC 中，這個組件的兩個副本就必須完全相符。 如果它們不相符，當 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] CLR 整合使用該組件時，將會發生錯誤。 如果為 GAC 中也註冊在資料庫中的任何程式集提供服務或升級,包括不支援的 .NET Framework 程式集,[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]請確保使用 ALTER **ASSEMBLY**語句在資料庫內為程式集的副本提供服務或升級。 有關詳細資訊,請參閱[知識庫文章 949080](https://support.microsoft.com/kb/949080)。  
  
## <a name="supported-libraries"></a>支援的程式庫  
 從 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 開始，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 就具備受支援之 .NET Framework 程式庫的清單，這些程式庫均經過測試，以確保符合與 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 互動的可靠性和安全性標準。 受支援的程式庫不需要在伺服器上明確地註冊，即可用於程式碼內，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 會從全域組件快取 (GAC) 直接載入這些程式庫。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中的 CLR 整合所支援的程式庫/命名空間是：  
  
-   CustomMarshalers  
  
-   Microsoft.VisualBasic  
  
-   Microsoft.VisualC  
  
-   mscorlib  
  
-   系統  
  
-   System.Configuration  
  
-   System.Data  
  
-   System.Data.OracleClient  
  
-   System.Data.SqlXml  
  
-   System.Deployment  
  
-   System.Security  
  
-   System.Transactions  
  
-   System.Web.Services  
  
-   System.Xml  
  
-   System.Core.dll  
  
-   System.Xml.Linq.dll  
  
## <a name="unsupported-libraries"></a>不支援的程式庫  
 不支援的程式庫仍可以從 Managed 預存程序、觸發程序、使用者定義函數、使用者定義型別和使用者定義彙總加以呼叫。 不支援的庫必須先使用**CREATE ASSEMBLY**[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]語句在資料庫中註冊,然後才能在代碼中使用。 為了確保安全性和可靠性，任何在伺服器上註冊及執行的不支援程式庫都應該經過檢閱和測試。  
  
 例如,不支援**System.Directory 服務**命名空間。 您必須註冊具有**UNSAFE**許可權的 System.Directory Services.dll 程式集,然後才能從代碼調用它。 **不安全**許可權是必需的,因為系統中的類 **.Directory Services**命名空間不符合**SAFE**或**EXTERNAL_ACCESS**的要求。 有關詳細資訊,請參閱[CLR 整合程式設計模型限制](../../../relational-databases/clr-integration/database-objects/clr-integration-programming-model-restrictions.md)和[CLR 整合程式碼存取安全性](../../../relational-databases/clr-integration/security/clr-integration-code-access-security.md)。  
  
## <a name="see-also"></a>另請參閱  
 [建立程式集](../../../relational-databases/clr-integration/assemblies/creating-an-assembly.md)   
 [CLR 整合程式碼存取安全性](../../../relational-databases/clr-integration/security/clr-integration-code-access-security.md)   
 [CLR 整合程式設計模型限制](../../../relational-databases/clr-integration/database-objects/clr-integration-programming-model-restrictions.md)  
  
  
