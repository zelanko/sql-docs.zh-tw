---
title: 使用加密 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
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
caps.latest.revision: 25
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a0d99702b9b6a48e02fe5acc36abed823718c560
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37236728"
---
# <a name="using-encryption"></a>使用加密
  在 SMO 中，服務主要金鑰由<xref:Microsoft.SqlServer.Management.Smo.ServiceMasterKey>物件。 這由參考<xref:Microsoft.SqlServer.Management.Smo.Server.ServiceMasterKey%2A>屬性<xref:Microsoft.SqlServer.Management.Smo.Server>物件。 可以使用重新產生<xref:Microsoft.SqlServer.Management.Smo.ServiceMasterKey.Regenerate%2A>方法。  
  
 資料庫主要金鑰由<xref:Microsoft.SqlServer.Management.Smo.MasterKey>物件。 <xref:Microsoft.SqlServer.Management.Smo.MasterKey.IsEncryptedByServer%2A>屬性會指出是否要將資料庫主要金鑰加密服務主要金鑰。 每當資料庫主要金鑰變更時，master 資料庫中的加密副本就會自動更新。  
  
 您可卸除服務金鑰加密使用<xref:Microsoft.SqlServer.Management.Smo.MasterKey.DropServiceKeyEncryption%2A>方法及加密資料庫主要金鑰與密碼。 在該種情況下，您必須明確地開啟資料庫主要金鑰，才能存取該金鑰所保護的私密金鑰。  
  
 當資料庫附加到的執行個體[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]，您必須提供資料庫主要金鑰的密碼，或執行<xref:Microsoft.SqlServer.Management.Smo.MasterKey.AddServiceKeyEncryption%2A>方法，讓資料庫主要金鑰的未加密的副本可以使用該服務進行加密主要金鑰。 建議使用此步驟，如此即不必明確地開啟資料庫主要金鑰。  
  
 <xref:Microsoft.SqlServer.Management.Smo.MasterKey.Regenerate%2A>方法會重新產生資料庫主要金鑰。 當重新產生資料庫主要金鑰時，所有利用資料庫主要金鑰加密的金鑰都會解密，然後再利用新的資料庫主要金鑰來加密。 <xref:Microsoft.SqlServer.Management.Smo.MasterKey.DropServiceKeyEncryption%2A>方法移除的資料庫主要金鑰，由服務主要金鑰加密。 <xref:Microsoft.SqlServer.Management.Smo.MasterKey.AddServiceKeyEncryption%2A> 會導致主要金鑰的副本使用服務主要金鑰加密，然後同時儲存在目前的資料庫和 master 資料庫中。  
  
 在 SMO 中，憑證由<xref:Microsoft.SqlServer.Management.Smo.Certificate>物件。 <xref:Microsoft.SqlServer.Management.Smo.Certificate>物件的屬性可指定公開金鑰、 主旨的名稱、 期間有效，以及簽發者的相關資訊。 若要存取此憑證的權限會受到使用`Grant`，`Revoke`和`Deny`方法。  
  
## <a name="example"></a>範例  
 在下列的程式碼範例中，您必須選取用於建立應用程式的程式設計環境、程式設計範本和程式設計語言。 如需詳細資訊，請參閱 < [Visual Studio.NET 中建立 Visual Basic SMO Project](../../../database-engine/dev-guide/create-a-visual-basic-smo-project-in-visual-studio-net.md)並[建立 Visual C&#35; Visual Studio.NET 中的 SMO 專案](../how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md)。  
  
## <a name="adding-a-certificate-in-visual-basic"></a>在 Visual Basic 中加入憑證  
 此程式碼範例會使用加密密碼來建立簡單的憑證。 不同於其他物件，<xref:Microsoft.SqlServer.Management.Smo.Certificate.Create%2A>方法有數個多載。 範例中使用的多載會利用加密密碼來建立新的憑證。  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBCertificate1](SMO How to#SMO_VBCertificate1)]  -->  
  
## <a name="adding-a-certificate-in-visual-c"></a>在 Visual C# 中加入憑證  
 此程式碼範例會使用加密密碼來建立簡單的憑證。 不同於其他物件，<xref:Microsoft.SqlServer.Management.Smo.Certificate.Create%2A>方法有數個多載。 範例中使用的多載會利用加密密碼來建立新的憑證。  
  
```  
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
 此程式碼範例會使用加密密碼來建立簡單的憑證。 不同於其他物件，<xref:Microsoft.SqlServer.Management.Smo.Certificate.Create%2A>方法有數個多載。 範例中使用的多載會利用加密密碼來建立新的憑證。  
  
```  
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
 [使用加密金鑰](using-encryption.md)  
  
  
