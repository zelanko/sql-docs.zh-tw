---
title: 建立程式集 |微軟文件
description: 使用 CREATE ASSEMBLY 在 SQL 伺服器中註冊程式集並指定其安全設置。 註冊程式集以使用其功能。
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
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
ms.openlocfilehash: 6ca6787abae22722a7bbb99d335e63d47051bb46
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2020
ms.locfileid: "81486827"
---
# <a name="creating-an-assembly"></a>建立組件
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  預存程序或觸發程序之類的 Managed 資料庫物件會經過編譯，然後再稱為組件的單元中進行部署。 必須先在[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]中 註冊託管 DLL 程式集,然後才能使用程式集提供的功能。 若要在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料庫中註冊組件，請使用 CREATE ASSEMBLY 陳述式。 本主題討論如何在資料庫中使用 CREATE ASSEMBLY 陳述式註冊組件，以及如何指定組件的安全性設定。  
  
## <a name="the-create-assembly-statement"></a>CREATE ASSEMBLY 陳述式  
 CREATE ASSEMBLY 陳述式用於在資料庫中註冊組件。 範例如下：  
  
```  
CREATE ASSEMBLY SQLCLRTest  
FROM 'C:\MyDBApp\SQLCLRTest.dll';  
```  
  
 FROM 子句會指定要建立之組件的路徑名稱。 此路徑可以是通用命名慣例 (UNC) 路徑，或是本機電腦的實體檔案路徑。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 不允許註冊具有相同名稱、文化特性及公開金鑰之不同版本的組件。  
  
 您可以建立參考其他組件的組件。 在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中建立組件時，如果在資料庫中尚未建立參考的組件，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 也會建立根層級組件所參考的組件。  
  
 資料庫使用者或使用者角色擁有建立並因而擁有資料庫中之組件的權限。 若要建立組件，資料庫使用者或角色應該擁有 CREATE ASSEMBLY 權限。  
  
 如果是下列狀況，組件只會成功參考其他組件：  
  
-   呼叫或參考的組件是由相同的使用者或角色所擁有。  
  
-   呼叫或參考的組件是在相同的資料庫中所建立。  
  
## <a name="specifying-security-when-creating-assemblies"></a>建立組件時指定安全性  
 將[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]程式集建立到資料庫中時,可以指定代碼可以執行的三個不同安全等級之一 **:SAFE、EXTERNAL_ACCESS**或**EXTERNAL_ACCESS****UNSAFE**。 運行**CREATE ASSEMBLY**語句時,對代碼程式集執行某些檢查,這可能導致程式集無法在伺服器上註冊。 有關詳細資訊,請參閱[CodePlex](https://msftengprodsamples.codeplex.com/)上的模擬範例。  
  
 **SAFE**是默認許可權集,適用於大多數方案。 若要指定給定的安全性層級，您要修改 CREATE ASSEMBLY 陳述式的語法，如下所示：  
  
```  
CREATE ASSEMBLY SQLCLRTest  
FROM 'C:\MyDBApp\SQLCLRTest.dll'  
WITH PERMISSION_SET = SAFE;  
```  
  
 還可以透過省略上面的第三行代碼來建立具有**SAFE**權限集的程式集:  
  
```  
CREATE ASSEMBLY SQLCLRTest  
FROM 'C:\MyDBApp\SQLCLRTest.dll';  
```  
  
 當程式集中的代碼在**SAFE**許可權集下運行時,它只能通過進程內託管提供程式在伺服器內執行計算和數據訪問。  
  
### <a name="creating-external_access-and-unsafe-assemblies"></a>建立 EXTERNAL_ACCESS 和 UNSAFE 組件  
 **EXTERNAL_ACCESS**解決了代碼需要訪問伺服器外部資源(如檔、網路、註冊表和環境變數)的方案。 每當伺服器存取外部資源時，它會模擬呼叫 Managed 程式碼之使用者的安全性內容。  
  
 **UNSAFE**代碼許可權適用於程式集不安全或需要對受限資源([!INCLUDE[msCoName](../../../includes/msconame-md.md)]如 Win32 API)進行額外存取的情況。  
  
 要在[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]中 建立**EXTERNAL_ACCESS**或**UNSAFE**程式集,必須滿足以下兩個條件之一:  
  
1.  組件是用強式名稱簽署，或用包含憑證的 Authenticode 簽署。 此強名稱(或證書)在內部[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]創建為非對稱密鑰(或證書),並且具有相應的登錄許可權(對於**外部存取**程式集)或 UNSAFE **ASSEMBLY**許可權(對於不安全程式集)。  
  
2.  資料庫擁有者 (DBO) 具有**外部 ACCESS 程式集**(用於**外部存取**程式集)或**UNSAFE ASSEMBLY(** 用於**不安全**程式集)的權限,並且資料庫將[「可信資料庫」屬性](../../../relational-databases/security/trustworthy-database-property.md)設定為**ON**。  

 以上列出的兩個條件也會在組件載入時間 (包括執行) 進行檢查。 若要載入組件，至少必須符合其中一個條件。  
  
 我們建議不要將資料庫上的[TRUSTWORTHY 資料庫屬性](../../../relational-databases/security/trustworthy-database-property.md)設置為**ON,** 而只用於在伺服器進程中運行通用語言運行時 (CLR) 代碼。 但是，建議從 master 資料庫的組件檔中建立非對稱金鑰。 然後,必須創建映射到此非對稱密鑰的登錄名,並且必須授予登錄名**外部存取程式集**或 UNSAFE **ASSEMBLY**許可權。  
  
 以下[!INCLUDE[tsql](../../../includes/tsql-md.md)]語句執行創建非對稱密鑰、將登錄映射到此密鑰以及授予**EXTERNAL_ACCESS**登錄許可權所需的步驟。 您必須先執行下列 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 陳述式，然後再執行 CREATE ASSEMBLY 陳述式。  
  
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
  
 要創建**外部 ACCESS**程式集,建立者需要具有**外部存取**許可權。 這是在建立組件時指定的：  
  
```  
CREATE ASSEMBLY SQLCLRTest  
FROM 'C:\MyDBApp\SQLCLRTest.dll'  
WITH PERMISSION_SET = EXTERNAL_ACCESS;  
```  
  
 以下[!INCLUDE[tsql](../../../includes/tsql-md.md)]語句執行創建非對稱密鑰、將登錄映射到此密鑰以及向登錄授予**UNSAFE**許可權所需的步驟。 您必須先執行下列 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 陳述式，然後再執行 CREATE ASSEMBLY 陳述式。  
  
```  
USE master;   
GO    
  
CREATE ASYMMETRIC KEY SQLCLRTestKey FROM EXECUTABLE FILE = 'C:\MyDBApp\SQLCLRTest.dll';     
CREATE LOGIN SQLCLRTestLogin FROM ASYMMETRIC KEY SQLCLRTestKey ;    
GRANT UNSAFE ASSEMBLY TO SQLCLRTestLogin ;  
GO  
```  
  
 要指定程式集載入有**UNSAFE**權限,請在將應用程式集載入到伺服器時指定**UNSAFE**權限集:  
  
```  
CREATE ASSEMBLY SQLCLRTest  
FROM 'C:\MyDBApp\SQLCLRTest.dll'  
WITH PERMISSION_SET = UNSAFE;  
```  
  
 有關每個設定的權限的詳細資訊,請參閱[CLR 整合安全](../../../relational-databases/clr-integration/security/clr-integration-security.md)。  
  
## <a name="see-also"></a>另請參閱  
 [管理 CLR 整合程式集](../../../relational-databases/clr-integration/assemblies/managing-clr-integration-assemblies.md)   
 [變更程式集](../../../relational-databases/clr-integration/assemblies/altering-an-assembly.md)   
 [移除程式集](../../../relational-databases/clr-integration/assemblies/dropping-an-assembly.md)   
 [CLR 整合程式碼存取安全性](../../../relational-databases/clr-integration/security/clr-integration-code-access-security.md)   
 [可信資料庫屬性](../../../relational-databases/security/trustworthy-database-property.md)   
 [允許部分信任的呼叫端](https://msdn.microsoft.com/library/20b0248f-36da-4fc3-97d2-3789fcf6e084)  
  
  
