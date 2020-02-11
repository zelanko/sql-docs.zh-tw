---
title: 使用加密 |Microsoft Docs
ms.custom: ''
ms.date: 08/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- database master key [SMO]
- cryptography [SMO]
- cryptography [SQL Server], SMO
- encryption keys [SMO]
- encryption [SQL Server], SMO
- encryption [SMO]
- certificates [SMO]
- service master key [SMO]
ms.assetid: 405e0ed7-50a9-430e-a343-471f54b4af76
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: fceb0baa62b7998534a5b7620d2c99fd1afc1f8f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "70148319"
---
# <a name="using-encryption"></a>使用加密
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  在 SMO 中，服務主要金鑰是由 <xref:Microsoft.SqlServer.Management.Smo.ServiceMasterKey> 物件表示， 這可藉由 <xref:Microsoft.SqlServer.Management.Smo.Server.ServiceMasterKey%2A> 物件的 <xref:Microsoft.SqlServer.Management.Smo.Server> 屬性加以參考， 並使用 <xref:Microsoft.SqlServer.Management.Smo.ServiceMasterKey.Regenerate%2A> 方法來重新產生。  
  
 資料庫主要金鑰是由 <xref:Microsoft.SqlServer.Management.Smo.MasterKey> 物件表示。 
  <xref:Microsoft.SqlServer.Management.Smo.MasterKey.IsEncryptedByServer%2A> 屬性會指出是否利用服務主要金鑰來加密資料庫主要金鑰。 每當資料庫主要金鑰變更時，master 資料庫中的加密副本就會自動更新。  
  
 您可以使用 <xref:Microsoft.SqlServer.Management.Smo.MasterKey.DropServiceKeyEncryption%2A> 方法來卸除服務金鑰加密，然後使用密碼對資料庫主要金鑰進行加密。 在該種情況下，您必須明確地開啟資料庫主要金鑰，才能存取該金鑰所保護的私密金鑰。  
  
 將資料庫附加到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的執行個體時，您必須為資料庫主要金鑰提供密碼，或執行 <xref:Microsoft.SqlServer.Management.Smo.MasterKey.AddServiceKeyEncryption%2A> 方法，讓資料庫主要金鑰的未加密副本可以使用服務主要金鑰進行加密。 建議使用此步驟，如此即不必明確地開啟資料庫主要金鑰。  
  
 
  <xref:Microsoft.SqlServer.Management.Smo.MasterKey.Regenerate%2A> 方法會重新產生資料庫主要金鑰。 當重新產生資料庫主要金鑰時，所有利用資料庫主要金鑰加密的金鑰都會解密，然後再利用新的資料庫主要金鑰來加密。 
  <xref:Microsoft.SqlServer.Management.Smo.MasterKey.DropServiceKeyEncryption%2A> 方法會利用服務主要金鑰移除資料庫主要金鑰的加密。 
  <xref:Microsoft.SqlServer.Management.Smo.MasterKey.AddServiceKeyEncryption%2A> 會導致主要金鑰的副本使用服務主要金鑰加密，然後同時儲存在目前的資料庫和 master 資料庫中。  
  
 在 SMO 中，憑證是由 <xref:Microsoft.SqlServer.Management.Smo.Certificate> 物件所表示。 
  <xref:Microsoft.SqlServer.Management.Smo.Certificate> 物件的屬性可指定公開金鑰、主旨的名稱、有效期間和簽發者的相關資訊。 存取此憑證的權限是藉由使用 **Grant**、 **Revoke** 和 **Deny** 方法來控制。  
  
## <a name="example"></a>範例  
 在下列的程式碼範例中，您必須選取用於建立應用程式的程式設計環境、程式設計範本和程式設計語言。 如需詳細資訊，請參閱[在 Visual Studio .net 中建立 Visual C&#35; SMO 專案](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md)。  
  
## <a name="adding-a-certificate-in-visual-c"></a>在 Visual C# 中加入憑證  
 此程式碼範例會使用加密密碼來建立簡單的憑證。 不同於其他物件，<xref:Microsoft.SqlServer.Management.Smo.Certificate.Create%2A> 方法有數個多載。 範例中使用的多載會利用加密密碼來建立新的憑證。  
  
```csharp  
{  
            //Connect to the local, default instance of SQL Server.   
            {  
                Server srv = new Server();  
  
                //Reference the AdventureWorks2012 database.   
                Database db = srv.Databases["AdventureWorks2012"];  
  
                //Define a Certificate object variable by supplying the parent database and name in the constructor.   
                Certificate c = new Certificate(db, "Test_Certificate");  
  
                //Set the start date, expiry date, and description.   
                System.DateTime dt;  
                DateTime.TryParse("January 01, 2010", out dt);  
                c.StartDate = dt;  
                DateTime.TryParse("January 01, 2015", out dt);  
                c.ExpirationDate = dt;  
                c.Subject = "This is a test certificate.";  
                //Create the certificate on the instance of SQL Server by supplying the certificate password argument.   
                c.Create("pGFD4bb925DGvbd2439587y");  
            }  
        }   
```  
  
## <a name="adding-a-certificate-in-powershell"></a>在 PowerShell 中加入憑證  
 此程式碼範例會使用加密密碼來建立簡單的憑證。 不同於其他物件，<xref:Microsoft.SqlServer.Management.Smo.Certificate.Create%2A> 方法有數個多載。 範例中使用的多載會利用加密密碼來建立新的憑證。  
  
```powershell  
# Set the path context to the local, default instance of SQL Server and get a reference to AdventureWorks2012  
CD \sql\localhost\default\databases  
$db = get-item AdventureWorks2012  
  
#Create a certificate  
  
$c = New-Object -TypeName Microsoft.SqlServer.Management.Smo.Certificate -argumentlist $db, "Test_Certificate"  
$c.StartDate = "January 01, 2010"  
$c.Subject = "This is a test certificate."  
$c.ExpirationDate = "January 01, 2015"  
  
#Create the certificate on the instance of SQL Server by supplying the certificate password argument.  
$c.Create("pGFD4bb925DGvbd2439587y")  
  
```  
  
## <a name="see-also"></a>另請參閱  
 [使用加密金鑰](../../../relational-databases/server-management-objects-smo/tasks/using-encryption.md)  
  
  
