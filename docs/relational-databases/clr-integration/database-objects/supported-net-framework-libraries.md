---
title: 支援的 .NET Framework 程式庫 |Microsoft Docs
description: 當 CLR 裝載于 SQL Server 中時，您可以使用支援的 .NET Framework 類別庫，以及您向資料庫註冊的不支援程式庫來撰寫。
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
ms.openlocfilehash: a676688176e164736552460667432919250f8e99
ms.sourcegitcommit: bfb5e79586fd08d8e48e9df0e9c76d1f6c2004e9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/29/2020
ms.locfileid: "82261845"
---
# <a name="supported-net-framework-libraries"></a>支援的 .NET Framework 程式庫
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  利用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中裝載的 Common Language Runtime (CLR)，您能夠以 Managed 程式碼撰寫預存程序、觸發程序、使用者定義函數、使用者定義型別及使用者定義彙總。 藉由 .NET Framework 類別庫所提供的功能，您可以存取預先建立的類別，這些類別可提供字串操作、進階數學運算、檔案存取、加密等多項功能。 您可以透過任何 Managed 預存程序、使用者定義型別、觸發程序、使用者定義函數或使用者定義彙總來存取這些類別。  
  
> [!NOTE]  
>  如果在全域組件快取 (GAC) 中服務或升級不受支援的組件，則 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 應用程式可能會停止運作。 這是因為 GAC 中的服務或升級程式庫不會升級 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 內的這些組件。 如果某個組件同時存在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料庫和 GAC 中，這個組件的兩個副本就必須完全相符。 如果它們不相符，當 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] CLR 整合使用該組件時，將會發生錯誤。 如果您在 GAC 中服務或升級也已在資料庫中註冊的任何元件（包括不支援的 .NET Framework 元件），請務必同時 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 使用**ALTER assembly**語句來服務或升級資料庫中的元件複本。 如需詳細資訊，請參閱[知識庫文章 949080](https://support.microsoft.com/kb/949080)。  
  
## <a name="supported-libraries"></a>支援的程式庫  
 從 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 開始，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 就具備受支援之 .NET Framework 程式庫的清單，這些程式庫均經過測試，以確保符合與 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 互動的可靠性和安全性標準。 受支援的程式庫不需要在伺服器上明確地註冊，即可用於程式碼內，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 會從全域組件快取 (GAC) 直接載入這些程式庫。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中的 CLR 整合所支援的程式庫/命名空間是：  
  
-   CustomMarshalers  
-   Microsoft.VisualBasic  
-   Microsoft.VisualC  
-   mscorlib  
-   系統  
-   System.Configuration  
-   System.Core  
-   System.Data  
-   System.Data.OracleClient  
-   System.Data.SqlXml  
-   System.Deployment  
-   System.Security  
-   System.Transactions  
-   System.Web.Services  
-   System.Xml  
-   System.Xml.Linq  

<!--
Any modifications to the list above should be duplicated on the following page:
https://docs.microsoft.com/sql/relational-databases/clr-integration/assemblies-designing#supported-net-framework-assemblies
-->

## <a name="unsupported-libraries"></a>不支援的程式庫  
 不支援的程式庫仍可以從 Managed 預存程序、觸發程序、使用者定義函數、使用者定義型別和使用者定義彙總加以呼叫。 不支援的程式庫必須先 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 使用**CREATE ASSEMBLY**語句在資料庫中註冊，然後才能在程式碼中使用。 為了確保安全性和可靠性，任何在伺服器上註冊及執行的不支援程式庫都應該經過檢閱和測試。  
  
 例如，不支援**microsoft.directoryservices**命名空間。 您必須先註冊具有**UNSAFE**許可權的 microsoft.directoryservices 元件，才能從程式碼呼叫它。 **UNSAFE**許可權是必要的，因為**microsoft.directoryservices**命名空間中的類別不符合**安全**或**EXTERNAL_ACCESS**的需求。 如需詳細資訊，請參閱[Clr 整合程式設計模型限制](../../../relational-databases/clr-integration/database-objects/clr-integration-programming-model-restrictions.md)和[clr 整合代碼啟用安全性](../../../relational-databases/clr-integration/security/clr-integration-code-access-security.md)。  
  
## <a name="see-also"></a>另請參閱  
 [建立元件](../../../relational-databases/clr-integration/assemblies/creating-an-assembly.md)   
 [CLR 整合代碼啟用安全性](../../../relational-databases/clr-integration/security/clr-integration-code-access-security.md)   
 [CLR 整合程式設計模型限制](../../../relational-databases/clr-integration/database-objects/clr-integration-programming-model-restrictions.md)  
  
  
