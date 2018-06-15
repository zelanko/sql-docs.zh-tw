---
title: 變更組件 |Microsoft 文件
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
- assemblies [CLR integration], modifying
- permissions [CLR integration]
- altering assemblies
- ALTER ASSEMBLY statement
ms.assetid: 9e765fbd-f339-473c-8537-22f478e79696
caps.latest.revision: 14
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 42a8ca545116bda764ed96a3093683d6e7d52bf9
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32919263"
---
# <a name="altering-an-assembly"></a>變更組件
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  已經在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中註冊的組件可以使用 ALTER ASSEMBLY 陳述式，從比較新的版本更新。 若要更新組件，請使用 ALTER ASSEMBLY 陳述式搭配下列語法：  
  
```  
ALTER ASSEMBLY SQLCLRTest  
FROM 'C:\MyDBApp\SQLCLRTest.dll'  
```  
  
 ALTER ASSEMBLY 不會中斷目前使用組件正在執行的處理序；處理序會繼續執行未變更的組件。 ALTER ASSEMBLY 無法用於變更 Common Language Runtime (CLR) 函數、彙總函式、預存程序和觸發程序的簽章。 新的公用方法可以加入到組件、私用方法可以用任何方式修改，而且只要簽章或屬性沒有變更，就可以修改公用方法。 包含在原生序列化使用者定義型別 (包括資料成員或基底類別) 中的欄位，不能使用 ALTER ASSEMBLY 加以變更。 所有其他變更亦不受支援。 如需詳細資訊，請參閱[ALTER ASSEMBLY &#40;TRANSACT-SQL&#41;](../../../t-sql/statements/alter-assembly-transact-sql.md)。  
  
## <a name="changing-the-permission-set-of-an-assembly"></a>變更組件的權限集合  
 組件的權限集合也可以使用 ALTER ASSEMBLY 陳述式進行變更。 下列陳述式變更 SQLCLRTest 組件的權限集**EXTERNAL_ACCESS**。  
  
```  
ALTER ASSEMBLY SQLCLRTest  
WITH PERMISSION_SET = EXTERNAL_ACCESS   
```  
  
 如果組件的權限集合正在變更從**安全**至**EXTERNAL_ACCESS**或**UNSAFE**，非對稱金鑰和對應的登入，而且**EXTERNAL ACCESS ASSEMBLY**權限或**UNSAFE ASSEMBLY**必須先建立組件的權限。 如需詳細資訊，請參閱 [建立組件](../../../relational-databases/clr-integration/assemblies/creating-an-assembly.md)。  
  
## <a name="adding-the-source-code-of-an-assembly"></a>加入組件的原始程式碼  
 ALTER ASSEMBLY 語法中的 ADD FILE 子句不存在於 CREATE ASSEMBLY 中。 您可以使用它來加入原始程式碼，或與組件相關聯的任何其他檔案。 這些檔案會從原始位置複製，並儲存在資料庫的系統資料表中。 如此可在您需要重新建立或記載 UDT 的目前版本時，確保您一定有原始程式碼或其他檔案可用。  
  
 下列陳述式會對 Point UDT 加入 Point.cs 類別原始程式碼。 這會複製 Point.cs 檔案中包含的文字，並將它儲存在名為 PointSource 的資料庫中。  
  
 `ALTER ASSEMBLY Point`  
  
 `ADD FILE FROM 'C:\Projects\Point\Point.cs' AS PointSource`  
  
## <a name="see-also"></a>另請參閱  
 [管理 CLR 整合組件](../../../relational-databases/clr-integration/assemblies/managing-clr-integration-assemblies.md)   
 [建立組件](../../../relational-databases/clr-integration/assemblies/creating-an-assembly.md)   
 [卸除組件](../../../relational-databases/clr-integration/assemblies/dropping-an-assembly.md)   
 [ALTER ASSEMBLY &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-assembly-transact-sql.md)  
  
  
