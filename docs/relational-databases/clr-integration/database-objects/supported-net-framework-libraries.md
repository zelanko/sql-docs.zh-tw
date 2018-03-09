---
title: "支援.NET Framework 程式庫 |Microsoft 文件"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: clr
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- common language runtime [SQL Server], .NET Framework libraries
- .NET Framework [CLR Integration]
ms.assetid: 417544ff-c25c-496e-add4-2f278f8a4911
caps.latest.revision: 
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e9b970822a872a03fa3f2ba3044d2e8432ac595e
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/09/2018
---
# <a name="supported-net-framework-libraries"></a>支援的 .NET Framework 程式庫
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
利用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中裝載的 Common Language Runtime (CLR)，您能夠以 Managed 程式碼撰寫預存程序、觸發程序、使用者定義函數、使用者定義型別及使用者定義彙總。 藉由 .NET Framework 類別庫所提供的功能，您可以存取預先建立的類別，這些類別可提供字串操作、進階數學運算、檔案存取、加密等多項功能。 您可以透過任何 Managed 預存程序、使用者定義型別、觸發程序、使用者定義函數或使用者定義彙總來存取這些類別。  
  
> [!NOTE]  
>  如果在全域組件快取 (GAC) 中服務或升級不受支援的組件，則 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 應用程式可能會停止運作。 這是因為 GAC 中的服務或升級程式庫不會升級 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 內的這些組件。 如果某個組件同時存在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料庫和 GAC 中，這個組件的兩個副本就必須完全相符。 如果它們不相符，當 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] CLR 整合使用該組件時，將會發生錯誤。 如果服務或升級 GAC 中的任何組件也會登錄在資料庫中，包括不支援的.NET Framework 組件，請務必也服務或升級的內部的組件複製您[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]資料庫與**ALTER ASSEMBLY**陳述式。 如需詳細資訊，請參閱[知識庫文件 949080](http://support.microsoft.com/kb/949080)。  
  
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
 不支援的程式庫仍可以從 Managed 預存程序、觸發程序、使用者定義函數、使用者定義型別和使用者定義彙總加以呼叫。 不支援程式庫必須先註冊在[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]資料庫，請使用**CREATE ASSEMBLY**陳述式，才能在程式碼中使用。 為了確保安全性和可靠性，任何在伺服器上註冊及執行的不支援程式庫都應該經過檢閱和測試。  
  
 例如， **System.DirectoryServices**不支援命名空間。 您必須註冊 System.DirectoryServices.dll 組件，與**UNSAFE**之前您可以從您的程式碼呼叫它的權限。 **UNSAFE**必要權限，是因為中的類別**System.DirectoryServices**命名空間不符合的需求**安全**或**EXTERNAL_ACCESS**。 如需詳細資訊，請參閱[CLR 整合程式設計模型限制](../../../relational-databases/clr-integration/database-objects/clr-integration-programming-model-restrictions.md)和[CLR 整合程式碼存取安全性](../../../relational-databases/clr-integration/security/clr-integration-code-access-security.md)。  
  
## <a name="see-also"></a>另請參閱  
 [建立組件](../../../relational-databases/clr-integration/assemblies/creating-an-assembly.md)   
 [CLR 整合程式碼存取安全性](../../../relational-databases/clr-integration/security/clr-integration-code-access-security.md)   
 [CLR 整合程式設計模型限制](../../../relational-databases/clr-integration/database-objects/clr-integration-programming-model-restrictions.md)  
  
  
