---
title: 建立組件 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- creating assemblies
- UNSAFE assemblies
- CREATE ASSEMBLY statement
- SAFE assemblies
- EXTERNAL_ACCESS assemblies
- assemblies [CLR integration], creating
ms.assetid: a2bc503d-b6b2-4963-8beb-c11c323f18e0
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: e28871e93bd718063692a31a4a3462399517dfc9
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62919577"
---
# <a name="creating-an-assembly"></a>建立組件
  預存程序或觸發程序之類的 Managed 資料庫物件會經過編譯，然後再稱為組件的單元中進行部署。 Managed 的 DLL 組件都必須註冊在[!INCLUDE[msCoName](../../../includes/ssnoversion-md.md)]才可使用的組件所提供的功能。 若要在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料庫中註冊組件，請使用 CREATE ASSEMBLY 陳述式。 本主題討論如何在資料庫中使用 CREATE ASSEMBLY 陳述式註冊組件，以及如何指定組件的安全性設定。  
  
## <a name="the-create-assembly-statement"></a>CREATE ASSEMBLY 陳述式  
 CREATE ASSEMBLY 陳述式用於在資料庫中註冊組件。 範例如下：  
  
```  
CREATE ASSEMBLY SQLCLRTest  
FROM 'C:\MyDBApp\SQLCLRTest.dll';  
```  
  
 FROM 子句會指定要建立之組件的路徑名稱。 此路徑可以是通用命名慣例 (UNC) 路徑，或是本機電腦的實體檔案路徑。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 不允許註冊具有相同名稱、文化特性及公開金鑰之不同版本的組件。  
  
 您可以建立參考其他組件的組件。 組件中的建立時[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]也會建立根層級組件所參考的組件，如果參考的組件沒有已建立資料庫。  
  
 資料庫使用者或使用者角色擁有建立並因而擁有資料庫中之組件的權限。 若要建立組件，資料庫使用者或角色應該擁有 CREATE ASSEMBLY 權限。  
  
 如果是下列狀況，組件只會成功參考其他組件：  
  
-   呼叫或參考的組件是由相同的使用者或角色所擁有。  
  
-   呼叫或參考的組件是在相同的資料庫中所建立。  
  
## <a name="specifying-security-when-creating-assemblies"></a>建立組件時指定安全性  
 在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料庫中建立組件時，您可以在能夠執行程式碼的三個不同安全性層級中，指定一個安全性層級：`SAFE`、`EXTERNAL_ACCESS` 或 `UNSAFE`。 執行 `CREATE ASSEMBLY` 陳述式時，系統會在可能造成組件無法在伺服器上註冊的程式碼組件上執行某些檢查。 如需詳細資訊，請參閱 「 模擬 」 範例上[CodePlex](http://msftengprodsamples.codeplex.com/)。  
  
 `SAFE` 是預設的權限集，而且適用於大部分的狀況。 若要指定給定的安全性層級，您要修改 CREATE ASSEMBLY 陳述式的語法，如下所示：  
  
```  
CREATE ASSEMBLY SQLCLRTest  
FROM 'C:\MyDBApp\SQLCLRTest.dll'  
WITH PERMISSION_SET = SAFE;  
```  
  
 只要省略上述程式碼的第三行，也可以建立包含 `SAFE` 權限集的組件：  
  
```  
CREATE ASSEMBLY SQLCLRTest  
FROM 'C:\MyDBApp\SQLCLRTest.dll';  
```  
  
 當組件中的程式碼在 `SAFE` 權限集下執行時，只能在伺服器內透過同處理序 Managed 提供者進行計算與資料存取。  
  
### <a name="creating-externalaccess-and-unsafe-assemblies"></a>建立 EXTERNAL_ACCESS 和 UNSAFE 組件  
 `EXTERNAL_ACCESS` 會處理程序碼需要存取伺服器外部資源的狀況，例如，檔案、網路、登錄和環境變數。 每當伺服器存取外部資源時，它會模擬呼叫 Managed 程式碼之使用者的安全性內容。  
  
 在組件不是可驗證的安全，或者需要對於 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Win32 API 之類的限制資源之額外存取時，可以使用 `UNSAFE` 程式碼權限。  
  
 若要在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中建立 `EXTERNAL_ACCESS` 或 `UNSAFE` 組件，必須符合下列其中一個條件：  
  
1.  組件是用強式名稱簽署，或用包含憑證的 Authenticode 簽署。 此強式名稱 (或憑證) 在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中會當做非對稱金鑰 (或憑證) 建立，而且擁有包含 `EXTERNAL ACCESS ASSEMBLY` 權限 (用於外部存取組件) 或 `UNSAFE ASSEMBLY` 權限 (用於不安全的組件) 的對應登入。  
  
2.  資料庫擁有者 (DBO) 有`EXTERNAL ACCESS ASSEMBLY`(如`EXTERNAL ACCESS`組件) 或`UNSAFE ASSEMBLY`(如`UNSAFE`組件) 權限，而且資料庫[TRUSTWORTHY 資料庫屬性](../../security/trustworthy-database-property.md)設為`ON`。  
  
 以上列出的兩個條件也會在組件載入時間 (包括執行) 進行檢查。 若要載入組件，至少必須符合其中一個條件。  
  
 我們建議最好讓[TRUSTWORTHY 資料庫屬性](../../security/trustworthy-database-property.md)在資料庫不會設定為`ON`僅執行 common language runtime (CLR) 程式碼中伺服器處理序。 但是，建議從 master 資料庫的組件檔中建立非對稱金鑰。 接著，必須建立對應到此非對稱金鑰的登入，並授與登入 `EXTERNAL ACCESS ASSEMBLY` 或 `UNSAFE ASSEMBLY` 權限。  
  
 下列[!INCLUDE[tsql](../../../includes/tsql-md.md)]執行 CREATE ASSEMBLY 陳述式之前的陳述式。  
  
```  
USE master;   
GO    
  
CREATE ASYMMETRIC KEY SQLCLRTestKey FROM EXECUTABLE FILE = 'C:\MyDBApp\SQLCLRTest.dll'     
CREATE LOGIN SQLCLRTestLogin FROM ASYMMETRIC KEY SQLCLRTestKey     
GRANT EXTERNAL ACCESS ASSEMBLY TO SQLCLRTestLogin;   
GO   
```  
  
> [!NOTE]  
>  您必須建立一個新的登入，並和非對稱金鑰相關聯。 這個登入只會用來授與權限，並不需要和使用者相關聯，也不需要在應用程式中使用。  
  
 若要建立 `EXTERNAL ACCESS` 組件，建立者必須擁有 `EXTERNAL ACCESS` 權限。 這是在建立組件時指定的：  
  
```  
CREATE ASSEMBLY SQLCLRTest  
FROM 'C:\MyDBApp\SQLCLRTest.dll'  
WITH PERMISSION_SET = EXTERNAL_ACCESS;  
```  
  
 下列[!INCLUDE[tsql](../../../includes/tsql-md.md)]執行 CREATE ASSEMBLY 陳述式之前的陳述式。  
  
```  
USE master;   
GO    
  
CREATE ASYMMETRIC KEY SQLCLRTestKey FROM EXECUTABLE FILE = 'C:\MyDBApp\SQLCLRTest.dll';     
CREATE LOGIN SQLCLRTestLogin FROM ASYMMETRIC KEY SQLCLRTestKey ;    
GRANT UNSAFE ASSEMBLY TO SQLCLRTestLogin ;  
GO  
```  
  
 若要指定組件以 `UNSAFE` 權限載入，您可以在將組件載入到伺服器時，指定 `UNSAFE` 權限集：  
  
```  
CREATE ASSEMBLY SQLCLRTest  
FROM 'C:\MyDBApp\SQLCLRTest.dll'  
WITH PERMISSION_SET = UNSAFE;  
```  
  
 如需進一步瞭解每個設定的權限的詳細資訊，請參閱[CLR 整合安全性](../security/clr-integration-security.md)。  
  
## <a name="see-also"></a>另請參閱  
 [管理 CLR 整合組件](managing-clr-integration-assemblies.md)   
 [變更組件](altering-an-assembly.md)   
 [卸除組件](dropping-an-assembly.md)   
 [CLR 整合程式碼存取安全性](../security/clr-integration-code-access-security.md)   
 [TRUSTWORTHY 資料庫屬性](../../security/trustworthy-database-property.md)   
 [允許部分信任的呼叫端](../../../database-engine/dev-guide/allowing-partially-trusted-callers.md)  
  
  
