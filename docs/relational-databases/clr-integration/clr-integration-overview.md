---
title: "CLR 整合的概觀 |Microsoft 文件"
ms.custom: 
ms.date: 04/19/2017
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
- common language runtime [SQL Server], about CLR integration
- extended stored procedures [SQL Server], vs. managed code
- objects [CLR integration]
- Transact-SQL vs. managed code
- managed code [SQL Server], vs. Transact-SQL
- managed code [SQL Server], vs. extended stored procedures
- execution at client vs. execution at server [CLR integration]
ms.assetid: 5aa176da-3652-4afa-a742-4c40c77ce5c3
caps.latest.revision: "50"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: f506da16cb9a5a98b2a270116ca7948f75c26ce8
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="clr-integration---overview"></a>CLR 整合的概觀
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]Common language runtime (CLR) 核心的 Microsoft.NET Framework，並提供了所有.NET Framework 程式碼的執行環境。 在 CLR 內執行的程式碼稱為 Managed 程式碼。 CLR 提供程式執行所需的各種功能及服務，包括 Just-In-Time (JIT) 編譯、配置及管理記憶體、強制使用型別安全、例外狀況處理、執行緒管理及安全性。  如需詳細資訊，請參閱 .NET Framework SDK。  
  
 利用 Microsoft SQL Server 中裝載的 CLR (稱為 CLR 整合)，您便能夠以 Managed 程式碼撰寫預存程序、觸發程序、使用者定義函數、使用者定義型別及使用者定義彙總。 因為 Managed 程式碼在執行前會編譯成原生程式碼，所以在部分案例中可大幅提升效能。  
  
 Managed 程式碼會使用程式碼存取安全性 (CAS) 來防止組件執行某些作業。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會使用 CAS 協助保護 Managed 程式碼，並防止損害作業系統或資料庫伺服器的安全。  
  
## <a name="advantages-of-clr-integration"></a>CLR 整合的優點  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 是專門為了資料庫中的直接資料存取和操作所設計。 儘管 [!INCLUDE[tsql](../../includes/tsql-md.md)] 擅長資料存取及管理，但它並不是單純的程式語言。 例如，[!INCLUDE[tsql](../../includes/tsql-md.md)] 不支援陣列、集合、for-each 迴圈、位元移位或類別。 雖然某些建構可以在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 中模擬，但是 Managed 程式碼已經整合了這些建構的支援。 根據情況而定，這些功能可提供重要的理由來以 Managed 程式碼實作某些資料庫功能。  
  
 Microsoft Visual Basic .NET 和 Microsoft Visual C# 提供物件導向的功能，例如封裝、繼承和多型 (Polymorphism)。 相關程式碼現在可以輕鬆地組織到類別和命名空間內。 當您處理大量的伺服器程式碼時，這可讓您更輕鬆地組織及維護程式碼。  
  
 Managed 程式碼要比 [!INCLUDE[tsql](../../includes/tsql-md.md)] 更適合用於計算和複雜的執行邏輯，而且配有許多複雜工作的廣泛支援，包括字串處理和規則運算式。 有了 .NET Framework 程式庫中的功能，您便可存取數千個預先建立的類別和常式。 可從任何預存程序、觸發程序或使用者定義函數輕鬆地存取這些項目。 基底類別程式庫 (BCL) 包含的類別可提供字串操作、進階數學運算、檔案存取、加密等多項功能。  
  
> [!NOTE]  
>  透過 SQL Server 中的 CLR 程式碼可使用其中的許多類別，但無法使用對伺服器端而言不適用的類別 (如視窗型類別)。 如需詳細資訊，請參閱[支援.NET Framework 程式庫](../../relational-databases/clr-integration/database-objects/supported-net-framework-libraries.md)。  
  
 Managed 程式碼的優點之一是型別安全，即能夠確保程式碼僅以完整定義及所允許的方式存取型別。 在執行 Managed 程式碼以前，CLR 會先驗證程式碼是否安全。 例如，會先檢查程式碼，以確保先前尚未寫入的記憶體並未讀取。 CLR 亦可協助確保程式碼不會管理 Unmanaged 記憶體。  
  
 CLR 整合有可能會增強效能。 如需資訊，請參閱[CLR 整合的效能](../../relational-databases/clr-integration/clr-integration-architecture-performance.md)。  
 
>  [!WARNING]
>  CLR 使用 .NET Framework 中的程式碼存取安全性 (CAS)，而這不再作為安全性界限受支援。 使用 `PERMISSION_SET = SAFE` 所建立的 CLR 組件可以存取外部系統資源、呼叫 Unmanaged 程式碼，以及取得系統管理員權限。 從 [!INCLUDE[sssqlv14](../../includes/sssqlv14-md.md)] 開始，引進稱為 `clr strict security` 的 `sp_configure` 選項，來增強 CLR 組件的安全性。 `clr strict security` 會依預設啟用，且將 `SAFE` 與 `EXTERNAL_ACCESS` 組件視作已標記為 `UNSAFE` 一樣。 可以基於回溯相容性停用 `clr strict security` 選項，但不建議這麼做。 Microsoft 建議透過具有已獲授與 master 資料庫中 `UNSAFE ASSEMBLY` 權限之對應登入的憑證或非對稱金鑰簽署所有組件。 如需詳細資訊，請參閱 [CLR 嚴格安全性](../../database-engine/configure-windows/clr-strict-security.md)。 
  
## <a name="choosing-between-transact-sql-and-managed-code"></a>在 Transact-SQL 與 Managed 程式碼之間選擇  
 在撰寫預存程序、觸發程序及使用者定義函數時，您必須決定是使用傳統的 [!INCLUDE[tsql](../../includes/tsql-md.md)]，或是 Visual Basic .NET 或 Visual C# 之類的 .NET Framework 語言。 當程式碼大部分執行較少或沒有程序邏輯的資料存取時，請使用 [!INCLUDE[tsql](../../includes/tsql-md.md)]。 若為需佔用大量 CPU 的函數及具有複雜邏輯的程序，或在想要利用 .NET Framework 的 BCL 時，請使用 Managed 程式碼。  
  
### <a name="choosing-between-execution-in-the-server-and-execution-in-the-client"></a>在伺服器上及用戶端上執行之間作選擇  
 在您決定是要使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 或 Managed 程式碼時，有另一個考量因素，那就是您希望程式碼位於何處 (伺服器電腦還是用戶端電腦)。 [!INCLUDE[tsql](../../includes/tsql-md.md)] 和 Managed 程式碼都可以在伺服器上執行。 這樣會將程式碼和資料放在一起，並讓您利用伺服器的處理能力。 另一方面，您可能會想要避免將處理器密集的工作放在資料庫伺服器上。 現今的大多數用戶端電腦都有非常強大的功能，您可能會想要盡量將程式碼放在用戶端上來利用這項處理功能。 Managed 程式碼可以在用戶端電腦上執行，[!INCLUDE[tsql](../../includes/tsql-md.md)] 則不行。  
  
## <a name="choosing-between-extended-stored-procedures-and-managed-code"></a>在擴充預存程序與 Managed 程式碼之間選擇  
 您可以建立擴充預存程序來執行無法以 [!INCLUDE[tsql](../../includes/tsql-md.md)] 預存程序執行的功能。 但是擴充預存程序可能會危害 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 處理序整合性，而驗證為具有型別安全的 Managed 程式碼則不會。 此外，記憶體管理、執行緒與 Fiber 排程及同步處理服務都會在 CLR 的 Managed 程式碼與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之間得到進一步整合。 CLR 整合為您提供比擴充預存程序更安全的方式來撰寫執行工作所需的預存程序，而這是無法在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 中執行的動作。 如需有關 CLR 整合與擴充預存程序的詳細資訊，請參閱[CLR 整合的效能](../../relational-databases/clr-integration/clr-integration-architecture-performance.md)。  
  
## <a name="see-also"></a>請參閱  
 [安裝.NET Framework](http://technet.microsoft.com/library/ms166014\(v=SQL.105\).aspx)   
 [CLR 整合的架構](http://msdn.microsoft.com/library/05e4b872-3d21-46de-b4d5-739b5f2a0cf9)   
 [從 CLR 資料庫物件的資料存取](../../relational-databases/clr-integration/data-access/data-access-from-clr-database-objects.md)   
 [CLR 整合使用者入門](../../relational-databases/clr-integration/database-objects/getting-started-with-clr-integration.md)  
  
  
