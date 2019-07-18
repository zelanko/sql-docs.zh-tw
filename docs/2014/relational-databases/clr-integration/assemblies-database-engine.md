---
title: 組件 (Database Engine) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- assemblies [CLR integration]
- assemblies [CLR integration], about assemblies
- managed code [SQL Server], assemblies
ms.assetid: 4b146437-3061-47f6-9e8c-26eeea10b54e
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 4830a677125cb03e2c53ed78065d94d5265d4a83
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62920784"
---
# <a name="assemblies-database-engine"></a>組件 (Database Engine)
  本節中的主題提供可協助您了解、設計和實作組件的資訊。  
  
 組件所使用的執行個體中的 DLL 檔案[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]部署函式、 預存程序、 觸發程序、 使用者定義彙總和使用者定義的型別所撰寫的所裝載的 managed 程式碼語言之一[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]通用語言執行平台 (CLR)，而不是在[!INCLUDE[tsql](../../../includes/tsql-md.md)]。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中的組件是會參考 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] Common Language Runtime 中所建立 Managed 應用程式模組 (.dll 檔案) 的物件。 組件包含類別中繼資料及 Managed 程式碼。 將組件上傳到 SQL Server 的執行個體是建立下列任何一個資料庫物件的首要步驟：  
  
-   CLR 函數。 如需詳細資訊，請參閱 <<c0> [ 建立 CLR 函數](../user-defined-functions/create-clr-functions.md)。  
  
-   CLR 預存程序。 如需詳細資訊，請參閱 < [CLR 預存程序](../../database-engine/dev-guide/clr-stored-procedures.md)。  
  
-   CLR 觸發程序。 如需詳細資訊，請參閱 <<c0> [ 建立 CLR 觸發程序](../triggers/create-clr-triggers.md)。  
  
-   使用者自訂彙總函式。 如需詳細資訊，請參閱 <<c0> [ 建立使用者定義彙總](../user-defined-functions/create-user-defined-aggregates.md)。  
  
-   使用者定義型別。 如需詳細資訊，請參閱[使用使用者定義型別](../native-client/features/using-user-defined-types.md)。  
  
 組件在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中會執行下列功能：  
  
-   包含執行先前所列之一或多個 CLR 資料庫物件功能的 Managed 程式碼。  
  
-   包含的中繼資料包括組件的版本號碼和文化特性、可唯一地識別組件之類別清單的選用公開金鑰、組件中定義的方法，以及組件的處理器架構。  
  
-   透過調整程式碼存取權限，管理 Managed 程式碼可存取外部資源的程度。  
  
-   包含組件所參考的其他組件之相依性的相關中繼資料。  
  
## <a name="in-this-section"></a>本節內容  
  
|主題|描述|  
|-----------|-----------------|  
|[設計組件](assemblies-designing.md)|解釋在建立組件之前，您必須考慮的項目。 包括封裝組件、程式碼存取權限，以及其他的限制。|  
|[實作組件](assemblies-implementing.md)|解釋如何建立和卸除組件、如何修改組件和修改組件的時機，以及如何擷取關於組件的中繼資料。|  
|[取得組件的相關資訊](assemblies-getting-information.md)|列出可用來查詢組件相關中繼資料的目錄檢視和函數。|  
  
## <a name="see-also"></a>另請參閱  
 [Common Language Runtime &#40;CLR&#41; 整合程式設計概念](common-language-runtime-clr-integration-programming-concepts.md)  
  
  
