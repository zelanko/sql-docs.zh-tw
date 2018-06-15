---
title: 組件 (Database Engine) |Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: clr
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- assemblies [CLR integration]
- assemblies [CLR integration], about assemblies
- managed code [SQL Server], assemblies
ms.assetid: 4b146437-3061-47f6-9e8c-26eeea10b54e
caps.latest.revision: 28
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 80fbed0b759f3b05688ee51156a9092294fe0ceb
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32921703"
---
# <a name="assemblies-database-engine"></a>組件 (Database Engine)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  本節中的主題提供可協助您了解、設計和實作組件的資訊。  
  
 組件所使用的執行個體中的 DLL 檔案[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]部署函式、 預存程序、 觸發程序、 使用者定義彙總和使用者定義的型別所撰寫的所裝載的 managed 程式碼語言之一[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]通用語言執行平台 (CLR)，而不是在[!INCLUDE[tsql](../../includes/tsql-md.md)]。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的組件是會參考 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] Common Language Runtime 中所建立 Managed 應用程式模組 (.dll 檔案) 的物件。 組件包含類別中繼資料及 Managed 程式碼。 將組件上傳到 SQL Server 的執行個體是建立下列任何一個資料庫物件的首要步驟：  
  
-   CLR 函數。 如需詳細資訊，請參閱[建立 CLR 函數](../../relational-databases/user-defined-functions/create-clr-functions.md)。  
  
-   CLR 預存程序。 如需詳細資訊，請參閱[CLR 預存程序](http://msdn.microsoft.com/library/bbdd51b2-a9b4-4916-ba6f-7957ac6c3f33)。  
  
-   CLR 觸發程序。 如需詳細資訊，請參閱[建立 CLR 觸發程序](../../relational-databases/triggers/create-clr-triggers.md)。  
  
-   使用者自訂彙總函式。 如需詳細資訊，請參閱[建立使用者定義彙總](../../relational-databases/user-defined-functions/create-user-defined-aggregates.md)。  
  
-   使用者定義型別。 如需詳細資訊，請參閱[Using User-Defined 類型](../../relational-databases/native-client/features/using-user-defined-types.md)。  
  
 組件在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中會執行下列功能：  
  
-   包含執行先前所列之一或多個 CLR 資料庫物件功能的 Managed 程式碼。  
  
-   包含的中繼資料包括組件的版本號碼和文化特性、可唯一地識別組件之類別清單的選用公開金鑰、組件中定義的方法，以及組件的處理器架構。  
  
-   透過調整程式碼存取權限，管理 Managed 程式碼可存取外部資源的程度。  
  
-   包含組件所參考的其他組件之相依性的相關中繼資料。  
  
## <a name="in-this-section"></a>本節內容  
  
|主題|Description|  
|-----------|-----------------|  
|[設計組件](../../relational-databases/clr-integration/assemblies-designing.md)|解釋在建立組件之前，您必須考慮的項目。 包括封裝組件、程式碼存取權限，以及其他的限制。|  
|[實作的組件](../../relational-databases/clr-integration/assemblies-implementing.md)|解釋如何建立和卸除組件、如何修改組件和修改組件的時機，以及如何擷取關於組件的中繼資料。|  
|[取得組件的相關資訊](../../relational-databases/clr-integration/assemblies-getting-information.md)|列出可用來查詢組件相關中繼資料的目錄檢視和函數。|  
  
## <a name="see-also"></a>另請參閱  
 [Common Language Runtime &#40;CLR&#41; 整合程式設計概念](../../relational-databases/clr-integration/common-language-runtime-clr-integration-programming-concepts.md)  
  
  
