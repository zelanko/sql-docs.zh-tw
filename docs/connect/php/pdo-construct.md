---
title: "Pdo:: __construct |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 3ee53aff-6fe4-44cd-a15b-51770c98c712
caps.latest.revision: 18
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 71404af3dfbcc0599d53bdb719f4150c77cac332
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="pdoconstruct"></a>PDO::__construct
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

建立 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 資料庫的連接。  
  
## <a name="syntax"></a>語法  
  
```  
  
PDO::__construct($dsn [,$username [,$password [,$driver_options ]]] )  
```  
  
#### <a name="parameters"></a>參數  
*$dsn*： 字串，包含前置詞名稱 (永遠`sqlsrv`)、 冒號與 Server 關鍵字。 例如 `"sqlsrv:server=(local)"`。 您可以選擇性地指定其他連接關鍵字。 如需 Server 關鍵字和其他連接關鍵字的說明，請參閱 [Connection Options](../../connect/php/connection-options.md) 。 整個 *$dsn* 會以引號括住，因此每個連接關鍵字不應分別加上引號。  
  
*$username*：選用。 包含使用者名稱的字串。 若要使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 驗證進行連接，請指定登入識別碼。 若要使用 Windows 驗證進行連接，請指定 `""`。  
  
*$password*：選用。 包含使用者密碼的字串。 若要使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 驗證進行連接，請指定密碼。 若要使用 Windows 驗證進行連接，請指定 `""`。  
  
*$driver_options*： 選擇性。 您可以指定 PDO 驅動程式管理員屬性和[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]特定驅動程式屬性--pdo:: SQLSRV_ATTR_ENCODING、 pdo:: SQLSRV_ATTR_DIRECT_QUERY。 無效的屬性不會產生例外狀況。 與 [PDO::setAttribute](../../connect/php/pdo-setattribute.md)一起指定時，無效的屬性會產生例外狀況。  
  
## <a name="return-value"></a>傳回值  
傳回 PDO 物件。 如果失敗，會傳回 PDOException 物件。  
  
## <a name="exceptions"></a>例外狀況  
PDOException  
  
## <a name="remarks"></a>備註  
您可以將執行個體設為 Null，以關閉連接物件。  
  
連接之後，PDO::errorCode 將會顯示 01000，而不是 00000。  
  
如果 PDO::__construct 因故失敗，將會擲回例外狀況，即使 PDO::ATTR_ERRMODE 設為 PDO::ERRMODE_SILENT 亦然。  
  
[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]2.0 版已加入 PDO 支援。  
  
## <a name="example"></a>範例  
此範例說明如何使用 Windows 驗證連接到伺服器，並指定資料庫。  
  
```  
<?php  
   $c = new PDO( "sqlsrv:Server=(local) ; Database = AdventureWorks ", "", "", array(PDO::SQLSRV_ATTR_DIRECT_QUERY => true));   
  
   $query = 'SELECT * FROM Person.ContactType';   
   $stmt = $c->query( $query );   
   while ( $row = $stmt->fetch( PDO::FETCH_ASSOC ) ) {   
      print_r( $row );   
   }  
   $c = null;   
?>  
```  
  
## <a name="example"></a>範例  
此範例說明如何在後續指定資料庫，以連接到伺服器。  
  
```  
<?php  
   $c = new PDO( "sqlsrv:server=(local)");  
  
   $c->exec( "USE AdventureWorks");  
   $query = 'SELECT * FROM Person.ContactType';  
   $stmt = $c->query( $query );  
   while ( $row = $stmt->fetch( PDO::FETCH_ASSOC ) ){  
      print_r( $row );  
   }  
   $c = null;  
?>  
```  
  
## <a name="see-also"></a>另請參閱  
[PDO 類別](../../connect/php/pdo-class.md)  
[PDO](http://go.microsoft.com/fwlink/?LinkID=187441)  
  

