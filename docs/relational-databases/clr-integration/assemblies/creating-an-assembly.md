---
title: 建立組件 |Microsoft 文件
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
- creating assemblies
- UNSAFE assemblies
- CREATE ASSEMBLY statement
- SAFE assemblies
- EXTERNAL_ACCESS assemblies
- assemblies [CLR integration], creating
ms.assetid: a2bc503d-b6b2-4963-8beb-c11c323f18e0
caps.latest.revision: 27
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 3b22443461b5bb11d4e4ca1933d4f1d1f931fda9
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32923603"
---
# <a name="creating-an-assembly"></a>建立組件
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  預存程序或觸發程序之類的 Managed 資料庫物件會經過編譯，然後再稱為組件的單元中進行部署。 Managed 的 DLL 組件必須登錄在[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]之前，可以使用組件所提供的功能。 若要在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料庫中註冊組件，請使用 CREATE ASSEMBLY 陳述式。 本主題討論如何在資料庫中使用 CREATE ASSEMBLY 陳述式註冊組件，以及如何指定組件的安全性設定。  
  
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
 建立組件時[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]資料庫時，您可以指定三個不同的安全性層級程式碼可以在其中執行的其中一個：**安全**， **EXTERNAL_ACCESS**，或**UNSAFE**. 當**CREATE ASSEMBLY**陳述式執行時，可能會導致無法在伺服器上註冊的組件的程式碼組件上執行某些檢查。 如需詳細資訊，請參閱 「 模擬 」 範例[CodePlex](http://msftengprodsamples.codeplex.com/)。  
  
 **安全**是的預設權限集合和適用於大部分的案例。 若要指定給定的安全性層級，您要修改 CREATE ASSEMBLY 陳述式的語法，如下所示：  
  
```  
CREATE ASSEMBLY SQLCLRTest  
FROM 'C:\MyDBApp\SQLCLRTest.dll'  
WITH PERMISSION_SET = SAFE;  
```  
  
 它也可建立的組件**安全**只要省略上述程式碼的第三行設定的權限：  
  
```  
CREATE ASSEMBLY SQLCLRTest  
FROM 'C:\MyDBApp\SQLCLRTest.dll';  
```  
  
 當組件中的程式碼會執行下**安全**權限設定，它只能執行計算和資料存取在伺服器內透過同處理序 managed 提供者。  
  
### <a name="creating-externalaccess-and-unsafe-assemblies"></a>建立 EXTERNAL_ACCESS 和 UNSAFE 組件  
 **EXTERNAL_ACCESS**解決的案例中的程式碼需要存取伺服器，例如檔案、 網路、 登錄和環境變數之外的資源。 每當伺服器存取外部資源時，它會模擬呼叫 Managed 程式碼之使用者的安全性內容。  
  
 **UNSAFE**程式碼權限是針對這些情況下，組件不是可驗證的安全或需要額外的存取權受限制的資源，例如[!INCLUDE[msCoName](../../../includes/msconame-md.md)]Win32 API。  
  
 若要建立**EXTERNAL_ACCESS**或**UNSAFE**中的組件[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]，必須符合下列兩種情況的其中一個：  
  
1.  組件是用強式名稱簽署，或用包含憑證的 Authenticode 簽署。 此強式名稱 （或憑證） 在建立[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]做為非對稱金鑰 （或憑證），而且有對應的登入與**EXTERNAL ACCESS ASSEMBLY** （適用於外部存取組件） 的權限或**UNSAFE 組件**權限 （用於 unsafe 組件）。  
  
2.  資料庫擁有者 (DBO) 有**EXTERNAL ACCESS ASSEMBLY** (如**外部存取**組件) 或**UNSAFE ASSEMBLY** (如**UNSAFE**組件） 權限，且資料庫的[TRUSTWORTHY 資料庫屬性](../../../relational-databases/security/trustworthy-database-property.md)設**ON**。  
  
 以上列出的兩個條件也會在組件載入時間 (包括執行) 進行檢查。 若要載入組件，至少必須符合其中一個條件。  
  
 我們建議最好讓[TRUSTWORTHY 資料庫屬性](../../../relational-databases/security/trustworthy-database-property.md)在資料庫上不能設定為**ON**僅執行 common language runtime (CLR) 程式碼中的伺服器處理序。 但是，建議從 master 資料庫的組件檔中建立非對稱金鑰。 然後您必須建立對應至這個非對稱金鑰的登入，並登入必須被授與**EXTERNAL ACCESS ASSEMBLY**或**UNSAFE ASSEMBLY**權限。  
  
 下列[!INCLUDE[tsql](../../../includes/tsql-md.md)]陳述式執行要建立非對稱金鑰，將登入對應到此金鑰，然後授與所需的步驟**EXTERNAL_ACCESS**登入的權限。 您必須先執行下列 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 陳述式，然後再執行 CREATE ASSEMBLY 陳述式。  
  
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
  
 若要建立**外部存取**組件，建立者必須擁有**外部存取**權限。 這是在建立組件時指定的：  
  
```  
CREATE ASSEMBLY SQLCLRTest  
FROM 'C:\MyDBApp\SQLCLRTest.dll'  
WITH PERMISSION_SET = EXTERNAL_ACCESS;  
```  
  
 下列[!INCLUDE[tsql](../../../includes/tsql-md.md)]陳述式執行要建立非對稱金鑰，將登入對應到此金鑰，然後授與所需的步驟**UNSAFE**登入的權限。 您必須先執行下列 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 陳述式，然後再執行 CREATE ASSEMBLY 陳述式。  
  
```  
USE master;   
GO    
  
CREATE ASYMMETRIC KEY SQLCLRTestKey FROM EXECUTABLE FILE = 'C:\MyDBApp\SQLCLRTest.dll';     
CREATE LOGIN SQLCLRTestLogin FROM ASYMMETRIC KEY SQLCLRTestKey ;    
GRANT UNSAFE ASSEMBLY TO SQLCLRTestLogin ;  
GO  
```  
  
 若要指定組件載入含有**UNSAFE**您所指定權限， **UNSAFE**組件載入至伺服器時設定的權限：  
  
```  
CREATE ASSEMBLY SQLCLRTest  
FROM 'C:\MyDBApp\SQLCLRTest.dll'  
WITH PERMISSION_SET = UNSAFE;  
```  
  
 如需每個設定的權限的詳細資訊，請參閱[CLR 整合安全性](../../../relational-databases/clr-integration/security/clr-integration-security.md)。  
  
## <a name="see-also"></a>另請參閱  
 [管理 CLR 整合組件](../../../relational-databases/clr-integration/assemblies/managing-clr-integration-assemblies.md)   
 [變更組件](../../../relational-databases/clr-integration/assemblies/altering-an-assembly.md)   
 [卸除組件](../../../relational-databases/clr-integration/assemblies/dropping-an-assembly.md)   
 [CLR 整合程式碼存取安全性](../../../relational-databases/clr-integration/security/clr-integration-code-access-security.md)   
 [TRUSTWORTHY 資料庫屬性](../../../relational-databases/security/trustworthy-database-property.md)   
 [允許部分信任呼叫端](http://msdn.microsoft.com/library/20b0248f-36da-4fc3-97d2-3789fcf6e084)  
  
  
