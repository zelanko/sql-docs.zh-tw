---
title: 使用同義字 |Microsoft Docs
ms.custom: ''
ms.date: 08/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: smo
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- synonyms [SMO]
ms.assetid: db0a9022-9549-43e5-b6b3-deb236f05fb8
caps.latest.revision: 49
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 7f58b4001468473d23f303de3f41bd0ee9551928
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2018
ms.locfileid: "43070408"
---
# <a name="using-synonyms"></a>使用同義字
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  同義字是結構描述範圍物件的替代名稱。 在 SMO 中，同義字由<xref:Microsoft.SqlServer.Management.Smo.Synonym>物件。 <xref:Microsoft.SqlServer.Management.Smo.Synonym> 物件是 <xref:Microsoft.SqlServer.Management.Smo.Database> 物件的子系。 這表示同義字只有在其定義所在的資料庫範圍內才有效。 不過，同義字可以參考另一個資料庫，或遠端執行個體上的物件[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。  
  
 已具有給定替代名稱的物件也稱為基底物件。 <xref:Microsoft.SqlServer.Management.Smo.Synonym> 物件的名稱屬性是為基底物件所提供的替代名稱。  
  
## <a name="example"></a>範例  
 在下列的程式碼範例中，您必須選取用於建立應用程式的程式設計環境、程式設計範本和程式設計語言。 如需詳細資訊，請參閱 <<c0> [ 建立 Visual C&#35; Visual Studio.NET 中的 SMO 專案](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md)。</c0>  
  
## <a name="creating-a-synonym-in-visual-c"></a>在 Visual C# 中建立同義字  
 此程式碼範例示範如何為結構描述範圍物件建立同義字或替代名稱。 用戶端應用程式可以透過同義字使用單一參考來參考基底物件，而不是使用多重部分名稱來參考基底物件。  
  
```csharp  
{  
            //Connect to the local, default instance of SQL Server.   
            Server srv = new Server();  
  
            //Reference the AdventureWorks2012 database.   
            Database db = srv.Databases["AdventureWorks2012"];  
  
            //Define a Synonym object variable by supplying the   
            //parent database, name, and schema arguments in the constructor.   
            //The name is also a synonym of the name of the base object.   
            Synonym syn = new Synonym(db, "Shop", "Sales");  
  
            //Specify the base object, which is the object on which   
            //the synonym is based.   
            syn.BaseDatabase = "AdventureWorks2012";  
            syn.BaseSchema = "Sales";  
            syn.BaseObject = "Store";  
            syn.BaseServer = srv.Name;  
  
            //Create the synonym on the instance of SQL Server.   
            syn.Create();  
        }  
```  
  
## <a name="creating-a-synonym-in-powershell"></a>在 PowerShell 中建立同義字  
 此程式碼範例示範如何為結構描述範圍物件建立同義字或替代名稱。 用戶端應用程式可以透過同義字使用單一參考來參考基底物件，而不是使用多重部分名稱來參考基底物件。  
  
```powershell  
#Get a server object which corresponds to the default instance  
$srv = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Server  
  
#And the database object corresponding to Adventureworks  
$db = $srv.Databases["AdventureWorks2012"]  
  
$syn = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Synonym `  
-argumentlist $db, "Shop", "Sales"  
  
#Specify the base object, which is the object on which the synonym is based.  
$syn.BaseDatabase = "AdventureWorks2012"  
$syn.BaseSchema = "Sales"  
$syn.BaseObject = "Store"  
$syn.BaseServer = $srv.Name  
  
#Create the synonym on the instance of SQL Server.  
$syn.Create()  
```  
  
## <a name="see-also"></a>另請參閱  
 [CREATE SYNONYM &#40;Transact-SQL&#41;](../../../t-sql/statements/create-synonym-transact-sql.md)  
  
  
