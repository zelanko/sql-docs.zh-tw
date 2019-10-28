---
title: SQL Server 中的應用程式安全性案例
description: 包含討論 ADO.NET 和 SQL Server 應用程式之各種應用程式安全性案例的主題。
ms.date: 09/26/2019
ms.assetid: 0164f3a4-406e-4693-bec3-03c8e18b46d7
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: 711086e881951d9e82fd34851c451e5472e49d7e
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452346"
---
# <a name="application-security-scenarios-in-sql-server"></a>SQL Server 中的應用程式安全性案例

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[下載 ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

建立安全 SQL Server 用戶端應用程式沒有一種正確的方式。 每個應用程式在其需求、部署環境和使用者群體中都是唯一的。 一開始部署時相當安全的應用程式，在一段時間內可能會變得較不安全。 未來可能會出現的威脅，無法以任何準確度進行預測。  
  
SQL Server，做為產品，已演變成許多版本，以納入最新的安全性功能，可讓開發人員建立安全的資料庫應用程式。 不過，安全性並沒有出現，它需要持續的監視和更新。  
  
## <a name="common-threats"></a>常見的威脅  
開發人員必須瞭解安全性威脅、提供來加以計數器的工具，以及如何避免自我造成的安全性漏洞。 安全性可以視為一種鏈，其中任何一個連結的中斷都會危害整體的強度。 下列清單包含一些常見的安全性威脅，在本節的主題中會有更詳細的討論。  
  
### <a name="sql-injection"></a>SQL 資料隱碼  
SQL 插入式攻擊是指惡意使用者輸入 Transact-sql 語句，而不是有效輸入的程式。 如果在未驗證的情況下將輸入直接傳遞至伺服器，而且應用程式不慎執行插入的程式碼，則攻擊可能會損毀或破壞資料。 您可以透過預存程序和參數化命令、避免動態 SQL 以及限制所有使用者的權限來防堵 SQL Server 插入式攻擊。  
  
### <a name="elevation-of-privilege"></a>提高權限  
當使用者能夠採用信任帳戶（例如擁有者或系統管理員）的許可權時，就會發生權限提高攻擊。 一律在最低許可權的使用者帳戶下執行，並只指派所需的許可權。 避免使用系統管理或擁有者帳戶來執行程式碼。 這會限制攻擊成功時可能發生的損毀量。 執行需要額外許可權的工作時，請在工作期間僅使用程式簽署或模擬。 您可以用憑證來簽署預存程序，或使用模擬來暫時指派權限。  
  
### <a name="probing-and-intelligent-observation"></a>探查和智慧型觀察  
探查攻擊可以使用應用程式所產生的錯誤訊息來搜尋安全性弱點。 在所有程式性程式碼中執行錯誤處理，以防止 SQL Server 錯誤資訊傳回給使用者。  
  
### <a name="authentication"></a>驗證  
如果以使用者輸入為基礎的連接字串是在執行時間所建立，則使用 SQL Server 登入時可能會發生連接字串插入式攻擊。 如果未檢查連接字串是否有有效的關鍵字組，攻擊者可以插入額外的字元，可能會存取伺服器上的機密資料或其他資源。 可能的話，請盡量使用 Windows 驗證。 如果您必須使用 SQL Server 登入，請使用 <xref:Microsoft.Data.SqlClient.SqlConnectionStringBuilder>，在執行時間建立及驗證連接字串。  
  
### <a name="passwords"></a>密碼  
許多攻擊都會成功，因為入侵者能夠取得或猜出特殊許可權使用者的密碼。 密碼是對抗入侵者的第一道防線，因此，設定強式密碼對於系統的安全性很重要。 建立和強制執行混合模式驗證的密碼原則。  
  
請一律將強式密碼指派給 `sa` 帳戶，即使是在使用 Windows 驗證時也一樣。  
  
## <a name="in-this-section"></a>本節內容  
[在 SQL Server 中撰寫安全的動態 SQL](writing-secure-dynamic-sql.md)  
說明使用預存程式撰寫安全動態 SQL 的技術。  

## <a name="next-steps"></a>後續步驟
- [SQL Server 安全性](sql-server-security.md)
