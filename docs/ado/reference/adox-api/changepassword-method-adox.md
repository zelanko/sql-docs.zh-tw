---
title: ChangePassword 方法 (ADOX) |Microsoft 文件
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _User25::raw_ChangePassword
- _User25::ChangePassword
helpviewer_keywords:
- ChangePassword method [ADOX]
ms.assetid: d187fbc6-5fac-4abb-803d-bf344dcf0302
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ce933eb04cfa830696f69f13fdb36c6eacc83c55
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="changepassword-method-adox"></a>ChangePassword 方法 (ADOX)
變更密碼[使用者](../../../ado/reference/adox-api/user-object-adox.md)帳戶。  
  
## <a name="syntax"></a>語法  
  
```  
  
User.ChangePassword OldPassword, NewPassword  
```  
  
#### <a name="parameters"></a>參數  
 *OldPassword*  
 A**字串**值，指定使用者的現有密碼。 如果在使用者目前不需要密碼，請使用空字串 ("") 為*OldPassword*。  
  
 *NewPassword*  
 A**字串**值，指定新密碼。  
  
## <a name="remarks"></a>備註  
 基於安全性理由，您必須指定舊密碼，除了新的密碼。  
  
 如果提供者不支援信任項目屬性的系統管理工作，會發生錯誤。  
  
## <a name="applies-to"></a>適用於  
 [User 物件 (ADOX)](../../../ado/reference/adox-api/user-object-adox.md)  
  
## <a name="see-also"></a>另請參閱  
 [Groups 和 Users Append、ChangePassword 方法範例 (VB)](../../../ado/reference/adox-api/groups-and-users-append-changepassword-methods-example-vb.md)
