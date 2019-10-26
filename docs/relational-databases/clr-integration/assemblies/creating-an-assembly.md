---
title: 建立元件 |Microsoft Docs
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
ms.openlocfilehash: 9493567f33cf07dbfa9ae4f19d037a7db6157eda
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/25/2019
ms.locfileid: "72907393"
---
# <a name="creating-an-assembly"></a>建立組件
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  預存程序或觸發程序之類的 Managed 資料庫物件會經過編譯，然後再稱為組件的單元中進行部署。 Managed DLL 元件必須先在 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中註冊，然後才能使用元件提供的功能。 若要在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料庫中註冊組件，請使用 CREATE ASSEMBLY 陳述式。 本主題討論如何在資料庫中使用 CREATE ASSEMBLY 陳述式註冊組件，以及如何指定組件的安全性設定。  
  
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
 在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料庫中建立元件時，您可以指定您的程式碼可在其中執行的三種不同安全性層級的其中一個： **SAFE**、 **EXTERNAL_ACCESS**或**UNSAFE**。 執行**CREATE ASSEMBLY**語句時，會在程式碼元件上執行某些檢查，這可能會導致元件無法在伺服器上註冊。 如需詳細資訊，請參閱[CodePlex](https://msftengprodsamples.codeplex.com/)上的模擬範例。  
  
 **SAFE**是預設的許可權集合，適用于大部分的案例。 若要指定給定的安全性層級，您要修改 CREATE ASSEMBLY 陳述式的語法，如下所示：  
  
```  
CREATE ASSEMBLY SQLCLRTest  
FROM 'C:\MyDBApp\SQLCLRTest.dll'  
WITH PERMISSION_SET = SAFE;  
```  
  
 您也可以直接省略上面的第三行程式碼，建立具有**SAFE**許可權集合的元件：  
  
```  
CREATE ASSEMBLY SQLCLRTest  
FROM 'C:\MyDBApp\SQLCLRTest.dll';  
```  
  
 當元件中的程式碼以**SAFE**許可權集合執行時，它只能透過同進程 managed 提供者在伺服器內執行計算和資料存取。  
  
### <a name="creating-external_access-and-unsafe-assemblies"></a>建立 EXTERNAL_ACCESS 和 UNSAFE 組件  
 **EXTERNAL_ACCESS**會解決程式碼需要存取伺服器外部資源的情況，例如檔案、網路、登錄和環境變數。 每當伺服器存取外部資源時，它會模擬呼叫 Managed 程式碼之使用者的安全性內容。  
  
 **UNSAFE**程式碼許可權適用于元件不是可驗證的安全或需要額外存取受限制資源（例如 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] WIN32 API）的情況。  
  
 若要在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]中建立**EXTERNAL_ACCESS**或**UNSAFE**元件，必須符合下列兩個條件之一：  
  
1.  組件是用強式名稱簽署，或用包含憑證的 Authenticode 簽署。 這個強式名稱（或憑證）是在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 內建立為非對稱金鑰（或憑證），並具有對應的登入，具有**外部存取元件**許可權（適用于外部存取元件）或**UNSAFE 元件**許可權（適用于unsafe 元件）。  
  
2.  資料庫擁有者（DBO）具有**外部存取元件**（適用于**外部存取**元件）或**Unsafe 元件**（適用于**unsafe**元件）許可權，而且資料庫的 [可信任的[資料庫] 屬性](../../../relational-databases/security/trustworthy-database-property.md)設定為**在上**。  

 以上列出的兩個條件也會在組件載入時間 (包括執行) 進行檢查。 若要載入組件，至少必須符合其中一個條件。  
  
 建議您不要將資料庫上的 [可[信任的資料庫] 屬性](../../../relational-databases/security/trustworthy-database-property.md)設為 [**開啟**]，以便在伺服器進程中執行 COMMON language runtime （CLR）程式碼。 但是，建議從 master 資料庫的組件檔中建立非對稱金鑰。 接著，必須建立對應到此非對稱金鑰的登入，而且必須將該登入授與**EXTERNAL ACCESS ASSEMBLY**或**UNSAFE ASSEMBLY**許可權。  
  
 下列 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 語句會執行建立非對稱金鑰所需的步驟、將登入對應到此金鑰，然後將**EXTERNAL_ACCESS**許可權授與登入。 您必須先執行下列 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 陳述式，然後再執行 CREATE ASSEMBLY 陳述式。  
  
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
  
 若要建立**外部存取**元件，建立者必須具有**外部訪問**許可權。 這是在建立組件時指定的：  
  
```  
CREATE ASSEMBLY SQLCLRTest  
FROM 'C:\MyDBApp\SQLCLRTest.dll'  
WITH PERMISSION_SET = EXTERNAL_ACCESS;  
```  
  
 下列 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 語句會執行建立非對稱金鑰所需的步驟、將登入對應到此金鑰，然後將**UNSAFE**許可權授與登入。 您必須先執行下列 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 陳述式，然後再執行 CREATE ASSEMBLY 陳述式。  
  
```  
USE master;   
GO    
  
CREATE ASYMMETRIC KEY SQLCLRTestKey FROM EXECUTABLE FILE = 'C:\MyDBApp\SQLCLRTest.dll';     
CREATE LOGIN SQLCLRTestLogin FROM ASYMMETRIC KEY SQLCLRTestKey ;    
GRANT UNSAFE ASSEMBLY TO SQLCLRTestLogin ;  
GO  
```  
  
 若要指定以**UNSAFE**許可權載入元件，請在將元件載入伺服器時，指定**unsafe**許可權集合：  
  
```  
CREATE ASSEMBLY SQLCLRTest  
FROM 'C:\MyDBApp\SQLCLRTest.dll'  
WITH PERMISSION_SET = UNSAFE;  
```  
  
 如需每個設定之許可權的詳細資訊，請參閱[CLR Integration Security](../../../relational-databases/clr-integration/security/clr-integration-security.md)。  
  
## <a name="see-also"></a>請參閱  
 [管理 CLR 整合元件](../../../relational-databases/clr-integration/assemblies/managing-clr-integration-assemblies.md)   
 [改變元件](../../../relational-databases/clr-integration/assemblies/altering-an-assembly.md)   
 卸載[元件](../../../relational-databases/clr-integration/assemblies/dropping-an-assembly.md)   
 [CLR 整合代碼啟用安全性](../../../relational-databases/clr-integration/security/clr-integration-code-access-security.md)   
 [TRUSTWORTHY 資料庫屬性](../../../relational-databases/security/trustworthy-database-property.md)   
 [允許部分信任的呼叫端](https://msdn.microsoft.com/library/20b0248f-36da-4fc3-97d2-3789fcf6e084)  
  
  
