---
title: 預存程序 (Database Engine) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.technology: stored-procedures
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- storing programs as stored procedures
- stored procedures [SQL Server], about stored procedures
ms.assetid: cc6daf62-9663-4c3e-950a-ab42e2830427
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f41eb44b026c78a3d99814b231f52b518c18a177
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68136575"
---
# <a name="stored-procedures-database-engine"></a>預存程序 (Database Engine)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的預存程序是一個或多個 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式的群組，或 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] Common Language Runtime (CLR) 方法的參考。 預存程序類似於其他程式設計語言中的建構，因為這些程序可以：  
  
-   接受輸入參數，並以輸出參數的形式將多個數值傳回呼叫程式。  
  
-   包含可在資料庫中執行作業的程式陳述式。 這些功能包括呼叫其他程序。  
  
-   將狀態值傳回呼叫程式，以指示成功或失敗 (及失敗原因)。  
  
## <a name="benefits-of-using-stored-procedures"></a>使用預存程序的好處  
 下列清單說明使用這些程序的一些優點。  
  
 減少伺服器/用戶端網路流量  
 程序中的指令會以單一批次的程式碼來執行。 這可以大幅降低伺服器與用戶端之間的網路流量，因為網路之間只會傳送執行程序的呼叫。 若程序沒有提供程式碼封裝，則每個個別的程式碼行都會在網路上傳送。  
  
 更強的安全性  
 多個使用者和用戶端程式都可以透過程序，在基礎資料庫物件上執行作業，即使使用者和程式不具備這些基礎物件的直接權限亦可。 程序也會控制要執行哪些程序和活動，並保護基礎資料庫物件。 這可避免在個別物件層級授與權限的需求，而簡化安全層。  
  
 [EXECUTE AS](../../t-sql/statements/execute-as-clause-transact-sql.md) 子句可指定在 CREATE PROCEDURE 陳述式中，以模擬其他使用者，或讓使用者或應用程式執行特定資料庫活動，而不需要具備基礎物件和指令的直接權限。 例如，有些動作 (如 TRUNCATE TABLE) 沒有可授與的權限。 若要執行 TRUNCATE TABLE，使用者必須擁有指定資料表的 ALTER 權限。 授與使用者資料表的 ALTER 權限可能不是很理想，因為使用者實際上將擁有不只截斷資料表的權限。 透過合併模組中的 TRUNCATE TABLE 陳述式，並指定有權限修改資料表的使用者來執行該模組，您即可針對授與該模組 EXECUTE 權限的使用者擴充其權限，使其可截斷資料表。  
  
 當透過網路呼叫程序時，僅有執行程序的呼叫是可見的。 因此，惡意使用者就無法查看資料表及資料庫物件名稱、內嵌自己的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式或搜尋重要的資料。  
  
 使用程序參數可協助預防 SQL 資料隱碼攻擊。 由於參數輸入會被視為常值而不是可執行的程式碼，因此更難以將指令插入程序中的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式以進行攻擊，並危及安全性。  
  
 您也可以加密程序，協助模糊化原始程式碼。 如需詳細資訊，請參閱 [SQL Server 加密](../../relational-databases/security/encryption/sql-server-encryption.md)。  
  
 重複使用程式碼  
 任何重複資料庫作業的程式碼，都是程序中非常適合封裝的項目。 這可避免重複撰寫相同程式碼、減少程式碼不一致，並且可讓具備所需權限的任何使用者或應用程式存取及執行程式碼。  
  
 維護更簡易  
 當用戶端應用程式呼叫程序並將資料庫作業保留在資料層中時，若基礎資料庫中有任何變更，只有程序必須更新。 應用程式層會維持獨立，也不需要知道資料庫配置、關聯性或程序間有什麼變更。  
  
 提升效能  
 依預設，第一次編譯程序時，將執行並建立執行計畫，以利後續的執行中重複使用。 由於查詢處理器不需要建立新計畫，通常可以花較少的時間來處理程序。  
  
 若資料表或程序所參照的資料有大幅變更，先行編譯的計畫實際上可能會導致程序執行變慢。 在此情況下，重新編譯程序並強制新的執行計畫可以改善效能。  
  
## <a name="types-of-stored-procedures"></a>預存程序類型  
 使用者自訂  
 您可以在使用者定義的資料庫或所有系統資料庫 ( **Resource** 資料庫除外) 中，建立使用者定義的程序。 您可以使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 或使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] Common Language Runtime (CLR) 方法作為參照的形式來建立程序。  
  
 暫存  
 暫存程序是一種使用者定義的程序。 暫存程序與永久程序類似，只不過暫存程序是儲存於 **tempdb**中。 暫存程序有兩種：本機與全域。 它們在名稱、可見性和可用性方面有些差異。 本機暫存程序是以單一數字符號 (#) 做為名稱的第一個字元；只有目前使用者連接才能看見，當連接中斷時，會將其刪除。 全域暫存程序是以兩個數字符號 (#) 做為名稱的前兩個字元；只要一建立好，任何使用者都能看見，只有當使用程序的最後一個工作階段結束時，才會將其刪除。  
  
 系統  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中包括系統程序。 它們實際上是儲存在內部隱藏的 **Resource** 資料庫中，但邏輯上會出現在每個系統和使用者定義資料庫的 **sys** 結構描述中。 此外， **msdb** 資料庫也包含 **dbo** 結構描述中用於排程警示和作業的系統預存程序。 因為系統程序會以 **sp_** 作為前置詞開頭，因此建議您命名使用者定義的程序時不要使用此前置詞。 如需系統程序的完整清單，請參閱[系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支援的系統程序，可對各種維護活動提供 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 到外部程式的介面。 這些擴充程序會使用 xp_ 前置詞。 如需擴充程序的完整清單，請參閱[一般擴充預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/general-extended-stored-procedures-transact-sql.md)。  
  
 擴充使用者定義  
 擴充程序能夠在 C 這類程式設計語言中，建立外部常式。這些程序是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體可以動態載入和執行的 DLL。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的未來版本將移除擴充預存程序。 請勿在新的開發工作中使用此功能，並且儘速修改使用此功能的應用程式。 改為建立 CLR 程序。 此方法會提供更強固及安全的替代方法來撰寫擴充程序。  
  
## <a name="related-tasks"></a>相關工作  
  
|||  
|-|-|  
|**工作描述**|**主題**|  
|描述如何建立預存程序。|[建立預存程序](../../relational-databases/stored-procedures/create-a-stored-procedure.md)|  
|描述如何修改預存程序。|[修改預存程序](../../relational-databases/stored-procedures/modify-a-stored-procedure.md)|  
|描述如何刪除預存程序。|[刪除預存程序](../../relational-databases/stored-procedures/delete-a-stored-procedure.md)|  
|描述如何執行預存程序。|[執行預存程序](../../relational-databases/stored-procedures/execute-a-stored-procedure.md)|  
|描述如何授與預存程序的權限。|[授與預存程序的權限](../../relational-databases/stored-procedures/grant-permissions-on-a-stored-procedure.md)|  
|描述如何從預存程序將資料傳回應用程式。|[從預存程序傳回資料](../../relational-databases/stored-procedures/return-data-from-a-stored-procedure.md)|  
|描述如何重新編譯預存程序。|[重新編譯預存程序](../../relational-databases/stored-procedures/recompile-a-stored-procedure.md)|  
|描述如何重新命名預存程序。|[重新命名預存程序](../../relational-databases/stored-procedures/rename-a-stored-procedure.md)|  
|描述如何檢視預存程序的定義。|[檢視預存程序的定義](../../relational-databases/stored-procedures/view-the-definition-of-a-stored-procedure.md)|  
|描述如何檢視預存程序的相依性。|[檢視預存程序的相依性](../../relational-databases/stored-procedures/view-the-dependencies-of-a-stored-procedure.md)|  
|描述如何在預存程序中使用參數。|[參數](../../relational-databases/stored-procedures/parameters.md)|  
  
## <a name="related-content"></a>相關內容  
 [CLR 預存程序](https://msdn.microsoft.com/library/bbdd51b2-a9b4-4916-ba6f-7957ac6c3f33)  
  
  
