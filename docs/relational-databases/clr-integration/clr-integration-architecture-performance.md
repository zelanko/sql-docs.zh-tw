---
title: CLR 整合的性能 |微軟文件
description: 本文討論 Microsoft SQL Server 與 .NET 框架 CLR 整合的設計選擇,包括編譯過程和效能。
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- common language runtime [SQL Server], performance
- common language runtime [SQL Server], compilation process
- performance [CLR integration]
ms.assetid: 7ce2dfc0-4b1f-4dcb-a979-2c4f95b4cb15
author: rothja
ms.author: jroth
ms.openlocfilehash: ac12bf75588d70f12b4550260f9911796c1c3a56
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2020
ms.locfileid: "81488144"
---
# <a name="clr-integration-architecture----performance"></a>CLR 整合架構 - 效能
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  本主題討論一些提高與[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[msCoName](../../includes/msconame-md.md)].NET Framework 通用語言運行時 (CLR) 整合效能的設計選擇。  
  
## <a name="the-compilation-process"></a>編譯程序  
 編譯 SQL 運算式期間，碰到 Managed 常式的參考時，就會產生 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Intermediate Language (MSIL) 虛設常式。 此虛設常式包含的程式碼可將常式參數從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 封送處理到 CLR、叫用函數，並傳回結果。 這個「黏附」程式碼是以參數類型以及參數方向 (in、out 或參考) 為基礎。  
  
 黏附程式碼允許類型專屬的最佳化，並確保有效的強制執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 語意，例如，Null 屬性、條件約束 Facet、傳值 (By Value)，以及標準例外狀況處理。 透過產生正確引數類型的程式碼，您可以跨引動過程界限避免強制型轉或包裝函數物件建立成本 (稱為「Boxing」)。  
  
 接著會使用 CLR 的 JIT (Just-In-Time) 編譯服務，將產生的虛設常式編譯為原生程式碼，並針對執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 所在的特定硬體架構最佳化。 JIT 服務會在方法層級叫用，並允許 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 主機環境建立可同時跨越 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 CLR 執行的單一編譯單位。 一旦虛設常式經過編譯之後，所產生的函數指標就會變成函數的執行階段實作。 這個程式碼產生方法可確保沒有與執行階段存取之反射或中繼資料相關的其他引動過程成本。  
  
### <a name="fast-transitions-between-sql-server-and-clr"></a>在 SQL Server 和 CLR 之間快速轉換  
 編譯程序會產生可以在執行階段，從原生程式碼呼叫的函數指標。 如果是純量值的使用者定義函數，此函數引動過程會以資料列為基礎發生。 若要將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 CLR 之間轉換的成本降至最低，包含任何 Managed 引動過程的陳述式都有一個識別目標應用程式網域的啟動步驟。 這個識別步驟會降低每個資料列轉換的成本。  
  
## <a name="performance-considerations"></a>效能考量  
 以下摘要說明 CLR 整合到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 時的特定效能考量。 有關更詳細的資訊,請參閱 MSDN 網站上的「[在 SQL Server 2005 中使用 CLR 整合](https://go.microsoft.com/fwlink/?LinkId=50332)」。 有關託管代碼性能的一般資訊,請參閱 MSDN 網站上的「[提高 .NET 應用程式性能和可伸縮性](https://go.microsoft.com/fwlink/?LinkId=50333)」。  
  
### <a name="user-defined-functions"></a>使用者定義的函式  
 CLR 函數會因為引動過程路徑比 [!INCLUDE[tsql](../../includes/tsql-md.md)] 使用者定義函數的引動過程更快速而獲益。 此外，Managed 程式碼在程序性程式碼、計算與字串操作的決定性效能優勢上優於 [!INCLUDE[tsql](../../includes/tsql-md.md)]。 需要大量計算而不執行資料存取的 CLR 函數以更好的 Managed 程式碼方式撰寫。 不過，[!INCLUDE[tsql](../../includes/tsql-md.md)] 函數在資料存取的執行上比 CLR 整合更有效率。  
  
### <a name="user-defined-aggregates"></a>使用者定義彙總  
 Managed 程式碼可能明顯優於資料指標型彙總。 Managed 程式碼的執行速度一般會比內建的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 彙總函式稍慢。 建議您在原生的內建彙總函式存在時使用它。 如果是原本不支援所需彙總的地方，請就效能上，考慮透過資料指標型實作使用 CLR 使用者定義彙總。  
  
### <a name="streaming-table-valued-functions"></a>資料流資料表值函式  
 應用程式通常需要傳回資料表做為叫用函數的結果。 範例包含在匯入作業期間從檔案讀取表格式資料，以及將逗號分隔值轉換成關聯式表示。 您通常可以先透過具體化與擴展結果資料表來完成這個動作，然後再讓呼叫端取用。 CLR 與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的整合會導入一個新的擴充性機制，稱為資料流資料表值函式 (STVF)。 Managed STVF 的執行效能比可比較的擴充預存程序實作更好。  
  
 STVF 是返回**IE500 介面的**託管函數。 **IEvble**具有導航 STVF 返回的結果集的方法。 調用 STVF 時,返回的**IE55ble**將直接連接到查詢計劃。 查詢計劃在需要提取行時呼叫**IE55 方法**。 此反覆運算模型可在產生第一個資料列之後，立即取用結果，而不會等到擴充整個資料表。 它也會大幅減少叫用函數所耗用的記憶體。  
  
### <a name="arrays-vs-cursors"></a>陣列與資料指標的比較  
 當 [!INCLUDE[tsql](../../includes/tsql-md.md)] 資料指標必須往返的資料當做陣列表示更為容易時，可以透過大幅提高效能使用 Managed 程式碼。  
  
### <a name="string-data"></a>字串資料  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]字元資料(如**varchar)** 可以是託管函數中的 SqlString 或 SqlChars 類型。 SqlString 變數會在記憶體中建立整個值的執行個體。 SqlChars 變數會提供資料流介面，不需要透過在記憶體中建立整個值的執行個體，就可以用於達到更好的效能與延展性。 這對於大型物件 (LOB) 資料而言，變得特別重要。 此外,伺服器XML數據可以通過**SqlXml.CreateReader()** 傳回的流式處理介面進行存取。  
  
### <a name="clr-vs-extended-stored-procedures"></a>CLR 與擴充預存程序的比較  
 允許 Managed 程序將結果集傳回用戶端之 Microsoft.SqlServer.Server 應用程式開發介面 (API) 的執行效能比擴充預存程序所使用的開放式資料服務 (ODS) API 更好。 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]此外,System.Data.SqlServer API 支援在 中引入的數據類型,如**xml、varchar(max)、nvarchar(max)** 和**varchar(max)****varbinary(max),** 而 ODS API 尚未擴展以支援新的資料類型。 **nvarchar(max)**  
  
 利用 Managed 程式碼，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可管理資源的使用，例如，記憶體、執行緒和同步處理。 這是因為公開這些資源的 Managed API 會在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資源管理員頂端實作。 相反地，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 無法檢視或控制擴充預存程序的資源使用量。 例如，如果擴充預存程序耗用太多 CPU 或記憶體資源，就無法利用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 偵測或控制這個擴充預存程序。 不過，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可以利用 Managed 程式碼偵測到給定的執行緒已經很長一段時間沒有產生，然後強制工作產生，如此就可以排程其他工作。 因此，使用 Managed 程式碼可以提供較佳的延展性與系統資源使用量。  
  
 Managed 程式碼可能會產生維護執行環境與執行安全性檢查所需的額外負擔。 例如，需要在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 內部執行，而且需要從 Managed 多次轉換到原生程式碼 (因為在移出和移回原生程式碼時，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 需要在執行緒專屬的設定上進行額外的維護) 時，會發生這個情形。 因此，擴充預存程序能夠明顯優於在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 內部執行的 Managed 程式碼，因為在 Managed 和原生程式碼之間會有頻繁的轉換。  
  
> [!NOTE]  
>  建議您不要開發新的擴充預存程序，因為此功能已被取代。  
  
### <a name="native-serialization-for-user-defined-types"></a>使用者定義型別的原生序列化  
 使用者定義型別 (UDT) 會針對純量類型系統，設計成一個擴充性機制。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]實現稱為格式的 UDT 的序列化**格式。** 在編譯期間，系統會檢查類型的結構來產生針對該特定類型定義自訂的 MSIL。  
  
 原生序列化是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的預設實作。 使用者定義序列化會叫用類型作者所定義的方法來進行序列化。 格式 **.應**盡可能使用本機序列化,以獲得最佳性能。  
  
### <a name="normalization-of-comparable-udts"></a>可比較 UDT 的正規化  
 排序和比較 UDT 之類的關聯式作業會直接針對值的二進位表示操作。 這會透過將 UDT 狀態的正規化 (二進位排序) 表示儲存在磁碟上完成。  
  
 正規化有兩個優點：它會透過避免類型執行個體的建構以及方法引動過程負擔，讓比較作業的成本變得相當低；而且它會建立 UDT 的二進位網域，以便建構長條圖、索引，以及類型值的長條圖。 因此，正規化的 UDT 與不包含方法引動過程作業的原生內建類型，擁有非常類似的效能設定檔。  
  
### <a name="scalable-memory-usage"></a>可擴充的記憶體使用量  
 為了讓 Managed 記憶體回收在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中妥善執行與調整，請避免使用大型的單一配置。 其大小大於 88 KB 的配置將會放在大型物件堆積上，這會讓記憶體回收的執行與調整比許多較小的配置差很多。 例如，如果您需要配置大型的多維度陣列，最好配置不規則 (散佈) 陣列。  
  
## <a name="see-also"></a>另請參閱  
 [CLR 使用者定義型別](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)  
  
  
